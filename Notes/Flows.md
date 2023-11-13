20231109 - 10:24

Status: #idea

Tags: [[Algorithms]]

# Flows
We have a directed weighted graph. The weight means the capacity, meaning the amount that can be "transported" on that edge in one time unit, this capacity will always be a positive integer, larger than 0. We than have a s (source) and t (sink). Goal is then to transport from s to t with maximum capacity. 

Formally this is a function f: E $\rightarrow R^{\geq 0}$ is a flow if $\forall e \in E: 0 \leq f(e) \leq c_e$. Also $\forall v \in V \{s,t\}: f^-(v) = f^+(v)$. $f^-$ means the incoming flow and $f^+$ is the outgoing flow. The outgoing flow will at max be that which comes in, meaning nothing is added in between. $val(f) := f^+(s) - f^-(s)$. f is maximum flow if val(f) is maximized. 

Flows is actually a [[Linear Programming]] problem. 

One might consider using a greedy algorithm and split output based capacity. But this will not hold, instead we need a smarter algorithm. 

Residual graph $G_f$
* Some node set as G
* For every $e \in E$ with $f(e) < c_e$, create a forward edge with capacity $c_e - f(e)$
* For every $e \in E$ with $f(e) > 0$, create a backward edge with capacity $f(e)$.  

P: any directed s-t path in $G_p$ 
b: Smallest residual capacity on P. (b>0). 

Then for each forward edge we add b, and on backward edges we subtract b. 

$f'(e) :=$ 
	$f(e+b)$ if $e \in P, forward$, 
	$f(e) -b$ if $e\in P, backward$
	$f(e), else$

f' is a flow $val(f')$ = val(f)+b. P is augmenting path. 

## Ford-Fulkerson (FF) Algorithm
* For edges, set the flow of the edge to 0. 
* Repeat as long as possible: 
	* Find some augmenting path in $G_p$
	* Compute $f'$ 
	* $f := f'$

#### To prove
If $G_f$ has no argument path, then $val(f)$ is maximal. For this proof we need some definitions. 

Cut: A partitioning of the node set V into two disjoint subsets A and B such that $A=A \cup B$ with $A \cap B = \emptyset$, $s \in A, t \in B$. Capacity of cut is weight of edges which connect A and B. 

For any $S \in V$ define: 
$f^-(S) = \sum_{e=(u,v), u \not\in s, v \in s}(e)$  
$f^+(S) = \sum_{e=(u,v), u \in s, v \not\in s}(e)$  

(A,B) cut $\implies val(f)=f^+(A)-f^-(A)$

$val(f) \leq f^+(A) = \sum f(e)$


## Applications of flows
* [[Bipartite Matching]]
* [[Edge Disjoint Paths]]
* [[Disconnecting Edge Sets]]
* [[Survey Design]]

# Flows with demands
Given a directed graph G. $0 \leq l_e \leq c_e$ for every $e \in E$. $d(v)$: Demand of $v \in V$.  We can now define these new flows as: $$f: E \rightarrow R^{\geq 0}$$This is a circulation if $\forall e \in E: l_e \leq f(e) \leq c_e$ and  
$\forall v \in V: f^-(v)-f^+(v)=d(v)$. 

$S = \{v | d(v) < 0\}, T=\{v | d(v) > 0$. 
A first question is if a circulation exists? 

This can be split into a number of different cases. 

Case $\forall e: l_e = 0$, this gives us $\sum_{v \in V}d(v) = 0$, then we get $d := \sum_{v \in T}d(v) = -\sum_{v \in S}d(v)$. Here we also have the following constraints: $d > 0, S \neq \emptyset, T \neq \emptyset$. 

CF-red, see slides for this

We also have a general case. 

\-\-\-
# References