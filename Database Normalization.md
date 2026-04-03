
>[!summary] Informal Design Guidelines for Relational DB 
>- Each tuple in a relation should represent one entity or relationship instance
>- Relations should be designed such that their tuples will have as few NULL values as possible
>- The lossless join property ensures that JOIN operations produce meaningful and accurate results

## Functional Dependencies
A functional dependency X → Y holds if whenever two tuples have the same value for X, they must also have the same value for Y. In other words, X uniquely determines Y.

The constraint must hold for every relation instance r(R). 

The functional dependency must be true for all possible valid states of the table, not just the current data.

  If K is a key of R, then K functionally determines all attributes in R.

