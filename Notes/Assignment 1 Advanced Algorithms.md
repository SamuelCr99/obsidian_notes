
# Assignment 1 Advanced Algorithms
Samuel Collier Ryder
collier@chalmers.se
Computer Science - Algorithms, Languages and Logic (Year 1)

# Exercise 1
#### Suggested Algorithm
* Perform a BFS search to find the size of the connected component. 
* If the size of the connected component is larger than c then remove the node with highest degree along with its connected edges. 
* Then keep performing this opperation until no 

#### Time Analysis
* This will depend on if an adjacency list or an adjacency matrix is used to keep track of connections in graph. I will assume a adjacency list is used. 
* Simply performing the BFS will take $O(V+E)$. 
* In each node we will have to check the number of connections and see if this number is larger than c-1. Worst case this will be $O(n)$ as we will have to count every node. 
* If the number is larger than c-1, we must then remove the node. This will once again depend on the implementation of the adjacency list, I will assume it is implemented using a normal array, meaning finding a element will take $O(n)$ time, we must also at worst delete our element from all other lists. So this will at worst be $O(n^2)$. 
* All in all this will be $O((V+E)*(O(n)+O(n^2)))$ which is the same as $O((V+E)*O(n^2))$. This is obviously a polynomial algorithm. 

#### Approximation Analysis
* In each connected we will have one of two different scenarios, either the the connected component has less c or less nodes. Or it has more than c nodes. 
* If a connected component has c or less nodes then we will not delete any nodes, thus this approximated 
* In the former scenario we don't have to remove any nodes, in the latter at least 1 node has to be deleted. 

#### Assumptions
* There only exists 1 edge between a pair of nodes. 
* I assume a adjacency list is used to keep track of connections in graph. 
# Exercise 2
#### Background 
* Consider a 1 dimensional line with a number of points, maybe a street with houses. How do we successfully choose a point on this graph such that the distance from each point  
#### Suggested Algorithm 
* We will consider the X axis and the Y axis independently. 
* For each axis, iterate over the available points and find which point which minimizes the overall cost. The point we find will be the correct point in that axis. 
* The best point will then be the combination of the points found from this. 

#### Time Analysis
* The time complexity will be $O(n^2)$ as when considering each point we must calculate the cost to get there from all other points, and then this must be applied to all other points. 

#### Approximation Analysis



#### Question for grader
Is this a good way of approaching these assignments, or should I change the format in some way for coming assignments? 