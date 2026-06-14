# BM25 vs TF-IDF on BEIR nfcorpus/test
## Implementation Choices

* Tokenization: lowercase → strip punctuation → split on whitespace.
* TF-IDF: raw term frequency in both query and document.
* TF-IDF IDF variant: $\ln(\frac{N}{df})$.
* Scoring: weighted dot product between query and document term weights.
* BM25 parameters: $k_1 = 1.5$, $b = 0.75$.
* BM25 IDF variant: $\ln(1 + \frac{N - df + 0.5}{df + 0.5})$.
* Evaluation metric: nDCG@10.
* Gain function: $2^{rel} - 1$.
* Discount function: $\frac{1}{\log_2(rank + 1)}$.

## Mean nDCG@10

| Ranker | Mean nDCG@10 |
| ------ | -----------: |
| TF-IDF |       0.2619 |
| BM25   |       0.2789 |

BM25 achieves a higher mean nDCG@10 than TF-IDF on the evaluated query set.

## Divergent Query Example

Query: **PLAIN-112 — Food Dyes and ADHD**

| Rank | TF-IDF Top-10    | BM25 Top-10      |
| ---: | ---------------- | ---------------- |
|    1 | MED-2618 (rel=0) | MED-3380 (rel=2) |
|    2 | MED-3380 (rel=2) | MED-2618 (rel=0) |
|    3 | MED-3383 (rel=0) | MED-2616 (rel=0) |
|    4 | MED-1153 (rel=0) | MED-3382 (rel=2) |
|    5 | MED-2616 (rel=0) | MED-3383 (rel=0) |
|    6 | MED-4655 (rel=0) | MED-4604 (rel=0) |
|    7 | MED-3382 (rel=2) | MED-1153 (rel=0) |
|    8 | MED-4604 (rel=0) | MED-4655 (rel=0) |
|    9 | MED-2992 (rel=0) | MED-2643 (rel=0) |
|   10 | MED-855 (rel=0)  | MED-2992 (rel=0) |

## Analysis

BM25 differs from TF-IDF because it applies term-frequency saturation and document-length normalization. In the TF-IDF ranking, document MED-2618 is placed first even though its relevance label is 0. This document contains many repetitions of query terms such as “dyes”, which increases its score because TF-IDF grows linearly with term frequency. BM25 instead ranks MED-3380 first (relevance label 2). BM25 limits the impact of repeated term occurrences and normalizes scores using document length, reducing the advantage of longer documents. As a result, BM25 places greater emphasis on informative terms such as “ADHD” and promotes the more relevant document. This behavior explains why BM25 achieves a higher nDCG@10 score than TF-IDF for this query and a higher mean nDCG@10 overall.
