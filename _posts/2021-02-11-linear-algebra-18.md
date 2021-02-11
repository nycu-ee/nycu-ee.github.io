---
layout: post
title: 線性代數筆記-18
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=19&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第十八講：行列式及其性質

本講我們討論出行列式（determinant）的性質：

1. $\det{I}=1$，單位矩陣行列式值為一。
2. 交換列行列式變號。

    在給出第三個性質之前，先由前兩個性質可知，對置換矩陣有$$\det P=\begin{cases}1\quad &even\\-1\quad &odd\end{cases}$$。

    舉例：$$\begin{vmatrix}1&0\\0&1\end{vmatrix}=1,\quad\begin{vmatrix}0&1\\1&0\end{vmatrix}=-1$$，於是我們猜想，對於二階方陣，行列式的計算公式為$$\begin{vmatrix}a&b\\c&d\end{vmatrix}=ad-bc$$。

3. a. $$\begin{vmatrix}ta&tb\\tc&td\end{vmatrix}=t\begin{vmatrix}a&b\\c&d\end{vmatrix}$$。

    b. $$\begin{vmatrix}a+a'&b+b'\\c&d\end{vmatrix}=\begin{vmatrix}a&b\\c&d\end{vmatrix}+\begin{vmatrix}a'&b'\\c&d\end{vmatrix}$$。
    
    **注意**：~~這里並不是指$\det (A+B)=\det A+\det B$，方陣相加會使每一列相加，這里僅是針對某一列的線性變換。~~

4. 如果兩列相等，則行列式為零。使用性質2交換兩行易證。
5. 從第$k$列中減去第$i$列的$l$倍，行列式不變。這條性質是針對消元的，我們可以先消元，將方陣變為上三角形式後再計算行列式。

    舉例：$$\begin{vmatrix}a&b\\c-la&d-lb\end{vmatrix}\stackrel{3.b}{=}\begin{vmatrix}a&b\\c&d\end{vmatrix}+\begin{vmatrix}a&b\\-la&-lb\end{vmatrix}\stackrel{3.a}{=}\begin{vmatrix}a&b\\c&d\end{vmatrix}-l\begin{vmatrix}a&b\\a&b\end{vmatrix}\stackrel{4}{=}\begin{vmatrix}a&b\\c&d\end{vmatrix}$$

6. 如果方陣的某一行為零，則其行列式值為零。使用性質3.a對為零行乘以不為零系數$l$，使$l\det A=\det A$即可證明；或使用性質5將某列加到為零列，使存在兩列相等後使用性質4即可證明。

7. 有上三角行列式$$U=\begin{vmatrix}d_{1}&*&\cdots&*\\0&d_{2}&\cdots&*\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&d_{n}\end{vmatrix}$，則$\det U=d_1d_2\cdots d_n$$。使用性質5，從最後一行開始，將對角元素上方的$*$元素依次變為零，可以得到型為$$D=\begin{vmatrix}d_{1}&0&\cdots&0\\0&d_{2}&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&d_{n}\end{vmatrix}$$的對角行列式，再使用性質3將對角元素提出得到$$d_nd_{n-1}\cdots d_1\begin{vmatrix}1&0&\cdots&0\\0&1&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&1\end{vmatrix}$$，得證。

8. 當矩陣$A$為奇異矩陣時，$\det A=0$；當且僅當$A$可逆時，有$\det A\neq0$。如果矩陣可逆，則化簡為上三角形式後各行都含有主元，行列式即為主元乘積；如果矩陣奇異，則化簡為上三角形式時會出現全零列，行列式為零。

    再回顧二階情況：$$\begin{vmatrix}a&b\\c&d\end{vmatrix}\xrightarrow{消元}\begin{vmatrix}a&b\\0&d-\frac{c}{a}b\end{vmatrix}=ad-bc$$，前面的猜想得到證實。

9. $\det AB=(\det A)(\det B)$。使用這一性質，$\det I=\det{A^{-1}A}=\det A^{-1}\det A$，所以$\det A^{-1}=\frac{1}{\det A}$。

    同時還可以得到：$\det A^2=(\det A)^2$，以及$\det 2A=2^n\det A$，這個式子就像是求體積，對三維物體有每邊翻倍則體積變為原來的八倍。

10. $\det A^T=\det A$，前面一直在關注列的屬性給行列式帶來的變化，有了這條性質，列的屬性同樣適用於行，比如對性質2就有“交換行行列式變號”。
    
    證明：$\left\|A^T\right\|=\left\|A\right\|\rightarrow\left\|U^TL^T\right\|=\left\|LU\right\|\rightarrow\left\|U^T\right\|\left\|L^T\right\|=\left\|L\right\|\left\|U\right\|$，值得注意的是，$L, U$的行列式並不因為轉置而改變，得證。
