---
layout: post
title: 線性代數筆記-17
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=18&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第十七講：正交矩陣和Gram-Schmidt正交化法

## 標準正交矩陣

定義標準正交向量（orthonormal）：$$q_i^Tq_j=\begin{cases}0\quad i\neq j\\1\quad i=j\end{cases}$$

我們將標準正交向量放入矩陣中，有$Q=\Bigg[q_1 q_2 \cdots q_n\Bigg]$。

上一講我們研究了$A^A$的特性，現在來觀察$$Q^TQ=\begin{bmatrix} & q_1^T & \\ & q_2^T & \\ & \vdots & \\ & q_n^T & \end{bmatrix}\Bigg[q_1 q_2 \cdots q_n\Bigg]$$

根據標準正交向量的定義，計算$$Q^TQ=\begin{bmatrix}1&0&\cdots&0\\0&1&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&1\end{bmatrix}=I$$，我們也把$Q$成為標準正交矩陣（orthonormal matrix）。

特別的，當$Q$恰好是方陣時，由於正交性，易得$Q$是可逆的，又$Q^TQ=I$，所以$Q^T=Q^{-1}$。

* 舉個置換矩陣的例子：$$Q=\begin{bmatrix}0&1&0\\1&0&0\\0&0&1\end{bmatrix}$$，則$$Q^T=\begin{bmatrix}0&1&0\\0&0&1\\1&0&0\end{bmatrix}$$，易得$Q^TQ=I$。
* 使用上一講的例子$$Q=\begin{bmatrix}\cos\theta&-\sin\theta\\\sin\theta&\cos\theta\end{bmatrix}$$，行向量長度為$1$，且行向量相互正交。
* 其他例子$$Q=\frac{1}{\sqrt 2}\begin{bmatrix}1&1\\1&-1\end{bmatrix}$$，行向量長度為$1$，且行向量相互正交。
* 使用上一個例子的矩陣，令$$Q'=c\begin{bmatrix}Q&Q\\Q&-Q\end{bmatrix}$$，取合適的$c$另行向量長度為$1$也可以構造標準正交矩陣：$$Q=\frac{1}{2}\begin{bmatrix}1&1&1&1\\1&-1&1&-1\\1&1&-1&-1\\1&-1&-1&1\end{bmatrix}$$，這種構造方法以阿德瑪（Adhemar）命名，對$2, 4, 16, 64, \cdots$階矩陣有效。
* 再來看一個例子，$$Q=\frac{1}{3}\begin{bmatrix}1&-2&2\\2&-1&-2\\2&2&1\end{bmatrix}$$，行向量長度為$1$，且行向量相互正交。格拉姆-施密特正交化法的缺點在於，由於要求得單位向量，所以我們總是除以向量的長度，這導致標準正交矩陣中總是帶有根號，而上面幾個例子很少有根號。

再來看標準正交化有什麽好處，假設要做投影，將向量$b$投影在標準正交矩陣$Q$的行空間中，根據上一講的公式得$P=Q(Q^TQ)^{-1}Q^T$，易得$P=QQ^T$。我們斷言，當行向量為標準正交基時，$QQ^T$是投影矩陣。極端情況，假設矩陣是方陣，而其行向量是標準正交的，則其行空間就是整個向量空間，而投影整個空間的投影矩陣就是單位矩陣，此時$QQ^T=I$。可以驗證一下投影矩陣的兩個性質：$(QQ^T)^T=(Q^T)^TQ^T=QQ^T$，得證；$(QQ^T)^2=QQ^TQQ^T=Q(Q^TQ)Q^T=QQ^T$，得證。

我們計算的$A^TA\hat x=A^Tb$，現在變為$Q^TQ\hat x=Q^Tb$，也就是$\hat x=Q^Tb$，分解開來看就是 $\underline{\hat x_i=q_i^Tb}$，這個式子在很多數學領域都有重要作用。當我們知道標準正交基，則解向量第$i$個分量為基的第$i$個分量乘以$b$，在第$i$個基方向上的投影就等於$q_i^Tb$。

