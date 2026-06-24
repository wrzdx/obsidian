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