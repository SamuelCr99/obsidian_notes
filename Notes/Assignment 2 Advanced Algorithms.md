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
We will once again argue the equivalence in both directions. First we assume that G has a flow f with val(f) = k. In G we know that k flow leaves the source and k flow enters the sink. We then add the demands for G(k). In 3.2 we perform the LZ-reduction meaning that we remove all the lower capacities and update demand and upper capacities. Finally in the CF reduction we insert new nodes s and t and add new directed edges to all sinks and sources. We give all of these new edges capacities $-d(u)$ and $+d(u)$. As this new s and t will connect to the nodes which were created by the LZ reduction in 2.2. We know that the demands created after the LZ reduction are based on the maximum flow value. And these values then become the new lower capacities. So if we have a flow of value k we know that this will translate to the capacities of the edges connected to $s'$ and $t'$. So if we have a flow these edges must be saturated.   

This also hold in the other direction. If the edges are saturated from $s'$ and $t'$ then there must also be a flow of value k in G, as the upper edge capacities are directly dependent on the value of k.  

# Exercise 4 
Start by considering the graph. Finding a maximum flow through a graph will not work if there are edges with a upper capacity of $\infty$. We must therefore substitute the upper capacities which are $\infty$ with a different value. I suggest all upper capacities which were previously set to $\infty$ are set to the sum of all the lower capacities. The reason for this suggestion is that when we are looking for the minimum possible flow later, the maximum which can be flow which will be sent across one edge will be the sum of lower capacities, this means that there is no need for any node to have a higher upper capacity than this. After this update has been done we can apply the Edmond Karp algorithm to find the maximum flow through this graph, we denote the found max flow as $k_{max}$. If no feasible flow exists we can return it at this stage. 

Now we wish to find the smallest k which does not violate any of the constraints. We will test if a value of $k$ is feasible by applying the steps taken in exercise 3. We know that $k$ must be larger or equal to $k_0$ and smaller or equal to $k_{max}$. From here we can perform a binary search. Begin with testing $k = \frac{k_{max}}{k_0}$. Apply steps from exercise 3, if there exists a flow we will choose a new value of which in in the middle of $k$ and $k_0$ and if there does not exist a flow we instead choose a value in the middle of $k_{max}$ and $k_0$. We will keep searching until the search window becomes empty, while always keeping track of the smallest $k$ value found.  

# Exercise 5
## 5.1
We will transform A into a graph G by making the s node in A into a source, the t node into a sink. After this we will add $l_e$ and $c_e$ for all edges. All $l_e$ will be set to 1 and all $c_e$ will be set to the sum of the lower bounds which is equal to the number of edges in this case. 

The proposed algorithm will then be as follows: 
* Check if any edges enter the source or exit the sink, if this is the case we can conclude that no solution exists. 
* Perform the algorithm from exercise 4, the returned minimum flow value will be the least number of paths going from s to t such that each edge is covered. 

If we can solve Path Edge Cover for a given graph G then we can also solve minimum flow for that graph with our given lower and upper capacity. As we know all edges must be reachable for both algorithms to be solved. 

We can also perform a transformation the other way around, this is done by removing the lower and upper bound from all edges. 
## 5.2
The time complexity will be the same as found in exercise 4. The difference here is that we know the maximum possible flow through any graph with $n$ nodes would be  $n^2$. Therefore we can rewrite the capacity as $O(log(V^2) * V * E^2*(E+V))$. 

The complexity for this algorithm will be $O(log(E) * V * E^2*(E+V))$. This clearly looks quite confusing so lets quickly break it down. The $log(E)$ part will come from performing the binary search, as we know that the lower capacity is 1 and the upper capacity becomes the sum of all lower capacities which then equals the number of edges. Then in the binary search we will have to perform the steps from exercise 3. The algorithm from exercise 3 will first perform a number of reductions reduction, these reductions will take $O(E+V)$ and then after this we will apply the Edmond Karp algorithm to find the maximum flow, which is $O(V*E^2)$. 
