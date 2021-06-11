---
layout: post
title: 線性代數筆記-23
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=24&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第二十三講：微分方程和$e^{At}$

## 微分方程$\frac{\mathrm{d}u}{\mathrm{d}t}=Au$

本講主要講解解一階方程（first-order system）一階倒數（first derivative）常系數（constant coefficient）線性方程，上一講介紹了如何計算矩陣的冪，本講將進一步涉及矩陣的指數形式。我們通過解一個例子來詳細介紹計算方法。

有方程組$$\begin{cases}\frac{\mathrm{d}u_1}{\mathrm{d}t}&=-u_1+2u_2\\\frac{\mathrm{d}u_2}{\mathrm{d}t}&=u_1-2u_2\end{cases}$$，則系數矩陣是$$A=\begin{bmatrix}-1&2\\1&-2\end{bmatrix}$$，設初始條件為在$0$時刻$$u(0)=\begin{bmatrix}u_1\\u_2\end{bmatrix}=\begin{bmatrix}1\\0\end{bmatrix}$$。

* 這個初始條件的意義可以看做在開始時一切都在$u_1$中，但隨著時間的推移，將有$\frac{\mathrm{d}u_2}{\mathrm{d}t}>0$，因為$u_1$項初始為正，$u_1$中的事物會流向$u_2$。隨著時間的发展我們可以追蹤流動的變化。

* 根據上一講所學的知識，我們知道第一步需要找到特征值與特征向量。$$A=\begin{bmatrix}-1&2\\1&-2\end{bmatrix}$$，很明顯這是一個奇異矩陣，所以第一個特征值是$\lambda_1=0$，另一個特征向量可以從跡得到$tr(A)=-3$。當然我們也可以用一般方法計算$$\left\|A-\lambda I\right\|=\begin{vmatrix}-1-\lambda&2\\1&-2-\lambda\end{vmatrix}=\lambda^2+3\lambda=0$$。

    （教授提前劇透，特征值$\lambda_2=-3$將會逐漸消失，因為答案中將會有一項為$e^{-3t}$，該項會隨著時間的推移趨近於$0$。答案的另一部分將有一項為$e^{0t}$，該項是一個常數，其值為$1$，並不隨時間而改變。通常含有$0$特征值的矩陣會隨著時間的推移達到穩態。）

* 求特征向量，$\lambda_1=0$時，即求$A$的零空間，很明顯$$x_1=\begin{bmatrix}2\\1\end{bmatrix}$$；$\lambda_2=-3$時，求$A+3I$的零空間，$$\begin{bmatrix}2&2\\1&1\end{bmatrix}$$的零空間為$$x_2=\begin{bmatrix}1\\-1\end{bmatrix}$$。

* 則方程組的通解為：$u(t)=c_1e^{\lambda_1t}x_1+c_2e^{\lambda_2t}x_2$，通解的前後兩部分都是該方程組的純解，即方程組的通解就是兩個與特征值、特征向量相關的純解的線性組合。我們來驗證一下，比如取$u=e^{\lambda_1t}x_1$帶入$\frac{\mathrm{d}u}{\mathrm{d}t}=Au$，對時間求導得到$\lambda_1e^{\lambda_1t}x_1=Ae^{\lambda_1t}x_1$，化簡得$\lambda_1x_1=Ax_1$。

    對比上一講，解$$u_{k+1}=Au_k$$時得到$$u_k=c_1\lambda^kx_1+c_2\lambda^kx_2$$，而解$$\frac{\mathrm{d}u}{\mathrm{d}t}=Au$$我們得到$$u(t)=c_1e^{\lambda_1t}x_1+c_2e^{\lambda_2t}x_2$$。
    
* 繼續求$c_1,c_2$，$$u(t)=c_1\cdot 1\cdot\begin{bmatrix}2\\1\end{bmatrix}+c_2\cdot e^{-3t}\cdot\begin{bmatrix}1\\-1\end{bmatrix}$$，已知$t=0$時，$$\begin{bmatrix}1\\0\end{bmatrix}=c_1\begin{bmatrix}2\\1\end{bmatrix}+c_2\begin{bmatrix}1\\-1\end{bmatrix}$$（$Sc=u(0)$），所以$c_1=\frac{1}{3}, c_2=\frac{1}{3}$。

