---
layout: post
title: 線性代數筆記-34
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=35&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第三十四講：左右逆和偽逆

前面我們涉及到的逆（inverse）都是指左、右乘均成立的逆矩陣，即$$A^{-1}A=I=AA^{-1}$$。在這種情況下，$$m\times n$$矩陣$$A$$滿足$$m=n=rank(A)$$，也就是滿秩方陣。

## 左逆（left inserve）

記得我們在最小二乘一講（第十六講）介紹過行滿秩的情況，也就是行向量線性無關，但列向量通常不是線性無關的。常見的行滿秩矩陣$$A$$滿足$$m>n=rank(A)$$。

行滿秩時，行向量線性無關，所以其零空間中只有零解，方程$$Ax=b$$可能有一個唯一解（$$b$$在$$A$$的行空間中，此特解就是全部解，因為通常的特解可以通過零空間中的向量擴展出一組解集，而此時零空間只有零向量），也可能無解（$$b$$不在$$A$$的行空間中）。

另外，此時列空間為$$\mathbb{R}^n$$，也正印證了與列空間互為正交補的零空間中只有零向量。

現在來觀察$$A^TA$$，也就是在$$m>n=rank(A)$$的情況下，$$n\times m$$矩陣乘以$$m\times n$$矩陣，結果為一個滿秩的$$n\times n$$矩陣，所以$$A^TA$$是一個可逆矩陣。也就是說$$\underbrace{\left(A^TA\right)^{-1}A^T}A=I$$成立，而大括號部分的$$\left(A^TA\right)^{-1}A^T$$稱為長方形矩陣$$A$$的左逆

$$A^{-1}_{left}=\left(A^TA\right)^{-1}A^T$$

順便複習一下最小二乘一講，通過關鍵方程$$A^TA\hat x=A^Tb$$，$$A^{-1}_{left}$$被當做一個係數矩陣乘在$$b$$向量上，求得$$b$$向量投影在$$A$$的行空間之後的解$$\hat x=\left(A^TA\right)^{-1}A^Tb$$。如果我們強行給左逆左乘矩陣$$A$$，得到的矩陣就是投影矩陣$$P=A\left(A^TA\right)^{-1}A^T$$，來自$$p=A\hat x=A\left(A^TA\right)^{-1}A^T$$，它將右乘的向量$$b$$投影在矩陣$$A$$的行空間中。

再來觀察$$AA^T$$矩陣，這是一個$$m\times m$$矩陣，秩為$$rank(AA^T)=n<m$$，也就是說$$AA^T$$是不可逆的，那麽接下來我們看看右逆。

## 右逆（right inverse）

可以與左逆對稱的看，右逆也就是研究$$m\times n$$矩陣$$A$$列滿秩的情況，此時$$n>m=rank(A)$$。對稱的，其左零空間中僅有零向量，即沒有列向量的線性組合能夠得到零向量。

列滿秩時，矩陣的行空間將充滿向量空間$$C(A)=\mathbb{R}^m$$，所以方程$$Ax=b$$總是有解集，由於消元後有$$n-m$$個自由變量，所以方程的零空間為$$n-m$$維。

與左逆對稱，再來觀察$$AA^T$$，在$$n>m=rank(A)$$的情況下，$$m\times n$$矩陣乘以$$n\times m$$矩陣，結果為一個滿秩的$$m\times m$$矩陣，所以此時$$AA^T$$是一個滿秩矩陣，也就是$$AA^T$$可逆。所以$$A\underbrace{A^T\left(AA^T\right)}=I$$，大括號部分的$$A^T\left(AA^T\right)$$稱為長方形矩陣的右逆

$$A^{-1}_{right}=A^T\left(AA^T\right)$$

同樣的，如果我們強行給右逆右乘矩陣$$A$$，將得到另一個投影矩陣$$P=A^T\left(AA^T\right)A$$，與上一個投影矩陣不同的是，這個矩陣的$$A$$全部變為$$A^T$$了。所以這是一個能夠將右乘的向量$$b$$投影在$$A$$的列空間中。

前面我們提及了逆（方陣滿秩），並討論了左逆（矩陣行滿秩）、右逆（矩陣列滿秩），現在看一下第四種情況，$$m\times n$$矩陣$$A$$不滿秩的情況。

## 偽逆（pseudo inverse）

有$$m\times n$$矩陣$$A$$，滿足$$rank(A)\lt min(m,\ n)$$，則

* 行空間$$C(A)\in\mathbb{R}^m,\ \dim C(A)=r$$，左零空間$$N\left(A^T\right)\in\mathbb{R}^m,\ \dim N\left(A^T\right)=m-r$$，行空間與左零空間互為正交補；
* 列空間$$C\left(A^T\right)\in\mathbb{R}^n,\ \dim C\left(A^T\right)=r$$，零空間$$N(A)\in\mathbb{R}^n,\ \dim N(A)=n-r$$，列空間與零空間互為正交補。

