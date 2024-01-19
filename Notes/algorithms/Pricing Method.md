20231102 - 11:06

Status: #idea

Tags:[[Algorithms]] [[Approximation_Algorithms]]

# Pricing Method
G = (V,E), we denote the nodes by integers. Every node has a positive weight, so $w_i$= weight of node i. H(d)-approx, where d=max degree. We achieve ratio 2. Every edge pays $p_e \geq 0$. Def: Prices are fair if $\forall i \Sigma_{e=(i,j)}p_e \leq w_i$. 

Definition: A node is tight if we can't increase the prices without making it unfair. 

Algorithm: 
for all dges $e \in E$ pick any edge where both end nodes are not yet tight. While some edge e=(i,j) i,j not tight exists we raise $p_e$ to make i or j tight. S = set of tight nodes. Terminates in polynomial time. S is a vertex cover. 





\-\-\-
# References