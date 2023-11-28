20231128 - 10:05

Status: #idea

Tags: [[Data Science and AI]]

# Markov Models
Used in a variety of classification applications, usually in the time-series form. A Markov is a random process where **the next state only depends on the current state**. 

#### Markov chain
A Markov chain is a Markov process that jumps between states at discrete times. The sum of all outgoing edges must sum to 1. We can estimate the transition probability by counting the occurences that each state transitions to another. But where do we start? We can calculate the probability of being in the different states, and then create a Markov Chain from this. 

![[markov_chain.png]]

#### Hidden Markov models (HMMs)
Now the actual state of the process is hidden, and we only observe something that is related to the underlying state. 

For example we have a person Bob, his mood partly depends on the weather. From this we can guess the weather by looking at Bob's mood. In this case the we call the probability of Bob being sad given a rainy day the emission probability. 

From this we can draw conclusions of the probability that Bob is happy. By looking at the probability of Bob being happy given that it's sunny multiplied by the chance that is is sunny plus same but for rainy.

To calculate the probability of it being sunny we can use Bayes.  

![[markov_chain_bob.png]]

#### Markov Decision Processes 
A Markov Decision Process (MDP) is a Markov Chain extended with actions and rewards. Given the environment/world-state we can do 3 things: 
* We can take an action 
* The environment jumps to a new state 
* We receive a reward

If we want to approach this as a video game we can imagine that we have score as the reward and moving left/right/up/down as the action.

The objective is to find the policy that vies the maximum reward in the long run. If the sequence is finite then the sum converges. If it is infinite then the sum may diverge. 

We can also weight long-term rewards. In many cases rewards earlier is better than rewards later. We include this by the introduction of a discount factor in the model. 

This is an example of reinforcement learning. The challenge is to learn from experience and eventually find a policy that gives the maximum expected reward. Note that focusing on a reward in the short run or in the long run may give different results. 

Breakout can be viewed as an MDP. 

Bandit problems are a subset of problems which can with some success be modeled with MDPs. The agent will choose from k many different slot machines, and wants to maximize the cumulative reward.  Thompson sampling can be used to solve this. 

Exploration-exploitation trade off. Go to the usual restaurant or try a new one? If we just exploit early and never try new moves we might never find a good restaurant. But if we always explore we do not use the accumulated experience to improve. 

Epsilon-greedy algorithms: At each interactions, exploit with probability of $1 - \epsilon$, explore with $\epsilon$. 

#### Q-learning
A very general algorithm that can be used in many different algorithms. In Q-learning we assign a value $Q(s,a)$ to each initial state-action pair (s,a). We want to find a policy such that $\pi (s) = argmax Q(s,a)$

Q-learning is an iterative algorithm with update formula at time t. 

\-\-\-
# References