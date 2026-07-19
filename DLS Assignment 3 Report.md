# Assignment 3 — RAG Retrieval and Evaluation

 **Dataset:** EnterpriseRAG-Bench · **Questions:** 200 · **Documents:** 3,050 · **Main index:** 14,886 chunks  
 **Encoder:** `all-MiniLM-L6-v2` · **Seed:** 20260605 · **Cutoff:** $K=10$

## 1. Experimental setup

The fixed subset is stratified by `question_type`: the first 20 questions of every type are selected in `question_id` order, then the first remaining questions fill the subset to 200. It contains 30 `basic` questions, 20 questions from each of eight other answerable or unanswerable categories, and 10 `high_level` questions.

The document split is streamed. A seed-fixed reservoir retains at most 300 documents per referenced source type, and every document in `expected_doc_ids` is added independently of sampling. Thus no gold document is dropped. The resulting corpus contains 3,050 documents.

All dense vectors are L2-normalized, so cosine similarity is a dot product:

$$
s(q,c)=\frac{e_q^\top e_c}{\lVert e_q\rVert_2\lVert e_c\rVert_2}=e_q^\top e_c.
$$

The main retrieval index uses recursive chunks of 256 words with overlap 32. It contains 14,886 chunks.

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

Plain dense retrieval ranks chunks using the original question vector. Multi-query uses the original question and three fixed, deterministic rewrites committed with the submission. A chunk receives its best score across the four runs:

$$
s_{\text{multi}}(c)=\max_j e_{q_j}^{\top}e_c.
$$

HyDE embeds a deterministic hypothetical enterprise passage and retrieves real chunks near it:

$$
s_{\text{HyDE}}(c)=e_h^\top e_c.
$$

The gold answer and answer facts are never used to form a retrieval query.

### RAG Fusion

The same four query rankings are fused by Reciprocal Rank Fusion with $k=60$:

$$
\operatorname{RRF}(d)=\sum_{r\in\mathcal R}\frac{1}{60+\operatorname{rank}_r(d)}.
$$

---

## 3. Metrics

The retrieval unit is a chunk. A chunk has binary relevance when its parent is in `expected_doc_ids`, so nDCG uses gains $2^{rel}-1\in\{0,1\}$. Recall counts distinct gold parent documents reached by the top ten chunks. For context precision, repeated parent documents are collapsed at their first occurrence as required by the assignment.

$$
\operatorname{MRR@K}=\frac{1}{|Q|}\sum_{q\in Q}\frac{1}{\operatorname{rank}_q},
$$

$$
\operatorname{DCG@K}=\sum_{i=1}^{K}\frac{2^{rel_i}-1}{\log_2(i+1)},
\qquad
\operatorname{nDCG@K}=\frac{\operatorname{DCG@K}}{\operatorname{IDCG@K}}.
$$

Context precision is AP@10 over the deduplicated document ranking:

$$
\operatorname{CP@K}=\frac{1}{\min(|G|,K)}
\sum_{i=1}^{K}P(i)\,rel_i.
$$

Generator-free context recall uses the same rule in every experiment: a gold answer fact is present when its maximum cosine similarity to a retrieved chunk is at least $0.6$.

$$
\operatorname{CR@K}=\frac{1}{|F|}\sum_{f\in F}
\mathbb{1}\left[\max_{c\in C_K}\cos(e_f,e_c)\ge0.6\right].
$$

For `info_not_found`, document and fact metrics are undefined. Abstention is reported instead: the top-ranked chunk is treated as insufficiently confident when the original-question cosine to that chunk is below $\tau=0.35$.

---

## 4. Chunking and the recall floor

| Method    | Size | Overlap | Chunks | Fact recall floor |
| --------- | ---: | ------: | -----: | ----------------: |
| Fixed     |  128 |       0 |  2,444 |            0.3238 |
| Fixed     |  128 |      32 |  3,089 |            0.3541 |
| Fixed     |  128 |      64 |  4,367 |            0.3889 |
| Recursive |  128 |       0 |  2,878 |            0.3782 |
| Recursive |  128 |      32 |  3,814 |            0.3836 |
| Recursive |  128 |      64 |  5,521 |        **0.4193** |
| Fixed     |  256 |       0 |  1,304 |            0.2435 |
| Fixed     |  256 |      32 |  1,428 |            0.2525 |
| Fixed     |  256 |      64 |  1,579 |            0.2632 |
| Recursive |  256 |       0 |  1,410 |            0.2533 |
| Recursive |  256 |      32 |  1,585 |        **0.2703** |
| Recursive |  256 |      64 |  1,778 |            0.2774 |
| Fixed     |  512 |       0 |    738 |            0.1918 |
| Fixed     |  512 |      32 |    761 |            0.1909 |
| Fixed     |  512 |      64 |    776 |            0.1855 |
| Recursive |  512 |       0 |    773 |            0.1918 |
| Recursive |  512 |      32 |    788 |            0.1820 |
| Recursive |  512 |      64 |    813 |            0.1909 |

