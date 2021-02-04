---
layout: post
title: 線性代數筆記-06
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=7&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第六講：行空間和零空間

對向量子空間$S$和$T$，有$S \cap T$也是向量子空間。

對$m \times n$矩陣$A$，$n \times 1$矩陣$x$，$m \times 1$矩陣$b$，運算$Ax=b$：

$$
\begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1(n-1)} & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2(n-1)} & a_{2n} \\
\vdots & \vdots & \ddots & \vdots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{m(n-1)} & a_{mn} \\
\end{bmatrix}
\cdot
\begin{bmatrix}
x_{1} \\
x_{2} \\
\vdots \\
x_{n-1} \\
x_{n} \\
\end{bmatrix}
=
\begin{bmatrix}
b_{1} \\
b_{2} \\
\vdots \\
b_{m} \\
\end{bmatrix}
$$

由$A$的行向量生成的子空間為$A$的行空間；

$Ax=b$有非零解當且僅當$b$屬於$A$的行空間

A的零空間是$Ax=0$中$x$的解組成的集合。
