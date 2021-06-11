---
layout: post
title: 線性代數筆記-30
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=31&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第三十講：奇異值分解

本講我們介紹將一個矩陣寫為$$A=U\varSigma V^T$$，分解的因子分別為正交矩陣、對角矩陣、正交矩陣，與前面幾講的分解不同的是，這兩個正交矩陣通常是不同的，而且這個式子可以對任意矩陣使用，不僅限於方陣、可對角化的方陣等。

* 在正定一講中（第二十八講）我們知道一個正定矩陣可以分解為$$A=Q\Lambda Q^T$$的形式，由於$$A$$對稱性其特征向量是正交的，且其$$\Lambda$$矩陣中的元素皆為正，這就是正定矩陣的奇異值分解。在這種特殊的分解中，我們只需要一個正交矩陣$$Q$$就可以使等式成立。

* 在對角化一講中（第二十二講），我們知道可對角化的矩陣能夠分解為$$A=S\Lambda S^T$$的形式，其中$$S$$的行向量由$$A$$的特征向量組成，但$$S$$並不是正交矩陣，所以這不是我們希望得到的奇異值分解。

我們現在要做的是，在$$A$$的**行空間**中找到一組特殊的正交基$$v_1,v_2,\cdots,v_r$$，這組基在$$A$$的作用下可以轉換為$$A$$的**列空間**中的一組正交基$$u_1,u_2,\cdots,u_r$$。

用矩陣語言描述為$$A\Bigg[v_1\ v_2\ \cdots\ v_r\Bigg]=\Bigg[\sigma_1u_1\ \sigma_2u_2\ \cdots\ \sigma_ru_r\Bigg]=\Bigg[u_1\ u_2\ \cdots\ u_r\Bigg]\begin{bmatrix}\sigma_1&&&\\&\sigma_2&&\\&&\ddots&\\&&&\sigma_n\end{bmatrix}$$，即$$Av_1=\sigma_1u_1,\ Av_2=\sigma_2u_2,\cdots,Av_r=\sigma_ru_r$$，這些$$\sigma$$是縮放因子，表示在轉換過程中有拉伸或壓縮。而$$A$$的左零空間和零空間將體現在$$\sigma$$的零值中。

另外，如果算上左零、零空間，我們同樣可以對左零、零空間取標準正交基，然後寫為$$A\Bigg[v_1\ v_2\ \cdots\ v_r\ v_{r+1}\ \cdots\ v_m\Bigg]=\Bigg[u_1\ u_2\ \cdots\ u_r\ u_{r+1}\ \cdots \ u_n\Bigg]\left[\begin{array}{c c c\|c}\sigma_1&&&\\&\ddots&&\\&&\sigma_r&\\\hline&&&\begin{bmatrix}0\end{bmatrix}\end{array}\right]$$，此時$$U$$是$$m\times m$$正交矩陣，$$\varSigma$$是$$m\times n$$對角矩陣，$$V^T$$是$$n\times n$$正交矩陣。

最終可以寫為$$AV=U\varSigma$$，可以看出這十分類似對角化的公式，矩陣$$A$$被轉化為對角矩陣$$\varSigma$$，我們也注意到$$U,\ V$$是兩組不同的正交基。（在正定的情況下，$$U,\ V$$都變成了$$Q$$。）。進一步可以寫作$$A=U\varSigma V^{-1}$$，因為$$V$$是標準正交矩陣所以可以寫為$$A=U\varSigma V^T$$

計算一個例子，$$A=\begin{bmatrix}4&4\\-3&3\end{bmatrix}$$，我們需要找到：

* 行空間$$\mathbb{R}^2$$的標準正交基$$v_1,v_2$$；
* 列空間$$\mathbb{R}^2$$的標準正交基$$u_1,u_2$$；
* $$\sigma_1>0, \sigma_2>0$$。

在$$A=U\varSigma V^T$$中有兩個標準正交矩陣需要求解，我們希望一次只解一個，如何先將$$U$$消去來求$$V$$？

這個技巧會經常出現在長方形矩陣中：求$$A^TA$$，這是一個對稱正定矩陣（至少是半正定矩陣），於是有$$A^TA=V\varSigma^TU^TU\varSigma V^T$$，由於$$U$$是標準正交矩陣，所以$$U^TU=I$$，而$$\varSigma^T\varSigma$$是對角線元素為$$\sigma^2$$的對角矩陣。

現在有$$A^TA=V\begin{bmatrix}\sigma_1&&&\\&\sigma_2&&\\&&\ddots&\\&&&\sigma_n\end{bmatrix}V^T$$，這個式子中$$V$$即是$$A^TA$$的特征向量矩陣而$$\varSigma^2$$是其特征值矩陣。

同理，我們只想求$$U$$時，用$$AA^T$$消掉$$V$$即可。

我們來計算$$A^TA=\begin{bmatrix}4&-3\\4&3\end{bmatrix}\begin{bmatrix}4&4\\-3&3\end{bmatrix}=\begin{bmatrix}25&7\\7&25\end{bmatrix}$$，對於簡單的矩陣可以直接觀察得到特征向量$$A^TA\begin{bmatrix}1\\1\end{bmatrix}=32\begin{bmatrix}1\\1\end{bmatrix},\ A^TA\begin{bmatrix}1\\-1\end{bmatrix}=18\begin{bmatrix}1\\-1\end{bmatrix}$$，化為單位向量有$$\sigma_1=32,\ v_1=\begin{bmatrix}\frac{1}{\sqrt{2}}\\\frac{1}{\sqrt{2}}\end{bmatrix},\ \sigma_2=18,\ v_2=\begin{bmatrix}\frac{1}{\sqrt{2}}\\-\frac{1}{\sqrt{2}}\end{bmatrix}$$。

