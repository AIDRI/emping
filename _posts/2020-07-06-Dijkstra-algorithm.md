---
layout: post
title:  "Dijkstra algorithm"
date:   2020-07-07 00:08:00 -0200
categories: algorithm
---

<img src="https://d1fmx1rbmqrxrr.cloudfront.net/cnet/optim/i/edit/2019/04/eso1644bsmall__w770.jpg" blank="">

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


So, let's quickly explain this script  
The principle of the loop is to assign each vertice a weight that will be equal to $$+\infty$$.  
Afterwards, we give the program the number of the original vertice, then we define two lists: one to store the processed vertices, one to store the unprocessed vertices.  

**Processing**  

While $$X \neq \emptyset$$ do  
&nbsp;&nbsp;&nbsp;&nbsp;Select in $$X$$ the vertice $$x$$ with the minimum $$\delta_s(x)$$  
&nbsp;&nbsp;&nbsp;&nbsp;Delete the vertice $$x$$ in $$X$$  
&nbsp;&nbsp;&nbsp;&nbsp;Add $$x$$ to $$E$$  
&nbsp;&nbsp;&nbsp;&nbsp;For each $$y \in V^+(x) \cap X$$ do  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If $$\delta_s(y) > \delta_s(x) + l(x,y)$$ then  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$$\delta_s(y) \leftarrow \delta_s(x) + l(x,y)$$  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$$p(y) \leftarrow x$$  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;End if  
&nbsp;&nbsp;&nbsp;&nbsp;End for  
End while  

After initializing my algorithm, we need to process each vertice in $$X$$.  
First, we are going to select the vertice with the minimum weight to move it into the $$E$$ list, where are the already process vertices.  
Second, we are going to review all $$y$$, $$y$$ being the successors of $$x$$.  
Third, if the weight of $$s_0$$ is greater than the previously established path plus the distance between $$x$$ and $$y$$, then we are define the temporary minimum distance between $$s_0$$ and $$y$$.  

### 3. Implementation in Python

After learning this algorithm, I am doing the problem 20C on [codeforce](https://codeforces.com/).  
Here is my [implementation](https://github.com/AIDRI/codeforce/blob/master/20C.py) of the algorithm, by adapting it to the setpoint and input format.
