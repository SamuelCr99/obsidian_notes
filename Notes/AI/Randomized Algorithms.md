20231116 - 11:31

Status: #idea

Tags: [[Algorithms]]

# Randomized Algorithms
## Basic facts about probabilty
Some basic facts about probability: 
* $\Omega$ = Set of elem events 
* Subsets of $\Omega$ are events. 
* $Pr: 2^\Omega \rightarrow [0,1]$ 
* $Pr(\emptyset)=0$
* $Pr(\Omega)=1$
* $A \cap B = \emptyset \implies Pr(A \cup B) = Pr(A)+Pr(b)$
* $Pr(\Omega \setminus A) = 1 - Pr(A)$ 
* $Pr(A \cup B) \leq Pr(A) + Pr(B)$, this is known as the union bound. 

#### Conditional Probability
$Pr(A|B) = Pr(A \cap B) / Pr(B)$. Is read as probability of A given B. 

A independent of B means $Pr(A|B) = P(A)$ which is equivalent to $Pr(A \cap B) = Pr(A)=Pr(B)$

Do not confuse independent and disjoint! 
### Random Variables
A random variable  $X: \Omega \rightarrow R$. $Pr(X = x) := Pr(X(w) = x)$. Distribution of X is $Pr(X=x)$ as a function of x. 

Expectation: $E[X] = \sum_{w \in \Omega}Pr(w)*X(w) = \sum_x Pr(X=x)*x$. NOTE: This is not the value one can expect, but rather a long running average. Take a dice for example, the expected value would be 3.5 but it is clearly impossible to get 3.5 on a 6 sided dice. Another misconception is what $Pr(X > E[X])$ should be. A common mistake is to say that it should be 0.5, this is clearly not true in most cases. 

$X,Y : \Omega \rightarrow R$. X and Y are independent if for all pair of values we have to following the joint probability is equal to the disjoint probability. Or in other words $$\forall x,y: Pr(X=x \land Y=y) = Pr(X = x) * Pr(Y=y)$$
* $(X+Y)(w) := X(w) + Y(w)$ 
* $(X*Y)(w) := X(w) * Y(w)$
* $f(X)(w) := f(X(w))$

### Linearity of Expectation
$E[X+Y] = E[X] + E[Y]$

Proof: $E[X+Y] = \sum_w Pr(w)*(X+Y)(w) = \sum_w Pr(w)*(X(w)+Y(w)) = E[X]+E[Y]$

If X and Y are independent then: $E[X*Y] = E[X]*E[Y]$. Note that the previous expression always holds while this only holds when X and Y are independent. 

### Repeat until Success
Coin flip. Where to probability of getting 1 has a probability of p and 0 has a probability of 1-p. How many independent trails until we get the first 1? We expect this to be 1/P. But we will prove it. 

Let $e_i$: Event that $i$ trails needed. $Pr(e_i)$ means that we succeed in step $e_i$. Meaning that all trails previously were not successful. So $Pr(e_i) = (1-p)^{i-1}p$. So $E[i] = \sum_{i=1}^{inf}(1-p)^{i-1}pi$. By solving this we get $\frac{1}{p}$. 

\-\-\-
# References