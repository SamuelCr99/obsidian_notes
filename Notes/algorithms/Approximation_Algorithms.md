220231030 - 12:44

Status: #idea

Tags:

# Approximation_Algorithms
My problem is NP-complete what now? We have a lot of NP-complete problems in the world, one option is to approximate a optimal solution in polynomial time. 

### Load balancing
Suppose we have n jobs to finish, with lengths $t_1 ... t_n$, to finish these jobs we have m machines available. All of these machines are identical. We wish to assign jobs to these machines, every job must be assigned to exactly 1 machine, and that given machine must be finished by that machine. We want to minimize the time when the last job is finished, we call this the **makespan**, T (max load of machines).  

Example: Consider m = 2. Job lengths = 3,3,2,2,2. Here we would assign 1 machine to do both 3 jobs and another do all the 2 jobs. So $T^*$ = 6. Where $T^*$ is the optimal value. This problem is NP complete. This can be easily reduced from subset sum. $Subset sum \leq_p load balancing$. So we can't find an optimal solution in polynomial time. But there might be an algorithm which gives us a good approximation! 

We attempt a greedy algorithm. Always assign the next job to some machine with minimum load. Following this greedy algorithm does not do great with our example from previous section, as this would give 3+2+2 and 3+2. So T=7. But 7 is not very far from 6, so maybe this is an ok approximation? This greedy algorithm is clearly in polynomial time. We need a way to measure the quality of our solution, maybe max $T-T^*$. This clearly does not work well, instead max ${T}/{T^*}$. This will work well. We call this ratio the **Approximation Ratio**. We will try to find tight upper bounds. 

But how do we achieve this? $T/T^* \leq$ upper bound on T / lower bound on $T^*$. The upper bound on T depends on the algos. While the lower bound on $T^*$ depends on the problem. $T^* \geq \frac{1}{m} \sum t_k$. Where k goes from 1 to n. We also have $\forall k: T^* \geq t_k$. Then we take the max of these two. It can be difficult to know when we stop with these assignments. 

$T_l$ = load of machine l. i = machine with max load $(T=T_i)$. j=last job on machine i. 
!(/images/)

$\forall l: T-t_j \leq T_l$. $mT - mt_j \leq \sum_{k=1}^n t_k$. We can keep rewriting this until we reach $T/T^* \leq 2$. Clearly this is not great. So can this be improved by a better ordering? Maybe we can sort the jobs such that the processing times decrease. Then apply the greedy algorithm to the new sorted array. We have to find the right way of approaching this. First assume that there are more jobs than machines, otherwise this is trivial. Assume that the machine i does at least 2 jobs. j $\geq$ m+1. So $T^* \geq 2*t_j$ so $T \leq \frac{3}{2}T^*$. So this is clearly better than the value we found previously. 

### Vertex Cover
We will approach the algorithm in the following way. Compute a maximal matching M. In this case maximal means that it can't be extended by adding another graph, NOT that it is of maximum size. We can find the maximal matching using a greedy algorithm. C := set of 2 | M| nodes in M. C is a vertex cover. $|C^*| \geq |M|$. $|C|=2|M| \leq 2|C^*|$. 


### Center Selection
metric: d(x,x) = 0, d(x,y) = d(y,x). Triangle equality: d(x,z) $\leq$ d(x,y)+d(y,z). We are given a set S of sites (points) at a positive integer k > 0. Goal is to find another set c of k points such that we minimize the distance sites have to centers. We can reformulate this with covering. Disk of radius r with center c. Cover S by k disks of min radius r. Here we have one Greedy algorithm for approximating this. It will output some C $\subseteq$ S. First say that C is some arbitrary site. Repeat k-1 times: Choose some s $\in$ S where s is the most disadvantaged site. 

Claim: If a solution with with radius r exists, then the algorithm finds a solutions with radius 2r.  

#### [[Dominating Set]]
Goal is to find the dominating set of minimum size. We can reduce dominating set to set cover problem. This is a $O(log n)$ approximation. 

We can also reduce from set cover to dominating set. Given u, |u| = n, sets $S_i \in u (i \in I)$. Construct: Graph G = (V,E), V := $u \cup I$. And E containing all edges ij, where $i \in I$, $u \in U$, $u \in S_{i,j}$,  and $ij, i \in I, j \in I$. Set cover with k sets exists is equivalent to dominate set with k nodes exist in G. 


\-\-\-
# References