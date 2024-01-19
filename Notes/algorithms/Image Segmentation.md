20231116 - 10:24

Status: #idea

Tags: [[Flows]], [[Algorithms]]

# Image Segmentation
We are given an image and want to decide which parts of the image contain foreground and which contain background. 

We consider neighboring pixels. We then have local criteria which tell us if a pixel is more likely to be foreground or background. We call these numbers strength of belief. For each $i \in V$, $\{a_i, b_i\}$ is "strength of belief" that pixel is {foreground, background}. 

For each $(i,j) \in E, p_{i,j} > 0$ is penalty if i,j have different labels. This is used as we expect pixels close have similar labels. 

Goal is now to find A,B such that $A \cap B = \emptyset, A \cup B = V$ with max $q(A,B) = \sum_{i \in A}a_i + \sum_{j \in B}b_j - \sum_{i \in A, j \in B}P_{i,j}$. This would be equivalent to min $q'(A,B) = \sum_{i \in A}b_i + \sum_{j \in A}a_j + \sum_{i \in A, b \in B}P_{ij}$




\-\-\-
# References