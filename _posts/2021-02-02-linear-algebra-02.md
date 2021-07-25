---
layout: post
title: 線性代數筆記-02
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=3&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第二講：矩陣消元

這個方法最早由高斯提出，我們以前解方程組的時候都會使用，現在來看如何使用矩陣實現消元法。

## 消元法

有三元方程组$\begin{cases}x&+2y&+z&=2\\\\3x&+8y&+z&=12\\\\&4y&+z&=2\end{cases}$對應的矩陣形式$Ax=b$為$\begin{bmatrix}1&2&1\\\\3&8&1\\\\0&4&1\end{bmatrix}\begin{bmatrix}x\\\\y\\\\z\end{bmatrix}=\begin{bmatrix}2\\\\12\\\\2\end{bmatrix}$。

按照我們以前做消元法的思路：

* 第一步，我們希望在第二個方程中消去$x$項，來操作係數矩陣$A=\begin{bmatrix}\underline{1}&2&1\\\\3&8&1\\\\0&4&1\end{bmatrix}$，下劃線的元素為第一步的主元（pivot）：$\begin{bmatrix}\underline{1}&2&1\\\\3&8&1\\\\0&4&1\end{bmatrix}\xrightarrow{row_2-3row_1}\begin{bmatrix}\underline{1}&2&1\\\\0&2&-2\\\\0&4&1\end{bmatrix}$

    這裡我們先不管$b$向量，等做完$A$的消元可以再做$b$的消元。 （這是MATLAB等工具經常使用的算法。）
* 第二步，我們希望在第三個方程中消去$y$項，現在第二列第一個非零元素成為了第二個主元：$\begin{bmatrix}\underline{1}&2&1\\\\0&\underline{2}&-2\\\\0&4&1\end{bmatrix}\xrightarrow{row_3-2row_2}\begin{bmatrix}\underline{1}&2&1\\\\0&\underline{2}&-2\\\\0&0&\underline{5}\end{bmatrix}$
  
    注意到第三列消元過後僅剩一個非零元素，所以它就成為第三個主元。做到這裡就算消元完成了。

再來討論一下消元失效的情形：首先，主元不能為零；其次，如果在消元時遇到主元位置為零，則需要交換列，使主元不為零；最後提一下，如果我們把第三個方程$z$前的係數成$-4$，會導致第二步消元時最後一列全部為零，則第三個主元就不存在了，至此消元不能繼續進行了，這就是下一講中涉及的不可逆情況。

* 接下來就該回代（back substitution）了，這時我們在$A$矩陣後面加上$b$向量寫成增廣矩陣（augmented matrix）的形式：
$\left[\begin{array}{c|c}A&b\end{array}\right]=\left[\begin{array}{ccc|c}1&2&1&2\\\\3&8&1&12\\\\0&4&1&2\end{array}\right]\to\left[\begin{array}{ccc|c}1&2&1&2\\\\0&2&-2&6\\\\0&4&1&2\end{array}\right]\to\left[\begin{array}{ccc|c}1&2&1&2\\\\0&2&-2&6\\\\0&0&5&-10\end{array}\right]$

    不難看出，$z$的解已經出現了，此時方程組變為$\begin{cases}x&+2y&+z&=2\\\\&2y&-2z&=6\\\\&&5z&=-10\end{cases}$，從第三個方程求出$z=-2$，代入第二個方程求出$y=1$，在代入第一個方程求出$x=2$。

## 消元矩陣

上一講我們學習了矩陣乘以向量的方法，有三個行向量的矩陣乘以另一個向量，按行的線性組合可以寫作$\Bigg[v_1\ v_2\ v_3\Bigg]\begin{bmatrix}3\\\\4\\\\5\end{bmatrix}=3v_1+4v_2+5v_3$。

但現在我們希望用矩陣乘法表示列操作，則有$\begin{bmatrix}1&2&7\end{bmatrix}\begin{bmatrix}&row_1&\\\\&row_2&\\\\&row_3&\end{bmatrix}=1row_1+2row_2+7row_3$。易看出這裡是一個列向量從左邊乘以矩陣，這個列向量按列操作矩陣的列向量，並將其合成為一個矩陣列向量的線性組合。

介紹到這裡，我們就可以將消元法所做的列操作寫成向量乘以矩陣的形式了。

* 消元法第一步操作為將第二列改成$row_2-3row_1$，其餘兩行不變，則有$\begin{bmatrix}1&0&0\\\\-3&1&0\\\\0&0&1\end{bmatrix}\begin{bmatrix}1&2&1\\\\3&8&1\\\\0&4&1\end{bmatrix}=\begin{bmatrix}1&2&1\\\\0&2&-2\\\\0&4&1\end{bmatrix}$（另外，如果三列都不變，消元矩陣就是單位矩陣$I=\begin{bmatrix}1&0&0\\\\0&1&0\\\\0&0&1\end{bmatrix}$，$I$之於矩陣運算相當於$1$之於四則運算。 ）這個消元矩陣我們記作$E_{21}$，即將第二列第一個元素變為零。

* 接下來就是求$E_{32}$消元矩陣了，即將第三列第二個元素變為零，則$\begin{bmatrix}1&0&0\\\\0&1&0\\\\0&-2&1\end{bmatrix}\begin{bmatrix}1&2&1\\\\0&2&-2\\\\0&4&1\end{bmatrix}=\begin{bmatrix}1&2&1\\\\0&2&-2\\\\0&0&5\end{bmatrix}$。這就是消元所用的兩個初等矩陣（elementary matrix）。

* 最後，我們將這兩步綜合起來，即$E_{32}(E_{12}A)=U$，也就是說如果我們想從$A$矩陣直接得到$U$矩陣的話，只需要$ (E_{32}E_{21})A$即可。注意，矩陣乘法雖然不能隨意變動相乘次序，但是可以變動括號位置，也就是滿足結合律（associative law），而結合律在矩陣運算中非常重要，很多定理的證明都需要巧妙的使用結合律。

既然提到了消元用的初等矩陣，那我們再介紹一種用於置換兩列的矩陣：置換矩陣（permutation matrix）：例如$\begin{bmatrix}0&1\\\\1&0\end{bmatrix}\begin{bmatrix}a&b\\\\c&d\end{bmatrix}=\begin{bmatrix}c&d\\\\a&b\end{bmatrix}$，置換矩陣將原矩陣的兩列做了互換。順便提一下，如果我們希望交換兩行，則有$\begin{bmatrix}a&b\\\\c&d\end{bmatrix}\begin{bmatrix}0&1\\\\1&0\end{bmatrix}=\begin{bmatrix}b&a\\\\d&c\end{bmatrix}$。

我們現在能夠將$A$通過列變換寫成$U$，那麼如何從$U$再變回$A$，也就是求消元的逆運算。對某些“壞”矩陣，並沒有逆，而本講的例子都是“好”矩陣。

## 逆

現在，我們以$E_{21}$為例，$\Bigg[\quad ?\quad \Bigg]\begin{bmatrix}1&0&0\\\\-3&1&0\\\\0&0&1\end{bmatrix}=\begin{bmatrix}1&0&0\\\\0&1&0\\\\0&0&1\end{bmatrix}$，什麼矩陣可以取消這次列變換？這次變換是從第二列中減去三倍的第一列，那麼其逆變換就是給第二列加上三倍的第一列，所以逆矩陣就是$\begin{bmatrix}1&0&0\\\\3&1&0\\\\0&0&1\end{bmatrix}$。

我們把矩陣$E$的逆記作$E^{-1}$，所以有$E^{-1}E=I$。
