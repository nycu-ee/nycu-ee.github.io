---
layout: post
title: 線性代數筆記-20
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=21&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第二十講：克拉默法則、逆矩陣、體積

本講主要介紹逆矩陣的應用。

## 求逆矩陣

我們從逆矩陣開始，對於二階矩陣有$$\begin{bmatrix}a&b\\c&d\end{bmatrix}^{-1}=\frac{1}{ad-bc}\begin{bmatrix}d&-b\\-c&a\end{bmatrix}$$。觀察易得，系數項就是行列式的倒數，而矩陣則是由一系列代數餘子式組成的。先給出公式：

$$
A^{-1}=\frac{1}{\det A}C^T
\tag{1}
$$

觀察這個公式是如何運作的，化簡公式得$AC^T=(\det A)I$，寫成矩陣形式有$$\begin{bmatrix}a_{11}&a_{12}&\cdots&a_{1n}\\\vdots&\vdots&\ddots&\vdots\\a_{n1}&a_{n2}&\cdots&a_{nn}\end{bmatrix}\begin{bmatrix}C_{11}&\cdots&C_{n1}\\C_{12}&\cdots&C_{n2}\\\vdots&\ddots&\vdots\\C_{1n}&\cdots&C_{nn}\end{bmatrix}=Res$$

對於這兩個矩陣的乘積，觀察其結果的元素$Res_{11}=a_{11}C_{11}+a_{12}C_{12}+\cdots+a_{1n}C_{1n}$，這正是上一講提到的將行列式按第一列展開的結果。同理，對$Res_{22}, \cdots, Res_{nn}$都有$Res_{ii}=\det A$，即對角線元素均為$\det A$。

再來看非對角線元素：回顧二階的情況，如果用第一列乘以第二列的代數餘子式$a_{11}C_{21}+a_{12}C_{22}$，得到$a(-b)+ab=0$。換一種角度看問題，$a(-b)+ab=0$也是一個矩陣的行列式值，即$$A_{s}=\begin{bmatrix}a&b\\a&b\end{bmatrix}$$。將$\det A_{s}$按第二列展開，也會得到$\det A_{s}=a(-b)+ab$，因為行列式有兩列相等所以行列式值為零。

推廣到$n$階，我們來看元素$Res_{1n}=a_{11}C_{n1}+a_{12}C_{n2}+\cdots+a_{1n}C_{nn}$，該元素是第一列與最後一行的代數餘子式相乘之積。這個式子也可以寫成一個特殊矩陣的行列式，即矩陣$$A_{s}=\begin{bmatrix}a_{11}&a_{12}&\cdots&a_{1n}\\a_{21}&a_{22}&\cdots&a_{2n}\\\vdots&\vdots&\ddots&\vdots\\a_{n-a1}&a_{n-12}&\cdots&a_{n-1n}\\a_{11}&a_{12}&\cdots&a_{1n}\end{bmatrix}$$。計算此矩陣的行列式，將$\det A_{s}$按最後一列展開，也得到$\det A_{s}=a_{11}C_{n1}+a_{12}C_{n2}+\cdots+a_{1n}C_{nn}$。同理，行列式$A_{s}$有兩列相等，其值為零。

結合對角線元素與非對角線元素的結果，我們得到$$Res=\begin{bmatrix}\det A&0&\cdots&0\\0&\det A&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&\det A\end{bmatrix}$$，也就是$(1)$等式右邊的$(\det A)I$，得證。

## 求解$Ax=b$

因為我們現在有了逆矩陣的計算公式，所以對$Ax=b$有$x=A^{-1}b=\frac{1}{\det A}C^Tb$，這就是計算$x$的公式，即克萊默法則（Cramer's rule）。

現在來觀察$x=\frac{1}{\det A}C^Tb$，我們將得到的解拆分開來，對$x$的第一個分量有$x_1=\frac{y_1}{\det A}$，這里$y_1$是一個數字，其值為$y_1=b_1C_{11}+b_2C_{21}+\cdots+b_nC_{n1}$，每當我們看到數字與代數餘子式乘之積求和時，都應該聯想到求行列式，也就是說$y_1$可以看做是一個矩陣的行列式，我們設這個矩陣為$B_1$。所以有$x_i=\frac{\det B_1}{\det A}$，同理有$x_2=\frac{\det B_2}{\det A}$，$x_2=\frac{\det B_2}{\det A}$。