![[assignment3_chunking.png|center|700]]

For a document of $L$ words, fixed-size chunk count is

$$
n_{\text{chunks}}=\left\lceil\frac{L-o}{s-o}\right\rceil,
$$

where $s$ is chunk size and $o$ is overlap. Recursive 128/64 gives the highest measured floor, but also produces the largest index. The selected 256/32 configuration has a recall floor of **0.2703** under the fixed fact-match rule. This is the measured upper bound on answer-fact coverage before retrieval errors are introduced.

A boundary case makes the mechanism concrete. For the fact *“Redwood proposed a 50,000 one-time onboarding or migration credit tied to milestones”*, maximum similarity is 0.5674 at overlap 0 and 0.6170 with a small overlap. The fact therefore changes from absent to present at the fixed threshold $0.6$.

Large chunks consistently reduce the floor. They preserve more local context but mix the target fact with unrelated text, diluting the fact–chunk embedding similarity. Overlap helps at 128 and 256, although its benefit is not monotonic at 512.

---

## 5. Retrieval results

The table gives macro means over the eight answerable categories that have document ground truth. `high_level` and `info_not_found` are handled separately below.

| Method | Recall@10 | MRR@10 | nDCG@10 | Context P@10 | Context R@10 |
|---|---:|---:|---:|---:|---:|
| BM25 | **0.9154** | **0.9281** | **0.7266** | **0.8692** | 0.2150 |
| Plain dense | 0.7641 | 0.7448 | 0.5093 | 0.6637 | 0.2160 |
| Multi-query | 0.7655 | 0.7139 | 0.4971 | 0.6354 | **0.2304** |
| HyDE | 0.7092 | 0.6568 | 0.4312 | 0.5686 | 0.2153 |
| RAG Fusion | 0.7211 | 0.6873 | 0.4645 | 0.6053 | 0.2147 |

![[assignment3_methods.png|center|700]]

Relative to plain dense retrieval, multi-query changes Recall@10 by $+0.0014$ and context recall by $+0.0144$, but decreases MRR by $-0.0309$, nDCG by $-0.0123$, and context precision by $-0.0283$. The extra variants recover a few facts but also promote irrelevant enterprise documents. RAG Fusion and HyDE do not produce a lift on the macro document metrics.

The vocabulary gap explains this result. Many questions already contain exact project names, metric identifiers, API terms, and policy wording present in the source. BM25 exploits these rare terms directly. Generic rewrites add broad expressions such as “enterprise record”, “policy”, and “procedure”; HyDE adds still more generic answer-like language. These changes can move the embedding toward topically similar but incorrect chunks.

---

## 6. Results by question type

Each cell below is **context precision / context recall**. A dash means that context precision is undefined because `expected_doc_ids` is empty. The accompanying heatmaps show the same values without hiding category variation.

| Question type            |         BM25 |       Plain | Multi-query |         HyDE |  RAG Fusion |
| ------------------------ | -----------: | ----------: | ----------: | -----------: | ----------: |
| basic                    |  .922 / .275 | .710 / .340 | .690 / .340 |  .681 / .339 | .707 / .357 |
| completeness             |  .652 / .413 | .399 / .345 | .444 / .394 |  .392 / .432 | .363 / .361 |
| conflicting_info         |  .933 / .095 | .618 / .076 | .609 / .085 |  .579 / .071 | .627 / .085 |
| constrained              |  .952 / .254 | .938 / .279 | .900 / .282 |  .871 / .282 | .904 / .279 |
| intra_document_reasoning | 1.000 / .079 | .583 / .133 | .576 / .133 |  .538 / .079 | .538 / .121 |
| miscellaneous            | 1.000 / .170 | .975 / .183 | .842 / .183 |  .663 / .183 | .710 / .183 |
| project_related          |  .876 / .311 | .730 / .315 | .746 / .320 |  .668 / .271 | .696 / .297 |
| semantic                 |  .618 / .124 | .356 / .056 | .277 / .106 |  .158 / .065 | .298 / .035 |
| high_level               |     — / .150 |    — / .507 |    — / .465 | — / **.590** |    — / .412 |

![[assignment3_categories.png|center|800]]

The aggregate result hides two different behaviours. BM25 dominates document precision, especially on identifiers and exact terminology. Dense methods can retrieve answer-like evidence without recovering the annotated parent document: this is most visible for `high_level`, where HyDE reaches context recall 0.590. `completeness` remains the hardest category for retrieving all facts because the answer is distributed across multiple pieces of evidence.

### Abstention and control

