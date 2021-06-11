---
layout: post
title: 線性代數筆記-03
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=FX4C-JpTFgY&list=PLE7DDD91010BC51F8&index=4)

<!-- more -->

# 第三講：乘法和逆矩陣

上一講大概介紹了矩陣乘法和逆矩陣，本講就來做進一步說明。

## 矩陣乘法

* 行列內積：有$m\times n$矩陣$A$和$n\times p$矩陣$B$（$A$的總行數必須與$B$的總列數相等），兩矩陣相乘有$AB=C$，$C$是一個$m\times p$矩陣，對於$C$矩陣中的第$i$列第$j$行元素$c_{ij}$，有：

    $$c_{ij}=row_i\cdot column_j=\sum_{k=i}^na_{ik}b_{kj}$$

    其中$a_{ik}$是$A$矩陣的第$i$列第$k$行元素，$b_{kj}$是$B$矩陣的第$k$列第$j$行元素。

    可以看出$c_{ij}$其實是$A$矩陣第$i$列點乘$B$矩陣第$j$行 $\begin{bmatrix}&\vdots&\\\\&row_i&\\\\&\vdots&\end{bmatrix}\begin{bmatrix}&&\\\\\cdots&column_j&\cdots\\\\&&\end{bmatrix}=\begin{bmatrix}&\vdots&\\\\\cdots&c_{ij}&\cdots\\\\&\vdots&\end{bmatrix}$

* 整行相乘：上一講我們知道了如何計算矩陣乘以向量，而整行相乘就是使用這種線性組合的思想：

    $\begin{bmatrix}&&\\\\A_{col1}&A_{col2}&\cdots&A_{coln}\\\\&&\end{bmatrix}\begin{bmatrix}\cdots&b_{1j}&\cdots\\\\\cdots&b_{2j}&\cdots\\\\\cdots&\vdots&\cdots\\\\\cdots&b_{nj}&\cdots\\\\\end{bmatrix}=\begin{bmatrix}&&\\\\\cdots&\left(b_{1j}A_{col1}+b_{2j}A_{col2}+\cdots+b_{nj}A_{coln}\right)&\cdots\\\\&&\end{bmatrix}$
    
    上面的運算為$B$的第$j$個行向量右乘矩陣$A$，求得的結果就是$C$矩陣的第$j$行，即$C$的第$j$行是$A$的行向量以$B$的第$j$行作為系數所求得的線性組合，$C_j=b_{1j}A_{col1}+b_{2j}A_{col2}+\cdots+b_{nj}A_{coln}$。

* 整列相乘：同樣的，也是利用列向量線性組合的思想：
  
    $\begin{bmatrix}\vdots&\vdots&\vdots&\vdots\\\\a_{i1}&a_{i2}&\cdots&a_{in}\\\\\vdots&\vdots&\vdots&\vdots\end{bmatrix}\begin{bmatrix}&B_{row1}&\\\\&B_{row2}&\\\\&\vdots&\\\\&B_{rown}&\end{bmatrix}=\begin{bmatrix}\vdots\\\\\left(a_{i1}B_{row1}+a_{i2}B_{row2}+\cdots+a_{in}B_{rown}\right)\\\\\vdots\end{bmatrix}$
    
    上面的運算為$A$的第$i$個列向量左乘矩陣$B$，求得的結果就是$C$矩陣的第$i$列，即$C$的第$i$列是$B$的列向量以$A$的第$i$列作為系數所求的的線性組合，$C_i=a_{i1}B_{row1}+a_{i2}B_{row2}+\cdots+a_{in}B_{rown}$。

* 行乘以列：用$A$矩陣的行乘以$B$矩陣的列，得到的矩陣相加即可：
  
    $\begin{bmatrix}&&\\\\A_{col1}&A_{col2}&\cdots&A_{coln}\\\\&&\end{bmatrix}\begin{bmatrix}&B_{row1}&\\\\&B_{row2}&\\\\&\vdots&\\\\&B_{rown}&\end{bmatrix}=A_{col1}B_{row1}+A_{col2}B_{row2}+\cdots+A_{coln}B_{rown}$
    
    注意，$A_{coli}B_{rowi}$是一個$m\times 1$向量乘以一個$1\times p$向量，其結果是一個$m\times p$矩陣，而所有的$m\times p$矩陣之和就是計算結果。

