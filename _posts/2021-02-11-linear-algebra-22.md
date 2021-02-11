---
layout: post
title: 線性代數筆記-22
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=23&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第二十二講：對角化和$A$的冪

## 對角化矩陣

上一講我們提到關鍵方程$Ax=\lambda x$，通過$\det(A-\lambda I)=0$得到特征向量$\lambda$，再帶回關鍵方程算出特征向量$x$。

在得到特征值與特征向量後，該如何使用它們？我們可以利用特征向量來對角化給定矩陣。

有矩陣$A$，它的特征向量為$x_1, x_2, \cdots, x_n$，使用特征向量作為行向量組成一個矩陣$S=\Bigg[x_1x_2\cdots x_n\Bigg]$，即特征向量矩陣， 再使用公式$$S^{-1}AS=\Lambda\tag{1}$$將$A$對角化。注意到公式中有$S^{-1}$，也就是說特征向量矩陣$S$必須是可逆的，於是我們需要$n$個線性無關的特征向量。

現在，假設$A$有$n$個線性無關的特征向量，將它們按行組成特征向量矩陣$S$，則$AS=A\Bigg[x_1x_2\cdots x_n\Bigg]$，當我們分開做矩陣與每一行相乘的運算時，易看出$Ax_1$就是矩陣與自己的特征向量相乘，其結果應該等於$\lambda_1x_1$。那麽$AS=\Bigg[(\lambda_1x_1)(\lambda_2x_2)\cdots(\lambda_nx_n)\Bigg]$。可以進一步化簡原式，使用右乘向量按行操作矩陣的方法，將特征值從矩陣中提出來，得到$$\Bigg[x_1x_2\cdots x_n\Bigg]\begin{bmatrix}\lambda_1&0&\cdots&0\\0&\lambda_2&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&\lambda_n\end{bmatrix}=S\Lambda$$。

於是我們看到，從$AS$出发，得到了$S\Lambda$，特征向量矩陣又一次出現了，後面接著的是一個對角矩陣，即特征值矩陣。這樣，再繼續左乘$S^{-1}$就得到了公式$(1)$。當然，所以運算的前提條件是特征向量矩陣$S$可逆，即矩陣$A$有$n$個線性無關的特征向量。這個式子還要另一種寫法，$A=S\Lambda S^{-1}$。

我們來看如何應用這個公式，比如說要計算$A^2$。

* 先從$Ax=\lambda x$開始，如果兩邊同乘以$A$，有$A^2x=\lambda Ax=\lambda^2x$，於是得出結論，對於矩陣$A^2$，其特征值也會取平方，而特征向量不變。
* 再從$A=S\Lambda S^{-1}$開始推導，則有$A^2=S\Lambda S^{-1}S\Lambda S^{-1}=S\Lambda^2S^{-1}$。同樣得到特征值取平方，特征向量不變。

兩種方法描述的是同一個現象，即對於矩陣冪運算$A^2$，其特征向量不變，而特征值做同樣的冪運算。對角矩陣$$\Lambda^2=\begin{bmatrix}\lambda_1^2&0&\cdots&0\\0&\lambda_2^2&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&\lambda_n^2\end{bmatrix}$$。

特征值和特征向量給我們了一個深入理解矩陣冪運算的方法，$A^k=S\Lambda^kS^{-1}$。

再來看一個矩陣冪運算的應用：如果$k\to\infty$，則$A^k\to 0$（趨於穩定）的條件是什麽？從$S\Lambda^kS^{-1}$易得，$\|\lambda_i\|<1$。再次強調，所有運算的前提是矩陣$A$存在$n$個線性無關的特征向量。如果沒有$n$個線性無關的特征向量，則矩陣就不能對角化。

關於矩陣可對角化的條件：

