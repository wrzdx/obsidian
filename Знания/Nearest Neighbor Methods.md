- **Assumption:** similar points have similar labels

## k-nearest Neighbor (KNN)
1) Choose a value of $k$
2) Take the $k$ neighbors of the new data point according to Euclidean distance 
3) Among these $k$ neighbor data points, count the number of points in each category
4) Assign the new data points to the category where you counted the most neighbors

### Computational Cost of KNN
1. Number of computations performed at training time: 0
2. For a naïve implementation, the number of computations performed at test time, per new point
	- Total points: 𝑛
	- Number of dimensions: 𝑑
	- Computing 𝑑-dimensional distance for 𝑛 points: 𝑂 𝑛𝑑
	- Sorting the distances: 𝑂 𝑛𝑙𝑜𝑔𝑛
	- Thus an expensive test time algorithm
3. Also, all the data have to be stored in memory
4. Efficiency can be increased using better data structures, such as k-d Trees, or Ball Trees

### Impact of K
- Small 𝑘
	- Good at capturing fine-grained paterns
	- May overfit
- Large 𝑘
	- Makes stable prediction by averaging over a large number of neighbors
	- May underfit
- Balancing 𝑘
	- Optimal choice depend on the number of data points 𝑛
	- Rule of thumb: 𝑘 < $\sqrt{n}$
	- Choose the optimal value using a validation set