* 於是我們寫出最終結果，$$u(t)=\frac{1}{3}\begin{bmatrix}2\\1\end{bmatrix}+\frac{1}{3}e^{-3t}\begin{bmatrix}1\\-1\end{bmatrix}$$。

穩定性：這個流動過程從$$u(0)=\begin{bmatrix}1\\0\end{bmatrix}$$開始，初始值$1$的一部分流入初始值$0$中，經過無限的時間最終達到穩態$$u(\infty)=\begin{bmatrix}\frac{2}{3}\\\frac{1}{3}\end{bmatrix}$$。所以，要使得$u(t)\to 0$，則需要負的特征值。但如果特征值為複數呢？如$\lambda=-3+6i$，我們來計算$$\left\|e^{(-3+6i)t}\right\|$$，其中的$$\left\|e^{6it}\right\|$$部分為$\left\|\cos 6t+i\sin 6t\right\|=1$，因為這部分的模為$\cos^2\alpha+\sin^2\alpha=1$，這個虛部就在單位圓上轉悠。所以只有實數部分才是重要的。所以我們可以把前面的結論改為**需要實部為負數的特征值**。實部會決定最終結果趨近於$0$或$\infty$，虛部不過是一些小雜音。

收斂態：需要其中一個特征值實部為$0$，而其他特征值的實部皆小於$0$。

发散態：如果某個特征值實部大於$0$。上面的例子中，如果將$A$變為$-A$，特征值也會變號，結果发散。

再進一步，我們想知道如何從直接判斷任意二階矩陣的特征值是否均小於零。對於二階矩陣$$A=\begin{bmatrix}a&b\\c&d\end{bmatrix}$$，矩陣的跡為$a+d=\lambda_1+\lambda_2$，如果矩陣穩定，則跡應為負數。但是這個條件還不夠，有反例跡小於$0$依然发散：$$\begin{bmatrix}-2&0\\0&1\end{bmatrix}$$，跡為$-1$但是仍然发散。還需要加上一個條件，因為$\det A=\lambda_1\cdot\lambda_2$，所以還需要行列式為正數。

總結：原方程組有兩個相互耦合的未知函數，$u_1, u_2$相互耦合，而特征值和特征向量的作則就是解耦，也就是對角化（diagonalize）。回到原方程組$\frac{\mathrm{d}u}{\mathrm{d}t}=Au$，將$u$表示為特征向量的線性組合$u=Sv$，代入原方程有$S\frac{\mathrm{d}v}{\mathrm{d}t}=ASv$，兩邊同乘以$S^{-1}$得$\frac{\mathrm{d}v}{\mathrm{d}t}=S^{-1}ASv=\Lambda v$。以特征向量為基，將$u$表示為$Sv$，得到關於$v$的對角化方程組，新方程組不存在耦合，此時$$\begin{cases}\frac{\mathrm{d}v_1}{\mathrm{d}t}&=\lambda_1v_1\\\frac{\mathrm{d}v_2}{\mathrm{d}t}&=\lambda_2v_2\\\vdots&\vdots\\\frac{\mathrm{d}v_n}{\mathrm{d}t}&=\lambda_nv_n\end{cases}$$，這是一個各未知函數間沒有聯系的方程組，它們的解的一般形式為$v(t)=e^{\Lambda t}v(0)$，則原方程組的解的一般形式為$u(t)=e^{At}u(0)=Se^{\Lambda t}S^{-1}u(0)$。這里引入了指數部分為矩陣的形式。

## 指數矩陣$e^{At}$

在上面的結論中，我們見到了$e^{At}$。這種指數部分帶有矩陣的情況稱為指數矩陣（exponential matrix）。

理解指數矩陣的關鍵在於，將指數形式展開稱為冪基數形式，就像$e^x=1+\frac{x^2}{2}+\frac{x^3}{6}+\cdots$一樣，將$e^{At}$展開成冪級數的形式為：

