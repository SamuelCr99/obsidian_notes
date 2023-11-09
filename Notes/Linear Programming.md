20231106 - 14:29

Status: #idea

Tags: [[Approximation_Algorithms]] [[Linear Programming]]

# Linear Programming
Example using [[Vertex Cover]]. 

We set label $x_i$ for each edge in the vertex cover. Either 1 if it is in S or 0 if it is not. We also know constraints by knowing that some edges must be in the graph for it to still be a vertex cover. We also know that each edge must always get an assigned value. This can be solved using vertex multiplication. 

$min w^T x$ such that $Ax \geq b$ where $\forall: x_i \in {0,1}$. In this case this is actually a integer linear programming. If we don't have the last constraint with the for all we have a normal linear programming problem. Here we have a nice proof that ILPs are NP-complete, as what we have done here is a reduction. 

Many problems can be reformulated as LP. And LP problems can be solved by black box LP solvers. 

### LP-relaxation
We will relax the for all constraint, So we replace the $\forall: x_i \in 0,1$ into $\forall: 0 \leq x_i \leq 1$, This will make our ILP problem into a LP problem. To solve this we apply this to the LP solver. Here we will get many fractional numbers, $S := \{i | x_i \geq 1/2\}$. S will be a vertex cover. 

$w_{LP}$: Weight of opt solution to the LP relaxation. $w(S^*)$ = weight of opt vertex cover. $$w_LP \leq w(S^*)$$
$$w(s) \leq 2* w_{LP} \leq 2*w(S^*)$$



\-\-\-
# References