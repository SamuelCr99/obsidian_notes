20231120 - 15:19

Status: #idea

Tags:

# Assignment 2 Advanced Algorithms
# Exercise 3
## 3.1 
The goal in this task is to prove that G has a flow with val(f) = k if and only if G(k) has a circulation. This is the same as proving that these two statements are equivalent. Therefore I will argue this in both directions. Assume that we have a circulation in G(k), by definition this means that for each edge $e$ we know that the follow, $l_e \leq f(e) \leq c_e$ and for each node in v: $f^-(v) - f^+(v) = d(v)$. 

We know that $d(s) := -k$ and $d(t) := +k$. As we have assumed that G(k) has a circulation we have that $\sum_{e=(s,v)}f(e) \geq k$ and that $\sum_{e=v,t}f(e)\geq k$. We also know that there are no other demands in G except the ones placed on s and t. So we know that we must also have a flow of value K. We could also approach this using a counter model. Assume we do not have a circulation. Meaning that either $\sum_{e=(s,v)}f(e) \not\geq k$ or $\sum_{e=v,t}f(e)\not\geq k$ (or both). This means that enough flow can't leave the source or enter the sink. Which obviously mean no flow with val(f) can exist. 

This also hold the other way. If we know that we have a flow value of k and the previously stated demands. Then we also know that we have a flow. 
## 3.2
From lectures we know that when applying the LZ-reduction we set the lower capacity for all edges to 0, set the upper capacity to $c_e - l_e$ and finally update the demand from the node with the outgoing flow to $d(u) + l_e$ and the node with the incoming flow to $d(v) - l_e$. This means the updated demand will not depend on k unless the demand depended on k before it was updated. And as the demands of nodes which are not s or t do not depend on k before the reduction, they will not depend on it after the reduction either. 

We also know that $k \geq k_0$. From this fact we know that $d(s) \leq 0$ and $d(t) \geq 0$ must hold. This as the updated demands for s and t will be $d(s) \leq d_{old}(s) + k_0$ and $d(t) \geq d_{old}(t) - k_0$. And as $d_{old}(s) = -k$ and $d_{new}(s)=k$ we know that $d(s) \leq 0$  and $d(t) \geq 0$. 

## 3.3 
We will perform the CF-reduction. We know from 3.1 that having a flow with $val(f) = k$ is equivalent to the graph having a circulation. We also know from the lecture slides that a circulation only exists if all nodes to and from s' and t' are saturated. Therefore we can conclude that G has a flow if and only if J(k) saturates all edges s' and t'. j

# Exercise 4 
We can calculate the maximum flow using the maximum flow algorithm found in the lecture notes. This will give us a upper bound. We also have a lower bound of 0. We can check if a flow value is feasible by applying the algorithm from exercise 3. From this we will use a binary search to find the smallest possible k which will not violate and lower or upper bounds. This will give us the smallest possible k which is a feasible flow. 

The complexity for this algorithm will be $O(log C * E * V^2*E)$ where C is the maximum flow possible in graph $G$. 

If the maximum flow in the graph is infinite we will have to approach this slightly differently. Instead of using binary search we will perform a linear search starting from 0. This will be valid as the minimum flow can't be infinite as the lower capacity of each edge is a finite value. 

This is of course the dumb solution which tests many candidate values for k. I would love a tip for the smarter version which does not simply test different values.  
# Exercise 5
## 5.1
We will transform A into a graph G by making the s node in A into a source, the t node into a sink. After this we will add $l_e$ and $c_e$ for all edges which are not source or sink. All $l_e$ will be set to 1 and all $c_e$ will be set to the total number of nodes in the graph. 

The proposed algorithm will then be as follows: 
* Check if any edges enter the source or exit the sink, if this is the case we can conclude that no solution exists. 
* Perform the algorithm from exercise 4, the returned minimum flow value will be the least number of paths going from s to t such that each edge is covered. 

If we can solve 

## 5.2
The time complexity of this will depend on a number of factors. When running the algorithm from exercise 4 we have a complexity of $O(log C*M)$, but in this case the know that C will at most be $n^2$. 

\-\-\-
# References