* 分塊乘法：
$\left[\begin{array}{c|c}A_1&A_2\\\\\hline A_3&A_4\end{array}\right]\left[\begin{array}{c|c}B_1&B_2\\\\\hline B_3&B_4\end{array}\right]=\left[\begin{array}{c|c}A_1B_1+A_2B_3&A_1B_2+A_2B_4\\\\\hline A_3B_1+A_4B_3&A_3B_2+A_4B_4\end{array}\right]$

    在分塊合適的情況下，可以簡化運算。

## 逆（方陣）

首先，並不是所有的方陣都有逆；而如果逆存在，則有$A^{-1}A=I=AA^{-1}$。教授這里提前劇透，對於方陣，左逆和右逆是相等的，但是對於非方陣（長方形矩陣），其左逆不等於右逆。

對於這些有逆的矩陣，我們稱其為可逆的或非奇異的。我們先來看看奇異矩陣（不可逆的）：$A=\begin{bmatrix}1&3\\\\2&6\end{bmatrix}$，在後面將要學習的行列式中，會发現這個矩陣的行列式為$0$。

觀察這個方陣，我們如果用另一個矩陣乘$A$，則得到的結果矩陣中的每一行應該都是$\begin{bmatrix}1\\\\2\end{bmatrix}$的倍數，所以我們不可能從$AB$的乘積中得到單位矩陣$I$。

另一種判定方法，如果$A$乘以任意非零向量能夠得到$0$向量，則矩陣$A$不可逆，即使用$Ax=0$判定。我們來用上面的矩陣為例：$\begin{bmatrix}1&3\\\\2&6\end{bmatrix}\begin{bmatrix}3\\\\-1\end{bmatrix}=\begin{bmatrix}0\\\\0\end{bmatrix}$。

證明：如果對於非零的$x$仍有$Ax=0$，而$A$有逆$A^{-1}$，則$A^{-1}Ax=0$，即$x=0$，與題設矛盾，得證。

現在來看看什麽矩陣有逆，設$A=\begin{bmatrix}1&3\\\\2&7\end{bmatrix}$，我們來求$A^{-1}$。$\begin{bmatrix}1&3\\\\2&7\end{bmatrix}\begin{bmatrix}a&b\\\\c&d\end{bmatrix}=\begin{bmatrix}1&0\\\\0&1\end{bmatrix}$，使用行向量線性組合的思想，我們可以說$A$乘以$A^{-1}$的第$j$行，能夠得到$I$的第$j$行，這時我會得到一個關於行的方程組。

接下來介紹高斯-若爾當（Gauss-Jordan）方法，該方法可以一次處理所有的方程：

* 這個方程組為
$\begin{cases}\begin{bmatrix}1&3\\\\2&7\end{bmatrix}\begin{bmatrix}a\\\\b\end{bmatrix}=\begin{bmatrix}1\\\\0\end{bmatrix}\\\\\begin{bmatrix}1&3\\\\2&7\end{bmatrix}\begin{bmatrix}c\\\\d\end{bmatrix}=\begin{bmatrix}0\\\\1\end{bmatrix}\end{cases}$，我們想要同時解這兩個方程；

* 構造這樣一個矩陣
$\left[\begin{array}{cc|cc}1&3&1&0\\\\2&7&0&1\end{array}\right]$，接下來用消元法將左側變為單位矩陣；
* $\left[\begin{array}{cc\|cc}1&3&1&0\\\\2&7&0&1\end{array}\right]\xrightarrow{row_2-2row_1}\left[\begin{array}{cc\|cc}1&3&1&0\\\\0&1&-2&1\end{array}\right]\xrightarrow{row_1-3row_2}\left[\begin{array}{cc\|cc}1&0&7&-3\\\\0&1&-2&1\end{array}\right]$
 
* 於是，我們就將矩陣從$\left[\begin{array}{c\|c}A&I\end{array}\right]$變為$\left[\begin{array}{c\|c}I&A^{-1}\end{array}\right]$

而高斯-若爾當法的本質是使用消元矩陣 $E$，對 $A$進行操作，$E\left[\begin{array}{c\|c}A&I\end{array}\right]$，利用一步步消元有$EA=I$，進而得到$\left[\begin{array}{c\|c}I&E\end{array}\right]$，其實這個消元矩陣 $E$就是 $A^{-1}$，而高斯-若爾當法中的$I$只是負責記錄消元的每一步操作，待消元完成，逆矩陣就自然出現了。
