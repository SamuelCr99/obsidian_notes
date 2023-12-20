# Assignment 2 Advanced Algorithms
*Samuel* Collier Ryder
collier@chalmers.se
Computer Science - Algorithms, Languages and Logic (Year 1)
# Exercise 3
## 3.1 
The goal in this task is to prove that G has a flow with val(f) = k if and only if G(k) has a circulation. This is the same as proving that these two statements are equivalent. Therefore I will argue this in both directions. Assume that we have a circulation in G(k), by definition this means that for each edge $e$ we know that the follow, $l_e \leq f(e) \leq c_e$ and for each node in v: $f^-(v) - f^+(v) = d(v)$. 

We know that $d(s) := -k$ and $d(t) := +k$. As we have assumed that G(k) has a circulation we have that $\sum_{e=(s,v)}f(e) \geq k$ and that $\sum_{e=v,t}f(e)\geq k$. We also know that there are no other demands in G except the ones placed on s and t. So we know that we must also have a flow of value K. We could also approach this using a counter model. Assume we do not have a circulation. Meaning that either $\sum_{e=(s,v)}f(e) \not\geq k$ or $\sum_{e=v,t}f(e)\not\geq k$ (or both). This means that enough flow can't leave the source or enter the sink. Which obviously mean no flow with val(f) can exist. 

This also hold the other way. If we know that we have a flow value of k and the previously stated demands. Then we also know that we have a circulation. 
## 3.2
From lectures we know that when applying the LZ-reduction we set the lower capacity for all edges to 0, set the upper capacity to $c_e - l_e$ and finally update the demand from the node with the outgoing flow to $d(u) + l_e$ and the node with the incoming flow to $d(v) - l_e$. This means the updated demand will not depend on k unless the demand depended on k before it was updated. And as the demands of nodes which are not s or t do not depend on k before the reduction, they will not depend on it after the reduction either. 

We also know that $k \geq k_0$. From this fact we know that $d(s) \leq 0$ and $d(t) \geq 0$ must hold. This as the updated demands for s and t will be $d(s) \leq d_{old}(s) + k_0$ and $d(t) \geq d_{old}(t) - k_0$. And as $d_{old}(s) = -k$ and $d_{new}(s)=k$ we know that $d(s) \leq 0$  and $d(t) \geq 0$. 

## 3.3 
We will once again argue this equivalence in both directions. First assume that we have a flow with $val(f) = k$ in G. From 3.1 we know that this means we must have a circulation in $G(k)$. We will apply the LZ-reduction to $G(k)$ which will give us $H(k)$, this reduction sets all the lower bounds to 0 and all upper bounds to $c_e - l_e$, it also updates the demand of each node to $d(v) + \sum_{e=(v,u)}l_e - \sum_{e=(u,v)}l_e$. This means that we must still have a circulation in $H(k)$ if we had a circulation in $G(k)$. And as we know that we have a circulation in $G(k)$ we can also conclude that we have a circulation in $H(k)$. Finally we will perform the CF-reduction on $H(k)$, this creates two new nodes $s'$ and $t'$. We create edges between $s'$ and all nodes with negative demands, and edges between $t'$ and all nodes with positive demands. We then set all edge capacities equal to  $-d(v)$ for nodes connected to $s'$ and $+d(v)$ for nodes connected to $t'$. We then set all demands to 0. We finally set the demands of $s'$ and $t'$ to $\pm$ some value d. In $J(k)$ we will still have a circulation as we are still not adding or deleting flow. And from the lecture notes we know that if $J(k)$ has a a circulation then the maximum $s'-t'$ flow in $J(k)$ must saturate all edges going from $s'$ and to $t'$. 

Now assume that we know that all edges from $s'$ and to $t'$ are saturated in $J(k)$. From the lecture notes we then know that this means there is also a circulation in $J(k)$. And if $J(k)$ has a circulation then we also know that $H(k)$ and $G(k)$ have circulations. And again from 3.1 if $G(k)$ has a circulation then G has a flow with $val(f)$ = k.  

