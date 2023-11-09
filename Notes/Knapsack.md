20231106 - 13:17

Status: #idea

Tags:

# Knapsack
We are given: 
W = Capacity
$w_i$ = Weight of item i
$v_i$ = Value of item i

Goal: Find sub set S such that the weight is at most the capacity and the value is maximum. 

Remark: All weight and value is positive whole numbers. 

This is a NP-complete problem. 

This will run in O(nW) time, but note that this is not truly polynomial by input size. 

### One DP solution
We have OPT function. OPT(i, V) := capacity needed to achieve a value $\geq$ V, with a subset of {1,...,i}.

OPT(i, V) = min {OPT(i-1, V), $w_i$+ OPT(i-1, V - max(v-$v_i$, 0))}. $i \leq n, V \leq ny$. The time complexity is $O(n^2y)$. 

### Approximation Algorithm
We will choose a scaling parameter, which we call b. This parameter will be larger than 1. A smaller parameter means a more exact solution but it will take more time to compute. 

$$\forall i: v_i' := \lceil{v_i/b}\rceil$$We run DP on these values. S is our solution and S* is the optimal solution. Our solution is feasible. 

$$\sum_{e \in S^*}v_i / b \leq \sum \lceil v_i/b \rceil = \sum v_i' \leq \sum  v_i' \leq \sum_{i \in S}(v_i/b + 1) \leq n + \sum_{i \in S}v_i/b$$
From this we can get: $$y \leq\sum_{i \in S^**}v_i \leq nb + \sum_{j \in S}v_i$$
But we wish to rewrite this as  $1 - \epsilon$ . We define b := $\epsilon*y / n$ if > 1. So from this we get: $$\sum_{i \in s} v_i \geq \sum_{i \in S^*} v_i - \epsilon*y \geq (1-\epsilon) * \sum_{i \in S^*} v_i$$
So here we have a trade off between running time and closeness of our algorithm. 

Time: 
* $b > 1 : O(n^2* y/b = O(n^3/\epsilon)$
* $b \leq 1: O(n^2*y)=O(n^3*b/\epsilon)=O(n^3/\epsilon)$

This is an example of a [[PTAS]]. 


\-\-\-
# References