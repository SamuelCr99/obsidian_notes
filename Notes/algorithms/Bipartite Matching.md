20231113 - 13:21

Status: #idea

Tags: [[Bipartite Graph]], [[Algorithms]]

# Bipartite Matching
Given a [[Bipartite Graph]], find a matching $M \leq E$ with max $|M|$. 

We can solve this using logic from [[Flows]]. We add a start and a sink, and add the start to the left connecting to all nodes in one part of the bipartite graph and the sink to the other size. We then make all nodes directed moving from left to right. $C_e := 1$ for all edges e. We then calculate the maximum flow f, according to rules from [[Flows]]. But we add a small condition, we have $f(e)$ are integers (0 or 1). $M := \{e \in E | f(e) = 1\}$. $|M| = val(f)$. 

From any matching $M' \subseteq E$ we can construct a flow $f'$ with $val(f') = |M'|$. 

The running time for this algorithm is mainly taken up by running Ford Fulkerson, so $O(mn)$. 



\-\-\-
# References