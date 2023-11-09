
# Assignment 1 Advanced Algorithms
Samuel Collier Ryder
collier@chalmers.se
Computer Science - Algorithms, Languages and Logic (Year 1)

# Exercise 1
#### Suggested Algorithm
* Choose a random node in the graph. 
* Perform a BFS search to find the size of the connected component. 
* If the size of the connected component is larger than c then remove the node with highest degree in that connected component along with its incident edges. 
* Now check the size of the connected component again. If the size is still larger than c, then once again remove the node with highest degree. 
* When all parts are smaller than c, select a new random node which we have not visited previously (this will be in another connected component). 

#### Time Analysis
* We will first perform a BFS, which will in the worst case visit all the nodes in the graph, this will take O(n+m). After that we will remove the node with the highest degree, then a BFS algorithm will be performed again, in the worst case this will not have made the component unconnected which means it will one again take $O((n+m))$. In the worst case this pattern could continue until all nodes but one are deleted, meaning the overall time complexity would be $O(n*(n+m))$. This is obviously a polynomiall time bound. 

#### Approximation Analysis
* We know the optimal value in this case is k. The upper bound can be at most $(c+1)k$ according to the problem definition, meaning that we can at most delete ck extra nodes. This algorithm will have this approximation ratio as it might not always choose the best node to delete, but it will always choose one node which does its best to split up a connected component, though not always in the most optimal way. In the worst case it will lead to ck extra nodes get deleted. 

#### Assumptions
* There only exists 1 edge between a pair of nodes. 
* I assume a adjacency list is used to keep track of connections in graph. 
# Exercise 2
#### Background 
* Consider a 1 dimensional line with a number of points, maybe a street with houses. How do we successfully choose a point on this line such that the total distance traveled for all nodes to this selected point is minimal? I will make the claim that the best point to choose will always be one of houses, (note that there might be multiple points which are all equally good, but one of these will always be a point where a house is located). The reason for this is that we always can select one of the nodes in the middle to be the meeting location. If we move the meeting point to the left it will indeed make the trips shorter for all the neighbors who live to the left, but it will make the trip longer for all the neighbors who live on the right. The key thing to notice is that this change will make it as much longer for all the people living on the right as shorter for people living on the left. But now the person who previously had the meeting at there house also have to travel a distance, and thusly the total distance has increased (or stayed the same depending on the layout of the houses). 
* This same reasoning holds when we are considering one line but also have weights. But in this case we must check all of the available points as we now also have to take into account there weights. 
#### Suggested Algorithm 
* We will consider the X-axis and the Y-axis independently. The reason we can consider these axes independently is because when moving by Manhattan distance the optimal point will be the point which minimized X and Y separately. The reason for this is that the optimal X value has nothing to do with the Y value, as to get to the Y value we must always traverse that many steps in the Y direction. This is not the case in the euclidean version as in that case a step can be in both X and Y direction, while each step here is always one of the directions.  
* For each axis, iterate over the available points and find which point which minimizes the overall Manhattan cost for that axis. The best point will be the point $(x^*,y^*)$ where $x^*$ is the best value when only considering the x-axis, and $y^*$ is the optimal in the y-axis. 

#### Time Analysis
* The time complexity will be $O(n^2)$ as when considering each point we must calculate the cost to get there from all other points, and then this must be applied to all other points. 

#### Approximation Analysis
* The approach of using the Manhattan distance means we do never consider diagonal lines. What we are minimizing for in this question is the shortest total length, also including weights which must be traveled. The extra distance which needs to be traveled when not considering diagonal lines will be at most $\sqrt{2}$ times more. This follows from Pythagoras's theorem. Assume a right triangle where both legs are of length X. By Pythagoras's theorem we know the length of the the hypotenuse will be $$\sqrt{x^2+x^2}=\sqrt{2x^2}=\sqrt{2}*\sqrt{x^2}=\sqrt{2}*x$$And the distance needed to traverse using only the legs will be 2x. So in this case the ratio between these distances is $$\frac{2x}{\sqrt{2}*x} = \sqrt{2}$$But this was the case where both legs were of equal size, what if they are not of equal size? Let's assume one of the legs is of size $x+\beta$ and the other leg of size $x-\beta$. Using Pythagoras's theorem once again we get the size of the hypotenuse to$$\sqrt{(x+\beta)^2+(x-\beta)^2} = \sqrt{x^2+2x\beta+\beta^2+x^2-2x\beta+\beta^2}=\sqrt{2x^2+2\beta^2}$$ The ratio between the hypotenuse and the length of the legs will similarly by $$\frac{x+\beta + x-\beta}{\sqrt{2x^2+2\beta^2}} = \frac{2x}{\sqrt{2x^2+2\beta^2}}$$ As we can clearly tell this ratio will be at its largest when $\beta=0$. So the case where both sides are of equal length is the case where the ratio is the largest, and as we concluded above that is $\sqrt{2}$. So the approximation ratio is equal to $\sqrt{2}$. 
 


#### Question for grader
Is this a good way of approaching these assignments, or should I change the format in some way for coming assignments? 