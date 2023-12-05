20231205 - 15:13

Status: #idea

Tags:

# Assignment 3 Advanced Algorithms
## Exercise 6
#### 6.1
This can not be simulated with a finate number of random bits. 

#### 6.2
This can be simulated!

## Exercise 7
* Proposed algorithm. Choose a random node in the graph. 
* Perform a BFS from that given node. One can stop if we find more than c nodes, this means that at least one of these nodes must be deleted. 
* Try to remove one of the found nodes at a time, if removing said node makes the graph satisfy the constraints we are done! 
* If not, consider a a new BFS in each direction from the node which we deleted. What would now happen if we removed two nodes, would that result in the constraint not being violated? 
* Keep running this process until we reach a scenario where the constraint is not violated. 



\-\-\-
# References