# Exercise 4 
For my proposed algorithm to work I will need to find the maximum flow from the source to the sink. Finding a maximum flow through a graph will not work if there are edges with a upper capacity of $\infty$. We must therefore substitute the upper capacities which are $\infty$ with a different value. I suggest all upper capacities equal to $\infty$ are set to the sum of all the lower capacities. This suggestion might sound strange, but we must not forget the goal of the exercise, we wish to find the minimum flow which does not violate any of the capacities. This means that our only goal when changing the upper capacity is to make sure that this new upper capacity never gives us an erroneous result when attempting to find the minimum flow. So why the sum of the minimum bounds? We know that at the absolute worst case the most which will be forced across one edge when trying to find the minimum flow will be the sum of all other lower capacities, this bound is quite pessimistic and there might exist better approximations. After this update has been done we can apply the Edmond Karp algorithm to find the maximum flow through this graph, we denote the found max flow as $k_{max}$. If no feasible flow exists we can return it at this stage. 

Now we wish to find the smallest k which does not violate any of the constraints in G. We will test if a value of $k$ is feasible by applying the steps taken in exercise 3. We know that: $k_0 \leq k \leq k_{max}$. From here we can perform a binary search. We will try if a value of $k$ is feasible by applying the steps from exercise 3. Begin with testing  $k = \frac{k_{max}}{k_0}$. If this value of $k$ is feasible we know that the smallest possible $k$ must be smaller or equal to k. If this value does not work we know that the smallest value must be bigger. We will keep searching until the search window becomes empty, while always keeping track of the smallest $k$ value found. After this we can return the smallest feasible value of k we found. The reason to perform the binary search is that it greatly cuts down the number of checks we have to perform.

Here is pseudocode of the algorithm: 
```
lo = k_0
hi = k_max
smallest_found = inf

while lo < hi: 
	mid = floor((hi + lo)/2)
	if mid is feasible according to steps in exercise 3: 
		hi = mid
		smallest_found = mid
	else: 
		lo = mid

return smallest_found
```

# Exercise 5
## 5.1
We will transform A into a graph G by making the s node in A into a source, the t node into a sink. After this we will add $l_e$ and $c_e$ to all edges in the graph. All $l_e$ will be set to 1 and all $c_e$ will be set to the sum of the lower bounds which is equal to the number of edges in this case, as each lower bound is 0. After this we can perform the steps from exercise 4. A smallest number of paths will exist if and only if a flow value exists. And the flow value will equal the smallest number of $s-t$ paths in A to cover every edge. All we are doing is adding upper and lower bounds to each edge, and denoting s as source and t as sink. Clearly all of this can be done in $O(E)$, which is polynomial.

Now for the equivalence proof. In A we wish to find the minimum number of $s - t$ such that each edge is covered. And in G our goal is to find the minimum flow from $s$ to $t$. By setting $l_e$ to 1 for each edge we require that every edge must have at least a flow value of 1. The upper bound is set in a similar way as in exercise 4, we set it so it never gets in the way of finding the minimum value. One way of thinking about this is that each edge has to be touched at least once by the flow when moving from source to sink for out lower capacity to be satisfied. This is exactly what we are trying to achieve in A, we want to cover every edge in A. And if we know k paths between $s$ and $t$ are enough to cover every edge in A we also know that there must exist a flow value of k in G, as we could easily transform A into G and check how many times each edge is traversed in the s-t paths in A, and the upper bound would not be an issue here for the same reason stated previosly. So with these constraints these problems are equivalent, G has a flow with a value of k if and only if k paths is sufficient to cover every edge between s and t in A.

## 5.2
The complexity for this algorithm will be $O(V*E^2 + log(E) * (E+V))$. This clearly looks quite confusing so lets quickly break it down. We first transform A into G. To do this we add $l_e$ and $c_e$ to each edge in A and transform nodes s and t into a source and sink. This will take $O(E)$ time. After this we will apply the steps from exercise 4. We perform the Edmond Karp algorithm to find if there exists a flow, and in the positive case also find the maximum flow in G, this will take $O(V*E^2)$. After this we will check a number of possible K values, this will be by using Binary search. We know that all upper bounds are set to E, this means that the absolute max flow value would be $E*E$, but as $O(log(E^2)) = O(log(E))$ we will simply write it as $O(log(E))$. Then for each of the values found in this binary search we must perform the reductions from exercise 3, this will take $O(E+V)$. 