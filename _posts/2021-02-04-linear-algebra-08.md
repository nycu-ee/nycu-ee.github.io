---
layout: post
title: 線性代數筆記-08
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=9&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第八講：求解$Ax=b$：可解性和解的結構

舉例，同上一講：$3 \times 4$矩陣
$$
A=
\begin{bmatrix}
1 & 2 & 2 & 2\\
2 & 4 & 6 & 8\\
3 & 6 & 8 & 10\\
\end{bmatrix}
$$，求$Ax=b$的特解：

寫出其增廣矩陣（augmented matrix）$\left[\begin{array}{c\|c}A & b\end{array}\right]$：

$$
\left[
\begin{array}{c c c c|c}
1 & 2 & 2 & 2 & b_1 \\
2 & 4 & 6 & 8 & b_2 \\
3 & 6 & 8 & 10 & b_3 \\
\end{array}
\right]
\underrightarrow{消元}
\left[
\begin{array}{c c c c|c}
1 & 2 & 2 & 2 & b_1 \\
0 & 0 & 2 & 4 & b_2-2b_1 \\
0 & 0 & 0 & 0 & b_3-b_2-b_1 \\
\end{array}
\right]
$$

顯然，有解的必要條件為$b_3-b_2-b_1=0$。

討論$b$滿足什麽條件才能讓方程$Ax=b$有解（solvability condition on b）：當且僅當$b$屬於$A$的行空間時。另一種描述：如果$A$的各列線性組合得到$0$列，則$b$端分量做同樣的線性組合，結果也為$0$時，方程才有解。

解法：令所有自由變量取$0$，則有
$$
\Big\lbrace
\begin{eqnarray*}
x_1 & + & 2x_3 & = & 1 \\
    &   & 2x_3 & = & 3 \\
\end{eqnarray*}
$$
，解得
$$
\Big\lbrace
\begin{eqnarray*}
x_1 & = & -2 \\
x_3 & = & \frac{3}{2} \\
\end{eqnarray*}
$$
，代入$Ax=b$求得特解
$$
x_p=
\begin{bmatrix}
-2 \\\\ 0 \\\\ \frac{3}{2} \\\\ 0
\end{bmatrix}
$$。

令$Ax=b$成立的所有解：
$$
\Big\lbrace
\begin{eqnarray}
A & x_p & = & b \\
A & x_n & = & 0 \\
\end{eqnarray}
\quad
\underrightarrow{兩式相加}
\quad
A(x_p+x_n)=b
$$

即$Ax=b$的解集為其特解加上零空間，對本例有：
$$
x_{complete}=
\begin{bmatrix}
-2 \\ 0 \\ \frac{3}{2} \\ 0
\end{bmatrix}
+
c_1\begin{bmatrix}-2\\1\\0\\0\\\end{bmatrix}
+
c_2\begin{bmatrix}2\\0\\-2\\1\\\end{bmatrix}
$$

對於$m \times n$矩陣$A$，有矩陣$A$的秩$r \leq min(m, n)$

列滿秩$r=n$情況：
$$
A=
\begin{bmatrix}
1 & 3 \\
2 & 1 \\
6 & 1 \\
5 & 1 \\
\end{bmatrix}
$$
，$rank(A)=2$，要使$Ax=b, b \neq 0$有非零解，$b$必須取$A$中各行的線性組合，此時A的零空間中只有$0$向量。

行滿秩$r=m$情況：
$$
A=
\begin{bmatrix}
1 & 2 & 6 & 5 \\
3 & 1 & 1 & 1 \\
\end{bmatrix}
$$
，$rank(A)=2$，$\forall b \in R^m都有x \neq 0的解$，因為此時$A$的行空間為$R^m$，$b \in R^m$恒成立，組成$A$的零空間的自由變量有n-r個。

行列滿秩情況：$r=m=n$，如
$$
A=
\begin{bmatrix}
1 & 2 \\
3 & 4 \\
\end{bmatrix}
$$
，則$A$最終可以化簡為$R=I$，其零空間只包含$0$向量。

總結：

$$\begin{array}{c|c|c|c}r=m=n&r=n\lt m&r=m\lt n&r\lt m,r\lt n\\R=I&R=\begin{bmatrix}I\\0\end{bmatrix}&R=\begin{bmatrix}I&F\end{bmatrix}&R=\begin{bmatrix}I&F\\0&0\end{bmatrix}\\1\ solution&0\ or\ 1\ solution&\infty\ solution&0\ or\ \infty\ solution\end{array}$$
