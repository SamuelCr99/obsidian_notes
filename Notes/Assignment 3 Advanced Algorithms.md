# Assignment 3 Advanced Algorithms
Samuel Collier Ryder
collier@chalmers.se
Computer Science - Algorithms, Languages and Logic (Year 1)
## Exercise 6
#### 6.1
This can not be simulated with a fixed finite number of random bits.  

The only probabilities which can be simulated with a fixed number of random bits are those on the form $m*(\frac{1}{2})^n$ where n is the number of bits and m is some integer. We can rewrite this as $m *\frac{1}{2^n}$. We know that $2^n$ can never equal a multiple of 3 (assuming n is an integer which we know as n equals the number of bits), this means that no matter the value of m, $m * \frac{1}{2^n}$ will never be able to simulate $\frac{1}{3}$. So it is impossible to simulate $\frac{1}{3}$ with a fixed number of random bits.  

#### 6.2
As opposed to 6.1 this can indeed be solved! 

Consider we use two bits, and set the following rules: 

1. Both bits return 1, return true
2. Both bits return 0, run the test again using two new bits
3. None of the above, return false.

Now lets break this down. Why would this simulate an event with probability $1/3$? We know that we have a probability of $1/4$ of returning 1 in the first iteration, but we also have a probability of $1/4$ of running the test again, and in that new test we also have a probability of $1/4$ of returning 1. This pattern will continue and we will get $$(\frac{1}{4})^1 + (\frac{1}{4})^2 + (\frac{1}{4})^3 ... = \sum_{n=1}^\infty \frac{1}{4^n} = \frac{1}{3}$$This is a well known geometric series which sums to $\frac{1}{3}$. This means that the probability of returning 1 is $\frac{1}{3}$. Another way of thinking about this is that the probability of returning 1 given that we return in that state is $\frac{1}{3}$, which also leads us to the same result, the probability of returning 1 is $\frac{1}{3}$. The difference in this solution compared to 6.1 is that we don't know how many bits will be used, but we do have an expected number. 

In each state there is a probability of $\frac{3}{4}$ that the program will terminate. This means that we can expect $\frac{4}{3}$ rounds. In each round we will use two bits meaning that the expected number of bits used will be $\frac{8}{3}$.

## Exercise 7
I will attempt to approach this as if it was a FPT problem. I assume that k is known, is this a correct assumption? 

Start from a random node in the graph, from that we perform a BFS. If we find c+1 nodes we know that one of these nodes must be deleted else the rule will be violated. From here we will create a bounded search tree, with one node for each possible deleted node. This bounded search tree will only have a depth of 1 as we know that only 1 node needs to be removed to satisfy the constraint, and it will have a total of $c+1$ leaves as an attempt to delete every node will be tried. 

We will now recursively do the same process for each of these leaves. This will make the tree grow by one level, and each level will contain exactly c+1 nodes. Before doing each recursive step we will first check if any of the new nodes contain a valid solution. 

We will then keep doing this process, note that we always start searching from the same node. If it has been deleted simply choose the next node, if there are many nodes connected a node can be chosen at random. Keep doing this until a successful solution is found or k nodes have been deleted. If a successful solution is found we return it, otherwise we declare that it is not possible to remove k nodes to fulfill the requirements. This will have created a bounded search tree with k levels, where each node has c+1 children, which means that $O^*(c+1)^k$. 

This could also slightly be improved by only adding the new leaf if it does not already exist in the tree. This will speed up the process as many states are present in the tree many times, which is unnecessary. 

This works as we know that if we have more than c+1 nodes one of the nodes must be deleted. And from here we check what would happen if we tried deleting the different nodes, we then check all future possible values. In a sense this is testing all possible values but limiting ourselves in how far we can see, but due to the fact that we know a node must be deleted from the smaller area we don't have to consider the entire graph all the time. 