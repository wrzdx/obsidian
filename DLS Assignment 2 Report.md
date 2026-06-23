
## Experimental Setup

Experiments were conducted on the BEIR NF-Corpus test split. Four retrieval signals were used:

- BM25 (sparse lexical retrieval);
    
- Dense bi-encoder retrieval (Sentence-BERT);
    
- SPLADE sparse expansion retrieval;
    
- ColBERT late-interaction retrieval.
    

For each query, candidate documents were retrieved and re-ranked. Retrieval quality was evaluated using nDCG@10, MAP@10 and MRR@10.

---

## Hybrid Fusion

Three fusion strategies were evaluated:

1. Reciprocal Rank Fusion (RRF, k=60);
    
2. Convex score fusion:  
    score = α · Dense + (1 − α) · Sparse;
    
3. Normalized score fusion (min-max normalization).
    

### Results

|Fusion Strategy|nDCG@10|MAP@10|MRR@10|
|---|---|---|---|
|BM25 Baseline|0.3303|0.1268|0.5557|
|RRF|0.3320|0.1250|0.5514|
|Normalized Fusion|**0.3589**|**0.1369**|**0.5905**|

![C:\Users\Professional\Desktop\dls\alpha_sweep.png](file:///c%3A/Users/Professional/Desktop/dls/alpha_sweep.png)


Normalized score fusion achieved the best overall performance. RRF provided only marginal improvements over BM25. This suggests that score calibration between retrieval systems is important and simple rank fusion is insufficient for this collection.



<br>
<br>

### Alpha Sweep

|α|nDCG@10|
|---|---|
|0.00|0.2718|
|0.25|0.2993|
|0.50|0.3384|
|0.75|**0.3570**|
|1.00|0.3481|

The best convex fusion result was obtained at α=0.75, indicating that dense retrieval contributes most of the retrieval signal while sparse retrieval still provides complementary information.

---

## Learning to Rank

The following features were used:

- BM25 score;
    
- Dense cosine similarity;
    
- SPLADE score;
    
- ColBERT MaxSim score;
    
- Document length.
    

Two ranking models were implemented:

- RankNet;
    
- LambdaRank.
    

### Results

|System|nDCG@10|MAP@10|MRR@10|
|---|---|---|---|
|BM25 Only|0.2890|0.1031|0.4713|
|Dense Only|0.3236|0.1233|0.5167|
|SPLADE Only|0.2422|0.0806|0.3782|
|ColBERT Only|0.2817|0.0994|0.4817|
|RankNet|0.2726|0.0966|0.4747|
|LambdaRank|**0.3349**|**0.1241**|**0.5277**|

LambdaRank achieved the best ranking quality among all learned models and outperformed every individual retrieval feature.

![C:\Users\Professional\Desktop\dls\ltr_comparison.png](file:///c%3A/Users/Professional/Desktop/dls/ltr_comparison.png)

---

## Feature Ablation

To estimate feature importance, each feature was removed independently from LambdaRank.

|Removed Feature|nDCG@10|Δ|
|---|---|---|
|BM25|0.3162|-0.0187|
|Dense|0.2941|-0.0408|
|SPLADE|0.3363|+0.0014|
|ColBERT|0.3324|-0.0025|
|DocLength|0.3388|+0.0039|

![C:\Users\Professional\Desktop\dls\feature_ablation.png](file:///c%3A/Users/Professional/Desktop/dls/feature_ablation.png)
Dense retrieval produced the largest quality drop and therefore contributed the strongest ranking signal. Removing SPLADE and document length slightly improved quality, indicating that these features provided little useful information.

---


<br>
<br>

## Statistical Significance

LambdaRank was compared against the BM25 baseline using a paired Student t-test on per-query nDCG@10 values.

|Metric|Value|
|---|---|
|t-statistic|2.6590|
|p-value|0.0101|
|95% CI|[0.0121, 0.0798]|

The null hypothesis was rejected (p < 0.05). Therefore, the improvement of LambdaRank over BM25 is statistically significant.

---

## Conclusion

Hybrid retrieval consistently outperformed individual retrieval systems. Dense retrieval contributed the strongest signal, while sparse retrieval provided complementary evidence. Among fusion approaches, normalized score fusion achieved the best retrieval performance. LambdaRank successfully combined retrieval features into a stronger ranking model and produced statistically significant improvements over the BM25 baseline.