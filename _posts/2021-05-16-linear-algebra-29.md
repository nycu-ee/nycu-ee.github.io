---
layout: post
title: 線性代數筆記-29
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=30&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第二十九講：相似矩陣和若爾當形

在本講的開始，先接著上一講來繼續說一說正定矩陣。

* 正定矩陣的逆矩陣有什麼性質？我們將正定矩陣分解為$$A=S\Lambda S^{-1}$$，引入其逆矩陣$$A^{-1}=S\Lambda^{-1}S^{-1}$$，我們知道正定矩陣的特征值均為正值，所以其逆矩陣的特征值也必為正值（即原矩陣特征值的倒數）所以，正定矩陣的逆矩陣也是正定的。

* 如果$$A,\ B$$均為正定矩陣，那麼$$A+B$$呢？我們可以從判定$$x^T(A+B)x$$入手，根據條件有$$x^TAx>0,\ x^TBx>0$$，將兩式相加即得到$$x^T(A+B)x>0$$。所以正定矩陣之和也是正定矩陣。

* 再來看有$$m\times n$$矩陣$$A$$，則$$A^TA$$具有什麼性質？我們在投影部分經常使用$$A^TA$$，這個運算會得到一個對稱矩陣，這個形式的運算用數字打比方就像是一個平方，用向量打比方就像是向量的長度平方，而對於矩陣，有$$A^TA$$正定：在式子兩邊分別乘向量及其轉置得到$$x^TA^TAx$$，分組得到$$(Ax)^T(Ax)$$，相當於得到了向量$$Ax$$的長度平方，則$$\|Ax\|^2\geq0$$。要保證模不為零，則需要$$Ax$$的零空間中僅有零向量，即$$A$$的各列線性無關（$$rank(A)=n$$）即可保證$$\|Ax\|^2>0$$，$$A^TA$$正定。

* 另外，在矩陣數值計算中，正定矩陣消元不需要進行“列交換”操作，也不必擔心主元過小或為零，正定矩陣具有良好的計算性質。

接下來進入本講的正題。

## 相似矩陣

先列出定義：矩陣$$A,\ B$$對於某矩陣$$M$$滿足$$B=M^{-1}AM$$時，成$$A,\ B$$互為相似矩陣。

對於在對角化一講（第二十二講）中學過的式子$$S^{-1}AS=\Lambda$$，則有$$A$$相似於$$\Lambda$$。

* 舉個例子，$$A=\begin{bmatrix}2&1\\1&2\end{bmatrix}$$，容易通過其特征值得到相應的對角矩陣$$\Lambda=\begin{bmatrix}3&0\\0&1\end{bmatrix}$$，取$$M=\begin{bmatrix}1&4\\0&1\end{bmatrix}$$，則$$B=M^{-1}AM=\begin{bmatrix}1&-4\\0&1\end{bmatrix}\begin{bmatrix}2&1\\1&2\end{bmatrix}\begin{bmatrix}1&4\\0&1\end{bmatrix}=\begin{bmatrix}-2&-15\\1&6\end{bmatrix}$$。

    我們來計算這幾個矩陣的的特征值（利用跡與行列式的性質），$$\lambda_{\Lambda}=3,\ 1$$、$$\lambda_A=3,\ 1$$、$$\lambda_B=3,\ 1$$。

所以，相似矩陣有相同的特征值。

* 繼續上面的例子，特征值為$$3,\ 1$$的這一族矩陣都是相似矩陣，如$$\begin{bmatrix}3&7\\0&1\end{bmatrix}$$、$$\begin{bmatrix}1&7\\0&3\end{bmatrix}$$，其中最特殊的就是$$\Lambda$$。

現在我們來證明這個性質，有$$Ax=\lambda x,\ B=M^{-1}AM$$，第一個式子化為$$AMM^{-1}x=\lambda x$$，接著兩邊同時左乘$$M^{-1}$$得$$M^{-1}AMM^{-1}x=\lambda M^{-1}x$$，進行適當的分組得$$\left(M^{-1}AM\right)M^{-1}x=\lambda M^{-1}x$$即$$BM^{-1}x=\lambda M^{-1}x$$。

$$BM^{-1}=\lambda M^{-1}x$$可以解讀成矩陣$$B$$與向量$$M^{-1}x$$之積等於$$\lambda$$與向量$$M^{-1}x$$之積，也就是$$B$$的仍為$$\lambda$$，而特征向量變為$$M^{-1}x$$。

