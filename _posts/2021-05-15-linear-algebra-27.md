---
layout: post
title: 線性代數筆記-27
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=28&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第二十七講：複數矩陣和快速傅里葉變換

本講主要介紹複數向量、複數矩陣的相關知識（包括如何做複數向量的點積運算、什麽是複數對稱矩陣等），以及傅里葉矩陣（最重要的複數矩陣）和快速傅里葉變換。

## 複數矩陣運算

先介紹複數向量，我們不妨換一個字母符號來表示：$$z=\begin{bmatrix}z_1\\z_2\\\vdots\\z_n\end{bmatrix}$$，向量的每一個分量都是複數。此時$$z$$不再屬於$$\mathbb{R}^n$$實向量空間，它現在處於$$\mathbb{C}^n$$複向量空間。

### 計算複向量的模

對比實向量，我們計算模只需要計算$$\left\|v\right\|=\sqrt{v^Tv}$$即可，而如果對複向量使用$$z^Tz$$則有$$z^Tz=\begin{bmatrix}z_1&z_2&\cdots&z_n\end{bmatrix}\begin{bmatrix}z_1\\z_2\\\vdots\\z_n\end{bmatrix}=z_1^2+z_2^2+\cdots+z_n^2$$，這里$$z_i$$是複數，平方後虛部為負，求模時本應相加的運算變成了減法。（如向量$$\begin{bmatrix}1&i\end{bmatrix}$$，右乘其轉置後結果為$$0$$，但此向量的長度顯然不是零。）

根據上一講我們知道，應使用$$\left\|z\right\|=\sqrt{\bar{z}^Tz}$$，即$$\begin{bmatrix}\bar z_1&\bar z_2&\cdots&\bar z_n\end{bmatrix}\begin{bmatrix}z_1\\z_2\\\vdots\\z_n\end{bmatrix}$$，即使用向量共軛的轉置乘以原向量即可。（如向量$$\begin{bmatrix}1&i\end{bmatrix}$$，右乘其共軛轉置後結果為$$\begin{bmatrix}1&-i\end{bmatrix}\begin{bmatrix}1\\i\end{bmatrix}=2$$。）

我們把共軛轉置乘以原向量記為$$z^Hz$$，$$H$$讀作埃爾米特（人名為Hermite，形容詞為Hermitian）

### 計算向量的內積

有了複向量模的計算公式，同理可得，對於複向量，內積不再是實向量的$$y^Tx$$形式，複向量內積應為$$y^Hx$$。

### 對稱性

對於實矩陣，$$A^T=A$$即可表達矩陣的對稱性。而對於複矩陣，我們同樣需要求一次共軛$$\bar{A}^T=A$$。舉個例子$$\begin{bmatrix}2&3+i\\3-i&5\end{bmatrix}$$是一個複數情況下的對稱矩陣。這叫做埃爾米特矩陣，有性質$$A^H=A$$。

### 正交性

在第十七講中，我們這樣定義標準正交向量：$$q_i^Tq_j=\begin{cases}0\quad i\neq j\\1\quad i=j\end{cases}$$。現在，對於複向量我們需要求共軛：$$\bar{q}_i^Tq_j=q_i^Hq_j=\begin{cases}0\quad i\neq j\\1\quad i=j\end{cases}$$。

第十七講中的標準正交矩陣：$$Q=\Bigg[q_1\ q_2\ \cdots\ q_n\Bigg]$$有$$Q^TQ=I$$。現在對於複矩陣則有$$Q^HQ=I$$。

就像人們給共軛轉置起了個“埃爾米特”這個名字一樣，正交性（orthogonal）在複數情況下也有了新名字，酉（unitary），酉矩陣（unitary matrix）與正交矩陣類似，滿足$$Q^HQ=I$$的性質。而前面提到的傅里葉矩陣就是一個酉矩陣。

## 傅里葉矩陣

$$n$$階傅里葉矩陣$$F_n=\begin{bmatrix}1&1&1&\cdots&1\\1&w&w^2&\cdots&w^{n-1}\\1&w^2&w^4&\cdots&w^{2(n-1)}\\\vdots&\vdots&\vdots&\ddots&\vdots\\1&w^{n-1}&w^{2(n-1)}&\cdots&w^{(n-1)^2}\end{bmatrix}$$，對於每一個元素有$$(F_n)_{ij}=w^{ij}\quad i,j=0,1,2,\cdots,n-1$$。矩陣中的$$w$$是一個非常特殊的值，滿足$$w^n=1$$，其公式為$$w=e^{i2\pi/n}$$。易知$$w$$在複平面的單位圓上，$$w=\cos\frac{2\pi}{n}+i\sin\frac{2\pi}{n}$$。

在傅里葉矩陣中，當我們計算$$w$$的冪時，$$w$$在單位圓上的角度翻倍。比如在$$6$$階情形下，$$w=e^{2\pi/6}$$，即位於單位圓上$$60^\circ$$角處，其平方位於單位圓上$$120^\circ$$角處，而$$w^6$$位於$$1$$處。從開方的角度看，它們是$$1$$的$$$6$$個六次方根，而一次的$$w$$稱為原根。

