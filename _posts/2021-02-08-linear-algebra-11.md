---
layout: post
title: 線性代數筆記-11
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=12&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第十一講：矩陣空間、秩一矩陣和小世界圖

## 矩陣空間

接上一講，使用$3 \times 3$矩陣舉例，其矩陣空間記為$M$。

則$M$的一組基為：
$$
\begin{bmatrix}
1 & 0 & 0 \\
0 & 0 & 0 \\
0 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 1 & 0 \\
0 & 0 & 0 \\
0 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 1 \\
0 & 0 & 0 \\
0 & 0 & 0 \\
\end{bmatrix} \\
\begin{bmatrix}
0 & 0 & 0 \\
1 & 0 & 0 \\
0 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 0 \\
0 & 0 & 1 \\
0 & 0 & 0 \\
\end{bmatrix} \\
\begin{bmatrix}
0 & 0 & 0 \\
0 & 0 & 0 \\
1 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 0 \\
0 & 0 & 0 \\
0 & 1 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 0 \\
0 & 0 & 0 \\
0 & 0 & 1 \\
\end{bmatrix} \\
$$

易得，$dim M=9$。

所以可以得出，對上講中的三階對稱矩陣空間有$dim S=6$、上三角矩陣空間有$dim U=6$、對角矩陣空間有$dim D=3$

求並（intersect）：$S \cup U=D, dim(S \cup U)=9$；

求交（sum）：$S \cap U=M, dim(S \cap U)=3$；

可以看出：$dim S + dim U=12=dim(S \cup U) + dim(S \cap U)$。

另一個例子來自微分方程：

$\frac{d^2y}{dx^2}+y=0$，即$y''+y=0$

方程的解有：$y=\cos{x}, \quad y=\sin{x}, \quad y=e^{ix}, \quad y=e^{-ix}$等等（$e^{ix}=\cos{x}+i\sin{x}, \quad e^{-ix}=\cos{x}-i\sin{x}$）

而該方程的所有解：$y=c_1 \cos{x} + c_2 \sin{x}$。

所以，該方程的零空間的一組基為$\cos{x}, \sin{x}$，零空間的維數為$2$。同理$e^{ix}, e^{-ix}$可以作為另一組基。

## 秩一矩陣

$2 \times 3$矩陣$$A=\begin{bmatrix}1&4&5\\2&8&10\end{bmatrix}=\begin{bmatrix}1\\2\end{bmatrix}\begin{bmatrix}1&4&5\end{bmatrix}$$。

且$dimC(A)=1=dimC(A^T)$，所有的秩一矩陣都可以劃為$A=UV^T$的形式，這里的$U, V$均為行向量。

秩一矩陣類似“積木”，可以搭建任何矩陣，如對於一個$5 \times 17$秩為$4$的矩陣，只需要$4$個秩一矩陣就可以組合出來。

令$M$代表所有$5 \times 17$，$M$中所有秩$4$矩陣組成的集合並不是一個子空間，通常兩個秩四矩陣相加，其結果並不是秩四矩陣。

現在，在$\mathbb{R}^4$空間中有向量$$v=\begin{bmatrix}v_1\\v_2\\v_3\\v_4\end{bmatrix}$$，取$\mathbb{R}^4$中滿足$v_1+v_2+v_3+v_4=0$的所有向量組成一個向量空間$S$，則$S$是一個向量子空間。

易看出，不論是使用系數乘以該向量，或是用兩個滿足條件的向量相加，其結果仍然落在分量和為零的向量空間中。

求$S$的維數：

從另一個角度看，$v_1+v_2+v_3+v_4=0$等價於$$\begin{bmatrix}1&1&1&1\end{bmatrix}\begin{bmatrix}v_1\\v_2\\v_3\\v_4\end{bmatrix}=0$$，則$S$就是$A=\begin{bmatrix}1&1&1&1\end{bmatrix}$的零空間。

$rank(A)=1$，則對其零空間有$rank(N(A))=n-r=3=dim N(A)$，則$S$的維數是$3$。

順便看一下$1 \times 4$矩陣$A$的四個基本子空間：

列空間：$dim C(A^T)=1$，其中的一組基是$$\begin{bmatrix}1\\1\\1\\1\end{bmatrix}$$；

零空間：$dim N(A)=3$，其中的一組基是$$\begin{bmatrix}-1\\1\\0\\0\end{bmatrix}\begin{bmatrix}-1\\0\\1\\0\end{bmatrix}\begin{bmatrix}-1\\0\\0\\1\end{bmatrix}$$

行空間：$dim C(A)=1$，其中一組基是$\begin{bmatrix}1\end{bmatrix}$，可以看出列空間就是整個$\mathbb{R}^1$空間。

左零空間：$dim N(A^T)=0$，因為$A$轉置後沒有非零的$v$可以使$Av=0$成立，就是$\begin{bmatrix}0\end{bmatrix}$。

綜上，$dim C(A^T)+dim N(A)=4=n, dim C(A)+dim N(A^T)=1=m$

## 小世界圖

圖（graph）由節點（node）與邊（edge）組成。

假設，每個人是圖中的一個節點，如果兩個人為朋友關系，則在這兩個人的節點間添加一條邊，通常來說，從一個節點到另一個節點只需要不超過$6$步（即六條邊）即可到達。
