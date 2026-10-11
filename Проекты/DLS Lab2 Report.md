### 1. Progress Ladder (mean nDCG@10)

The evaluation was conducted on the first 30 test queries sorted by `query_id` from the BEIR `nfcorpus/test` dataset. The table below presents the performance across the different stages of the retrieval pipeline:

|**Cascade Stage**|**mean nDCG@10**|**Relative Gain (vs. BM25 Baseline)**|
|---|---|---|
|**BM25** (Lexical Baseline)|0.2789|—|
|**Dense** (Bi-Encoder)|0.2815|+0.93%|
|**BM25 + Cross-Encoder** ($k=100$)|**0.2954**|**+5.92%**|
|**Dense + Cross-Encoder** ($k=100$)|0.2938|+5.34%|

**Scout Selection Analysis:** At the maximum depth of $k=100$, the **BM25 lexical Scout provided a slightly better candidate pool for the Cross-Encoder Judge**, achieving a final nDCG@10 of 0.2954 compared to 0.2938 for the Dense Scout. On the medical terminology of `nfcorpus`, explicit keyword overlaps (BM25) ensure that highly specific document IDs remain within the top 100 pool. However, at lower depths ($k \le 50$), the Dense Scout consistently provides a higher-quality short-list to the Judge.

### 2. Reranking Depth Sweep (Cost vs. Quality)
![C:\Users\Professional\Desktop\dls\cascade_sweep.png](file:///c%3A/Users/Professional/Desktop/dls/cascade_sweep.png)

The ranking pool depth $k$ determines the computational load (exactly $k$ Cross-Encoder forward passes per query).

- **Point of Diminishing Returns:** For the **Dense + Cross-Encoder** configuration, the optimal trade-off occurs exactly at **$k=50$**, yielding a peak nDCG@10 of **0.3085**. Pushing the depth further to $k=100$ decreases performance to 0.2938 due to the model getting distracted by low-quality semantic noise.
    
- For the **BM25 + Cross-Encoder** pipeline, a sharp performance plateau is reached at **$k=10$** (nDCG@10 = 0.2900). Increasing the computational budget tenfold to $k=100$ only yields a marginal improvement (+0.0054).
    
- **Conclusion:** The sweet spot balancing cost and retrieval quality lies within the **$k \in [10, 50]$** range.
    

### 3. Rank Change Case Study (Before vs. After)

- **Query ID:** `PLAIN-1109`
    
- **Query Text:** _"endocrine disruptors"_ * **Document ID:** `MED-2627` (True Relevance Label: 1)
    
- **Rank BEFORE Reranking (BM25 Pool):** 18 (hidden from the user's Top-10)
    
- **Rank AFTER Reranking (Cross-Encoder):** 3 (successfully promoted into the active visibility window)
    

**Why Cross-Encoder Helps:** BM25 evaluates documents independently based on term frequencies. If a relevant document mentions the exact phrase _"endocrine disruptors"_ only once but thoroughly discusses specific chemicals like _bisphenol A_ or _phthalates_, BM25 penalizes its rank. The Cross-Encoder processes the query and the document _simultaneously_ via intense Cross-Attention mechanisms. It maps out deep contextual semantics, recognizes that the granular text directly answers the query's intent, and lifts it from rank 18 to rank 3.

### 4. Why Deep Reranking Saturates

1. **Pool Exhaustion:** Past $k > 50$, the Scout's candidate generator has already exhausted nearly all highly relevant documents. The remaining documents are background noise, meaning the Judge has no actual valuable assets left to pull to the top.
    
2. **Model False Positives:** At extreme depths, the Judge is forced to score hundreds of low-relevance items. Because complex Cross-Encoders are highly sensitive to overlapping contextual sub-topics, they can generate false-positive scores for noisy documents, inadvertently pushing them into the Top-10 and displacing genuinely useful hits.