20231116 - 11:00

Status: #idea

Tags: [[Flows]], [[Algorithms]]

# Project Selection
P is a set of projects, $p_i$ = profit of $i \in P$. $p_i > 0$ or $p_i < 0$. Set of constraints, $i \implies j$ which can be read as "if i then j". So some projects need that we have finished other projects before we can begin them. This can be visualized using a DAG, as if it was not a DAG then we could never start any of them. 

Another name for this problem is the open pit mining problem. 

$A \subseteq P$ is  feasible if $\forall i \in A, (i,j) \in E : j \in A$. Find a feasible $A \subseteq P$ with max $\sum_{a \in A} P_i$. 

### Proof of equivalence
$c (A \cup \{s\}, B \cup {t})$




\-\-\-
# References