| Method | Basic abstention | Basic mean top-1 sim. | `info_not_found` abstention | `info_not_found` mean top-1 sim. |
|---|---:|---:|---:|---:|
| BM25 | 0.000 | 0.584 | **0.300** | 0.439 |
| Plain dense | 0.000 | 0.639 | 0.000 | 0.551 |
| Multi-query | 0.000 | 0.629 | 0.000 | 0.534 |
| HyDE | 0.000 | 0.630 | 0.000 | 0.517 |
| RAG Fusion | 0.000 | 0.631 | 0.000 | 0.537 |

![[assignment3_abstention.png|center|700]]

At $\tau=0.35$, no method abstains on the `basic` control. BM25 abstains on 6 of 20 unanswerable questions, while every dense or rewrite-based method returns a confident result for all 20. The cosine gap between answerable and unanswerable questions is real but insufficiently calibrated at this threshold.

---

## 7. Statistical significance

Multi-query has the highest macro context recall among rewrite methods, so its per-query context precision is compared with BM25 on the 170 answerable questions with document ground truth.

| Statistic | Value |
|---|---:|
| Mean difference, multi-query $-$ BM25 | $-0.2337$ |
| 95% confidence interval | $[-0.2874,-0.1800]$ |
| Paired t-test p-value | $5.59\times10^{-15}$ |
| Wilcoxon p-value | $2.63\times10^{-13}$ |

Both tests reject equal average context precision in favour of BM25. Statistical significance is necessary but not sufficient: it does not establish practical usefulness, robustness outside this fixed subset, or correctness of the metric itself. The contender was selected after examining several rewrite and chunking configurations, so uncorrected $p$-values are optimistic under multiple comparisons. A confirmatory run should pre-register one configuration or correct for the number of tested alternatives.

---

## 8. Judge audit and Goodhart check

The audit uses `Qwen2.5-7B-Instruct-Q4_K_M`, frozen at temperature 0 and seed 20260605. It selects 20 questions with gold answers. For position bias, each gold answer is paired with a fact-preserving paraphrase and evaluated in both A/B orders. For verbosity bias, the same gold answer is paired with a longer version containing on-topic filler but no additional answer fact. The fixed prompt scores relevance, grounding, and completeness from 1 to 5 and accepts only `A`, `B`, or `TIE` in a one-line format.

| Measurement | Empirical rate |
|---|---:|
| Position-follow rate | 0.000 |
| Tie decisions on paraphrase pairs | 0.925 |
| Longer-answer win rate | 0.025 |
| Swap-and-average consistent-winner rate | 0.000 |
| Position rate after swap-and-average | 0.000 |
| Position-rate reduction | 0.000 |
| Invalid-output rate | 0.000 |

All 80 comparison outputs were valid. Across the 40 paraphrase-order runs, the judge returned `TIE` 37 times and never followed the same display position in both orderings. Consequently, no position bias was measured and swap-and-average had nothing to reduce. This is a valid zero effect rather than evidence that position bias is impossible for other prompts or models.

Across the 40 verbosity-order runs, the longer answer won once, the shorter gold answer won 19 times, and 20 comparisons were ties. The measured longer-answer win rate is therefore $1/40=0.025$. Under this rubric and model, explicit instructions to ignore length prevented a verbosity preference and instead produced a mild preference for the unpadded answer.

Swap-and-average counts a winner only when the same underlying answer wins in both orderings. A pure preference for the A or B position therefore becomes inconsistent after swapping and is discarded. None of the position pairs produced a consistent non-tie winner, so the consistent-winner rate is also zero.

The manual Goodhart check compares an honest answer $A$ with a padded answer $C$:

$$
A=\frac{5+5+3}{3}=4.3333,
\qquad
C=\frac{4+3+5}{3}=4.0.
$$

With completeness counted twice,

$$
C'=\frac{4+3+2\cdot5}{4}=4.25.
$$

The requested numerical values do not actually flip the winner: $4.3333>4.25$. They do move the padded answer substantially closer without changing either answer. A true flip would require a slightly larger completeness weight or different component scores. This exposes the intended Goodhart point without making the false claim that $4.25$ exceeds $4.3333$: rubric weights are an attack surface, and optimization can reward padding rather than better evidence.

---

## 9. Conclusion

Quality is first limited by chunk reachability: the selected chunking exposes only 0.2703 of gold answer facts under the fixed semantic match rule. Retrieval then lowers usable coverage further. Overlap repairs some boundary failures, while large chunks dilute fact similarity.

BM25 remains the strongest document retriever for this enterprise subset because exact names and identifiers carry unusually high signal. Multi-query provides a small context-recall gain over plain dense retrieval but sacrifices ranking precision; HyDE is useful mainly on `high_level` questions. Dense similarity is also poorly calibrated for abstention.

Document retrieval, fact coverage, abstention, and judge behaviour therefore need separate evaluation. Optimizing one combined score would conceal where an error entered the pipeline and would invite overfitting to an unaudited judge.
