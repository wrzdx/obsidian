## L1:
- **Why is search done in two stages (retrieve → rank) instead of scoring the whole corpus with the best model?**
  The best scorer is a cross-encoder, which reads the (query, doc) pair jointly and costs roughly tens of ms per pair — running it over a ~10^9-doc corpus is about 10^8x over a 200ms budget, so it cannot scale. The cascade instead retrieves cheap-and-wide (BM25 / ANN, optimising recall) to shrink ~10^9 → ~10^3, then spends the expensive model on the few survivors (optimising precision@k). Each stage spends ~10x more compute on ~10x fewer candidates, which keeps total latency under SLA.

```
cascade  : 10^9  --retrieve-->  10^3  --rank-->  10^2  --rerank-->  10
optimise :        recall              order             precision@k
cost/doc :        very cheap          moderate          expensive
why not score all: 10^9 docs x ~tens-of-ms = ~10^8x over the 200ms budget
```

- **"ML code is approx 5% of the iceberg." Name three of the larger hidden components of a production search system.**
  Sculley et al. (the "hidden technical debt" iceberg) point out the trained model is a tiny box; the bulk is engineering around it: configuration, data collection, feature extraction / a feature store, data verification, serving infrastructure, monitoring, process-management tooling, and analysis. The lesson for system design is that most of the failure modes and most of the work live outside the model code, so a good ML system is mostly disciplined data and serving engineering.

- **What is the lexical gap? Give an example of a relevant document that keyword search misses.**
  The lexical gap is the failure of exact term matching to bridge synonyms, paraphrase, and morphology: a query "couch" misses a relevant doc that only says "sofa", and "car insurance" misses "auto coverage". BM25 scores shared terms and has no notion of meaning, so two pages about the same thing in different words look unrelated to it. Closing this gap is exactly the motivation for the embedding / dense-retrieval half of the course (L5 onward).

- **Describe a feedback loop ("flywheel") in a search system and how it becomes a rich-get-richer bias.**
  The loop is clicks → logs → training labels → ranking model → what gets shown → more clicks. Items shown high get clicked because they are on top (position bias), those clicks become positive training signal, the model ranks them higher still, and popularity compounds independently of true relevance. The system optimises a proxy (engagement) and silently entrenches whatever was already on top, which is why click logs are biased data, not ground truth, and need de-biasing or A/B confirmation.

- **State Goodhart's law with a search-specific example.**
  Goodhart's law: when a measure becomes a target, it stops being a good measure. In search, optimising click-through rate (a proxy for satisfaction) rewards clickbait titles and thumbnail bait, so CTR climbs while real user satisfaction and dwell time fall. The defence is to never trust a single proxy: triangulate offline graded metrics, significance tests, guardrail metrics (dwell, return rate), and live A/B tests so no one number can be gamed.

- **Back-of-envelope: a cross-encoder scores at ~50 ms/doc and the corpus has 1,000,000 docs. Show why brute-force O(N) scoring per query is infeasible, and how a bi-encoder makes it cheap.**
  Scoring every document with a cross-encoder is 50 ms x 1,000,000 = 50,000,000 ms = 50,000 s, about 13.9 hours per single query, because the score is a property of the (q, d) pair and nothing can be cached. A bi-encoder breaks the dependence: it encodes each document offline once into a vector, so at query time you encode the query once (~50 ms) and reduce scoring to ~10^6 cheap dot products, which finishes in well under a second. The lesson is that precompute-then-dot turns an O(N) model-pass-per-doc cost into an O(N) cheap-arithmetic cost — many orders of magnitude smaller — which is the whole reason dense retrieval is a first-stage retriever and cross-encoders are reserved for reranking.

```
N = 1,000,000 docs   cross-encoder = 50 ms / doc
brute force  : 50 ms x 1e6 = 5e7 ms = 5e4 s ~ 13.9 hours  PER QUERY  (no caching: score is per-pair)
bi-encoder offline : encode 1e6 doc vectors ONCE (reused for every query)
bi-encoder online  : encode query ~50 ms  +  1e6 dot products
  one 768-d dot ~ 768 mul+add ;  1e6 x 768 ~ 7.7e8 flops  <  1 s on CPU
speedup  : ~5e4 s  ->  < 1 s   (>1e4 x)  ;  cross-encoder kept for reranking only
```

- **Put numbers on the retrieve → rank → rerank funnel (10^6 → 10^3 → 10) and show the cost spent at each stage; compare the rerank cost to scoring the whole corpus.**
  The funnel shrinks the candidate set by about 10x at each stage so each stage can afford a ~10x more expensive model: cheap BM25/ANN over 10^6 (optimising recall), a moderate GBDT/LTR over the ~10^3 survivors, then an expensive cross-encoder over only ~10 (optimising precision@k). Putting a 50 ms cross-encoder only on the final ~10 docs costs ~500 ms, versus ~13.9 hours to run it over all 10^6 — the same accurate model becomes affordable purely because the funnel handed it a tiny set. The catch is the recall ceiling: anything stage-1 drops can never be recovered, so the funnel only works if early recall is high.

```
stage      set size   model            cost/doc     ~ stage cost
retrieve   1e6        BM25 / ANN       very cheap   sublinear (skip-lists / index)
rank       1e3        GBDT / LTR       moderate     1e3 x moderate
rerank     1e1        cross-encoder    50 ms        10 x 50 ms = 500 ms
contrast : same cross-encoder over ALL 1e6 = 1e6 x 50 ms ~ 13.9 h
so rerank is affordable ONLY because the funnel cut 1e6 -> 10  (~1e5 x fewer)
recall ceiling: if stage-1 recall = 80%, a perfect reranker still caps at 80%
```