* 我們現在來看$$4$$階傅里葉矩陣，先計算$$w$$有$$w=i,\ w^2=-1,\ w^3=-i,\ w^4=1$，$F_4=\begin{bmatrix}1&1&1&1\\1&i&i^2&i^3\\1&i^2&i^4&i^6\\1&i^3&i^6&i^9\end{bmatrix}=\begin{bmatrix}1&1&1&1\\1&i&-1&-i\\1&-1&1&-1\\1&-i&-1&i\end{bmatrix}$$。

    矩陣的四個行向量正交，我們驗證一下第二行和第四行，$$\bar{c_2}^Tc_4=1-0+1-0=0$$，正交。不過我們應該注意到，$$F_4$$的行向量並不是標準的，我們可以給矩陣乘上係數$$\frac{1}{2}$$（除以行向量的長度）得到標準正交矩陣$$F_4=\frac{1}{2}\begin{bmatrix}1&1&1&1\\1&i&-1&-i\\1&-1&1&-1\\1&-i&-1&i\end{bmatrix}$$。此時有$$F_4^HF_4=I$$，於是該矩陣的逆矩陣也就是其共軛轉置$$F_4^H$$。
    
## 快速傅里葉變換（Fast Fourier transform/FFT）

對於傅里葉矩陣，$$F_6,\ F_3$、$F_8,\ F_4$、$F_{64},\ F_{32}$$之間有著特殊的關系。

舉例，有傅里葉矩陣$$F_64$$，一般情況下，用一個行向量右乘$$F_{64}$$需要約$$64^2$$次計算，顯然這個計算量是比較大的。我們想要減少計算量，於是想要分解$$F_{64}$$，聯系到$$F_{32}$$，有$$\Bigg[F_{64}\Bigg]=\begin{bmatrix}I&D\\I&-D\end{bmatrix}\begin{bmatrix}F_{32}&0\\0&F_{32}\end{bmatrix}\begin{bmatrix}1&&\cdots&&&0&&\cdots&&\\0&&\cdots&&&1&&\cdots&&\\&1&\cdots&&&&0&\cdots&&\\&0&\cdots&&&&1&\cdots&&\\&&&\ddots&&&&&\ddots&&\\&&&\ddots&&&&&\ddots&&\\&&&\cdots&1&&&&\cdots&0\\&&&\cdots&0&&&&\cdots&1\end{bmatrix}$$。

我們分開來看等式右側的這三個矩陣：

* 第一個矩陣由單位矩陣$$I$$和對角矩陣$$D=\begin{bmatrix}1&&&&\\&w&&&\\&&w^2&&\\&&&\ddots&\\&&&&w^{31}\end{bmatrix}$$組成，我們稱這個矩陣為修正矩陣，顯然其計算量來自$$D$$矩陣，對角矩陣的計算量約為$$32$$即這個修正矩陣的計算量約為$$32$$，單位矩陣的計算量忽略不計。

* 第二個矩陣是兩個$$F_{32}$$與零矩陣組成的，計算量約為$$2\times 32^2$$。

* 第三個矩陣通常記為$$P$$矩陣，這是一個置換矩陣，其作用是講前一個矩陣中的奇數行提到偶數行之前，將前一個矩陣從$$\Bigg[x_0\ x_1\ \cdots\Bigg]$變為$\Bigg[x_0\ x_2\ \cdots\ x_1\ x_3\ \cdots\Bigg]$$，這個置換矩陣的計算量也可以忽略不計。（這里教授似乎在黑板上寫錯了矩陣，可以參考[FFT](https://math.berkeley.edu/~berlek/classes/CLASS.110/LECTURES/FFT)、[How the FFT is computed](http://vmm.math.uci.edu/ODEandCM/PDF_Files/FFT_Appendix_K.pdf)做進一步討論。）

所以我們把$$64^2$$複雜度的計算化簡為$$2\times 32^2+32$$複雜度的計算，我們可以進一步化簡$$F_{32}$得到與$F_{16}$有關的式子$\begin{bmatrix}I_{32}&D_{32}\\I_{32}&-D_{32}\end{bmatrix}\begin{bmatrix}I_{16}&D_{16}&&\\I_{16}&-D_{16}&&\\&&I_{16}&D_{16}\\&&I_{16}&-D_{16}\end{bmatrix}\begin{bmatrix}F_{16}&&&\\&F_{16}&&\\&&F_{16}&\\&&&F_{16}\end{bmatrix}\begin{bmatrix}P_{16}&\\&P_{16}\end{bmatrix}\Bigg[\ P_{32}\ \Bigg]$$。而$$32^2$$的計算量進一步分解為$$2\times 16^2+16$$的計算量，如此遞歸下去我們最終得到含有一階傅里葉矩陣的式子。

來看化簡後計算量，$$2\left(2\left(2\left(2\left(2\left(2\left(1\right)^2+1\right)+2\right)+4\right)+8\right)+16\right)+32$，約為$6\times 32=\log_264\times \frac{64}{2}$$，算法複雜度為$$\frac{n}{2}\log_2n$$。

於是原來需要$$n^2$$的運算現在只需要$$\frac{n}{2}\log_2n$$就可以實現了。不妨看看$$n=10$$的情況，不使用FFT時需要$$n^2=1024\times 1024$$次運算，使用FFT時只需要$$\frac{n}{2}\log_2n=5\times 1024$$次運算，運算量大約是原來的$$\frac{1}{200}$$。

下一講將繼續介紹特征值、特征向量及正定矩陣。
