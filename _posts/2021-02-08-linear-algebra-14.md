---
layout: post
title: 線性代數筆記-14
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=15&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第十四講：正交向量與子空間

在四個基本子空間中，提到對於秩為r的$m \times n$矩陣，其列空間（$dim C(A^T)=r$）與零空間（$dim N(A)=n-r$）同屬於$\mathbb{R}^n$空間，其行空間（$dim C(A)=r$）與左零空間（$dim N(A^T)$=m-r）同屬於$\mathbb{R}^m$空間。

對於向量$x, y$，當$x^T \cdot y=0$即$x_1y_1+x_2y_x+\cdots+x_ny_n=0$時，有向量$x, y$正交（vector orthogonal）。

畢達哥拉斯定理（Pythagorean theorem）中提到，直角三角形的三條邊滿足：

$$
\begin{aligned}
\left\|\overrightarrow{x}\right\|^2+\left\|\overrightarrow{y}\right\|^2 &= \left\|\overrightarrow{x+y}\right\|^2 \\
x^Tx+y^Ty &= (x+y)^T(x+y) \\ 
x^Tx+y^Ty &= x^Tx+y^Ty+x^Ty+y^Tx \\
0 &= x^Ty+y^Tx \qquad 對於向量點乘，x^Ty=y^Tx \\
0 &= 2x^Ty \\
x^Ty &=0
\end{aligned}
$$

由此得出，兩正交向量的點積為$0$。另外，$x, y$可以為$0$向量，由於$0$向量與任意向量的點積均為零，所以$0$向量與任意向量正交。

舉個例子：
$x=\begin{bmatrix}1\\\\2\\\\3\end{bmatrix}, y=\begin{bmatrix}2\\\\-1\\\\0\end{bmatrix}, x+y=\begin{bmatrix}3\\\\1\\\\3\end{bmatrix}$，有$\left\| \overrightarrow{x} \right\|^2=14, \left\| \overrightarrow{y} \right\|^2=5, \left\| \overrightarrow{x+y} \right\|^2=19$，而$x^Ty=1\times2+2\times (-1)+3\times0=0$。

向量$S$與向量$T$正交，則意味著$S$中的每一個向量都與$T$中的每一個向量正交。若兩個子空間正交，則它們一定不會相交於某個非零向量。

現在觀察列空間與零空間，零空間是$Ax=0$的解，即$x$若在零空間，則$Ax$為零向量；

而對於列空間，有 $$
\begin{bmatrix}row_1\\row_2\\ \vdots \\row_m\end{bmatrix}
\Bigg[x\Bigg]=
\begin{bmatrix}0\\0\\ \vdots\\ 0\end{bmatrix}
$$，可以看出：
$$
\begin{bmatrix}row_1\end{bmatrix}\Bigg[x\Bigg]=0 \\
\begin{bmatrix}row_2\end{bmatrix}\Bigg[x\Bigg]=0 \\
\vdots \\
\begin{bmatrix}row_m\end{bmatrix}\Bigg[x\Bigg]=0 \\
$$

所以這個等式告訴我們，$x$同$A$中的所有列正交；

接下來還驗證$x$是否與$A$中各行的線性組合正交，
$$
\begin{cases}
c_1(row_1)^Tx=0 \\
c_2(row_2)^Tx=0 \\
\vdots \\
c_n(row_m)^Tx=0 \\
\end{cases}
$$，各式相加得$$(c_1row_1+c_2row_2+\cdots+c_nrow_m)^Tx=0$$，得證。

我們可以說，列空間與零空間將$\mathbb{R}^n$分割為兩個正交的子空間，同樣的，行空間與左零空間將$\mathbb{R}^m$分割為兩個正交的子空間。

舉例，$$A=\begin{bmatrix}1&2&5\\2&4&10\end{bmatrix}$$，則可知$m=2, n=3, rank(A)=1, dim N(A)=2$。

有$$Ax=\begin{bmatrix}1&2&5\\2&4&10\end{bmatrix}\begin{bmatrix}x_1\\x_2\\x_3\end{bmatrix}=\begin{bmatrix}0\\0\end{bmatrix}$$，解得零空間的一組基$$x_1=\begin{bmatrix}-2\\1\\0\end{bmatrix}\quad x_2=\begin{bmatrix}-5\\0\\1\end{bmatrix}$$。

而列空間的一組基為$r=\begin{bmatrix}1\\\\2\\\\5\end{bmatrix}$，零空間與列空間正交，在本例中列空間也是零空間的法向量。

補充一點，我們把列空間與零空間稱為$n$維空間里的正交補（orthogonal complement），即零空間包含了所有與列空間正交的向量；同理行空間與左零空間為$m$維空間里的正交補，即左零空間包含了所有與零空間正交的向量。

接下來看長方矩陣，$m>n$。對於這種矩陣，$Ax=b$中經常混入一些包含“壞數據”的方程，雖然可以通過篩選的方法去掉一些我們不希望看到的方程，但是這並不是一個穩妥的方法。

於是，我們引入一個重要的矩陣：$A^TA$。這是一個$n \times m$矩陣點乘$m \times n$矩陣，其結果是一個$n \times n$矩陣，應該注意的是，這也是一個對稱矩陣，證明如下：

$$
(A^TA)^T=A^T(A^T)^T=A^TA
$$

這一章節的核心就是$A^TAx=A^Tb$，這個變換可以將“壞方程組”變為“好方程組”。

舉例，有$$\begin{bmatrix}1&1\\1&2\\1&5\end{bmatrix}\begin{bmatrix}x_1\\x_2\end{bmatrix}=\begin{bmatrix}b_1\\b_2\\b_3\end{bmatrix}$$，只有當$$\begin{bmatrix}b_1\\b_2\\b_3\end{bmatrix}$$在矩陣的行空間時，方程才有解。

現在來看$$\begin{bmatrix}1&1&1\\1&2&5\end{bmatrix}\begin{bmatrix}1&1\\1&2\\1&5\end{bmatrix}=\begin{bmatrix}3&8\\8&30\end{bmatrix}$$，可以看出此例中$A^TA$是可逆的。然而並非所有$A^TA$都是可逆的，如$$\begin{bmatrix}1&1&1\\3&3&3\end{bmatrix}\begin{bmatrix}1&3\\1&3\\1&3\end{bmatrix}=\begin{bmatrix}3&9\\9&27\end{bmatrix}$$（注意到這是兩個秩一矩陣相乘，其結果秩不會大於一）

先給出結論：

$$
N(A^TA)=N(A)\\
rank(A^TA)=rank(A)\\
A^TA可逆當且僅當N(A)為零向量，即A的行線性無關\\
$$

下一講涉及投影，很重要。
