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
$$A = 
\begin{bmatrix} 
A_{11} & A_{12} \\  
A_{21} & A_{22} 
\end{bmatrix} 
and\ B = 
\begin{bmatrix} 
B_{11} & B_{12} \\  
B_{21} & B_{22} 
\end{bmatrix} $$  
The objective is to get a final matrix $C$ such as :  
$$C = 
\begin{bmatrix} 
C_{11} & C_{12} \\  
C_{21} & C_{22} 
\end{bmatrix}$$

## 1. Basics  

On this part, we are going to see the basics of matrix multiplication, and fix the problematic.

Matrix multiplication is a very simple operation in linear algebra.  
The naive method of a multiplication of matrices would like us to proceed in this way :  
$C_{11} = A_{11} \times B_{11} + A_{12} \times B_{21}$  
$C_{12} = A_{11} \times B_{12} + A_{12} \times B_{22}$  
$C_{21} = A_{21} \times B_{11} + A_{22} \times B_{21}$  
$C_{22} = A_{21} \times B_{12} + A_{22} \times B_{22}$  
Here, we use 8 operations.  
This method is very easy to compute by hands, but when we have big matrices, this algorithm is too slow to be used. So we need to found an algorithm with a complexity lower than $O(N^3)$.  

## 2. Strassen algorithm : $O(N^{2.81})$  

### 2.1 Algorithm for $n = 2$  

So Strassen wanted to simplify this naive algorithm by using a new combination of multiplications.  
We thus go from 8 to 7 multiplications.  
First, we have to calculate M seven times :  
$E_1 = (A_{11} - A_{22}) (B_{11} + B_{22})$  
$E_2 = (A_{21} + A_{22}) B_{11}$  
$E_3 = A_{11} (B_{12} - B_{22})$  
$E_4 = A_{22} (B_{21} - B_{11})$  
$E_5 = (A_{11} + A_{12}) B_{22}$  
$E_6 = (A_{21} - A_{11}) (B_{11} + B_{12})$  
$E_7 = (A_{12} - A_{22}) (B_{21} + B_{22})$  

And now, we can compute each C :  
$C_{11} = E_1 + E_4 - E_5 + E_7$  
$C_{12} = E_3 + E_5$  
$C_{21} = E_2 + E_4$  
$C_{22} = E_1 - E_2 + E_3 + E_6$  

We have therefore calculated the matrix C.  
With 7 multiplications and 18 additions / substractions, we can think that the algorithm does not perform well compared to the naive algorithm.  
We will therefore prove the opposite by generalizing this algorithm for a matrix $N \times N$.  

### 2.2 Generalization  

We will now use the algorithm seen above, but recursively.  
Before that, we must partition our C matrix into four blocks $C_{11}, C_{12}, C_{21}, C_{22}$ of size $N/2 \times N/2$.  

$$C_{11} = 
\begin{bmatrix} 
C_{11} & C_{12} & ... & C_{1, N/2}\\  
C_{21} & ... & ... & ...\\  
... & ... & ... & ...\\  
C_{N/2, 1} & ... & ... & C_{N/2, N/2}\\  
\end{bmatrix} 
\ \ \ \ \ C_{12} = 
\begin{bmatrix} 
C_{1, N/2 + 1} & ... & ... & C_{1, N}\\  
... & ... & ... & ...\\  
... & ... & ... & ...\\  
C_{N/2, N/2 + 1} & ... & ... & C_{N/2, N}\\  
\end{bmatrix} $$  
$$C_{21} = 
\begin{bmatrix} 
C_{N/2 + 1, 1} & ... & ... & C_{N/2 + 1, N/2}\\  
... & ... & ... & ...\\  
... & ... & ... & ...\\  
C_{N, 1} & ... & ... & C_{N, N/2}\\  
\end{bmatrix} 
C_{22} = 
\begin{bmatrix} 
C_{N/2 + 1, N/2 + 1} & ... & ... & C_{N/2 + 1, N}\\  
... & ... & ... & ...\\  
... & ... & ... & ...\\  
C_{N, N/2 + 1} & ... & ... & C_{N, N}\\  
\end{bmatrix} $$  

Now, we can do the same thing on A and B.  

I think we can now see what Strassen wanted to do.  
From $2^n$, we get sub matrices $A_{ij}, B_{ij}, C_{ij}$ of size $2^{n-1}$. So there is indeed a recursive algorithm.  

The complexity of this algorithm is : $O(N^{log_2 7+o(1)})$ or $O(N^{2.8074...})$.  

### 2.3 Usage and improvements  

As we have seen, it is preferable to use a naive algorithm for matrix calculations with a small n ($2^n$ with $n < 9$).  
To optimize a multiplication with a very large n or even very very large n, we can therefore start by using the Strassen algorithm, to finish with the naive agorithm.  
In 1970, Winograd improved this algorithm, from 18 to 15 additions / subtractions. Winograd, Hopcroft and Kerr were able to demonstrate that it was impossible to multiply $2 \times 2$ matrices with less than 7 multiplications.


## 3. Coppersmith & Winograd algorithm $O(N^{2,404})$  

### 3.1 Definitions  

**Definition 1** : Let $V, W, X$, three vector spaces over the same field $F$, which is a function $B : V \times W \rightarrow X$ such that for all $w \in W$, the map $B_w$, $v \rightarrow B(v,w)$ is a linear map from $V$ to $X$, and for all $v \in V$, the map $B_v$, $w \rightarrow B(v,w)$ is a linear map from $W$ to $X$.  
**Definiton 2** : A trilinear form of a matrix multiplication written $z_{ij} = \sum_{k \in n} x_{i,k}j_{k,j}$ for all $i, j \in [n]$ is the form $\sum_{i,j \in [n]} \sum_{k \in n} x_{ik}y_{kj}z_{ij}$  

### 3.2 Coppersmith & Winnograd algorithm  

First, we're going to define the algorithm.  
Let's define $\lambda$, an indeteminate value.  
Let's define $O(\lambda)$, the error term.  

The trilinear form of the CW is the following one :  
$\lambda^{-2} \times \sum^q_{i=1} (x_0 + \lambda x_i)(y_0 + \lambda y_i)(z_0 + \lambda z_i) - \lambda^{-3} \times (x_0 + \lambda^2 \sum^q_{i=1}x_i)(y_0 + \lambda^2 \sum^q_{i=1}y_i)(z_0 + \lambda^2 \sum^q_{i=1}z_i) + $  
$(\lambda^{-3} - q \lambda^{-2}) \times (x_0 + \lambda^3 x_{q+1})(y_0 + \lambda^3 y_{q+1})(z_0 + \lambda^3 x_{z+1})$  
$=$  
$x$
