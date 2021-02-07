---
layout: post
title: 線性代數筆記-10
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=11&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第十講 四個基本子空間

對於$m \times n$矩陣$A$，$rank(A)=r$有：

* 列空間$C(A^T) \in \mathbb{R}^n, dim C(A^T)=r$，基見例1。

* 零空間$N(A) \in \mathbb{R}^n, dim N(A)=n-r$，自由元所在的行即可組成零空間的一組基。

* 行空間$C(A) \in \mathbb{R}^m, dim C(A)=r$，主元所在的行即可組行空間的一組基。

* 左零空間$N(A^T) \in \mathbb{R}^m, dim N(A^T)=m-r$，基見例2。

例1，對於列空間
$$
A=
\begin{bmatrix}
1 & 2 & 3 & 1 \\
1 & 1 & 2 & 1 \\
1 & 2 & 3 & 1 \\
\end{bmatrix}
\underrightarrow{消元、化簡}
\begin{bmatrix}
1 & 0 & 1 & 1 \\
0 & 1 & 1 & 0 \\
0 & 0 & 0 & 0 \\
\end{bmatrix}
=R
$$

由於我們做了列變換，所以A的行空間受到影響，$C(R) \neq C(A)$，而列變換並不影響列空間，所以可以在$R$中看出前兩列就是列空間的一組基。

所以，可以得出無論對於矩陣$A$還是$R$，其列空間的一組基，可以由$R$矩陣的前$r$列向量組成（這里的$R$就是第七講提到的簡化列階梯形式）。

例2，對於左零空間，有$A^Ty=0 \rightarrow (A^Ty)^T=0^T\rightarrow y^TA=0^T$，因此得名。

采用Gauss-Jordan消元，將增廣矩陣$\left[\begin{array}{c\|c}A_{m \times n} & I_{m \times m}\end{array}\right]$中$A$的部分劃為簡化列階梯形式$\left[\begin{array}{c\|c}R_{m \times n} & E_{m \times m}\end{array}\right]$，此時矩陣$E$會將所有的列變換記錄下來。

則$EA=R$，而在前幾講中，有當$A'$是$m$階可逆方陣時，$R'$即是$I$，所以$E$就是$A^{-1}$。

本例中

$$
\left[\begin{array}{c|c}A_{m \times n} & I_{m \times m}\end{array}\right]=
\left[
\begin{array}
{c c c c|c c c}
1 & 2 & 3 & 1 & 1 & 0 & 0 \\
1 & 1 & 2 & 1 & 0 & 1 & 0 \\
1 & 2 & 3 & 1 & 0 & 0 & 1 \\
\end{array}
\right]
\underrightarrow{消元、化簡}
\left[
\begin{array}
{c c c c|c c c}
1 & 0 & 1 & 1 & -1 & 2 & 0 \\
0 & 1 & 1 & 0 & 1 & -1 & 0 \\
0 & 0 & 0 & 0 & -1 & 0 & 1 \\
\end{array}
\right]
=\left[\begin{array}{c|c}R_{m \times n} & E_{m \times m}\end{array}\right]
$$

則

$$
EA=
\begin{bmatrix}
-1 & 2  & 0 \\
1  & -1 & 0 \\
-1 & 0  & 1 \\
\end{bmatrix}
\cdot
\begin{bmatrix}
1 & 2 & 3 & 1 \\
1 & 1 & 2 & 1 \\
1 & 2 & 3 & 1 \\
\end{bmatrix}
=
\begin{bmatrix}
1 & 0 & 1 & 1 \\
0 & 1 & 1 & 0 \\
0 & 0 & 0 & 0 \\
\end{bmatrix}
=R
$$


很明顯，式中$E$的最後一列對$A$的列做線性組合後，得到$R$的最後一列，即$0$向量，也就是$y^TA=0^T$。

最後，引入矩陣空間的概念，矩陣可以同向量一樣，做求和、數乘。

舉例，設所有$3 \times 3$矩陣組成的矩陣空間為$M$。則上三角矩陣、對稱矩陣、對角矩陣（前兩者的交集）。

觀察一下對角矩陣，如果取
$$
\begin{bmatrix}
1 & 0 & 0 \\
0 & 0 & 0 \\
0 & 0 & 0 \\
\end{bmatrix} \quad
\begin{bmatrix}
1 & 0 & 0 \\
0 & 3 & 0 \\
0 & 0 & 0 \\
\end{bmatrix} \quad
\begin{bmatrix}
0 & 0 & 0 \\
0 & 0 & 0 \\
0 & 0 & 7 \\
\end{bmatrix}
$$
，可以发現，任何三階對角矩陣均可用這三個矩陣的線性組合生成，因此，他們生成了三階對角矩陣空間，即這三個矩陣是三階對角矩陣空間的一組基。
