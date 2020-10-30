---
layout: post
title:  "Matrix multiplication with a time complexity lower than $O(N^3)$"
date:   2020-10-30 00:08:00 -0200
categories: algorithm
---

> In this post, we will try to understand differents algorithms for matrix multiplication with a time complexity lower than $O(N^3)$.  

> We will study three different algorithms : Strassen's algorithm, Coppersmith & Winograd's algorithm and finally William's algorithm.  

> The complexity of the algorithms will decrease as the post progresses.  

> You can find other posts on my [blog](https://aidri.github.io/emping/blog/).  

> Some characters can bug on the phone version.

For the following algorithms, we will base ourselves on two matrix $A$ and $B$ such as :
$$A = \begin{bmatrix} A11 & A12 //
A21 & A22 \end{bmatrix}$$

## 1. Basics  

Matrix multiplication is a very simple operation in linear algebra.  
The naive method of a multiplication of matrices would like us to proceed in this way :  