* 如果一個矩陣有$n$個互不相同的特征值（即沒有重覆的特征值），則該矩陣具有$n$個線性無關的特征向量，因此該矩陣可對角化。
* 如果一個矩陣的特征值存在重覆值，則該矩陣可能具有$n$個線性無關的特征向量。比如取$10$階單位矩陣，$I_{10}$具有$10$個相同的特征值$1$，但是單位矩陣的特征向量並不短缺，每個向量都可以作為單位矩陣的特征向量，我們很容易得到$10$個線性無關的特征向量。當然這里例子中的$I_{10}$的本來就是對角矩陣，它的特征值直接寫在矩陣中，即對角線元素。
  
    同樣的，如果是三角矩陣，特征值也寫在對角線上，但是這種情況我們可能會遇到麻煩。矩陣$$A=\begin{bmatrix}2&1\\0&2\end{bmatrix}$$，計算行列式值$$\det(A-\lambda I)=\begin{vmatrix}2-\lambda&1\\0&2-\lambda\end{vmatrix}=(2-\lambda)^2=0$$，所以特征值為$\lambda_1=\lambda_2=2$，帶回$Ax=\lambda x$得到計算$$\begin{bmatrix}0&1\\0&0\end{bmatrix}$$的零空間，我們发現$$x_1=x_2=\begin{bmatrix}1\\0\end{bmatrix}$$，代數重度（algebraic multiplicity，計算特征值重覆次數時，就用代數重度，就是它作為多項式根的次數，這里的多項式就是$(2-\lambda)^2$）為$2$，這個矩陣無法對角化。這就是上一講的退化矩陣。
    

我們不打算深入研究有重覆特征值的情形。

## 求$u_{k+1}=Au_k$

從$u_1=Au_0$開始，$u_2=A^2u_0$，所有$u_k=A^ku_0$。下一講涉及微分方程（differential equation），會有求導的內容，本講先引入簡單的差分方程（difference equation）。本例是一個一階差分方程組（first order system）。

要解此方程，需要將$u_0$展開為矩陣$A$特征向量的線性組合，即$$u_0=c_1x_1+c_2x_2+\cdots+c_nx_n=\Bigg[x_1x_2\cdots x_n\Bigg]\begin{bmatrix}c_1\\c_2\\\vdots\\c_n\end{bmatrix}=Sc$$。於是$$Au_0=c_1Ax_1+c_2Ax_2+\cdots+c_nAx_n=c_1\lambda_1x_1+c_2\lambda_2x_2+\cdots+c_n\lambda_nx_n$$。繼續化簡原式，$$Au_0=\Bigg[x_1x_2\cdots x_n\Bigg]\begin{bmatrix}\lambda_1&0&\cdots&0\\0&\lambda_2&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&\lambda_n\end{bmatrix}\begin{bmatrix}c_1\\c_2\\\vdots\\c_n\end{bmatrix}=S\Lambda c$$。用矩陣的方式同樣可以得到該式：$Au_0=S\Lambda S^{-1}u_0=S\Lambda S^{-1}Sc=S\Lambda c$。

那麽如果我們要求$A^{100}u_0$，則只需要將$\lambda$變為$\lambda^{100}$，而系數$c$與特征向量$x$均不變。

當我們真的要計算$A^{100}u_0$時，就可以使用$S\Lambda^{100}c=c_1\lambda_1^{100}x_1+c_2\lambda_2^{100}x_2+\cdots+c_n\lambda_n^{100}x_n$。

接下來看一個斐波那契數列（Fibonacci sequence）的例子：

$0,1,1,2,3,5,8,13,\cdots,F_{100}=?$，我們要求第一百項的公式，並觀察這個數列是如何增長的。可以想象這個數列並不是穩定數列，因此無論如何該矩陣的特征值並不都小於一，這樣才能保持增長。而他的增長速度，則有特征值來決定。

已知$F_{k+2}=F_{k_1}+F_{k}$，但這不是$u_{k+1}=Au_{k}$的形式，而且我們只要一個方程，而不是方程組，同時這是一個二階差分方程（就像含有二階導數的微分方程，希望能夠化簡為一階倒數，也就是一階差分）。

使用一個**小技巧**，令$$u_{k}=\begin{bmatrix}F_{k+1}\\F_{k}\end{bmatrix}$$，再追加一個方程組成方程組：$$\begin{cases}F_{k+2}&=F_{k+1}+F_{k}\\F_{k+1}&=F_{k+1}\end{cases}$$，再把方程組用矩陣表達得到$$\begin{bmatrix}F_{k+2}\\F_{k+1}\end{bmatrix}=\begin{bmatrix}1&1\\1&0\end{bmatrix}\begin{bmatrix}F_{k+1}\\F_{k}\end{bmatrix}$$，於是我們得到了$$u_{k+1}=Au_{k}, A=\begin{bmatrix}1&1\\1&0\end{bmatrix}$$。我們把二階標量方程（second-order scalar problem）轉化為一階向量方程組（first-order system）。