## Gram-Schmidt正交化法

我們有兩個線性無關的向量$a, b$，先把它們化為正交向量$A, B$，再將它們單位化，變為單位正交向量$q_1=\frac{A}{\left\|A\right\|}, q_2=\frac{B}{\left\|B\right\|}$：

* 我們取定$a$向量的方向，$a=A$；
* 接下來將$b$投影在$A$的法方向上得到$B$，也就是求子空間投影一講中，我們提到的誤差向量$e=b-p$，即$B=b-\frac{A^Tb}{A^TA}A$。檢驗一下$A\bot B$，$A^TB=A^Tb-A^T\frac{A^Tb}{A^TA}A=A^Tb-\frac{A^TA}{A^TA}A^Tb=0$。（$\frac{A^Tb}{A^TA}A$就是$A\hat x=p$。）

如果我們有三個線性無關的向量$a, b, c$，則我們現需要求它們的正交向量$A, B, C$，再將它們單位化，變為單位正交向量$q_1=\frac{A}{\left\|A\right\|}, q_2=\frac{B}{\left\|B\right\|}, q_3=\frac{C}{\left\|C\right\|}$：

* 前兩個向量我們已經得到了，我們現在需要求第三個向量同時正交於$A, B$；
* 我們依然沿用上面的方法，從$c$中減去其在$A, B$上的分量，得到正交與$A, B$的$C$：$C=c-\frac{A^Tc}{A^TA}A-\frac{B^Tc}{B^TB}B$。

現在我們試驗一下推導出來的公式，$$a=\begin{bmatrix}1\\1\\1\end{bmatrix}, b=\begin{bmatrix}1\\0\\2\end{bmatrix}$$：

* 則$$A=a=\begin{bmatrix}1\\1\\1\end{bmatrix}$$；
* 根據公式有$B=a-hA$，$h$是比值$\frac{A^Tb}{A^TA}=\frac{3}{3}$，則$$B=\begin{bmatrix}1\\1\\1\end{bmatrix}-\frac{3}{3}\begin{bmatrix}1\\0\\2\end{bmatrix}=\begin{bmatrix}0\\-1\\1\end{bmatrix}$$。驗證一下正交性有$A\cdot B=0$。
* 單位化，$$q_1=\frac{1}{\sqrt 3}\begin{bmatrix}1\\1\\1\end{bmatrix},\quad q_2=\frac{1}{\sqrt 2}\begin{bmatrix}1\\0\\2\end{bmatrix}$$，則標準正交矩陣為$$Q=\begin{bmatrix}\frac{1}{\sqrt 3}&0\\\frac{1}{\sqrt 3}&-\frac{1}{\sqrt 2}\\\frac{1}{\sqrt 3}&\frac{1}{\sqrt 2}\end{bmatrix}$$，對比原來的矩陣$$D=\begin{bmatrix}1&1\\1&0\\1&2\end{bmatrix}$$，有$D, Q$的行空間是相同的，我們只是將原來的基標準正交化了。

我們曾經用矩陣的眼光審視消元法，有$A=LU$。同樣的，我們也用矩陣表達標準正交化，$A=QR$。設矩陣$A$有兩個行向量$\Bigg[a_1 a_2\Bigg]$，則標準正交化後有$$\Bigg[a_1 a_2\Bigg]=\Bigg[q_1 q_2\Bigg]\begin{bmatrix}a_1^Tq_1&a_2^Tq_1\\a_1^Tq_2&a_2^Tq_2\end{bmatrix}$$，而左下角的$a_1^Tq_2$始終為$0$，因為Gram-Schmidt正交化總是使得$a_1\bot q_2$，後來構造的向量總是正交於先前的向量。所以這個$R$矩陣是一個上三角矩陣。
