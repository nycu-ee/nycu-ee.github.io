---
layout: post
title: 線性代數筆記-04
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=5&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第四講：$A$ 的 $LU$ 分解

$AB$的逆矩陣：
$$
\begin{aligned}
A \cdot A^{-1} = I & = A^{-1} \cdot A\\
(AB) \cdot (B^{-1}A^{-1}) & = I\\
\textrm{則} AB \textrm{的逆矩陣為} & B^{-1}A^{-1}
\end{aligned}
$$

$A^{T}$的逆矩陣：
$$
\begin{aligned}
(A \cdot A^{-1})^{T} & = I^{T}\\
(A^{-1})^{T} \cdot A^{T} & = I\\
\textrm{則} A^{T} \textrm{的逆矩陣為} & (A^{-1})^{T}
\end{aligned}
$$

## 將一個 $n$ 階方陣 $A$ 變換為 $LU$ 需要的計算量估計：

1. 第一步，將$a_{11}$作為主元，需要的運算量約為$n^2$
$$
\begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1} & a_{n2} & \cdots & a_{nn} \\
\end{bmatrix}
\underrightarrow{消元}
\begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
0      & a_{22} & \cdots & a_{2n} \\
0      & \vdots & \ddots & \vdots \\
0      & a_{n2} & \cdots & a_{nn} \\
\end{bmatrix}
$$

2. 以此類推，接下來每一步計算量約為$(n-1)^2、(n-2)^2、\cdots、2^2、1^2$。

3. 則將 $A$ 變換為 $LU$ 的總運算量應為$O(n^2+(n-1)^2+\cdots+2^2+1^2)$，即$O(\frac{n^3}{3})$。

置換矩陣(Permutation Matrix)：

3階方陣的置換矩陣有6個：
$$
\begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1 \\
\end{bmatrix}
\begin{bmatrix}
0 & 1 & 0 \\
1 & 0 & 0 \\
0 & 0 & 1 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 1 \\
0 & 1 & 0 \\
1 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
1 & 0 & 0 \\
0 & 0 & 1 \\
0 & 1 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 1 & 0 \\
0 & 0 & 1 \\
1 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 1 \\
1 & 0 & 0 \\
0 & 1 & 0 \\
\end{bmatrix}
$$

$n$階方陣的置換矩陣有$\binom{n}{1}=n!$個。
