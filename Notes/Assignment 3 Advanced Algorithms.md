# Assignment 3 Advanced Algorithms
Samuel Collier Ryder
collier@chalmers.se
Computer Science - Algorithms, Languages and Logic (Year 1)
## Exercise 6
#### 6.1
This can not be simulated with a fixed finite number of random bits.  

When we consider the outcome of the random bits we can choose to consider this in one of two different ways. Either we consider the order of the result, or we don't care about the order. 

Lets first consider the case where we take the ordering into account. In this case we will only ever be able to simulate probabilities on the form $(\frac{1}{2})^n$, where $n \in \mathbf{N}$. This as each coin toss will be its own Bernoulli distribution, being completely independent from previous coin tosses. 

Now let's instead choose to ignore the ordering of the results. This now takes on the form of a Binomial Distribution. The formula for a binomial distribution is: $$Pr(X=k) = {n\choose k}*p^k*(1-p)^{n-k} $$
Applying our value of p=0.5 we get: $$Pr(X=k) = {n\choose k}*0.5^k*(0.5)^{n-k} $$
We also know that $n - k \geq 0$ and that ${n \choose k}$ will be some positive whole number. Knowing all of this we can draw the conclusion that $Pr(X=k)$ will always be some multiple of $0.5$. And as $1/3$ is no multiple of $1/2$ this can't be simulated with some fixed finite number of bits. 

This same reasoning also holds cumulative distribution functions, as we are still just multiplying some positive integer to $0.5$ and then summing it, which means the result will still just be a multiple of $0.5$. 
#### 6.2
As opposed to 6.1 this can indeed be solved! 

Consider we use two bits, and set the following rules: 

1. Both bits return 1, return true
2. Both bits return 0, run the test again using two new bits
3. None of the above, return false.

Now lets break this down. Why would this simulate an event with probability $1/3$? We know that we have a probability of $1/4$ of returning 1 in the first iteration, but we also have a $1/4$ of running the test again, and in that new test we also have a probability of $1/4$ of returning 1. This pattern will continue and we will get $$(\frac{1}{4})^1 + (\frac{1}{4})^2 + (\frac{1}{4})^3 ... = \sum_{n=1}^\infty \frac{1}{4^n} = \frac{1}{3}$$This is a well known geometric series which sums to $\frac{1}{3}$. This means that the probability of returning 1 is $\frac{1}{3}$. The difference in this solution compared to 6.1 is that we don't know how many bits will be used, but we do have an expected number. 

The expected number of bits used will be $\frac{8}{3}$ as there is a $3/4$ chance in each state that the program will terminate. Meaning that we expect there to be $\frac{4}{3}$ expected rounds. And in each round we will use two bits. Meaning that we expect to use $\frac{8}{3}$ bits.  

## Exercise 7
I will attempt to approach this as if it was a FPT problem. I assume that k is known, is this a correct assumption? 

Start from a random node in the graph, from that we perform a BFS. If we find c+1 nodes we know that one of these nodes must be deleted else the rule will be violated. From here we will create a bounded search tree, with one node for each possible deleted node. This bounded search tree will only have a depth of 1 as we know that only 1 node needs to be removed to satisfy the constraint, and it will have a total of $c+1$ leaves as an attempt to delete every node will be tried. 

We will now recursively do the same process for each of these leaves. This will make the tree grow by one level, and each level will contain exactly c+1 nodes. Before doing each recursive step we will first check if any of the new nodes contain a valid solution. 

We will then keep doing this process, note that we always start searching from the same node. If it has been deleted simply choose the next node, if there are many nodes connected a node can be chosen at random. Keep doing this until a successful solution is found or k nodes have been deleted. If a successful solution is found we return it, otherwise we declare that it is not possible to remove k nodes to fulfill the requirements. This will have created a bounded search tree with k levels, where each node has c+1 children, which means that $O^*(c+1)^k$. 

This could also slightly be improved by only adding the new leaf if it does not already exist in the tree. This will speed up the process as many states are present in the tree many times, which is unnecessary. 

This works as we know that if we have more than c+1 nodes one of the nodes must be deleted. And from here we check what would happen if we tried deleting the different nodes, we then check all future possible values. In a sense this is testing all possible values but limiting ourselves in how far we can see, but due to the fact that we know a node must be deleted from the smaller area we don't have to consider the entire graph all the time. 