我們的矩陣$$A=\begin{bmatrix}1&1\\1&0\end{bmatrix}$$是一個對稱矩陣，所以它的特征值將會是實數，且他的特征向量將會互相正交。因為是二階，我們可以直接利用跡與行列式解方程組$$\begin{cases}\lambda_1+\lambda_2&=1\\\lambda_1\cdot\lambda_2&=-1\end{cases}$$。在求解之前，我們先寫出一般解法並觀察$$\left\|A-\lambda I\right\|=\begin{vmatrix}1-\lambda&1\\1&-\lambda\end{vmatrix}=\lambda^2-\lambda-1=0$$，與前面斐波那契數列的遞歸式$F_{k+2}=F_{k+1}+F_{k}\rightarrow F_{k+2}-F_{k+1}-F_{k}=0$比較，我們发現這兩個式子在項數與冪次上非常相近。

* 用求根公式解特征值得$$\begin{cases}\lambda_1=\frac{1}{2}\left(1+\sqrt{5}\right)\approx{1.618}\\\lambda_2=\frac{1}{2}\left(1-\sqrt{5}\right)\approx{-0.618}\end{cases}$$，得到兩個不同的特征值，一定會有兩個線性無關的特征向量，則該矩陣可以被對角化。

我們先來觀察這個數列是如何增長的，數列增長由什麽來控制？——特征值。哪一個特征值起決定性作用？——較大的一個。

$F_{100}=c_1\left(\frac{1+\sqrt{5}}{2}\right)^{100}+c_2\left(\frac{1-\sqrt{5}}{2}\right)^{100}\approx c_1\left(\frac{1+\sqrt{5}}{2}\right)^{100}$，由於$-0.618$在冪增長中趨近於$0$，所以近似的忽略該項，剩下較大的項，我們可以說數量增長的速度大約是$1.618$。可以看出，這種問題與求解$Ax=b$不同，這是一個動態的問題，$A$的冪在不停的增長，而問題的關鍵就是這些特征值。

* 繼續求解特征向量，$$A-\lambda I=\begin{bmatrix}1-\lambda&1\\1&1-\lambda\end{bmatrix}$$，因為有根式且矩陣只有二階，我們直接觀察$$\begin{bmatrix}1-\lambda&1\\1&1-\lambda\end{bmatrix}\begin{bmatrix}?\\?\end{bmatrix}=0$$，由於$\lambda^2-\lambda-1=0$，則其特征向量為$$\begin{bmatrix}\lambda\\1\end{bmatrix}$$，即$$x_1=\begin{bmatrix}\lambda_1\\1\end{bmatrix}, x_2=\begin{bmatrix}\lambda_2\\1\end{bmatrix}$$。

最後，計算初始項$$u_0=\begin{bmatrix}F_1\\F_0\end{bmatrix}=\begin{bmatrix}1\\0\end{bmatrix}$$，現在將初始項用特征向量表示出來$$\begin{bmatrix}1\\0\end{bmatrix}=c_1x_1+c_2x_2$$，計算系數得$c_1=\frac{\sqrt{5}}{5}, c_2=-\frac{\sqrt{5}}{5}$。

來回顧整個問題，對於動態增長的一階方程組，初始向量是$u_0$，關鍵在於確定$A$的特征值及特征向量。特征值將決定增長的趨勢，发散至無窮還是收斂於某個值。接下來需要找到一個展開式，把$u_0$展開成特征向量的線性組合。

* 再下來就是套用公式，即$A$的$k$次方表達式$A^k=S\Lambda^kS^{-1}$，則有$u_{99}=Au_{98}=\cdots=A^{99}u_{0}=S\Lambda^{99}S^{-1}Sc=S\Lambda^{99}c$，代入特征值、特征向量得$$u_{99}=\begin{bmatrix}F_{100}\\F_{99}\end{bmatrix}=\begin{bmatrix}\frac{1+\sqrt{5}}{2}&\frac{1-\sqrt{5}}{2}\\1&1\end{bmatrix}\begin{bmatrix}\left(\frac{1+\sqrt{5}}{2}\right)^{99}&0\\0&\left(\frac{1-\sqrt{5}}{2}\right)^{99}\end{bmatrix}\begin{bmatrix}\frac{\sqrt{5}}{5}\\-\frac{\sqrt{5}}{5}\end{bmatrix}=\begin{bmatrix}c_1\lambda_1^{100}+c_2\lambda_2^{100}\\c_1\lambda_1^{99}+c_2\lambda_2^{99}\end{bmatrix}$$，最終結果為$F_{100}=c_1\lambda_1^{100}+c_2\lambda_2^{100}$。

* 原式的通解為$u_k=c_1\lambda^kx_1+c_2\lambda^kx_2$。

下一講將介紹求解微分方程。
