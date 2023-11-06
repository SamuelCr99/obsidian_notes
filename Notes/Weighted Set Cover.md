20231102 - 10:04

Status: #idea

Tags:

# Weighted Set Cover
Given a set U, with |U| = n. Find a family C of sets $S_i$ such that the union of $S_i$ is U while minimizing the weight. This is a very general problem and therefore it would be great if we had a good algorithm for it. This problem is NP complete. It can be reduced from vertex cover. 

Let's assume a greedy algorithm, let R denote the remainder. In the beginning R=U. C is the empty family of sets. 
``` Python
while R != empty:
	take some S_i with ?
	C = C u {S_i}
	R = R \ S_i # Note that \ means subtraction in sets
```

In this case the ? might be min $w_i/|s_i|$. This is not great, as we might select overlapping things. Instead we try min $w_i/|S_i \cap R|$. $H(n)=\Sigma_i^n 1/i \sim ln(n)$. 

We suppose a new idea. Each element s newly covered by $S_i$ pays $C_s = w_i/|S_i \cap R|$. We denote C: greedy solution with weight $\Sigma_{s_i \in C} w_i = \Sigma_{S \in U} c_s$. We now consider any $S_k={s_1,..., s_d}$, now consider any $s_j$ in $S_k$, just before $s_j$ get covered: $|S_k \cap R| \geq d-j+1$. Algorithm chooses $S_i$ with $w_i / |S_i \cap R| \leq w_k / |S_k \cap R| \leq w_k/(d-j+1)$. This says that $s_j$ pays $c_{s_j} \leq w_k/(d-j+1)$. $S_k$ pays $\leq \Sigma_{j=1}^d w_k/(d-j+1) = w_k * H(d)$. Redefine d = $max |S_k|$


\-\-\-
# References