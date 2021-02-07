---
layout: post
title: 線性代數筆記-09
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=10&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第九講：線性相關性、基、維數

$v_1,\ v_2,\ \cdots,\ v_n$是$m\times n$矩陣$A$的行向量：

如果$A$零空間中有且僅有$0$向量，則各向量線性無關，$rank(A)=n$。

如果存在非零向量$c$使得$Ac=0$，則存在線性相關向量，$rank(A)\lt n$。

向量空間$S$中的一組基（basis），具有兩個性質：

1. 他們線性無關；
2. 他們可以生成$S$。

對於向量空間$\mathbb{R}^n$，如果$n$個向量組成的矩陣為可逆矩陣，則這$n$個向量為該空間的一組基，而數字$n$就是該空間的維數（dimension）。

舉例：
$$
A=
\begin{bmatrix}
1 & 2 & 3 & 1 \\
1 & 1 & 2 & 1 \\
1 & 2 & 3 & 1 \\
\end{bmatrix}
$$
，A的行向量線性相關，其零空間中有非零向量，所以$rank(A)=2=主元存在的行數=行空間維數$。

可以很容易的求得$Ax=0$的兩個解，如
$$
x_1=
\begin{bmatrix}
-1 \\
-1 \\
1 \\
0 \\
\end{bmatrix}, 
x_2=
\begin{bmatrix}
-1 \\
0 \\
0 \\
1 \\
\end{bmatrix}
$$，根據前幾講，我們知道特解的個數就是自由變量的個數，所以$n-rank(A)=2=自由變量存在的行數=零空間維數$

我們得到：行空間維數$dim C(A)=rank(A)$，零空間維數$dim N(A)=n-rank(A)$
