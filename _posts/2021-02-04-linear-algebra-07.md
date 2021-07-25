---
layout: post
title: 線性代數筆記-07
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=8&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第七講：求解$Ax=0$，主變量，特解

舉例：$3 \times 4$矩陣
$$
A=
\begin{bmatrix}
1 & 2 & 2 & 2 \\
2 & 4 & 6 & 8 \\
3 & 6 & 8 & 10 \\
\end{bmatrix}
$$，求$Ax=0$的特解：

找出主變量（pivot variable）：
$$
A=
\begin{bmatrix}
1 & 2 & 2 & 2\\
2 & 4 & 6 & 8\\
3 & 6 & 8 & 10\\
\end{bmatrix}
\underrightarrow{消元}
\begin{bmatrix}
\underline{1} & 2 & 2 & 2\\
0 & 0 & \underline{2} & 4\\
0 & 0 & 0 & 0\\
\end{bmatrix}
=U
$$
主變量（pivot variable，下劃線元素）的個數為2，即矩陣$A$的秩（rank）為2，即$r=2$。

主變量所在的行為主行（pivot column），其余列為自由行（free column）。

自由行中的變量為自由變量（free variable），自由變量的個數為$n-r=4-2=2$。

通常，給自由行變量賦值，去求主行變量的值。如，令$x_2=1, x_4=0$求得特解
$x=c_1\begin{bmatrix}-2\\\\1\\\\0\\\\0\\\\\end{bmatrix}$；
再令$x_2=0, x_4=1$求得特解
$x=c_2\begin{bmatrix}2\\\\0\\\\-2\\\\1\\\\\end{bmatrix}$。

該例還能進一步簡化，即將$U$矩陣化簡為$R$矩陣（Reduced row echelon form），即簡化列階梯形式。

在簡化列階梯形式中，主元上下的元素都是$0$：
$$
U=
\begin{bmatrix}
\underline{1} & 2 & 2 & 2\\
0 & 0 & \underline{2} & 4\\
0 & 0 & 0 & 0\\
\end{bmatrix}
\underrightarrow{化簡}
\begin{bmatrix}
\underline{1} & 2 & 0 & -2\\
0 & 0 & \underline{1} & 2\\
0 & 0 & 0 & 0\\
\end{bmatrix}
=R
$$
將$R$矩陣中的主變量放在一起，自由變量放在一起（行交換），得到
$$
R=
\begin{bmatrix}
\underline{1} & 2 & 0 & -2\\
0 & 0 & \underline{1} & 2\\
0 & 0 & 0 & 0\\
\end{bmatrix}
\underrightarrow{行交換}
\left[
\begin{array}{c c | c c}
1 & 0 & 2 & -2\\
0 & 1 & 0 & 2\\
\hline
0 & 0 & 0 & 0\\
\end{array}
\right]
=
\begin{bmatrix}
I & F \\
0 & 0 \\
\end{bmatrix}
\textrm{，其中}I\textrm{為單位矩陣，}F\textrm{為自由變量組成的矩陣}
$$
計算零空間矩陣$N$（nullspace matrix），其列為特解，有$RN=0$。

$$
x_{pivot}=-Fx_{free} \\
\begin{bmatrix}
I & F \\
\end{bmatrix}
\begin{bmatrix}
x_{pivot} \\
x_{free} \\
\end{bmatrix}=0 \\
N=\begin{bmatrix}
-F \\
I \\
\end{bmatrix}
$$

在本例中
$$
N=
\begin{bmatrix}
-2 & 2 \\
0 & -2 \\
1 & 0 \\
0 & 1 \\
\end{bmatrix}
$$，與上面求得的兩個$x$特解一致。

另一個例子，矩陣
$$
A=
\begin{bmatrix}
1 & 2 & 3 \\
2 & 4 & 6 \\
2 & 6 & 8 \\
2 & 8 & 10 \\
\end{bmatrix}
\underrightarrow{消元}
\begin{bmatrix}
1 & 2 & 3 \\
0 & 2 & 2 \\
0 & 0 & 0 \\
0 & 0 & 0 \\
\end{bmatrix}
\underrightarrow{化簡}
\begin{bmatrix}
1 & 0 & 1 \\
0 & 1 & 1 \\
0 & 0 & 0 \\
0 & 0 & 0 \\
\end{bmatrix}
=R
$$

矩陣的秩仍為$r=2$，有$2$個主變量，$1$個自由變量。

同上一例，取自由變量為$x_3=1$，求得特解
$$
x=c
\begin{bmatrix}
-1 \\
-1 \\
1 \\
\end{bmatrix}
$$
