20231130 - 10:37

Status: #idea

Tags: [[Algorithms]] [[Randomized Algorithms]]

# Selection Problem
Given a set of n numbers in random order and an integer $k \leq n$. Find the kth smallest element (element of rank k).  

One solution would of course be to sort the array and then simply choose the kth element in the list. But this is too expensive. This can actually be solved using divide and conquer, but in this case the constant factor will be very large. 

We can solve this using a randomization algorithm, where the expected complexity will be $O(n)$ and worst case $O(n^2)$. 

Goal: Find a O(n) expected time Las Vegas algorithm. 

**Algorithm:**
* Choose some splitter s at random. 
* Compare s to all other elements. r := rank of s. 
* If r = k then return s. 
* If r > k then search among the elements smaller than s.
* If r < k then search among the elements larger than s. 
* Also update k := k - r. 

In each iteration we only need linear time, but how many times will we perform this operation? This depends on how good of a splitter we choose. We say that a splitter is central if its rank, is somewhere between $\frac{1}{4}n \leq r \leq \frac{3}{4}n$. If a splitter is central we get rid of at least 1/4.  

Algorithm is in phase j if the number of remaining elements is between $(\frac{3}{4})^{j+1}n$ and $(\frac{3}{4})^{j}n$. This means that we will move to a new phase each time we find a central splitter. The probability of choosing a central splitter is 1/2, therefore the expected time we spend in each phase is: $O((\frac{3}{4})^jn)$. Therefore the expected total time will be $O(n)$. 



\-\-\-
# References