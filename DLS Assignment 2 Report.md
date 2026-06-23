## 1. Experimental Metrics Table

Below are the aggregated metrics evaluated over the full test queries and the hold-out evaluation split:

|**Evaluation Scope / Model**|**mean nDCG@10**|**mean MAP@10**|**mean MRR@10**|
|---|---|---|---|
|**BM25 Baseline** (Full Test)|0.3058|—|—|
|**RRF Hybrid Fusion** (Full Test)|0.3048|—|—|
|**BM25 Baseline** (Test Split)|**0.3700**|—|—|
|**Handmade LambdaRank** (Test Split)|0.2970|0.2009|0.4382|
![](Pasted%20image%2020260623124733.png)

## 2. Feature Importance & Weights Breakdown

The final learned weight vector for the combination features is:

$$\mathbf{w} = [5.0635,\, 0.6749,\, 1.4529,\, 0.4245,\, 0.2488]$$

Corresponding to `[BM25, Dense, SPLADE, ColBERT, DocLength]` respectively.

- **Analysis:** The model heavily prioritizes the lexical **BM25** score ($w_0 = 5.0635$), confirming that precise token overlaps are the most reliable signal in bio-medical information retrieval (`nfcorpus`). **SPLADE** acts as the secondary strongest contributor ($w_2 = 1.4529$), providing lexical expansion capabilities.
    
- **Overfitting Observation:** The gap between BM25 (0.3700) and LambdaRank (0.2970) on the evaluation split indicates mild optimization overfitting to the training distribution. Without proper feature normalization (e.g., Min-Max or Standard scaling across queries) and regularisation, a basic linear LTR combiner tends to over-rely on raw score distributions seen during training.