以上就是我們得到的一族特征值為$$3,\ 1$$的矩陣，它們具有相同的特征值。接下來看特征值重複時的情形。

* 特征值重複可能會導致特征向量短缺，來看一個例子，設$$\lambda_1=\lambda_2=4$$，寫出具有這種特征值的矩陣中的兩個$$\begin{bmatrix}4&0\\0&4\end{bmatrix}$$，$$\begin{bmatrix}4&1\\0&4\end{bmatrix}$$。其實，具有這種特征值的矩陣可以分為兩族，第一族僅有一個矩陣$$\begin{bmatrix}4&0\\0&4\end{bmatrix}$$，它只與自己相似（因為$$M^{-1}\begin{bmatrix}4&0\\0&4\end{bmatrix}M=4M^{-1}IM=4I=\begin{bmatrix}4&0\\0&4\end{bmatrix}$$，所以無論$$M$$如何取值該對角矩陣都只與自己相似）；另一族就是剩下的諸如$$\begin{bmatrix}4&1\\0&4\end{bmatrix}$$的矩陣，它們都是相似的。在這個“大家族”中，$$\begin{bmatrix}4&1\\0&4\end{bmatrix}$$是“最好”的一個矩陣，稱為若爾當形。

若爾當形在過去是線性代數的核心知識，但現在不是了（現在是下一講的奇異值分解），因為它並不容易計算。

* 繼續上面的例子，我們在在出幾個這一族的矩陣$$\begin{bmatrix}4&1\\0&4\end{bmatrix},\ \begin{bmatrix}5&1\\-1&3\end{bmatrix},\ \begin{bmatrix}4&0\\17&4\end{bmatrix}$$，我們總是可以構造出一個滿足$$trace(A)=8,\ \det A=16$$的矩陣，這個矩陣總是在這一個“家族”中。

## 若爾當形

再來看一個更加“糟糕”的矩陣：

* 矩陣$$\begin{bmatrix}0&1&0&0\\0&0&1&0\\0&0&0&0\\0&0&0&0\end{bmatrix}$$，其特征值為四個零。很明顯矩陣的秩為$$2$$，所以其零空間的維數為$$4-2=2$$，即該矩陣有兩個特征向量。可以发現該矩陣在主對角線的上方有兩個$$1$$，在對角線上每增加一個$$1$$，特征向量個個數就減少一個。

* 令一個例子，$$\begin{bmatrix}0&1&0&0\\0&0&0&0\\0&0&0&1\\0&0&0&0\end{bmatrix}$$，從特征向量的數目看來這兩個矩陣是相似的，其實不然。

    若爾當認為第一個矩陣是由一個$$3\times 3$$的塊與一個$$1\times 1$$的塊組成的 $$\left[\begin{array}{ccc\|c}0&1&0&0\\0&0&0&0\\0&0&0&1\\\hline0&0&0&0\end{array}\right]$$，而第二個矩陣是由兩個$$2\times 2$$矩陣組成的$$\left[\begin{array}{cc\|cc}0&1&0&0\\0&0&0&0\\\hline0&0&0&1\\0&0&0&0\end{array}\right]$$，這些分塊被稱為若爾當塊。

若爾當塊的定義型為$$J_i=\begin{bmatrix}\lambda_i&1&&\cdots&\\&\lambda_i&1&\cdots&\\&&\lambda_i&\cdots&\\\vdots&\vdots&\vdots&\ddots&\\&&&&\lambda_i\end{bmatrix}$$，它的對角線上只為同一個數，僅有一個特征向量。

所以，每一個矩陣$$A$$都相似於一個若爾當矩陣，型為$$J=\left[\begin{array}{c\|c\|c\|c}J_1&&&\\\hline&J_2&&\\\hline&&\ddots&\\\hline&&&J_d\end{array}\right]$$。注意，對角線上方還有$$1$$。若爾當塊的個數即為矩陣特征值的個數。

在矩陣為“好矩陣”的情況下，$$n$$階矩陣將有$$n$$個不同的特征值，那麼它可以對角化，所以它的若爾當矩陣就是$$\Lambda$$，共$$n$$個特征向量，有$$n$$個若爾當塊。
