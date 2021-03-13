---
layout: post
title: 線性代數筆記-26
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=27&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第二十六講：對稱矩陣及正定性

## 對稱矩陣

前面我們學習了矩陣的特征值與特征向量，也了解了一些特殊的矩陣及其特征值、特征向量，特殊矩陣的特殊性應該會反映在其特征值、特征向量中。如馬爾科夫矩陣，有一特征值為$1$，本講介紹（實）對稱矩陣。

先提前介紹兩個對稱矩陣的特性：

1. 特征值為實數；（對比第二十一講介紹的旋轉矩陣，其特征值為純虛數。）
2. 特征向量相互正交。（當特征值重覆時，特征向量也可以從子空間中選出相互正交正交的向量。）

典型的狀況是，特征值不重覆，特征向量相互正交。

* 那麽在通常（可對角化）情況下，一個矩陣可以化為：$A=S\varLambda S^{-1}$；
* 在矩陣對稱的情況下，通過性質2可知，由特征向量組成的矩陣$S$中的行向量是相互正交的，此時如果我們把特征向量的長度統一化為$1$，就可以得到一組標準正交的特征向量。則對於對稱矩陣有$A=Q\varLambda Q^{-1}$，而對於標準正交矩陣，有$Q=Q^T$，所以對稱矩陣可以寫為$$A=Q\varLambda Q^T\tag{1}$$

觀察$(1)$式，我們发現這個分解本身就代表著對稱，$\left(Q\varLambda Q^T\right)^T=\left(Q^T\right)^T\varLambda^TQ^T=Q\varLambda Q^T$。$(1)$式在數學上叫做譜定理（spectral theorem），譜就是指矩陣特征值的集合。（該名稱來自光譜，指一些純事物的集合，就像將特征值分解成為特征值與特征向量。）在力學上稱之為主軸定理（principle axis theorem），從幾何上看，它意味著如果給定某種材料，在合適的軸上來看，它就變成對角化的，方向就不會重覆。

* 現在我們來證明性質1。對於矩陣$\underline{Ax=\lambda x}$，對於其共軛部分總有$\bar A\bar x=\bar\lambda \bar x$，根據前提條件我們只討論實矩陣，則有$A\bar x=\bar\lambda \bar x$，將等式兩邊取轉置有$\overline{\bar{x}^TA=\bar{x}^T\bar\lambda}$。將“下劃線”式兩邊左乘$\bar{x}^T$有$\bar{x}^TAx=\bar{x}^T\lambda x$，“上劃線”式兩邊右乘$x$有$\bar{x}^TAx=\bar{x}^T\bar\lambda x$，觀察发現這兩個式子左邊是一樣的，所以$\bar{x}^T\lambda x=\bar{x}^T\bar\lambda x$，則有$\lambda=\bar{\lambda}$（這里有個條件，$\bar{x}^Tx\neq 0$），證畢。

    觀察這個前提條件，$$\bar{x}^Tx=\begin{bmatrix}\bar x_1&\bar x_2&\cdots&\bar x_n\end{bmatrix}\begin{bmatrix}x_1\\x_2\\\vdots\\x_n\end{bmatrix}=\bar x_1x_1+\bar x_2x_2+\cdots+\bar x_nx_n$$，設$x_1=a+ib, \bar x_1=a-ib$則$\bar x_1x_1=a^2+b^2$，所以有$\bar{x}^Tx>0$。而$\bar{x}^Tx$就是$x$長度的平方。

    拓展這個性質，當$A$為複矩陣，根據上面的推導，則矩陣必須滿足$A=\bar{A}^T$時，才有性質1、性質2成立（教授稱具有這種特征值為實數、特征向量相互正交的矩陣為“好矩陣”）。

繼續研究$$A=Q\varLambda Q^T=\Bigg[q_1\ q_2\ \cdots\ q_n\Bigg]\begin{bmatrix}\lambda_1& &\cdots& \\&\lambda_2&\cdots&\\\vdots&\vdots&\ddots&\vdots\\& &\cdots&\lambda_n\end{bmatrix}\begin{bmatrix}\quad q_1^T\quad\\\quad q_1^T\quad\\\quad \vdots \quad\\\quad q_1^T\quad\end{bmatrix}=\lambda_1q_1q_1^T+\lambda_2q_2q_2^T+\cdots+\lambda_nq_nq_n^T$$，注意這個展開式中的$qq^T$，$q$是單位列向量所以$q^Tq=1$，結合我們在第十五講所學的投影矩陣的知識有$\frac{qq^T}{q^Tq}=qq^T$是一個投影矩陣，很容易驗證其性質，比如平方它會得到$qq^Tqq^T=qq^T$於是多次投影不變等。

**每一個對稱矩陣都可以分解為一系列相互正交的投影矩陣。**

在知道對稱矩陣的特征值皆為實數後，我們再來討論這些實數的符號，因為特征值的正負號會影響微分方程的收斂情況（第二十三講，需要實部為負的特征值保證收斂）。用消元法取得矩陣的主元，觀察主元的符號，**主元符號的正負數量與特征向量的正負數量相同**。

## 正定性

如果對稱矩陣是“好矩陣”，則正定矩陣（positive definite）是其一個更好的子類。正定矩陣指特征值均為正數的矩陣（根據上面的性質有矩陣的主元均為正）。

舉個例子，$$\begin{bmatrix}5&2\\2&3\end{bmatrix}$$，由行列式消元知其主元為$5,\frac{11}{5}$，按一般的方法求特征值有$$\begin{vmatrix}5-\lambda&2\\2&3-lambda\end{vmatrix}=\lambda^2-8\lambda+11=0, \lambda=4\pm\sqrt 5$$。

正定矩陣的另一個性質是，所有子行列式為正。對上面的例子有$$\begin{vmatrix}5\end{vmatrix}=5, \begin{vmatrix}5&2\\2&3\end{vmatrix}=11$$。

我們看到正定矩陣將早期學習的的消元主元、中期學習的的行列式、後期學習的特征值結合在了一起。