而$B_1$是一個型為$\Bigg[b a_2 a_3 \cdots a_n\Bigg]$的矩陣，即將矩陣$A$的第一行變為$b$向量而得到的新矩陣。其實很容易看出，$\det B_1$可以沿第一行展開得到$y_1=b_1C_{11}+b_2C_{21}+\cdots+b_nC_{n1}$。

一般的，有$B_j=\Bigg[a_1 a_2 \cdots a_{j-1} b a_{j+1} \cdots a_n\Bigg]$，即將矩陣$A$的第$j$行變為$b$向量而得到的新矩陣。所以，對於解的分量有$x_j=\frac{\det B_j}{\det A}$。

這個公式雖然很漂亮，但是並不方便計算。

## 關於體積（Volume）

先提出命題：行列式的絕對值等於一個箱子的體積。

來看三維空間中的情形，對於$3$階方陣$A$，取第一行$(a_1,a_2,a_3)$，令其為三維空間中點$A_1$的坐標，同理有點$A_2, A_3$。連接這三個點與原點可以得到三條邊，使用這三條邊展開得到一個平行六面體，$\left\|\det A\right\|$就是該平行六面體的體積。

對於三階單位矩陣，其體積為$\det I=1$，此時這個箱子是一個單位立方體。這其實也證明了前面學過的行列式性質1。於是我們想，如果能接著證明性質2、3即可證明體積與行列式的關系。

對於行列式性質2，我們交換兩列並不會改變箱子的大小，同時行列式的絕對值也沒有改變，得證。

現在我們取矩陣$A=Q$，而$Q$是一個標準正交矩陣，此時這個箱子是一個立方體，可以看出其實這個箱子就是剛才的單位立方體經過旋轉得到的。對於標準正交矩陣，有$Q^TQ=I$，等式兩邊取行列式得$\det(Q^TQ)=1=\left\|Q^T\right\|\left\|Q\right\|$，而根據行列式性質10有$\left\|Q^T\right\|=\left\|Q\right\|$，所以$原式=\left\|Q\right\|^2=1, \left\|Q\right\|=\pm 1$。

接下來在考慮不再是“單位”的立方體，即長方體。 假設$Q$矩陣的第一列翻倍得到新矩陣$Q_2$，此時箱子變為在第一列方向上增加一倍的長方體箱子，也就是兩個“標準正交箱子”在第一列方向上的堆疊。易知這個長方體箱子是原來體積的兩倍，而根據行列式性質3.a有$\det Q_2=\det Q$，於是體積也符合行列式的數乘性質。

我們來看二階方陣的情形，$$\begin{vmatrix}a+a'&b+b'\\c&d\end{vmatrix}=\begin{vmatrix}a&b\\c&d\end{vmatrix}+\begin{vmatrix}a'&b'\\c&d\end{vmatrix}$$。在二階情況中，行列式就是一個求平行四邊形面積的公式，原來我們求由四個點$(0,0), (a,b), (c,d), (a+c,b+d)$圍成的四邊形的面積，需要先求四邊形的底邊長，再做高求解，現在只需要計算$\det A=ad-bc$即可（更加常用的是求由$(0,0), (a,b), (c,d)$圍成的三角形的面積，即$\frac{1}{2}ad-bc$）。也就是說，如果知道了歪箱子的頂點坐標，求面積（二階情形）或體積（三階情形）時，我們不再需要開方、求角度，只需要計算行列式的值就行了。

再多說兩句我們通過好幾講得到的這個公式，在一般情形下，由點$(x_1,y_1), (x_2,y_2), (x_3,y_3)$圍成的三角形面積等於$$\frac{1}{2}\begin{vmatrix}x_1&y_1&1\\x_2&y_2&1\\x_3&y_3&1\end{vmatrix}$$，計算時分別用第二列、第三列減去第一列化簡到第三行只有一個$1$（這個操作實際作用是將三角形移動到原點），得到$$\frac{1}{2}\begin{vmatrix}x_1&y_1&1\\x_2-x_1&y_2-y_1&0\\x_3-x_1&y_3-y_1&0\end{vmatrix}$$，再按照第三行展開，得到三角形面積等於$\frac{(x_2-x_1)(y_3-y_1)-(x_3-x_1)(y_2-y_1)}{2}$。
