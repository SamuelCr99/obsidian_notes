20231106 - 14:21

Status: #idea

Tags: [[Algorithms]]

# Vertex Cover
G = (V,E) graph. Vertex cover is $C \subseteq V$ such that the nodes are incident to all nodes. 
ADD IMAGE 2. 

This is also a NP-complete problem, but it can be approximated well! Matching: M $\subseteq$ E, pairwise disjoint. So edges which do not share a node. 

For  normal approximation see [[Approximation_Algorithms]]

On small examples this can also be solved using FPT. This will give us $O(1.47^n*kn)$. This can be improved further using kernelization. If a node has more than k neighbors then we know that this node must be selected, along with the incident edges. This is known as a reduction rule and runs in polynomial time. After that we will have a remaining graph which we will call H. This remaining graph will have some nice properties: All degrees are at most k, we can also say H has at most $k^2$ edges, else no solution exists. After this clever change we have $O(1.47^k*k^2+kn)$. Kernel must be computable in polynomial time in n, and the size must only depend on k. This is removing the easy parts of a problem. 

### Weighted Vertex Cover 
T = G = (V,E), |V| = n. $w(v)$: Weight of $v \in V$. We will only consider trees. If we quickly consider the unweighted version, this can be solved using a greedy algorithm, where we never select a leaf but rather the leaf's parent. 

In the weighted case this approach will not work, as the weight of the greedy node might be very heavy. So here we will need a [[Dynamic Programming]] solution. Select a random which is not the node. We will use a OPT function. OPT(v) = min weight of vertex cover S in $T_v$. This will note be enough sadly, thus we update the OPT function with another boolean flag. 

OPT(v,1) := min weight of a vertex cover S in $T_v$ with $v \in S$
OPT(v,0) := min weight of a vertex cover S in $T_v$ with $v \not\in S$
OPT(v) = min{OPT(V,1), OPT(v,0)}


v leaf: OPT(v,0) = 0, OPT(v,1) = w(v)
v inner node: $v_1, ..., v_d =$ children
		$OPT(v,0) := \sum_{i=0}^d OPT(v_i,1)$
		$OPT(v,1) := w(v) + \sum_{i=1}^d min(OPT(v_i,0), OPT(v_i,1))$

**Time:** $O(n)$. 

\-\-\-
# References