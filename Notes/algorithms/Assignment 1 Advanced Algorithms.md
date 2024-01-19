
# Assignment 1 Advanced Algorithms
Samuel Collier Ryder
collier@chalmers.se
Computer Science - Algorithms, Languages and Logic (Year 1)

# Exercise 1
#### Suggested Algorithm
* Start from a random node. From that node perform a BFS. If I find c+1 nodes I know that one of these nodes must be deleted for the constraint to not be violated. In an optimal solution one would have to find which of these nodes would be optimal to delete, but in this questions, as the approximation ratio is so generous I can simply choose to delete all the found nodes. After this deletion I select a new random node and perform a new BFS, if this new BFS finds c+1 nodes I once again delete all of them, if else I select a new random node not previously visited in this iteration. I continue until all subgraphs are smaller to or equal to c nodes in size. This solution will most likely delete many unnecessary nodes, but it will stay within the approximation ratio. This algorithm will always work as I am performing searches and always deleting when I find more than c nodes. And I are not done until I have made sure all subgraphs are of correct size. 

#### Time Analysis
* This algorithm will be polynomial as I will only be performing a number of BFS and deletions. And I know that BFS has a time complexity of $O(|V|+|E|)$ and that of deletions of $O(V)$. I also know that the number of times I do these operations will be limited by the number of nodes in our graph.  

#### Approximation Analysis
* I know that $T^* = k$. Performing my suggested algorithm I will search the graph and each time c+1 nodes are found I delete one. Meaning that at most $(c+1)*k$ nodes will be deleted, so $T = (c+1)*k$. This gives us the approximation ratio of $\frac{T}{T^*} = c+1$. 

#### Assumptions
* I assume a adjacency list is used to keep track of connections in graph. 

# Exercise 2
#### Background 
* Consider a 1 dimensional line with a number of points, maybe a street with houses. How do I successfully choose a point on this line such that the total distance traveled from all houses to this selected point is minimal? I will make the claim that the best point to choose will always be one of houses, (note that there might be multiple points which are all equally good, but one of these will always be a point where a house is located). The reason for this is that I always can select one of the nodes in the middle to be the meeting location. If I move the meeting point to the left it will indeed make the trips shorter for all the neighbors who live to the left, but it will make the trip longer for all the neighbors who live on the right. The key thing to notice is that this change will make the distance as much longer for all the people living on the right as shorter for people living on the left. But now the person who previously had the meeting at their house also have to travel a distance, and thusly the total distance has increased (or stayed the same depending on the layout of the houses). 
* This same reasoning holds when I are considering one line but also have weights. But in this case I must check all of the available points as I now also have to take into account there weights. 
#### Suggested Algorithm 
* I will consider the X-axis and the Y-axis independently. The reason I can consider these axes independently is because when moving by Manhattan distance the optimal point will be the point which minimized X and Y separately. The reason for this is that the optimal X value has nothing to do with the Y value, as only one direction can be traversed at a time. This is not the case in the Euclidean version as in that case a step can be in both X and Y direction. And as I discussed above, the optimal point for minimizing the total distance will always be in one of the available points. For this reason the optimal meeting point will have the x-value of the optimal point when only considering the x-axis and the y-value of the optimal point when considering the y-axis. So the minimum will always be attained in coordinates which are available in our points. Note that this does not mean that the optimal meeting point is one of the given points, just that the optimal meeting point will contain coordinates which are in the available points.  With this knowledge I continue with the algorithm below:   
* For each axis, iterate over the available points and find which point which minimizes the overall  cost for that axis. If there are multiple points which are equally good return all of these points. Now loop over all the returned x values and all the selected y values and try all combinations. The optimal point will always be one of the of these combined values. 

* Example of code for calculating optimal solution for one dimension: ```
``` 
smallest_running_sum = inf
optimal_x = []
for x in x_values:
	running_sum = 0
	for x_i2 in x_values:
		running_sum += w_i * |x - x_i|
	if running_sum < smallest_running_sum:
		smallest_running_sum = running_sum
		optimal_x.append(x) 
```

#### Time Analysis
* The time complexity will be $O(n^2)$ as when considering each point I must calculate the cost to get there from all other points, and then this must be applied to all other points. 

#### Approximation Analysis
First I will consider a small example problem. I will start by considering the simple problem below with only two points each with a weight of 1.  
![[graph2_assignment1.png]]
Using the algorithm proposed above I will consider the x-axis and the y-axis independently, and the algorithm will state that (0,0), (0,1), (1,0) and (1,1) all are equally good, as they all have a weighted Manhattan sum of 2. So (0,1) is a optimal point in this graph according to our algorithm. The real optimal point would be anywhere on the diagonal line between the two points. If I now calculate the Euclidean distance for the point found by my algorithm and the optimal solution I see that the distance found by my algorithm above will be 2, and the distance found be the optimal solution will be $\sqrt{2}$. So in this case the approximation ratio will be  $\frac{2}{\sqrt{2}} = \sqrt{2}$.   

Now let's compare the ratio between the two weighted sums. The ratio can be calculated using the following formula: $$\frac{\sum_{i=1}^n w_i*(|x - x_i| + |y - y_i|)}{\sum_{i=i}^n w_i * \sqrt{(x-x_i)^2 + (y - y_i) ^2}}$$
To calculate the fraction of these sums I will need to rewrite them. I am interested in the case where this fraction becomes as big as possible. Using Pythagoras's theorem I know that the largest difference between Manhattan and Euclidean distance comes from the case we must travel diagonally and both edges are of equal length meaning $|x - x_i| = |y - y_i|$.  I define $z_i := |x - x_i|$. I use this to rewrite the fraction as:
$$\frac{\sum_{i=1}^n w_i*(|x - x_i| + |x - x_i|)}{\sum_{i=i}^n w_i * \sqrt{(x-x_i)^2 + (x - x_i) ^2}} = \frac{\sum_{i=1}^n w_i*2z_i}{\sum_{i=i}^n w_i * \sqrt{2z_i^2}} = \frac{2 *\sum_{i=1}^n w_i*z_i}{\sqrt{2}*\sum_{i=i}^n w_i * z_i} = \frac{2}{\sqrt{2}} = \sqrt{2}$$
Note that this does not tell me the approximation, only that the weighted Manhattan sum will at most be $\sqrt{2}$ times larger than the weighted Euclidean sum. 

The formula to calculate the approximation ratio will be the fraction below, where $(x_{man}, y_{man})$ are the optimal coordinates for minimizing the weighted Manhattan distance.    $$\frac{\sum_{i=i}^n w_i * \sqrt{(x_{man}-x_i)^2 + (y_{man} - y_i) ^2}}{\sum_{i=i}^n w_i * \sqrt{(x-x_i)^2 + (y - y_i) ^2}}$$
This fraction will be the largest when: $$\sum_{i=i}^n w_i * \sqrt{(x_{man}-x_i)^2 + (y_{man} - y_i) ^2} = \sum_{i=1}^n w_i*(|x - x_i| + |y - y_i|)$$
This because the weighted Manhattan distance can never be lower than the weighted Euclidean distance.

So in the worst case the approximation ratio can be calculated using the below formula: $$\frac{\sum_{i=1}^n w_i*(|x - x_i| + |y - y_i|)}{\sum_{i=i}^n w_i * \sqrt{(x-x_i)^2 + (y - y_i) ^2}}$$
And as we know from the calculations above this is at most $\sqrt{2}$. Meaning the approximation ratio is $\sqrt{2}$.
