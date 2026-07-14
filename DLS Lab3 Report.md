# Lab 3 — Approximate Nearest-Neighbour Search

**Setup.** EnterpriseRAG-Bench, the first 30 questions sorted by `question_id`, one source slice with 5,030 documents (all gold documents included), and normalized `all-MiniLM-L6-v2` embeddings. The random seed is `20260605`. Exact cosine top-10 is the reference ranking. IVF uses `nlist = 71`; PQ uses asymmetric distance computation (ADC), and the final configuration uses `m = 8`, `k = 256` with exact reranking of the best 100 candidates.

## Trade-off table

| Method | Recall@10 | Fraction scanned | Bytes/vector | Compression |
|---|---:|---:|---:|---:|
| Exact | 1.0000 | 1.0000 | 1536 | 1× |
| IVF (`nprobe=16`) | 0.9467 | 0.2331 | 1536 | 1× |
| PQ + exact rerank | 0.8933 | 1.0000 | 8 | 192× |
| IVF-PQ | 0.8767 | 0.2331 | 8 | 192× |

````col
```col-md
flexGrow=1
===
## IVF recall/work

![C:\Users\Professional\Desktop\Projects\dls\labs\outputs\lab3\lab3_ivf_sweep.png](file:///c%3A/Users/Professional/Desktop/Projects/dls/labs/outputs/lab3/lab3_ivf_sweep.png)

```
```col-md
flexGrow=1
===
## PQ memory/recall

![C:\Users\Professional\Desktop\Projects\dls\labs\outputs\lab3\lab3_pq_memory.png](file:///c%3A/Users/Professional/Desktop/Projects/dls/labs/outputs/lab3/lab3_pq_memory.png)

```
````

## Analysis

Increasing `nprobe` gives a smooth recall/work trade-off: recall@10 rises from 0.5100 at `nprobe=1` to 0.9467 at `nprobe=16`, while only 23.31% of the vectors are scored. Scanning every list recovers exact search, so `nprobe=16` is the useful knee. The observed boundary miss occurs because a true neighbour lies in cell 63 while the query probes adjacent cell 10; probing more cells removes this coarse-quantization error. For PQ, larger `m` and `k` reduce quantization error at the cost of longer codes: `(4,16)` uses 2 bytes/vector but reaches only 0.3900 recall, whereas `(16,256)` reaches 0.9500 with 16 bytes/vector. The selected `(8,256)` setting is a middle point at 8 bytes/vector and 0.8933 recall after reranking. IVF-PQ combines both approximations and therefore loses slightly more recall (0.8767), but it evaluates only 23.31% of the corpus and compresses stored vectors by 192×. Exact reranking recovers many ADC ordering errors, improving the plain PQ result from 0.4100 to 0.8933.

