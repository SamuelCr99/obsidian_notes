20231130 - 11:23

Status: #idea

Tags:

# Quicksort
Efficient divide and conquer algorithm for sorting. Expected $O(n log(n))$, worst case $O(n^2)$. A typical las vegas algorithm. 

### Slow Quicksort
We choose splitter but only accept the splitter if it is central. 

Def: A subproblem is of type j if it contains between $(\frac{3}{4})^{j+1}n$ and $(\frac{3}{4})^{j}n$ elements. All subproblems of type j are pairwise disjoint. For all j: O(n) expected time is needed on all subproblems of type j. O(log n) different types j. This gives us an expected time of O(n log n). Now as we know that the expected time of slow quicksort is O(n log n) we can also conclude that the expected time of normal quicksort must be atleast $O(n log n)$.

\-\-\-
# References