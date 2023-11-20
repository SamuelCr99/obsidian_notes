20231116 - 10:08

Status: #idea

Tags: [[Flows]], [[Algorithms]]

# Airline Scheduling
Given DAG of flights and reachability relations, k number of planes. The questions is if we can operate all flights by k planes? 

We create a source and a sink and add all nodes to the left to the source and all nodes at the right to the sink. 

We then set demands, $d(s) = -k$, $d(t)=+k$, $d(v) = 0$, $\forall v \pm s,t$. We then set the lower capacity of all flight edges to 1, also set the upper capacity to 1. When a flight is reused we set the lower bound to 0, and upper bound to 1. 
\-\-\-
# References