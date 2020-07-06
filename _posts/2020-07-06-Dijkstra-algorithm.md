---
layout: post
title:  "Dijkstra algorithm"
date:   2020-06-18 13:07:00 -0200
categories: algorithm
---

## Dijkstra algorithm

### 1. History

The Dijkstra Algorithm is an algorithm invented by the Dutch computer scientist Edsger Dijkstra in 1959 to solve the shortest path problem. It belongs to the field of graph theory.

### 2. Algorithm

**Let's define some useful therms :**  

$$S$$ is the list of the vertices of the graph  
$$s_0$$ is the original vertice  
$$l(x,y)$$ is the weight of the edge (between two vertices)  
$$\delta_s(x)$$ is the length between the vertice $$s_0$$ and the vertice $$x$$  
$$V^+(x)$$ is the list of successors to vertice $$x$$  
$$p(x)$$ is the predecessor of the vertice $$x$$  
$$X$$ is the list of vertices still to be processed  
$$E$$ is the list of vertices already processed  

**Initialization**  

For each $$x \in S$$ do  
&nbsp;&nbsp;&nbsp;&nbsp;$$\delta_s(x) \leftarrow \infty$$  

$$\delta_s(s_0) \leftarrow 0$$  
$$X \leftarrow S$$  
$$E \leftarrow \emptyset$$

```
so, let's quickly explain this script  
The principle of the loop is to assign each peak a weight that will be equal to $$+\infty$$.  
Afterwards, we give the program the number of the original sumet, then we define two lists: one to store the processed vertices, one to store the unprocessed vertices.
```
