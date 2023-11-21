20231115 - 08:04

Status: #idea

Tags:

# Clustering


## K-means clustering
Not always perfect, and we can make it to be arbitrarily bad. 

## DBSCAN
From 1996. The ingredients for DBSCAN are: 
* A distance measure

First we do a labeling step where each node either becomes a 

## Hierarchical Clustering
We can use a dendrogram to show the entire hierarchical clustering process, without STOP. These dendrograms are always 2D graphs. 

## Bi-clustering

## Validating Clustering
A clustering is determines to be stable if removing a proportion of random points does not change the clustering fundamentally. So we want them to stay roughly in the same place. 

We can also look at co-occurence, for all pairs(i,j), count how frequently i and j are in the same cluster when we repeat. 

Silhouette coefficient: Is calculated using this formula: $$s = \frac{b-a}{max(a,b)}$$a: The mean distance between a sample and all other points in the same class 
b: The mean distance between a sample and all other points in the next nearest cluster. 

\-\-\-
# References