20231113 - 13:56

Status: #idea

Tags:

# Disconnecting Edge Sets
Delete a set $F \subseteq E$ with min $|F|$ so as to disconnect s and t. 

Let $c_e := 1$ for all $e \in E$. Compute a maximum flow f. 

$k := val(f)$, compute a cut with $c(A,B)=k$. 

$F_0 :=$ set of edges from A to B. 

k = max number of [[Edge Disjoint Paths]]. Now we know that we must at least as many edges as there are edges in the edge disjoint paths. 

Consider F with min $|F|$, this gives us that $F \geq k$ and $|F_0| = k$. 




\-\-\-
# References