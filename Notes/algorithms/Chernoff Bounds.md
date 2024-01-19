20231211 - 13:17

Status: #idea

Tags: [[Algorithms]]

# Chernoff Bounds
A class of similar bounds. 

Consider n coins, we want to know how often we get heads, and the probability of deviating largely from this. 

$x_i$ = 1, prob $p_i$ and 0, prob, $1-p_i$. $x_i$ mutually independent. $X = \sum_{i=1}^n x_i$. $\mu = E[x_i] = p_i$. $E[X] = \sum_{i=1}^n p_i$. $Pr(X > (1 + \delta)\mu) \leq ?$. Note that all of this reasoning is only valid if the probabilities are mutually independent.  

### Markov's inequality
Y = Positive random number
y > 0 : real number
$E[Y] \geq \gamma * Pr(Y > \gamma)$
$Pr(Y \geq \gamma) \leq \frac{E[Y]}{\gamma}$

$e^{tX}$ where $t > 0$, parameter
$$Pr(e^{tX} > e^{t(1+\gamma))\mu}) \leq \frac{E[e^{tX}]}{e^{t(1+\gamma)\mu}}$$
$Y := e^{tX}$ r(\)
$\gamma := e^{t(1+\gamma)\mu}$

$$E[e^{tX}]= E[e^{t \sum_{i=1}^n x_i}] = E[\Pi_{i=1}^n e^{t x_i}] = \Pi_{i=1}^n E[e^{t*x_i}] = \Pi_{i=1}^n(p_i e^t + (1-p_i)) =
$$
$$Pi_{i=1}^n(1+p_i(e^t-1) \leq \Pi_{i=1}^n e^{p_i(e^t - 1)} = e^{\sum_{i=1}^n p_i (e^t - 1)} = e^{\mu(e^t - 1)} = $$
$t := ln(1+\delta)$ $$e^{\mu \delta}$$
$$Pr(X < (1+ \delta) \mu) \leq (\frac{e^\delta}{(1+\delta)^{(1+\delta)}})^\delta$$

We can also that hte fraction above will be smaller than 1. Then we get $e^{- \delta^2\mu}$. 


### Load Balancing
Consider n jobs and n machines. Jobs choose machines independently and at random. $Y_i$ is number of jobs assigned to machine i. 

**Balls and Bins**: Assume we have a number of bins, and then throw balls into these bins. Many would assume that each bin has roughly same value. But this is not the case. 

Back to load balancing: $Pr(Y_i) > c \leq ?$ where c is some threshold. We want to find the probability that some machine is heavily loaded. $Pr(\exists i: Y_i > c) \leq ?$. For this we apply the Chernoff bounds. 

$E[Y_i] = 1$
$\delta = c-1$
$$\frac{e^{\delta}}{(1+\delta)^{1+\delta}} = \frac{e^{c-1}}{c^c} < (\frac{e}{c})^c$$
This would be the bound for one, the bound for all of the machines: 
$$Pr(\exists i: Y_i > c) \leq n (\frac{e}{c})^c$$
For which c is this "small"? $c^c > n$ is necessary. 
We define x by $x^x = n$ 
$x * log (x) = log (n)$ 
$log(x) + log(log(x)) = log(log(n))$
$log(x) < log(log(n)) < 2 log(x)$
$$\frac{1}{x} < \frac{log(log(n))}{log(n)} < \frac{2}{x}$$
$$x = \frac{log(n)}{log(log(n))}$$
With c = ex we get: 
$$n(\frac{e}{c})^c = \frac{n}{x^{x*e}} < \frac{n}{x^{x*2}} = \frac{1}{n}$$
With probability > $1 - \frac{1}{n}$, all loads are $O(\frac{log(n)}{log(log(n))})$

### Verify a Matrix Product
A, B: n x n matrices. Is $A*B$ = C. So we are given A, B and C. And want to verify if $A*B$ is actually C. Using the usual method of matrix multiplication we need $O(n^3)$. One way to verify the result would of course be to calculate it again, but this would clearly take $O(n^3)$. Our goal is to do this in a shorter amount of time, but with some small probability that our algorithm gives the wrong result. x = vector of length n. If AB=C then ABx = Cx. Note that in this case we need to calculate A(Bx)= Cx. Otherwise we are just doing our matrix multiplication again. But the other way is not true, it might be the case that A(Bx) = Cx but not AB  = C. So we instead use a random vector. We will use a binary vector. Where each bit is chosen with a probability of 0.5 independently. 

The interesting case is when AB != C. We define D = AB - C. Z is defined as the first value after the multiplication. As D is non-zero Z != 0 with a probability $\geq 0.5$. After doing this once we will have a probability 0.5 of being able to trust our result. But we do this test multiple times, which gives us $0.5^t$. This is called Freivald's technique. 










\-\-\-
# References