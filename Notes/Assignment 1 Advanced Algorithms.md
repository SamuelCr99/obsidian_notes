
# Assignment 1 Advanced Algorithms
Samuel Collier Ryder
collier@chalmers.se
Computer Science - Algorithms, Languages and Logic (Year 1)

# Exercise 1
#### Suggested Algorithm
* Start from a random node. From that node perform a BFS. If we find c+1 nodes we know that one of these nodes must be deleted for the constraint to not be violated. In an optimal solution one would have to find which of these nodes would be optimal to delete, but in this questions, as the approximation ratio is so generous we can simply choose to delete all the found nodes. After this deletion we select a new random node and perform a new BFS, we continue this process until we reach a graph will less than c+1 nodes. This solution will most likely delete many unnecessary nodes, but it will stay within the approximation ratio. 

#### Time Analysis
* This algorithm will be polynomial as we will only be performing a number of BFS and deletions. And we know that BFS has a time complexity of $O(|V|+|E|)$ and that of deletions of $O(V)$. We also know that the number of times we do these operations will be limited by the number of nodes in our graph.  

#### Approximation Analysis
* We know that $T = k$. Performing my suggested algorithm we will search the graph and each time c+1 nodes are found we delete one. Meaning that at most $(c+1)*k$ nodes will be deleted, so $T^* = (c+1)*k$. This gives us the approximation ratio of $\frac{T^*}{T} = c+1$. 

#### Assumptions
* There only exists 1 edge between a pair of nodes. 
* I assume a adjacency list is used to keep track of connections in graph. 

# Exercise 2
#### Background 
* Consider a 1 dimensional line with a number of points, maybe a street with houses. How do we successfully choose a point on this line such that the total distance traveled for all nodes to this selected point is minimal? I will make the claim that the best point to choose will always be one of houses, (note that there might be multiple points which are all equally good, but one of these will always be a point where a house is located). The reason for this is that we always can select one of the nodes in the middle to be the meeting location. If we move the meeting point to the left it will indeed make the trips shorter for all the neighbors who live to the left, but it will make the trip longer for all the neighbors who live on the right. The key thing to notice is that this change will make the distance as much longer for all the people living on the right as shorter for people living on the left. But now the person who previously had the meeting at their house also have to travel a distance, and thusly the total distance has increased (or stayed the same depending on the layout of the houses). 
* This same reasoning holds when we are considering one line but also have weights. But in this case we must check all of the available points as we now also have to take into account there weights. 
#### Suggested Algorithm 
* We will consider the X-axis and the Y-axis independently. The reason we can consider these axes independently is because when moving by Manhattan distance the optimal point will be the point which minimized X and Y separately. The reason for this is that the optimal X value has nothing to do with the Y value, as to get to the Y value we must always traverse that many steps in the Y direction, as only one direction can be traversed at a time. This is not the case in the euclidean version as in that case a step can be in both X and Y direction, while each step here is always one of the directions. And as we discussed above, the optimal point for minimizing the total distance will always be in one of the available points. For this reason the optimal meeting point will have the x-value of the optimal point when only considering the x-axis and the y-value of the optimal point when considering the y-axis. So the minimum will always be attained in coordinates which are available in our points. Note that this does not mean that the optimal meeting point is one of the given points, just that the optimal meeting point will contain coordinates which are in the available points.  With this knowledge we continue with the algorithm below:   
* For each axis, iterate over the available points and find which point which minimizes the overall  cost for that axis. The best point will be the point $(x^*,y^*)$ where $x^*$ is the best value when only considering the x-axis, and $y^*$ is the optimal in the y-axis. 

* Example of code for calculating optimal solution for one dimension: ```
``` 
smallest_running_sum = inf
optimal_x = None
for x in x_values:
	running_sum = 0
	for x_i2 in x_values:
		running_sum += w_i * |x - x_i|
	if running_sum < smallest_running_sum:
		smallest_running_sum = running_sum
		optimal_x = x 
```

#### Time Analysis
* The time complexity will be $O(n^2)$ as when considering each point we must calculate the cost to get there from all other points, and then this must be applied to all other points. 

#### Approximation Analysis
First we will consider the geometry of a problem. From Pythagoras's theorem we know that the maximal extra distance from not traveling diagonally will be $\sqrt{2}$. Now for the actual approximation ratio. The approximation ratio can be calculated by $\frac{T}{T^*}$ where T will be the minimum weighed sum using the Manhattan distance and $T^*$ will be the minimum weighted sum using the Euclidean distance. Clearly the Manhattan distance must always be larger or equal to the Euclidean distance. The approximation ratio can be calculated using the following formula: $$\frac{\sum_{i=1}^n w_i*(|x - x_i| + |y - y_i|)}{\sum_{i=i}^n w_i * \sqrt{(x-x_i)^2 + (y - y_i) ^2}}$$
To calculate the fraction of these sums we will need to rewrite them. For the approximation ratio we are interested in the case where the Euclidean distance and Manhattan distance differ the most, using Pythagoras's theorem we know that the largest difference between Manhattan and Euclidean distance comes from when both edges are of equal length meaning $|x - x_i| = |y - y_i|$, we also define $z_i := |x - x_i|$. We use this to rewrite the fraction as: $$\frac{\sum_{i=1}^n w_i*(|x - x_i| + |x - x_i|)}{\sum_{i=i}^n w_i * \sqrt{(x-x_i)^2 + (x - x_i) ^2}} = \frac{\sum_{i=1}^n w_i*2z_i}{\sum_{i=i}^n w_i * \sqrt{2z_i^2}} = \frac{2 *\sum_{i=1}^n w_i*z_i}{\sqrt{2}*\sum_{i=i}^n w_i * z_i} = \frac{2}{\sqrt{2}} = \sqrt{2}$$
To reiterate this is the case where both edges are of equal length for all of the points when traveling to the optimal point. 