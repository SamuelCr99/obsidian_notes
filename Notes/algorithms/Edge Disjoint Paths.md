20231113 - 13:41

Status: #idea

Tags: [[Algorithms]], [[Flows]]

# Edge Disjoint Paths
Given a directed graph, find a man numbers k of edge-disjoint s-t paths. We create a network from the path. 

Let $c_e := 1$ for all $e \in E$. Compute a maximum flow, $k := val(f)$. Partition f into k s-t paths. To find these we choose any path and follow that until we get stuck, we know that we will only get stuck in the sink due to the rules of conservation. We keep applying this but delete any of the edges we just used to reach the sink.  

#### Time 
$O(mC) = O(mn)$






\-\-\-
# References