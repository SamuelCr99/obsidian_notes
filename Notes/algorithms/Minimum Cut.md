20231120 - 14:25

Status: #idea

Tags: [[Algorithms]] [[Randomized Algorithms]]

# Minimum Cut
There are a number of different minimum cut problems.
## Global Minimum Cut
Given a undirected graph G. Partition G into two sets A and B. And minimize the number of edges that connect A and B. This is almost normal [[Minimum Cut]] but here we do not have starts and sinks. 

One approach would be to have A as only one node. In this case the number of connections would be the connections of this node. 

One solution would be to fix a node and call it the source, then try all other possible nodes as a sink and then use  normal [[Minimum Cut]]. This will take a lot of time. 

We will allow parallel edges but no loops. 

We use an operation we call contraction. 

Algorithm: Contract an edge chosen at random. Then do this n-2 times. 

Analysis: (A,B): some minimum cut. F: Set of edges between A and B. k = |F|. Now consider graph after j steps, it now has n-j nodes. The minimum degree is at least k. Hence $\geq \frac{1}{2} * l(n-j)$ edges. Some edge F is contracted, with probability $\leq \frac{2}{n-j}$. The algorithm returns (A,B) with probability $$\geq \Pi_{j=0}^{n-3}(1 - \frac{2}{n-j}) = \Pi_{j=0}^{n-3}\frac{n-j-2}{n-2}=\frac{2}{n(n-1)} > \frac{2}{n^2}$$
So this probability is not very high but we can perform this algorithm many times. This idea is known as algorithm amplification. Repeat algorithm $tn^2$ times. The probability of failure is $\leq (1 - \frac{2}{n^2})^{tn^2}$ which is approximately $e^{-2t}$. 

Algorithms which are run in polynomial time but there are chances of error are called Monte Carlo algorithms. Las Vegas algorithms always give correct result but the running time can be randomly bad, a good example of a Las Vegas algorithm is Quicksort, which normally runs in $O(n log n$) but could become $O(n^2)$. 





\-\-\-
# References