## L2
- **Run the BPE merge loop on the toy string aaabdaaabac; show the full merge ledger and the final symbol count.**
  BPE repeatedly counts adjacent symbol pairs, merges the single most frequent pair into a new symbol, and repeats. On aaabdaaabac (11 chars) the most frequent pair aa (twice) merges to Z; then ab (twice) merges to Y; then ZY (twice) merges to X, leaving XdXac with 5 symbols and no repeated adjacent pair. The ordered ledger {aa->Z, ab->Y, ZY->X} is the learned vocabulary, and re-applied in that exact order it tokenizes new text — the same loop on a frequency-weighted word corpus is the subword tokenizer.

```
start : a a a b d a a a b a c            (11 symbols)
count pairs: aa=2  ab=2  ... -> top = aa
merge 1  aa->Z : Z a b d Z a b a c       (9)   ledger: aa->Z
count pairs: ab=2 -> top
merge 2  ab->Y : Z Y d Z Y a c           (7)   ledger: ab->Y
count pairs: ZY=2 -> top
merge 3  ZY->X : X d X a c                (5)   ledger: ZY->X
stop: no adjacent pair repeats. 11 -> 5 symbols, vocab = {aa,ab,ZY}
```

- **Train BPE on the word corpus {low^5, lower^2, newest^6, widest^3}: do the frequency-weighted pair counts and the first merges, then tokenize the unseen word "lowest".**
  Each word is split into characters plus an end-of-word marker \</w> and pair counts are weighted by the word's corpus frequency, so the pair "e s" scores 6 (newest) + 3 (widest) = 9, the maximum. Merging gives es (9), then est (9), then est\</w> (9), then lo (7 = low^5 + lower^2) and low (7). The payoff: "lowest" never appeared in training, yet it tokenizes cleanly as low + est\</w> from the learned pieces — no \[UNK\] token — which is exactly why subword tokenization generalises to unseen and inflected words.

```
corpus (with freq):  low^5  lower^2  newest^6  widest^3
split: low->l o w </w> ; newest->n e w e s t </w> ; widest->w i d e s t </w>
pair counts (freq-weighted):
  e s = 6 + 3 = 9   <- max      s t = 6 + 3 = 9      l o = 5 + 2 = 7
merge 1  e+s -> es      (9)
merge 2  es+t -> est    (9)
merge 3  est+</w> -> est</w>  (9)
merge 4  l+o -> lo      (7)
merge 5  lo+w -> low    (7)
tokenize UNSEEN "lowest": l o w e s t </w> -> low + est</w>   (no UNK)
```

- **Why do sub-word tokenizers (BPE/WordPiece) beat whole-word on OOV and morphology?**
  A whole-word vocabulary is fixed at training time, so any word it never saw falls out as \[UNK\], destroying information; sub-word tokenizers instead share a vocabulary of reusable pieces, so a rare or inflected or never-seen word decomposes into known sub-units (e.g. "lowest" -> low + est) with no UNK. This also captures morphology for free: shared stems and suffixes ("play", "##ing", "##ed") are reused across words, giving the model a notion of word structure and keeping the vocabulary bounded while coverage stays open.

- **Contrast BPE, WordPiece, and Unigram-SentencePiece: how does each choose its merges/tokens — frequency vs likelihood?**
  All three end with a bounded sub-word vocabulary but differ in how they pick it. BPE builds bottom-up, greedily merging the single most frequent adjacent pair (pure count). WordPiece also builds bottom-up but merges the pair that most increases corpus likelihood, scored as $\frac{freq(AB)}{freq(A)*freq(B)}$ — a PMI-like measure that favours pairs co-occurring more than chance, and it marks word-internal pieces with ##. Unigram-SentencePiece goes top-down: it seeds a large vocabulary, fits a unigram language model, and prunes the tokens whose removal least hurts corpus likelihood until the target size; SentencePiece additionally treats whitespace as an ordinary symbol (rendered \_) so it is reversible and language-agnostic. One-liner: BPE = most-frequent pair, WordPiece = highest likelihood gain, Unigram = least likelihood loss.

```
algorithm  direction          criterion                         marker  used by
BPE        bottom-up (merge)  most FREQUENT pair                byte    GPT-2/4, RoBERTa
WordPiece  bottom-up (merge)  highest LIKELIHOOD gain (PMI-ish) ##      BERT
Unigram    top-down  (prune)  least LIKELIHOOD loss             _       T5, LLaMA, Mistral
WordPiece score(A,B) = freq(AB) / ( freq(A) * freq(B) )
  (some impls use freq(AB)*|V| / (freq(A)*freq(B)); the merge ordering is unchanged)
```