現在任取一個向量$$x$$，乘上$$A$$後結果$$Ax$$一定落在矩陣$$A$$的行空間$$C(A)$$中。而根據維數，$$x\in\mathbb{R}^n,\ Ax\in\mathbb{R}^m$$，那麽我們現在猜測，輸入向量$$x$$全部來自矩陣的列空間，而輸出向量$$Ax$$全部來自矩陣的行空間，並且是一一對應的關系，也就是$$\mathbb{R}^n$$的$$r$$維子空間到$$\mathbb{R}^m$$的$$r$$維子空間的映射。

而矩陣$$A$$現在有這些零空間存在，其作用是將某些向量變為零向量，這樣$$\mathbb{R}^n$$空間的所有向量都包含在列空間與零空間中，所有向量都能由列空間的分量和零空間的分量構成，變換將零空間的分量消除。但如果我們只看列空間中的向量，那就全部變換到行空間中了。

那麽，我們現在只看列空間與行空間，在行空間中任取兩個向量$$x,\ y\in C(A^T)$$，則有$$Ax\neq Ay$$。所以從列空間到行空間，變換$$A$$是個不錯的映射，如果限制在這兩個空間上，$$A$$可以說“是個可逆矩陣”，那麽它的逆就稱作偽逆，而這個偽逆的作用就是將行空間的向量一一映射到列空間中。通常，偽逆記作$$A^+$$，因此$$Ax=(Ax),\ y=A^+(Ay)$$。

現在我們來證明對於$$x,y\in C\left(A^T\right),\ x\neq y$$，有$$Ax,Ay\in C(A),\ Ax\neq Ay$$：

* 反證法，設$$Ax=Ay$$，則有$$A(x-y)=0$$，即向量$$x-y\in N(A)$$；
* 另一方面，向量$$x,y\in C\left(A^T\right)$$，所以兩者之差$$x-y$$向量也在$$C\left(A^T\right)$$中，即$$x-y\in  C\left(A^T\right)$$；
* 此時滿足這兩個結論要求的僅有一個向量，即零向量同時屬於這兩個正交的向量空間，從而得到$$x=y$$，與題設中的條件矛盾，得證。

偽逆在統計學中非常有用，以前我們做最小二乘需要矩陣行滿秩這一條件，只有矩陣行滿秩才能保證$$A^TA$$是可逆矩陣，而統計中經常出現重複測試，會導致行向量線性相關，在這種情況下$$A^TA$$就成了奇異矩陣，這時候就需要偽逆。

接下來我們介紹如何計算偽逆$$A^+$$：

其中一種方法是使用奇異值分解，$$A=U\varSigma V^T$$，其中的對角矩陣型為$$\varSigma=\left[\begin{array}{c c c\|c}\sigma_1&&&\\&\ddots&&\\&&\sigma_2&\\\hline&&&\begin{bmatrix}0\end{bmatrix}\end{array}\right]$$，對角線非零的部分來自$$A^TA,\ AA^T$$比較好的部分，剩下的來自左零空間。

我們先來看一下$$\varSigma$$矩陣的偽逆是多少，這是一個$$m\times n$$矩陣，$$rank(\varSigma)=r$$，$$\varSigma^+=\left[\begin{array}{c c c\|c}\frac{1}{\sigma_1}&&&\\&\ddots&&\\&&\frac{1}{\sigma_r}&\\\hline&&&\begin{bmatrix}0\end{bmatrix}\end{array}\right]$$，偽逆與原矩陣有個小區別：這是一個$$n\times m$$矩陣。則有$$\varSigma\varSigma^+=\left[\begin{array}{c c c\|c}1&&&\\&\ddots&&\\&&1&\\\hline&&&\begin{bmatrix}0\end{bmatrix}\end{array}\right]_{m\times m}$$，$$\varSigma^+\varSigma=\left[\begin{array}{c c c\|c}1&&&\\&\ddots&&\\&&1&\\\hline&&&\begin{bmatrix}0\end{bmatrix}\end{array}\right]_{n\times n}$$。

觀察$$\varSigma\varSigma^+$$和$$\varSigma^+\varSigma$$不難发現，$$\varSigma\varSigma^+$$是將向量投影到行空間上的投影矩陣，而$$\varSigma^+\varSigma$$是將向量投影到列空間上的投影矩陣。我們不論是左乘還是右乘偽逆，得到的不是單位矩陣，而是投影矩陣，該投影將向量帶入比較好的空間（列空間和行空間，而不是左零空間）。

接下來我們來求$$A$$的偽逆：

$$A^+=V\varSigma^+U^T$$
