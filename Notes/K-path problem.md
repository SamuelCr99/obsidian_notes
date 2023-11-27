20231127 - 13:35

Status: #idea

Tags: [[Algorithms]] [[Randomized Algorithms]] [[Dynamic Programming]] 

# K-path problem
Given: We are given a graph G = (V,E), undirected, connected, |v| = n, $k \geq 0$ (integer). 

Goal: Find a path with exactly k nodes, such that the path does not cross itself. In other words, each node can only be visited once. 

![[k-path.png]]

This has application in biology. 

Diameter in a graph is defined as the maximum shortest distance between any two point. If the diameter is at least k this becomes easy. As we know the shortest path can't cover itself. Therefore we can compute all diamaters and choose the largest one.  

But this becomes harder if the largest diameter is not higher than k. Here we simply choose a node and start searching from there. This will build a search tree of depth k. Each node can have at most n children. So this will give us a time complexity of $O(n^k)$. Which is a XP time algorithm. We want to perform better than this. 

![[k-path-tree.png]]

To improve this we will use "coloring". We work with a set K which contains k "colors", after this we will paint the nodes. Each nodes gets a coloring. Note that coloring in this case has nothing to do with the graph coloring problem. Find a path with exactly k nodes, that uses every color exactly once. This updated version is known as the colorful k-path problem. This restriction will make this easier to solve. 

![[kpath-color.png]]

Now consider all ordering of K. 

We split the nodes into groups with there colors. We now want one path which touches each group. We can now add a source and sink and find a way through this. This will give us $O^*(k!)$

Here the heavy part is finding all possible colorings. Here we can actually use dynamic programming. We use something called dynamic programming on subsets. 

$C \subseteq K$ (variable with $2^k$ values)
Def: $p(C, v)$ = 1 if path of |C| nodes exits, that ends in $v$ and uses exactly the colors in $C$. Else 0.  

Computation: for |C| = 1: p(C,v) = 1 $\iff$ C = {c(v)}. Suppose that all p(C,V), |C| = i are known. 

$|C'|= i+1$ 
$p(C', v) = 1 \iff \exists u: uv \in E \land p(C' \setminus \{c(v)\}, u)$

After this backtracing can be used to find correct values. Finally we end up with $O(2^kn^2)$. But this was simply the solution for the colorful k-paths problem. How do we apply it to the general problem? 

We use a [[Randomized Algorithms]]. Choose the $c(v)\in k$ at random and independently. 

**P**: Some k-path.
P can be colored in $k^k$ ways. And all of these have the same probability, namely $1/k^k$. There are $k!$ good colorings. So the success ratio will be $k! / k^k$. This can be approximated using Stirling's formula as $k^k/(e^k*k^k)*\sqrt{2nk}=O(\sqrt{k}/e^k$). All in all this would give us $O^*((2e)^k$ time. 

\-\-\-
# References