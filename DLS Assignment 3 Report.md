# Assignment 3 — RAG Retrieval and Evaluation

**Dataset:** EnterpriseRAG-Bench · **Questions:** 200 · **Documents:** 3,050 · **Chunks:** 14,886  
**Encoder:** all-MiniLM-L6-v2 · **Seed:** 20260605 · **Cutoff:** $K=10$

## 1. Experimental setup

The evaluation uses a deterministic stratified subset of 200 questions. Up to 20 questions are selected from every *question_type*, and the remaining positions are filled in sorted *question_id* order. The final subset contains 30 basic questions, 20 questions from each of eight categories, and 10 high-level questions.

The document split is read in streaming mode. For every source type, a seed-fixed reservoir retains at most 300 documents, while every document listed in *expected_doc_ids* is always included. This produces a corpus of 3,050 documents without loading the full collection into memory.

All dense vectors are L2-normalized, so cosine similarity is evaluated as a dot product:

$$
s(q,c)=\frac{e_q^\top e_c}{\lVert e_q\rVert_2\lVert e_c\rVert_2}=e_q^\top e_c.
$$

The main run uses recursive chunks of 256 words with an overlap of 32 words. This produced 14,886 chunks.

---

## 2. Retrieval and recombination

### BM25

BM25 is implemented directly with $k_1=1.5$ and $b=0.75$:

$$
\operatorname{BM25}(q,d)=\sum_{t\in q}\operatorname{idf}(t)
\frac{tf(t,d)(k_1+1)}
{tf(t,d)+k_1\left(1-b+b\frac{|d|}{\operatorname{avgdl}}\right)},
$$

$$
\operatorname{idf}(t)=\ln\left(1+\frac{N-df(t)+0.5}{df(t)+0.5}\right).
$$

### Dense retrieval, multi-query and HyDE

Plain dense retrieval ranks chunks using the original question vector. Multi-query uses the original question, a keyword-oriented rewrite, and an enterprise-record rewrite. The variants are recombined by maximum score:

$$
s_{\text{multi}}(c)=\max_j e_{q_j}^{\top}e_c.
$$

HyDE embeds a neutral hypothetical answer passage and ranks real chunks using

$$
s_{\text{HyDE}}(c)=e_h^\top e_c.
$$

The rewrite set is deterministic. The gold answer is never used to create retrieval queries.

### RAG Fusion

The rewrite rankings are combined using Reciprocal Rank Fusion with $k=60$:

$$
\operatorname{RRF}(d)=\sum_{r\in\mathcal R}\frac{1}{60+\operatorname{rank}_r(d)}.
$$

---

## 3. Metrics

All metrics are implemented directly. Before document-level evaluation, chunks are mapped back to their parent documents and repeated parents are removed.

$$
\operatorname{MRR@K}=\frac{1}{|Q|}\sum_{q\in Q}\frac{1}{\operatorname{rank}_q}.
$$

For nDCG, the gain is $2^{rel}-1$:

$$
\operatorname{DCG@K}=\sum_{i=1}^{K}\frac{2^{rel_i}-1}{\log_2(i+1)},
\qquad
\operatorname{nDCG@K}=\frac{\operatorname{DCG@K}}{\operatorname{IDCG@K}}.
$$

Context precision is computed as AP@10 over the deduplicated parent-document ranking:

$$
\operatorname{CP@K}=\frac{1}{\min(|G|,K)}
\sum_{i=1}^{K}P(i)\,rel_i.
$$

Generator-free context recall checks whether each gold answer fact appears in at least one retrieved chunk, using $\tau=0.6$:

$$
\operatorname{CR@K}=\frac{1}{|F|}\sum_{f\in F}
\mathbb{1}\left[\max_{c\in C_K}\cos(e_f,e_c)\ge\tau\right].
$$

For *info_not_found*, a result is treated as an abstention when its highest retrieval score is below $0.35$.

---

## 4. Chunking experiment

| Method    | Size | Overlap | Chunks | Fact recall floor |
| --------- | ---: | ------: | -----: | ----------------: |
| Fixed     |  128 |       0 |  2,444 |            0.3238 |
| Recursive |  128 |       0 |  2,878 |            0.3782 |
| Fixed     |  128 |      32 |  3,089 |            0.3541 |
| Recursive |  128 |      32 |  3,814 |        **0.3836** |
| Fixed     |  256 |       0 |  1,304 |            0.2435 |
| Recursive |  256 |       0 |  1,410 |            0.2533 |
| Fixed     |  256 |      32 |  1,428 |            0.2525 |
| Recursive |  256 |      32 |  1,585 |            0.2703 |
| Fixed     |  512 |       0 |    738 |            0.1918 |
| Recursive |  512 |       0 |    773 |            0.1918 |
| Fixed     |  512 |      32 |    761 |            0.1909 |
| Recursive |  512 |      32 |    788 |            0.1820 |