- **WordPiece picks merges by score(A,B) = freq(AB)/(freq(A)\*freq(B)), not raw frequency. On toy counts, show a frequent-but-common pair losing to a rarer-but-sticky pair.**
  The denominator divides by the marginal counts of each piece, so a pair of two very common pieces (th + ##e) gets a big numerator but an even bigger denominator and scores low, while a pair where a piece almost always glues to one specific neighbour (un + ##able) scores high even at lower raw frequency. This is pointwise mutual information without the log: it rewards co-occurrence beyond chance, which is why WordPiece tends to keep meaningful morphemes together rather than just gluing the commonest characters. So WordPiece can prefer a merge that BPE (which only looks at raw frequency) would skip.

```
score(A,B) = freq(AB) / ( freq(A) * freq(B) )
pair  (th, ##e):  freq(AB)=30  freq(th)=30  freq(##e)=100
   score = 30 / (30 * 100) = 30 / 3000 = 0.010
pair  (un, ##able): freq(AB)=10  freq(un)=10  freq(##able)=10
   score = 10 / (10 * 10)  = 10 / 100  = 0.100
BPE (raw freq): picks (th,##e), freq 30 > 10
WordPiece (score): picks (un,##able), 0.100 > 0.010  <- sticky morpheme wins
(some impls scale by |V|: freq(AB)*|V|/(freq(A)*freq(B)); merge ORDER unchanged)
```

- **What is the multilingual "token tax" / fertility, and why does it make low-resource languages cost more to serve?**
  Fertility is tokens-per-word; a tokenizer trained mostly on English splits English cheaply but shatters other scripts into many byte-level pieces — e.g. a 16k BPE trained on (mostly English) 20 Newsgroups turns the Russian word "привет" into 12 tokens while English "tokenization" takes 3. Because attention is O(n^2), roughly 2x fertility means about 4x training compute, about 2x API price and latency, and a smaller effective context window for the same content. This is a fairness problem, not just efficiency: low-resource-language speakers pay more for slower, worse service on identical information.

```
fertility = tokens / word   (a CORPUS AVERAGE, not one word)
per-word examples (different words, illustrative only):
  English  "tokenization"  -> 3 tokens
  Russian  "privet"        -> 12 byte-level tokens  (16k BPE, mostly-English)
corpus-average fertility (RU vs EN) ~ 2x   <- the figure that drives cost
  (do NOT read 12/3 = 4x: those are two DIFFERENT words, not the ratio)
attention O(n^2) : ~2x fertility -> ~4x train compute
                   ~2x API cost , ~2x latency , ~half the usable context window
```

- **State Zipf's and Heaps' laws and what each implies for an IR system.**
  Zipf's law: a term's frequency is roughly inversely proportional to its rank (frequency proportional to 1/rank), so a handful of head terms dominate and a long tail of rare terms remains — this is why idf weighting and stopword handling matter, since common words carry little discriminating signal. Heaps' law: vocabulary size grows sub-linearly (about V proportional to n^beta, beta around 0.5) with corpus size n, so you keep seeing new terms no matter how large the corpus gets — which is precisely why a fixed whole-word vocabulary fails on OOV and why sub-word tokenization is needed.

- **Compute the cosine similarity of a=(1,2,2) and b=(2,0,1) by hand (dot, norms, divide); then say why text uses cosine rather than Euclidean.**
  cos = (a . b)/(||a|| ||b||): the dot is 1\*2 + 2\*0 + 2\*1 = 4, the norms are sqrt(1+4+4)=3 and sqrt(4+0+1)=sqrt(5)~2.236, so cos = 4/(3\*sqrt(5)) = 4/6.708 ~ 0.596, an angle of about 53 degrees ("moderately similar"). Text uses cosine because it is length-invariant: it measures only the direction (the topic mix), so a long document is not scored as more relevant just for repeating words, which is exactly the artifact raw dot product or Euclidean distance on raw counts would introduce.

```
a = (1, 2, 2)   b = (2, 0, 1)
dot   a.b = 1*2 + 2*0 + 2*1 = 2 + 0 + 2 = 4
norm  ||a|| = sqrt(1^2+2^2+2^2) = sqrt(9)  = 3
norm  ||b|| = sqrt(2^2+0^2+1^2) = sqrt(5)  ~ 2.236
cos = 4 / (3 * 2.236) = 4 / 6.708 ~ 0.596
angle = arccos(0.596) ~ 53.4 deg  -> moderately similar
```

- **Two vectors share a direction but differ in magnitude: u=(1,1) vs v=(10,10). Compute cosine and Euclidean by hand and say what each measure concludes.**
  Cosine is exactly 1.0: the dot is 20 and the norm-product is sqrt(2)\*sqrt(200) = sqrt(400) = 20, so 20/20 = 1 — identical, because they point the same way. Euclidean distance is large: sqrt((1-10)^2 + (1-10)^2) = sqrt(162) ~ 12.73 — far apart, because magnitudes differ tenfold. For text we usually want the angle (the topic), not the length, so cosine treats these as the same document at different verbosity while Euclidean wrongly penalises the longer one; the two agree only on L2-normalized vectors.

```
u = (1, 1)   v = (10, 10)   (same direction)
dot   u.v = 1*10 + 1*10 = 20
||u|| = sqrt(1+1) = sqrt(2) ~ 1.414
||v|| = sqrt(100+100) = sqrt(200) = 10*sqrt(2) ~ 14.14
cos = 20 / (sqrt(2) * 10*sqrt(2)) = 20 / (10*2) = 20/20 = 1.0   -> identical
euclid ||u-v|| = sqrt((1-10)^2 + (1-10)^2) = sqrt(81+81) = sqrt(162) ~ 12.73  -> far
```

- **Compute the Jaccard similarity and Jaccard distance of two short token sets by hand.**
  Jaccard similarity is J(A,B) = |A intersect B| / |A union B|, the fraction of the combined vocabulary the two sets share. For A = {the, quick, brown, fox} and B = {the, lazy, brown, dog}, the intersection is {the, brown} (size 2) and the union is {the, quick, brown, fox, lazy, dog} (size 6), so J = 2/6 = 1/3 ~ 0.333, and the Jaccard distance 1 - J = 2/3 ~ 0.667 (a true metric). Jaccard is the natural measure for sets/bags — shingled documents, categorical features, user-item interactions — and MinHash estimates it at web scale because the probability two sketches collide equals exactly J.

```
A = { the, quick, brown, fox }   B = { the, lazy, brown, dog }
A intersect B = { the, brown }                 -> |.| = 2
A union B     = { the, quick, brown, fox, lazy, dog } -> |.| = 6
J(A,B) = 2 / 6 = 1/3 ~ 0.333
Jaccard distance = 1 - J = 1 - 0.333 = 2/3 ~ 0.667  (a true metric)
```

- **Dot product vs cosine and MIPS: why normalize, and when does maximum-inner-product search disagree with cosine?**
  The dot product a.b = ||a|| ||b|| cos(theta) is cosine without the normalization, so it rewards both direction and magnitude and its range is the whole line (it is not a metric). You normalize (use cosine) when length is an artifact rather than signal — e.g. raw TF-IDF, where a long document scores high just for being long. But trained dual encoders (DPR) deliberately learn meaningful norms, pushing confident, information-rich passages to larger magnitude, so MIPS (argmax a.b) intentionally rewards that length and disagrees with cosine: two candidates with the same direction but different norms tie under cosine yet MIPS strictly prefers the larger-norm one. So normalize when magnitude is noise, score by dot when the model was trained to put signal in the length.

```
a . b = sum_i a_i b_i = ||a|| ||b|| cos(theta)   (cosine WITHOUT normalization)
worked: u=(2,-3), v=(4,2) -> 2*4 + (-3)*2 = 8 - 6 = 2
MIPS != cosine example:  q=(1,0)  a=(1,0)  b=(3,0)
  cos(q,a)=1   cos(q,b)=1            -> cosine TIES (same direction)
  q.a = 1      q.b = 3               -> MIPS prefers b (bigger norm = learned signal)
rule: normalize when length is artifact (raw TF-IDF); dot when norms are trained signal (DPR)
```

- **The curse of dimensionality: what are distance concentration, hubness, and anisotropy, and how do they hurt nearest-neighbour search?**
  Distance concentration: in high dimensions the ratio of the farthest to the nearest pairwise distance approaches 1, so all points look about equally far and there is no contrast to rank by. Hubness: a few points become "hubs" that appear in a disproportionate number of other points' nearest-neighbour lists, distorting retrieval. Anisotropy: learned embeddings crowd into a narrow cone rather than filling the space, so cosines are all high and undiscriminative. Together they erode the signal nearest-neighbour search relies on, which is why we whiten / contrastively train embeddings and use ANN structures rather than trusting raw high-dimensional distances.

## L3

- **Why an inverted index instead of a linear scan? What does a postings list store, and what is the rarest-term-first optimization for a conjunctive query?**
  A linear scan is O(N·|d|) per query — unusable at web scale. An inverted index maps term → postings list \[(doc_id, tf, positions), …] sorted by doc_id, so you visit only the docs that actually contain a query term. Postings also carry doc lengths and term positions (for phrase/proximity). For an AND of several terms, intersect starting from the rarest term (smallest df): the running result can only shrink, so each later merge runs against a tiny list.

```
cat   -> [1, 2, 4, 5]   df=4
dog   -> [2, 4, 5]      df=3
bird  -> [1, 5]         df=2

cat AND dog  =  {1,2,4,5} ∩ {2,4,5}  = [2, 4, 5]
plan: start from rarest (bird, df=2):
  bird ∩ cat = {1,5} ∩ {1,2,4,5} = {1,5}   (already tiny)
  vs. starting cat ∩ dog first scans the long list
```

- **Compute a full BM25 term score given tf=3, df=10, N=1000, |d|=200, avgdl=250, with k₁=1.5, b=0.75. Show idf, the length bracket, the saturating tf factor, and the final number.**
  score = idf · tf·(k₁+1) / (tf + k₁·(1 − b + b·|d|/avgdl)), with smoothed idf = ln(1 + (N−df+0.5)/(df+0.5)). Here idf = ln(1+990.5/10.5) = 4.5574, the length bracket = 0.25 + 0.75·(200/250) = 0.85 (doc shorter than average → mild boost), the tf factor B = 3·2.5/(3 + 1.5·0.85) = 7.5/4.275 = 1.7544, so score = 4.5574·1.7544 ≈ 7.9954. The rare term (df=10 of 1000) carries most of the weight via its large idf.

```
tf=3  df=10  N=1000  |d|=200  avgdl=250  k1=1.5  b=0.75

idf = ln(1 + (N − df + 0.5)/(df + 0.5))
    = ln(1 + (1000 − 10 + 0.5)/(10 + 0.5))
    = ln(1 + 990.5/10.5) = ln(95.333) = 4.5574

bracket = (1 − b) + b·|d|/avgdl
        = 0.25 + 0.75·(200/250) = 0.25 + 0.75·0.8 = 0.85

B = tf·(k1+1) / (tf + k1·bracket)
  = 3·2.5 / (3 + 1.5·0.85) = 7.5 / 4.275 = 1.7544

score = idf · B = 4.5574 · 1.7544 = 7.9954
```

- **In BM25, what do k₁ and b control? What happens at b=0 and b=1, and at k₁→0 vs k₁→∞? Show the length bracket at b=0 and b=1 for a doc twice the average length.**
  k₁ sets term-frequency saturation: small k₁ makes the tf factor flatten almost immediately (one occurrence ≈ many), large k₁ keeps tf nearly linear. b sets document-length normalization: b=0 turns it off (bracket = 1 always, length ignored), b=1 applies it fully (bracket = |d|/avgdl). For |d| = 2·avgdl the bracket is 1.0 at b=0 but 2.0 at b=1, so the long doc is penalised twice as hard — its repeated terms are discounted as padding.

```
bracket = (1 − b) + b·|d|/avgdl,   take |d| = 2·avgdl  (ratio = 2)

b = 0:  bracket = 1 + 0·2 = 1.0     → length ignored
b = 1:  bracket = 0 + 1·2 = 2.0     → full length penalty
b = 0.75: bracket = 0.25 + 0.75·2 = 1.75

tf factor B = tf·(k1+1)/(tf + k1·bracket):
  k1 → 0    : B → (tf·1)/(tf) = 1   (tf saturates instantly)
  k1 → ∞    : B → tf·(k1+1)/(k1·bracket) ≈ tf/bracket  (near-linear in tf)
```

- **Query {common, rare} with N=1000, df(common)=500, df(rare)=10. Doc DA stuffs the common term ten times; doc DB has common×1 + rare×1. Rank DA vs DB under TF-IDF (raw tf, idf=log₁₀(N/df)) and under BM25 — show the ranking flip and why.**
  TF-IDF grows linearly in tf and rewards the term-stuffed DA: DA = 10·0.301 = 3.01 beats DB = 0.301 + 2.00 = 2.30, so TF-IDF ranks the spam doc first. BM25 flips it: its smoothed idf weights the rare term far higher (ln-idf rare = 4.5574 vs common = 0.6931) AND its tf factor saturates, so ten common occurrences only reach B = 2.17 (not 10×). DA = 0.6931·2.17 = 1.51 while DB = 0.6931·1.0 + 4.5574·1.0 = 5.25 — DB wins decisively. BM25 refuses to be gamed by repeating a frequent word.

```
N=1000  df(common)=500  df(rare)=10  (assume |d|=avgdl ⇒ bracket=1)

TF-IDF   idf = log10(N/df):
  common = log10(1000/500) = log10(2) = 0.3010
  rare   = log10(1000/10)  = log10(100) = 2.0000
  DA = 10·0.3010 + 0·2.0 = 3.0103
  DB =  1·0.3010 + 1·2.0 = 2.3010
  TF-IDF order:  DA > DB

BM25   idf = ln(1 + (N−df+0.5)/(df+0.5)):
  common = ln(1 + 500.5/500.5) = ln(2)   = 0.6931
  rare   = ln(1 + 990.5/10.5)  = ln(95.3) = 4.5574
  B(tf=10) = 10·2.5/(10 + 1.5·1) = 25/11.5 = 2.1739
  B(tf=1)  =  1·2.5/(1 + 1.5·1)  = 2.5/2.5 = 1.0000
  DA = 0.6931·2.1739          = 1.5068
  DB = 0.6931·1.0 + 4.5574·1.0 = 5.2505
  BM25 order:  DB > DA   ← FLIPPED
```

- **RRF (k=60): fuse BM25 list [A,B,C,D] with cosine list [C,A,D,B]. Compute score(d)=Σ 1/(60+rankᵢ(d)) for every doc and give the fused order. Show how a consensus doc beats a list’s #1 that the other list buries.**
  RRF throws away raw scores and sums reciprocal ranks: score(d)=Σᵢ 1/(60+rankᵢ(d)). A is rank 1 (BM25) and rank 2 (cosine) → 0.016393 + 0.016129 = 0.032522, the highest. C is rank 3 + rank 1 → 0.032266. D ranks 4 + 3 (=0.031498) and B ranks 2 + 4 (=0.031754). Fused order: A > C > B > D. The consensus doc A wins even though cosine’s #1 was C — two solidly-high ranks sum higher than one great rank dragged down by a poor one. Ranks are calibration-free, so incomparable score scales (BM25 vs cosine) never distort the fusion.

```
BM25 :  A B C D   (ranks A=1 B=2 C=3 D=4)
cosine:  C A D B   (ranks C=1 A=2 D=3 B=4)
k = 60

A: 1/(60+1) + 1/(60+2) = 0.016393 + 0.016129 = 0.032522
C: 1/(60+3) + 1/(60+1) = 0.015873 + 0.016393 = 0.032266
B: 1/(60+2) + 1/(60+4) = 0.016129 + 0.015625 = 0.031754
D: 1/(60+4) + 1/(60+3) = 0.015625 + 0.015873 = 0.031498

fused order:  A > C > B > D
(A, never #1 alone-but-consensus, beats C the cosine #1)
```

- **What do WAND / BlockMax-WAND solve, and how? Sketch the skip condition with a toy upper-bound and threshold.**
  They make top-k retrieval effectively sublinear. Each term (WAND) or each block of a postings list (BlockMax-WAND) carries a precomputed maximum contribution. While scanning, you keep θ = the current k-th-best score; if the sum of upper bounds of the terms a candidate could match is ≤ θ, that document cannot enter the top-k, so it is skipped without a full score. BlockMax refines this to per-block max-scores, skipping whole blocks of postings at once.

```
maxscore(cat) = 1.8   maxscore(dog) = 0.9
current top-k threshold  θ = 2.0

candidate matches only {dog}:  UB = 0.9  ≤ θ=2.0  → SKIP
candidate matches {cat,dog}:   UB = 1.8+0.9 = 2.7 > θ → score it

BlockMax: store max per block; if blockmax(block) ≤ θ skip the whole block.
```

- **RRF is rank-based — why is that more robust than mixing raw scores across rankers? Show what a raw-sum does when one ranker’s scale is 100× the other.**
  Different rankers’ score scales are incomparable — BM25 ≈ 0–30, cosine ∈ \[−1,1], a logit can be anything — so a naive sum is dominated by whichever scale is larger; the small-scale ranker contributes almost nothing. RRF maps every list to ranks (1,2,3,…) before fusing, which is calibration-free and invariant to monotone score transforms, so each ranker gets a fair, bounded vote. (Min-max normalization is the alternative but is sensitive to outliers and the score distribution.)

```
docX: BM25=28.0  cosine=0.20
docY: BM25= 2.0  cosine=0.95

raw sum:  X = 28.0+0.20 = 28.2   Y = 2.0+0.95 = 2.95   → X wins on BM25 scale alone
          (cosine vote of 0.95 vs 0.20 is invisible)

RRF (X rank 1/2, Y rank 2/1):
  X = 1/61 + 1/62 = 0.032522
  Y = 1/62 + 1/61 = 0.032522   → tie; the disagreement is fairly averaged
```

- **Bag-of-Words by hand: given the 3-doc corpus D1 “the cat sat”, D2 “the dog sat”, D3 “the cat and the dog”, build the sorted vocabulary, write the term-document count matrix, and express the query “cat dog” as a BoW vector over the same vocabulary.**
  Collect every distinct token and sort: V = \[and, cat, dog, sat, the], so |V| = 5 and each doc becomes a count vector in ℝ⁵. D1 = \[0,1,0,1,1], D2 = \[0,0,1,1,1], D3 = \[1,1,1,0,2] (note “the” appears twice in D3). The query “cat dog” is just another vector over V: \[0,1,1,0,0]. BoW discards word order entirely — “cat dog” and “dog cat” map to the same vector — and the high count of the stopword “the” carries no topic signal, which is exactly what IDF later down-weights.

```
tokens: D1{the,cat,sat} D2{the,dog,sat} D3{the,cat,and,the,dog}
vocabulary (sorted) V = [ and, cat, dog, sat, the ]   |V| = 5

          and  cat  dog  sat  the
D1         0    1    0    1    1
D2         0    0    1    1    1
D3         1    1    1    0    2

query "cat dog"  →  [ 0, 1, 1, 0, 0 ]
("dog cat" would give the SAME vector — order is lost)
```

- **Boolean & phrase queries on a tiny inverted index. Postings: cat→[1,2,4,5], dog→[2,4,5], bird→[1,5]. Evaluate (cat AND dog), (cat OR bird), (cat AND NOT dog), and (cat AND dog) AND NOT bird. Then, with positional postings machine→D7:[2,9], learning→D7:[3,15], decide whether the phrase “machine learning” matches D7.**
  Boolean operators are set operations on doc-id lists: AND = intersection, OR = union, NOT = difference. cat AND dog = {1,2,4,5}∩{2,4,5} = \[2,4,5]; cat OR bird = {1,2,4,5}∪{1,5} = \[1,2,4,5]; cat AND NOT dog = {1,2,4,5}∖{2,4,5} = \[1]; (cat AND dog) AND NOT bird = {2,4,5}∖{1,5} = \[2,4]. For the phrase, doc-level AND first confirms both terms are in D7; then walk the position lists for offsets exactly one apart: machine@2, learning@3 gives 3−2=1 → a hit, while machine@9 vs learning@15 has gap 6 → not adjacent. So “machine learning” matches D7 (once). Generalising the gap to ≤ k gives proximity search.

```
cat=[1,2,4,5]  dog=[2,4,5]  bird=[1,5]

cat AND dog            = {1,2,4,5} ∩ {2,4,5} = [2, 4, 5]
cat OR  bird           = {1,2,4,5} ∪ {1,5}   = [1, 2, 4, 5]
cat AND NOT dog        = {1,2,4,5} \ {2,4,5} = [1]
(cat AND dog) AND NOT bird = {2,4,5} \ {1,5} = [2, 4]

phrase "machine learning" in D7:
  machine @ [2, 9]   learning @ [3, 15]
  need p_learning − p_machine = 1
  3 − 2 = 1  ✓ hit      15 − 9 = 6  ✗
  → matches D7 (one occurrence)
```

- **One power-iteration step of PageRank (d=0.85) on the 4-edge graph A→B, A→C, B→C, C→A. Start uniform v₀=(⅓,⅓,⅓), tabulate out-degrees, apply PR(p)=(1−d)/n + d·Σ_(q→p) PR(q)/outdeg(q), and give the updated rank vector.**
  Out-degrees: A=2 (→B,→C), B=1 (→C), C=1 (→A). In-links: A←C, B←A, C←A,B. The teleport base is (1−0.85)/3 = 0.05. A gets all of C’s vote (C/1); B gets half of A’s (A/2, since A links to two pages); C gets half of A’s plus all of B’s. With v₀ = ⅓ each: PR₁(A)=0.05+0.85·0.3333=0.3333, PR₁(B)=0.05+0.85·0.1667=0.1917, PR₁(C)=0.05+0.85·(0.1667+0.3333)=0.4750. The vector sums to 1.0 and C — the only node with two in-links — already leads after a single step.

```
edges: A→B, A→C, B→C, C→A     d = 0.85,  n = 3
outdeg: A=2,  B=1,  C=1
in-links: A←C ;  B←A ;  C←A,B
base = (1−d)/n = 0.15/3 = 0.05
v0 = (1/3, 1/3, 1/3) = (0.3333, 0.3333, 0.3333)

PR1(A) = 0.05 + 0.85·(PR0(C)/1)            = 0.05 + 0.85·0.3333 = 0.3333
PR1(B) = 0.05 + 0.85·(PR0(A)/2)            = 0.05 + 0.85·0.1667 = 0.1917
PR1(C) = 0.05 + 0.85·(PR0(A)/2 + PR0(B)/1) = 0.05 + 0.85·0.5000 = 0.4750

v1 = (0.3333, 0.1917, 0.4750)   Σ = 1.0    C leads (2 in-links)
```

- **Why do postings lists compress so well? Explain delta/gap encoding + variable-byte, and show the byte saving on docIDs [3, 8, 12, 30].**
  Postings dominate index size, and the doc-ids in a list are sorted, so instead of storing absolute ids you store the gaps between successive ids — these are small, and small numbers need few bits. Variable-byte coding packs each gap into bytes of 7 data bits + 1 continuation bit, so any value 0–127 fits in a single byte. On \[3,8,12,30] the gaps are \[3,5,4,18], all < 128, so 4 bytes instead of 4×4 = 16 raw → a 4× reduction. A smaller index stays in cache and cuts I/O, the real query-time bottleneck. (Real engines use PForDelta / Simple-9 / Roaring, but the gap-then-encode idea is identical.)

```
docIDs [3, 8, 12, 30]  raw = 4 × 4-byte int = 16 bytes

gaps  = [3, 8−3, 12−8, 30−12] = [3, 5, 4, 18]   (all small)

varbyte: 1 byte = 1 continuation bit + 7 data bits → holds 0–127
max(gaps) = 18 < 128  ⇒ each gap = 1 byte ⇒ 4 bytes total

16 bytes → 4 bytes  =  4× compression
```

## L4
- **Binary vs graded relevance — which metrics need graded qrels and why? Show on one ranking how the gain 2^rel−1 separates a “highly relevant” hit from a “mildly relevant” one.**
  Precision, Recall, MRR and MAP collapse every judgment to relevant/not, so they only need binary qrels and cannot tell a perfect hit from a merely okay one. nDCG needs graded judgments because its gain function rewards higher grades super-linearly — the exponential gain 2^rel−1 maps grades 0/1/2/3 to gains 0/1/3/7, so a grade-3 doc is worth 7× a grade-1 doc, not 3×. That is exactly what lets nDCG distinguish “put the perfect answer first” from “put a so-so answer first.”

```
grade rel :  0    1    2    3
linear gain (=rel)        : 0    1    2    3
exponential gain 2^rel−1  : 0    1    3    7

so a grade-3 hit is worth 7×, not 3×, a grade-1 hit
binary metrics (P,R,MRR,MAP) would score both as just "relevant=1"
(scale shown 0/1/2/3; this course usually grades 0/1/3 — same exponential idea)
```

- **For the ranking with relevance pattern [1,0,1,1,0] and 4 relevant docs total (one not retrieved), compute P@3, P@5, R@5, and the reciprocal rank for MRR.**
  P@k = (#relevant in top-k)/k. Top-3 has 2 relevant → P@3 = 2/3 ≈ 0.667; top-5 has 3 relevant → P@5 = 3/5 = 0.6. R@k = (#relevant in top-k)/(total relevant). With 4 relevant overall, R@5 = 3/4 = 0.75 — the fourth relevant doc was never retrieved, so recall is capped below 1. The reciprocal rank is 1/(rank of first relevant); the first hit is at rank 1, so RR = 1/1 = 1.0, and MRR is the mean of RR across queries (here a single query → 1.0).

```
ranking relevance = [1, 0, 1, 1, 0]      total relevant R = 4

P@3 = (#rel in top-3)/3 = 2/3 = 0.6667
P@5 = (#rel in top-5)/5 = 3/5 = 0.6000
R@5 = (#rel in top-5)/R = 3/4 = 0.7500   (4th relevant never retrieved)

first relevant at rank 1  →  RR = 1/1 = 1.0
MRR = mean of RR over queries
```

- **Compute nDCG@4 by hand for graded ranking [2,0,3,1] using exponential gain 2^rel−1 and discount log₂(i+1): DCG → IDCG (ideal order) → ratio.**
  DCG = Σᵢ (2^relᵢ−1)/log₂(i+1). For \[2,0,3,1]: rank 1 gives 3/1 = 3.0, rank 2 gives 0, rank 3 gives 7/2 = 3.5, rank 4 gives 1/2.3219 = 0.4307, so DCG = 6.9307. The ideal ranking sorts grades descending \[3,2,1,0]: IDCG = 7/1 + 3/1.585 + 1/2 + 0 = 7.0 + 1.8928 + 0.5 = 9.3928. nDCG = 6.9307/9.3928 ≈ 0.7379 — a single comparable score in \[0,1]. It is below 1 mainly because the best doc (grade 3) sits at rank 3 instead of rank 1, where the discount is gentlest.

```
grades g = [2, 0, 3, 1]    gain = 2^rel − 1,   discount = log2(i+1)

rank 1: (2^2−1)/log2(2) = 3/1.0000 = 3.0000
rank 2: (2^0−1)/log2(3) = 0/1.5850 = 0.0000
rank 3: (2^3−1)/log2(4) = 7/2.0000 = 3.5000
rank 4: (2^1−1)/log2(5) = 1/2.3219 = 0.4307
DCG = 3.0000 + 0 + 3.5000 + 0.4307 = 6.9307

ideal order (sort grades desc) = [3, 2, 1, 0]:
rank 1: 7/1.0000 = 7.0000
rank 2: 3/1.5850 = 1.8928
rank 3: 1/2.0000 = 0.5000
rank 4: 0/2.3219 = 0.0000
IDCG = 9.3928

nDCG = DCG/IDCG = 6.9307/9.3928 = 0.7379
(grades on the 0–3 scale, grade 2 included; the deck examples often use {0,1,3})
```

- **Compute AP for two queries and then MAP. Q1 = [0,1,0,1,0,1,0,1], Q2 = [1,0,1,1,0,0,1,0], each with 4 relevant docs. AP averages P@k at each relevant-doc rank.**
  AP = (1/R)·Σ over relevant ranks r of P@r. Q1’s hits are at ranks 2,4,6,8, where precisions are 1/2, 2/4, 3/6, 4/8 — all exactly 0.5 — so AP₁ = (0.5·4)/4 = 0.5. Q2’s hits are front-loaded at ranks 1,3,4,7 with precisions 1/1, 2/3, 3/4, 4/7 = 1.0, 0.6667, 0.75, 0.5714, giving AP₂ = (1.0+0.6667+0.75+0.5714)/4 = 0.747. MAP is the mean of the per-query APs: (0.5+0.747)/2 = 0.6235 — equal to neither AP, and AP rewards placing relevant docs early (Q2 > Q1 despite the same count).

```
Q1 = [0,1,0,1,0,1,0,1]   R = 4   hits at ranks 2,4,6,8
  P@2=1/2=0.5  P@4=2/4=0.5  P@6=3/6=0.5  P@8=4/8=0.5
  AP1 = (0.5+0.5+0.5+0.5)/4 = 0.5

Q2 = [1,0,1,1,0,0,1,0]   R = 4   hits at ranks 1,3,4,7
  P@1=1/1=1.0  P@3=2/3=0.6667  P@4=3/4=0.75  P@7=4/7=0.5714
  AP2 = (1.0+0.6667+0.75+0.5714)/4 = 0.747

MAP = (AP1 + AP2)/2 = (0.5 + 0.747)/2 = 0.6235
```

- **You beat BM25 by +2% nDCG — is it real? Which test, what does p mean, and how does per-query variance decide it? Sketch a paired comparison on a few queries.**
  Use a paired significance test on the per-query scores. The most defensible in IR is the randomization / permutation test (Smucker, Allan & Carterette) — it assumes almost nothing about the score distribution; the paired t-test and the Wilcoxon signed-rank test are common, faster approximations. They are paired because each query runs through both systems, so you analyse the per-query differences, which removes query-difficulty noise. p is the probability of seeing a difference this large (or larger) if the two systems were truly equal; small p (e.g. < 0.05) means the gap is unlikely to be chance. The verdict hinges on variance: a +2% mean with tiny, consistently-positive per-query deltas is significant, but the same +2% with deltas swinging ±20% across queries is not. Testing many variants inflates false positives — correct for it.

```
per-query nDCG (new − BM25):  +0.03  +0.01  +0.02  +0.02  +0.02
  mean Δ = +0.02   sd ≈ 0.007   → tight & all positive → likely significant

contrast:  +0.22  −0.18  +0.20  −0.16  +0.02
  mean Δ = +0.02   sd ≈ 0.20    → huge swings → NOT significant

randomization/permutation (preferred · Smucker–Allan–Carterette):
  shuffle which system each query is credited to, many times;
  p = fraction of shuffles with |mean Δ| ≥ the observed |mean Δ|
paired t:  t = mean(Δ) / (sd/√n);   small p ⇒ gap unlikely under H0 (systems equal)
Wilcoxon signed-rank: ranks of |Δ|, no normality assumption
```

- **Why do offline metrics + click logs mislead (position bias), and what does an A/B test add? What does interleaving / IPS fix?**
  Clicks are biased by rank: a document gets clicked partly because it sits at the top, not only because it is the best answer, so click-through is not ground truth and offline metrics computed from logged clicks inherit that bias. An A/B test measures real user behaviour under each system on live traffic, so it captures actual satisfaction rather than a proxy. Interleaving blends two rankers’ results into one list and attributes each click to the ranker that contributed the item — far more sensitive per user than A/B. Inverse-Propensity Scoring (IPS) reweights each click by 1/P(examined at that rank) to debias the logs directly.

```
logged CTR by rank:  r1=8%  r2=5%  r3=3% ...  (decays even for equally-relevant docs)
→ a doc clicked at r1 may just be top, not best  (position bias)

IPS: weight click by 1/P(examine | rank).
  click at r1, P=0.8 → weight 1/0.8 = 1.25
  click at r3, P=0.3 → weight 1/0.3 = 3.33   (rare-examination clicks count more)

interleaving: merge A,B into one list; click → credit to the source ranker
```