$$e^{At}=I+At+\frac{(At)^2}{2}+\frac{(At)^3}{6}+\cdots+\frac{(At)^n}{n!}+\cdots$$

再說些題外話，有兩個極具美感的泰勒級數：$e^x=\sum \frac{x^n}{n!}$與$\frac{1}{1-x}=\sum x^n$，如果把第二個泰勒級數寫成指數矩陣形式，有$(I-At)^{-1}=I+At+(At)^2+(At)^3+\cdots$，這個式子在$t$非常小的時候，後面的高次項近似等於零，所以可以用來近似$I-At$的逆矩陣，通常近似為$I+At$，當然也可以再加幾項。第一個級數對我們而言比第二個級數好，因為第一個級數總會收斂於某個值，所以$e^x$總會有意義，而第二個級數需要$A$特征值的絕對值小於$1$（因為涉及矩陣的冪運算）。我們看到這些泰勒級數的公式對矩陣同樣適用。

回到正題，我們需要證明$Se^{\Lambda t}S^{-1}=e^{At}$，繼續使用泰勒級數：

$$
e^{At}=I+At+\frac{(At)^2}{2}+\frac{(At)^3}{6}+\cdots+\frac{(At)^n}{n!}+\cdots\\
e^{At}=SS^{-1}+S\Lambda S^{-1}t+\frac{S\Lambda^2S^{-1}}{2}t^2+\frac{S\Lambda^3S^{-1}}{6}t^3+\cdots+\frac{S\Lambda^nS^{-1}}{n!}t^n+\cdots\\
e^{At}=S\left(I+\Lambda t+\frac{\Lambda^2t^2}{2}+\frac{\Lambda^3t^3}{3}+\cdots+\frac{\Lambda^nt^n}{n}+\cdots\right)S^{-1}\\
e^{At}=Se^{\Lambda t}S^{-1}
$$

需要注意的是，$e^{At}$的泰勒級數展開是恒成立的，但我們推出的版本卻需要**矩陣可對角化**這個前提條件。

最後，我們來看看什麽是$e^{\Lambda t}$，我們將$e^{At}$變為對角矩陣就是因為對角矩陣簡單、沒有耦合，$$e^{\Lambda t}=\begin{bmatrix}e^{\lambda_1t}&0&\cdots&0\\0&e^{\lambda_2t}&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&e^{\lambda_nt}\end{bmatrix}$$。

有了$u(t)=Se^{\Lambda t}S^{-1}u(0)$，再來看矩陣的穩定性可知，所有特征值的實部均為負數時矩陣收斂，此時對角線上的指數收斂為$0$。如果我們畫出覆平面，則要使微分方程存在穩定解，則特征值存在於覆平面的左側（即實部為負）；要使矩陣的冪收斂於$0$，則特征值存在於單位圓內部（即模小於$1$），這是冪穩定區域。（上一講的差分方程需要計算矩陣的冪。）

同差分方程一樣，我們來看二階情況如何計算，有$y''+by'+k=0$。我們也模仿差分方程的情形，構造方程組$$\begin{cases}y''&=-by'-ky\\y'&=y'\end{cases}$$，寫成矩陣形式有$$\begin{bmatrix}y''\\y'\end{bmatrix}=\begin{bmatrix}-b&-k\\1&0\end{bmatrix}\begin{bmatrix}y'\\y\end{bmatrix}$$，令$$u'=\begin{bmatrix}y''\\y'\end{bmatrix}, \ u=\begin{bmatrix}y'\\y\end{bmatrix}$$。

繼續推廣，對於$5$階微分方程$y'''''+by''''+cy'''+dy''+ey'+f=0$，則可以寫作$$\begin{bmatrix}y'''''\\y''''\\y'''\\y''\\y'\end{bmatrix}=\begin{bmatrix}-b&-c&-d&-e&-f\\1&0&0&0&0\\0&1&0&0&0\\0&0&1&0&0\\0&0&0&1&0\end{bmatrix}\begin{bmatrix}y''''\\y'''\\y''\\y'\\y\end{bmatrix}$$，這樣我們就把一個五階微分方程化為$5\times 5$一階方程組了，然後就是求特征值、特征向量的步驟了。
