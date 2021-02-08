---
layout: post
title: 線性代數筆記-13
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=14&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第十三講：複習一

1. 令$u, v, w$是$\mathbb{R}^7$空間內的非零向量：則$u, v, w$生成的向量空間可能是$1, 2, 3$維的。

2. 有一個$5 \times 3$矩陣$U$，該矩陣為階梯矩陣（echelon form），有$3$個主元：則能夠得到該矩陣的秩為$3$，即三行向量線性無關，不存在非零向量使得三行的線性組合為零向量，所以該矩陣的零空間應為$\begin{bmatrix}0\\\\0\\\\0 \end{bmatrix}$。

3. 接上一問，有一個$10 \times 3$矩陣$B=\begin{bmatrix}U\\\\2U \end{bmatrix}$，則化為最簡形式（階梯矩陣）應為$\begin{bmatrix}U\\\\0 \end{bmatrix}$，$rank(B)=3$。

4. 接上一問，有一個矩陣型為$$C=\begin{bmatrix}U & U \\ U & 0 \end{bmatrix}$$，則化為最簡形式應為$$\begin{bmatrix}U & 0 \\ 0 & U \end{bmatrix}$$，$rank(C)=6$。矩陣$C$為$10 \times 6$矩陣，$dim N(C^T)=m-r=4$。

5. 有$Ax=\begin{bmatrix}2\\\\4\\\\2 \end{bmatrix}$，並且$x=\begin{bmatrix}2\\\\0\\\\0\\ \end{bmatrix}+c\begin{bmatrix}1\\\\1\\\\0 \end{bmatrix}+d\begin{bmatrix}0\\\\0\\\\1 \end{bmatrix}$，則等號右側$b$向量的行數應為$A$的列數，且解行的數應為$A$的行數，所以$A$是一個$3 \times 3$矩陣。從解的結構可知自由元有兩個，則$rank(A)=1, dim N(A)=2$。從解的第一個向量得出，矩陣$A$的第一行是$\begin{bmatrix}1\\\\2\\\\1 \end{bmatrix}$；解的第二個向量在零空間中，說明第二行與第一行符號相反，所以矩陣第二行是$\begin{bmatrix}-1\\\\-2\\\\-1 \end{bmatrix}$；解的第三個向量在零空間中，說明第三行為零向量；綜上，$$A=\begin{bmatrix}1 & -1 & 0\\ 2 & -2 & 0\\ 1 & -1 & 0\\ \end{bmatrix}$$。

6. 接上一問，如何使得$Ax=b$有解？即使$b$在矩陣$A$的行空間中。易知$A$的行空間型為$c\begin{bmatrix}1\\\\2\\\\1 \end{bmatrix}$，所以使$b$為向量$\begin{bmatrix}1\\\\2\\\\1 \end{bmatrix}$的倍數即可。

7. 有一方陣的零空間中只有零向量，則其左零空間也只有零向量。

8. 由$5 \times 5$矩陣組成的矩陣空間，其中的可逆矩陣能否構成子空間？兩個可逆矩陣相加的結果並不一定可逆，況且零矩陣本身並不包含在可逆矩陣中。其中的奇異矩陣（singular matrix，非可逆矩陣）也不能組成子空間，因為其相加的結果並不一定能夠保持不可逆。

9. 如果$B^2=0$，並不能得出$B=0$，反例：$$\begin{bmatrix}0 & 1\\ 0 & 0\\ \end{bmatrix}$$，**這個矩陣經常會被用作反例**。

10. $n \times n$矩陣的行向量線性無關，則是否$\forall b, Ax=b$有解？是的，因為方陣各行線性無關，所以方陣滿秩，它是可逆矩陣，肯定有解。

11. 有
$$
B=
\begin{bmatrix}
1 & 1 & 0 \\
0 & 1 & 0 \\
1 & 0 & 1 \\
\end{bmatrix}
\begin{bmatrix}
1 & 0 & -1 & 2 \\
0 & 1 & 1 & -1 \\
0 & 0 & 0 & 0 \\
\end{bmatrix}
$$，在不解出$B$的情況下，求$B$的零空間。可以觀察得出前一個矩陣是可逆矩陣，設$B=CD$，則求零空間$Bx=0, CDx=0$，而$C$是可逆矩陣，則等式兩側同時乘以$C^{-1}$有$C^{-1}CDx=Dx=0$，所以當$C$為可逆矩陣時，有$N(CD)=N(D)$，即左乘逆矩陣不會改變零空間。本題轉化為求$D$的零空間，$N(B)$的基為
$\begin{bmatrix}-F\\\\I \end{bmatrix}$，也就是$\begin{bmatrix}1\\\\-1\\\\1\\\\0 \end{bmatrix}\quad\begin{bmatrix}-2\\\\1\\\\0\\\\1\end{bmatrix}$

12. 接上題，求$Bx=\begin{bmatrix}1\\\\0\\\\1 \end{bmatrix}$的通解。觀察$B=CD$，易得$B$矩陣的第一行為$\begin{bmatrix}1\\\\0\\\\1 \end{bmatrix}$，恰好與等式右邊一樣，所以$\begin{bmatrix}1\\\\0\\\\0\\\\0 \end{bmatrix}$可以作為通解中的特解部分，再利用上一問中求得的零空間的基，得到通解
$
x=
\begin{bmatrix}1\\\\0\\\\0\\\\0 \end{bmatrix}+
c_1\begin{bmatrix}1\\\\-1\\\\1\\\\0 \end{bmatrix}+c_2\begin{bmatrix}-2\\\\1\\\\0\\\\1\end{bmatrix}
$

13. 對於任意方陣，其行空間等於列空間？不成立，可以使用$$\begin{bmatrix}0 & 1\\ 0 & 0\\ \end{bmatrix}$$作為反例，其列空間是向量$$\begin{bmatrix}0 & 1\\ \end{bmatrix}$$的任意倍數，而行空間是向量$$\begin{bmatrix}1 & 0\\ \end{bmatrix}$$的任意倍數。但是如果該方陣是對稱矩陣，則成立。

14. $A$與$-A$的四個基本子空間相同。

15. 如果$A, B$的四個基本子空間相同，則$A, B$互為倍數關系。不成立，如任意兩個$n$階可逆矩陣，他們的列空間、行空間均為$\mathbb{R}^n$，他們的零空間、左零空間都只有零向量，所以他們的四個基本子空間相同，但是並不一定具有倍數關系。

16. 如果交換矩陣的某兩列，則其列空間與零空間保持不變，而行空間與左零空間均已改變。

17. 為什麽向量$v=\begin{bmatrix}1\\\\2\\\\3 \end{bmatrix}$不能同時出現在矩陣的列空間與零空間中？令$A\begin{bmatrix}1\\\\2\\\\3 \end{bmatrix}=\begin{bmatrix}0\\\\0\\\\0 \end{bmatrix}$，很明顯矩陣$A$中不能出現值為$\begin{bmatrix}1 & 2 & 3 \end{bmatrix}$的列向量，否則無法形成等式右側的零向量。這里引入正交（perpendicular）的概念，矩陣的列空間與零空間正交，它們僅共享零向量。
