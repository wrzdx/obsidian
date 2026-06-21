## Assignment 1: Deeper Experiments on BEIR NF Corpus

### 1. Experimental Setup

All experiments were performed on the BEIR NF Corpus test collection.

Dataset statistics:

| Statistic         | Value |
| ----------------- | ----: |
| Documents         |  3633 |
| Evaluated Queries |   323 |

The following rankers were implemented from scratch:

* Boolean OR
* TF-IDF (cosine similarity)
* BM25
* RRF fusion of BM25 and TF-IDF

The following evaluation metrics were implemented from scratch:

* nDCG@10
* MAP
* MRR

For nDCG@10, graded gain was defined as:
$$2^{rel} - 1$$

and logarithmic discount:

$$\frac{1}{\log_2(rank + 1)}$$

### 2. Ranker Comparison

| Ranker              | Mean nDCG@10 |    MAP |    MRR |
| ------------------- | -----------: | -----: | -----: |
| BM25                |       0.3117 | 0.1475 | 0.5240 |
| RRF (BM25 + TF-IDF) |       0.3096 | 0.1461 | 0.5157 |
| TF-IDF Cosine       |       0.2958 | 0.1395 | 0.4867 |
| Boolean OR          |       0.2206 | 0.1046 | 0.3696 |

![C:\Users\Professional\Desktop\dls\assignment1\outputs\per_query_ndcg_boxplot.svg](file:///c%3A/Users/Professional/Desktop/dls/assignment1/outputs/per_query_ndcg_boxplot.svg)
![C:\Users\Professional\Desktop\dls\assignment1\outputs\per_query_ap_boxplot.svg](file:///c%3A/Users/Professional/Desktop/dls/assignment1/outputs/per_query_ap_boxplot.svg)
![C:\Users\Professional\Desktop\dls\assignment1\outputs\per_query_rr_boxplot.svg](file:///c%3A/Users/Professional/Desktop/dls/assignment1/outputs/per_query_rr_boxplot.svg)

BM25 achieved the best overall retrieval quality across all three evaluation metrics. TF-IDF cosine performed better than the Boolean OR baseline but remained below BM25. RRF produced results close to BM25 but did not outperform it on this dataset.

### 3. BM25 Parameter Study

The BM25 parameter sweep evaluated:

* k1 ∈ {0.5, 1.0, 1.2, 1.5, 2.0, 3.0}
* b ∈ {0, 0.25, 0.5, 0.75, 1.0}

Best parameter combination:

|  k1 |    b | nDCG@10 |    MAP |    MRR |
| --: | ---: | ------: | -----: | -----: |
| 2.0 | 0.75 |  0.3137 | 0.1483 | 0.5295 |

![C:\Users\Professional\Desktop\dls\assignment1\outputs\bm25_k1_sweep_b075.svg](file:///c%3A/Users/Professional/Desktop/dls/assignment1/outputs/bm25_k1_sweep_b075.svg)![C:\Users\Professional\Desktop\dls\assignment1\outputs\bm25_b_sweep_k15.svg](file:///c%3A/Users/Professional/Desktop/dls/assignment1/outputs/bm25_b_sweep_k15.svg)
The best performance was achieved with k1 = 2.0 and b = 0.75. Small values of k1 cause term-frequency saturation too quickly, while large values allow repeated occurrences to contribute too strongly. For the document-length parameter, intermediate values performed better than the extremes b = 0 and b = 1, indicating that partial length normalization is beneficial.

### 4. Tokenization Study

Three tokenization pipelines were evaluated using the best BM25 parameters.

| Pipeline            | Vocabulary | Avg. Doc Length | nDCG@10 |    MAP |    MRR |
| ------------------- | ---------: | --------------: | ------: | -----: | -----: |
| Porter Stemming     |      18935 |          169.76 |  0.3333 | 0.1538 | 0.5395 |
| Stopword Removal    |      26382 |          169.76 |  0.3156 | 0.1474 | 0.5315 |
| Whitespace Baseline |      26472 |          245.79 |  0.3137 | 0.1483 | 0.5295 |

Porter stemming produced the strongest results across all metrics. Stemming reduced vocabulary size and merged morphological variants of terms, which improved retrieval effectiveness. Stopword removal slightly improved ranking quality compared to the baseline by reducing the influence of very common terms. The whitespace tokenizer achieved the weakest performance among the three tokenization strategies.

### 5. Statistical Significance

The best-performing system (BM25 with Porter stemming) was compared against the BM25 whitespace baseline using per-query nDCG@10 scores.

| Statistic             |     Value |
| --------------------- | --------: |
| Mean Difference       |    0.0196 |
| 95% CI Lower Bound    |    0.0080 |
| 95% CI Upper Bound    |    0.0312 |
| Paired t-test p-value | 0.0009466 |
| Wilcoxon p-value      |  0.002416 |

The improvement obtained by Porter stemming is statistically significant according to both tests. The confidence interval does not include zero, and both p-values are below 0.01. This suggests that the observed improvement is unlikely to be caused by random variation in the query set.

### 6. Discussion

The experiments show that BM25 remains the strongest individual lexical ranking model on NF Corpus. The parameter sweep demonstrates that both term-frequency saturation and document-length normalization influence retrieval quality. The tokenization study shows that document representation is also important, as stemming noticeably improved performance. Finally, the significance tests indicate that the improvement obtained through stemming is statistically reliable. Overall, the results suggest that retrieval quality depends not only on the ranking formula itself but also on how terms are represented and weighted within the retrieval system.