到目前為止，我們得到$$\begin{bmatrix}4&4\\-3&3\end{bmatrix}=\begin{bmatrix}u_?&u_?\\u_?&u_?\end{bmatrix}\begin{bmatrix}\sqrt{32}&0\\0&\sqrt{18}\end{bmatrix}\begin{bmatrix}\frac{1}{\sqrt{2}}&\frac{1}{\sqrt{2}}\\\frac{1}{\sqrt{2}}&-\frac{1}{\sqrt{2}}\end{bmatrix}$$，接下來繼續求解$$U$$。

$$AA^T=U\varSigma V^TV\varSigma^TU^T=U\varSigma^2U^T$$，求出$$AA^T$$的特征向量即可得到$$U$$，$$\begin{bmatrix}4&4\\-3&3\end{bmatrix}\begin{bmatrix}4&-3\\4&3\end{bmatrix}=\begin{bmatrix}32&0\\0&18\end{bmatrix}$$，觀察得$$AA^T\begin{bmatrix}1\\0\end{bmatrix}=32\begin{bmatrix}1\\0\end{bmatrix},\ AA^T\begin{bmatrix}0\\1\end{bmatrix}=18\begin{bmatrix}0\\1\end{bmatrix}$$。但是我們不能直接使用這一組特征向量，因為式子$$AV=U\varSigma$$明確告訴我們，一旦$$V$$確定下來，$$U$$也必須取能夠滿足該式的向量，所以此處$$Av_2=\begin{bmatrix}0\\-\sqrt{18}\end{bmatrix}=u_2\sigma_2=\begin{bmatrix}0\\-1\end{bmatrix}\sqrt{18}$$，則$$u_1=\begin{bmatrix}1\\0\end{bmatrix},\ u_2=\begin{bmatrix}0\\-1\end{bmatrix}$$。（這個問題在[本講的官方筆記](http://ocw.mit.edu/courses/mathematics/18-06sc-linear-algebra-fall-2011/positive-definite-matrices-and-applications/singular-value-decomposition/MIT18_06SCF11_Ses3.5sum.pdf)中有詳細說明。）

* 補充：$$AB$$的特征值與$$BA$$的特征值相同，證明來自[Are the eigenvalues of AB equal to the eigenvalues of BA? (Citation needed!)](http://math.stackexchange.com/questions/124888/are-the-eigenvalues-of-ab-equal-to-the-eigenvalues-of-ba-citation-needed)：

    取$$\lambda\neq 0$$，$$v$$是$$AB$$在特征值取$$\lambda$$時的的特征向量，則有$$Bv\neq 0$$，並有$$\lambda Bv=B(\lambda v)=B(ABv)=(BA)Bv$$，所以$$Bv$$是$$BA$$在特征值取同一個$$\lambda$$時的特征向量。
    
    再取$$AB$$的特征值$$\lambda=0$$，則$$0=\det{AB}=\det{A}\det{B}=\det{BA}$$，所以$$\lambda=0$$也是$$BA$$的特征值，得證。

最終，我們得到$$\begin{bmatrix}4&4\\-3&3\end{bmatrix}=\begin{bmatrix}1&0\\0&-1\end{bmatrix}\begin{bmatrix}\sqrt{32}&0\\0&\sqrt{18}\end{bmatrix}\begin{bmatrix}\frac{1}{\sqrt{2}}&\frac{1}{\sqrt{2}}\\\frac{1}{\sqrt{2}}&-\frac{1}{\sqrt{2}}\end{bmatrix}$$。

再做一個例子，$$A=\begin{bmatrix}4&3\\8&6\end{bmatrix}$$，這是個秩一矩陣，有零空間。$$A$$的列空間為$$\begin{bmatrix}4\\3\end{bmatrix}$$的倍數，$$A$$的行空間為$$\begin{bmatrix}4\\8\end{bmatrix}$$的倍數。

* 標準化向量得$$v_1=\begin{bmatrix}0.8\\0.6\end{bmatrix},\ u_1=\frac{1}{\sqrt{5}}\begin{bmatrix}1\\2\end{bmatrix}$$。
* $$A^TA=\begin{bmatrix}4&8\\3&6\end{bmatrix}\begin{bmatrix}4&3\\8&6\end{bmatrix}=\begin{bmatrix}80&60\\60&45\end{bmatrix}$$，由於$$A$$是秩一矩陣，則$$A^TA$$也不滿秩，所以必有特征值$$0$$，則另特征值一個由跡可知為$$125$$。
* 繼續求零空間的特征向量，有$$v_2=\begin{bmatrix}0.6\\-0,8\end{bmatrix},\ u_1=\frac{1}{\sqrt{5}}\begin{bmatrix}2\\-1\end{bmatrix}$$

最終得到$$\begin{bmatrix}4&3\\8&6\end{bmatrix}=\begin{bmatrix}1&\underline {2}\\2&\underline{-1}\end{bmatrix}\begin{bmatrix}\sqrt{125}&0\\0&\underline{0}\end{bmatrix}\begin{bmatrix}0.8&0.6\\\underline{0.6}&\underline{-0.8}\end{bmatrix}$$，其中下劃線部分都是與零空間相關的部分。

* $$v_1,\ \cdots,\ v_r$$是列空間的標準正交基；
* $$u_1,\ \cdots,\ u_r$$是行空間的標準正交基；
* $$v_{r+1},\ \cdots,\ v_n$$是零空間的標準正交基；
* $$u_{r+1},\ \cdots,\ u_m$$是左零空間的標準正交基。

通過將矩陣寫為$$Av_i=\sigma_iu_i$$形式，將矩陣對角化，向量$$u,\ v$$之間沒有耦合，$$A$$乘以每個$$v$$都能得到一個相應的$$u$$。