![Chunking method, size and overlap comparison|center|700](file:///c%3A/Users/Professional/Desktop/Projects/dls/labs/outputs/assignment3/assignment3_chunking.png)

For a document of $L$ words, the number of fixed-size chunks is

$$
n_{\text{chunks}}=\left\lceil\frac{L-o}{s-o}\right\rceil,
$$

where $s$ is the chunk size and $o$ is the overlap.

The best generator-free recall floor came from recursive chunking with size 128 and overlap 32. Larger chunks contained more unrelated text, which reduced fact-level cosine similarity. A clear boundary example was also observed. For the fact *“Redwood proposed a 50,000 one-time onboarding or migration credit tied to milestones”*, overlap raised similarity from 0.5674 to 0.6170, crossing the $0.6$ threshold.

The main retrieval comparison uses 256/32. It retains more context in each chunk and gives a smaller index than 128/32.

---

## 5. Retrieval results

The table contains macro means over answerable categories with document ground truth. The *high_level* and *info_not_found* categories are analysed separately because they require different metrics.

| Method      |  Recall@10 |     MRR@10 |    nDCG@10 | Context P@10 | Context R@10 |
| ----------- | ---------: | ---------: | ---------: | -----------: | -----------: |
| BM25        | **0.9184** | **0.9277** | **0.7219** |   **0.8723** |       0.2186 |
| Plain dense |     0.7662 |     0.7428 |     0.5058 |       0.6664 |       0.2232 |
| Multi-query |     0.7653 |     0.7110 |     0.4938 |       0.6363 |   **0.2335** |
| HyDE        |     0.7126 |     0.6581 |     0.4303 |       0.5752 |       0.2226 |
| RAG Fusion  |     0.7450 |     0.7077 |     0.4789 |       0.6317 |       0.2246 |

![Retrieval method comparison|center|700](file:///c%3A/Users/Professional/Desktop/Projects/dls/labs/outputs/assignment3/assignment3_methods.png)

BM25 was the strongest method on every document-level metric. Multi-query gave the highest context recall, but the difference from plain dense retrieval was small and its context precision was lower. HyDE performed worst among the dense variants.

Many enterprise questions already contain the same names, identifiers and terminology as the source documents. The generic rewrites added common terms such as “policy” and “procedure”, which often moved the embedding toward unrelated chunks. In this experiment, rewriting was not an automatic improvement.

---

## 6. Category analysis and abstention

The *high_level* questions contain answer facts but no *expected_doc_ids*. Because of this, document recall, nDCG and context precision are undefined for that category. Only fact-based context recall is used for that category.

For *info_not_found*, the abstention rate is reported:

| Method | Abstention rate, $\tau=0.35$ |
|---|---:|
| BM25 | **0.300** |
| Plain dense | 0.000 |
| Multi-query | 0.000 |
| HyDE | 0.000 |
| RAG Fusion | 0.000 |

BM25 abstained on 6 of the 20 unanswerable questions. Every dense or rewrite-based method returned a result for all 20 questions. This suggests that semantic similarity alone was not well calibrated for deciding that the corpus did not contain an answer.

---

## 7. Statistical significance

Multi-query was the strongest rewrite method by context recall, so its per-query context precision is compared with BM25 on 170 answerable questions.

| Statistic | Value |
|---|---:|
| Mean difference, multi-query $-$ BM25 | $-0.2360$ |
| 95% confidence interval | $[-0.2899,-0.1822]$ |
| Paired t-test p-value | $3.87\times10^{-15}$ |
| Wilcoxon p-value | $2.12\times10^{-13}$ |

Both tests reject the null hypothesis. The difference is significant in favour of BM25. This is a negative result, but it is reproducible: on this subset, the selected rewrites reduced context precision.

---

## 8. Judge audit and Goodhart check

Final 7B/8B judge measurements are not included. Smaller local models were tested, but they frequently broke the required output format and produced unreliable comparisons; those numbers were therefore excluded. The full evaluation procedure remains implemented: both answer orders, verbosity pairs, and swap-and-average scoring. A suitable fixed 7B/8B local model is required for the final judge run.

The manual Goodhart check compares an honest answer $A$ with a padded answer $C$:

$$
A=\frac{5+5+3}{3}=4.3333,
\qquad
C=\frac{4+3+5}{3}=4.0.
$$

If completeness is counted twice, the padded answer becomes

$$
C'=\frac{4+3+2\cdot5}{4}=4.25.
$$

The score moves toward the padded answer even though neither answer changed. This is a simple example of how optimizing a judge score can reward verbosity or rubric gaming instead of better retrieval.

---

## 9. Conclusion

The main result is that BM25 remained a very strong baseline for enterprise data with exact names and identifiers. Chunk boundaries also mattered: overlap recovered facts split across boundaries, while large chunks diluted semantic similarity. Dense retrieval was overconfident on unanswerable questions, and the tested generic rewrites did not improve retrieval quality.

Document retrieval, fact coverage, abstention and judge behaviour should therefore be evaluated document retrieval, fact coverage, abstention and judge behaviour separately instead of optimizing one combined score.

