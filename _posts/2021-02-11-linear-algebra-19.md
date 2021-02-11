---
layout: post
title: 線性代數筆記-19
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=20&ab_channel=MITOpenCourseWare)

<!-- more -->

# 行列式公式和代數餘子式

上一講中，我們從三個簡單的性質擴展出了一些很好的推論，本講將繼續使用這三條基本性質：

1. $\det I=1$；
2. 交換列行列式變號；
3. 對行列式的每一列都可以單獨使用線性運算，其值不變；

我們使用這三條性質推導二階方陣行列式：

$$\begin{vmatrix}a&b\\c&d\end{vmatrix}=\begin{vmatrix}a&0\\c&d\end{vmatrix}+\begin{vmatrix}0&b\\c&d\end{vmatrix}=\begin{vmatrix}a&0\\c&0\end{vmatrix}+\begin{vmatrix}a&0\\0&d\end{vmatrix}+\begin{vmatrix}0&b\\c&0\end{vmatrix}+\begin{vmatrix}0&b\\0&d\end{vmatrix}=ad-bc$$

按照這個方法，我們繼續計算三階方陣的行列式，可以想到，我們保持第二、三列不變，將第一列拆分為個行列式之和，再將每一部分的第二列拆分為三部分，這樣就得到九個行列式，再接著拆分這九個行列式的第三列，最終得到二十七個行列式。可以想象到，這些矩陣中有很多值為零的行列式，我們只需要找到不為零的行列式，求和即可。

$$\begin{vmatrix}a_{11}&a_{12}&a_{13}\\a_{21}&a_{22}&a_{23}\\a_{31}&a_{32}&a_{33}\end{vmatrix}=\begin{vmatrix}a_{11}&0&0\\0&a_{22}&0\\0&0&a_{33}\end{vmatrix}+\begin{vmatrix}a_{11}&0&0\\0&0&a_{23}\\0&a_{32}&0\end{vmatrix}+\begin{vmatrix}0&a_{12}&0\\a_{21}&0&0\\0&0&a_{33}\end{vmatrix}+\begin{vmatrix}0&a_{12}&0\\0&0&a_{23}\\a_{31}&0&0\end{vmatrix}+\begin{vmatrix}0&0&a_{13}\\a_{21}&0&0\\0&a_{32}&0\end{vmatrix}+\begin{vmatrix}0&0&a_{13}\\0&a_{22}&0\\a_{31}&0&0\end{vmatrix}$$

$$原式=a_{11}a_{22}a_{33}-a_{11}a_{23}a_{32}-a_{12}a_{21}a_{33}+a_{12}a_{23}a_{31}+a_{13}a_{21}a_{32}-a_{13}a_{22}a_{31}\tag{1}$$

同理，我們想繼續推導出階數更高的式子，按照上面的式子可知$n$階行列式應該可以分解成$n!$個非零行列式（占據第一列的元素有$n$種選擇，占據第二列的元素有$n-1$種選擇，以此類推得$n!$）：

$$\det A=\sum_{n!} \pm a_{1\alpha}a_{2\beta}a_{3\gamma}\cdots a_{n\omega}, (\alpha, \beta, \gamma, \omega)=P_n^n\tag{2}$$

這個公式還不完全，接下來需要考慮如何確定符號：

$$\begin{vmatrix}0&0&\overline 1&\underline 1\\0&\overline 1&\underline 1&0\\\overline 1&\underline 1&0&0\\\underline 1&0&0&\overline 1\end{vmatrix}$$
* 觀察帶有下劃線的元素，它們的排列是$(4,3,2,1)$，變為$(1,2,3,4)$需要兩步操作，所以應取$+$；
* 觀察帶有上劃線的元素，它們的排列是$(3,2,1,4)$，變為$(1,2,3,4)$需要一步操作，所以應取$-$。
* 觀察其他元素，我們無法找出除了上面兩種以外的排列方式，於是該行列式值為零，這是一個奇異矩陣。

此處引入代數餘子式（cofactor）的概念，它的作用是把$n$階行列式化簡為$n-1$階行列式。

於是我們把$(1)$式改寫為：

$$a_{11}(a_{22}a_{33}-a_{23}a_{32})+a_{12}(a_{21}a_{33}-a_{23}a_{31})+a_{13}(a_{21}a_{32}-a_{22}a_{31})$$

$$\begin{vmatrix}a_{11}&0&0\\0&a_{22}&a_{23}\\0&a_{32}&a_{33}\end{vmatrix}+\begin{vmatrix}0&a_{12}&0\\a_{21}&0&a_{23}\\a_{31}&0&a_{33}\end{vmatrix}+\begin{vmatrix}0&0&a_{13}\\a_{21}&a_{22}&0\\a_{31}&a_{32}&0\end{vmatrix}$$

於是，我們可以定義$a_{ij}$的代數餘子式：將原行列式的第$i$列與第$j$行抹去後得到的$n-1$階行列式記為$C_{ij}$，$i+j$為偶時時取$+$，$i+j$為奇時取$-$。

現在再來完善式子$(2)$：將行列式$A$沿第一列展開：

$$\det A=a_{11}C_{11}+a_{12}C_{12}+\cdots+a_{1n}C_{1n}$$

到現在為止，我們了解了三種求行列式的方法：

1. 消元，$\det A$就是主元的乘積；
2. 使用$(2)$式展開，求$n!$項之積；
3. 使用代數餘子式。

計算例題：
$$A_4=\begin{vmatrix}1&1&0&0\\1&1&1&0\\0&1&1&1\\0&0&1&1\end{vmatrix}\stackrel{沿第一行展開}{=}\begin{vmatrix}1&1&0\\1&1&1\\0&1&1\end{vmatrix}-\begin{vmatrix}1&1&0\\0&1&1\\0&1&1\end{vmatrix}=-1-0=-1$$
