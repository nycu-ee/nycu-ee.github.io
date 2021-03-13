---
layout: post
title: 線性代數筆記-24
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=25&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第二十四講：馬爾科夫矩陣、傅里葉級數

## 馬爾科夫矩陣

馬爾科夫矩陣（Markov matrix）是指具有以下兩個特性的矩陣：

1. 矩陣中的所有元素**大於等於**$0$；（因為馬爾科夫矩陣與概率有關，而概率是非負的。）
2. 每一行的元素之和為$1$

對於馬爾科夫矩陣，我們關心冪運算過程中的穩態（steady state）。與上一講不同，指數矩陣關系特征值是否為$0$，而冪運算要達到穩態需要特征值為$1$。

根據上面兩條性質，我們可以得出兩個推論：

1. 馬爾科夫矩陣必有特征值為$1$；
2. 其他的特征值的絕對值皆小於$1$。

使用第二十二講中得到的公式進行冪運算$u_k=A^ku_0=S\Lambda^kS^{-1}u_0=S\Lambda^kS^{-1}Sc=S\Lambda^kc=c_1\lambda_1^kx_1+c_2\lambda_2^kx_2+\cdots+c_n\lambda_n^kx_n$，從這個公式很容易看出冪運算的穩態。比如我們取$\lambda_1=1$，其他的特征值絕對值均小於$1$，於是在經過$k$次叠代，隨著時間的推移，其他項都趨近於$0$，於是在$k\to\infty$時，有穩態$u_k=c_1x_1$，這也就是初始條件$u_0$的第$1$個分量。

我們來證明第一個推論，取$$A=\begin{bmatrix}0.1&0.01&0.3\\0.2&0.99&0.3\\0.7&0&0.4\end{bmatrix}$$，則$$A-I=\begin{bmatrix}-0.9&0.01&0.3\\0.2&-0.01&0.3\\0.7&0&-0.6\end{bmatrix}$$。觀察$A-I$易知其行向量中元素之和均為$0$，因為馬爾科夫矩陣的性質就是各行向量元素之和為$1$，現在我們從每一行中減去了$1$，所以這是很自然的結果。而如果行向量中元素和為$0$，則矩陣的任意列都可以用“零減去其他列之和”表示出來，即該矩陣的列向量線性相關。

用以前學過的子空間的知識描述，當$n$階方陣各列向量元素之和皆為$1$時，則有$$\begin{bmatrix}1\\1\\\vdots\\1\end{bmatrix}$$在矩陣$A-I$左零空間中，即$(A-I)^T$行向量線性相關。而$A$特征值$1$所對應的特征向量將在$A-I$的零空間中，因為$Ax=x\rightarrow(A-I)x=0$。

另外，特征值具有這樣一個性質：矩陣與其轉置的特征值相同。因為我們在行列式一講了解了性質10，矩陣與其轉置的行列式相同，那麽如果$\det(A-\lambda I)=0$，則有$\det(A-\lambda I)^T=0$，根據矩陣轉置的性質有$\det(A^T-\lambda I^T)=0$，即$\det(A^T-\lambda I)=0$。這正是$A^T$特征值的計算式。

然後計算特征值$\lambda_1=1$所對應的特征向量，$(A-I)x_1=0$，得出$$x_1=\begin{bmatrix}0.6\\33\\0.7\end{bmatrix}$$，特征向量中的元素皆為正。

接下來介紹馬爾科夫矩陣的應用，我們用麻省和加州這兩個州的人口遷移為例：

$$\begin{bmatrix}u_{cal}\\u_{mass}\end{bmatrix}_{k+1}\begin{bmatrix}0.9&0.2\\0.1&0.8\end{bmatrix}\begin{bmatrix}u_{cal}\\u_{mass}\end{bmatrix}_k$$，元素非負，行和為一。這個式子表示每年有$10%$的人口從加州遷往麻省，同時有$20%$的人口從麻省遷往加州。注意使用馬爾科夫矩陣的前提條件是隨著時間的推移，矩陣始終不變。

設初始情況$$\begin{bmatrix}u_{cal}\\u_{mass}\end{bmatrix}_0=\begin{bmatrix}0\\1000\end{bmatrix}$$，我們先來看第一次遷徙後人口的變化情況：$$\begin{bmatrix}u_{cal}\\u_{mass}\end{bmatrix}_1=\begin{bmatrix}0.9&0.2\\0.1&0.8\end{bmatrix}\begin{bmatrix}0\\1000\end{bmatrix}=\begin{bmatrix}200\\800\end{bmatrix}$$，隨著時間的推移，會有越來越多的麻省人遷往加州，而同時又會有部分加州人遷往麻省。

計算特征值：我們知道馬爾科夫矩陣的一個特征值為$\lambda_1=1$，則另一個特征值可以直接從跡算出$\lambda_2=0.7$。

計算特征向量：帶入$\lambda_1=1$求$A-I$的零空間有$$\begin{bmatrix}-0.1&0.2\\0.1&-0.2\end{bmatrix}$$，則$$x_1=\begin{bmatrix}2\\1\end{bmatrix}$$，此時我們已經可以得出無窮步後穩態下的結果了。$$u_{\infty}=c_1\begin{bmatrix}2\\1\end{bmatrix}$$且人口總數始終為$1000$，則$c_1=\frac{1000}{3}$，穩態時$$\begin{bmatrix}u_{cal}\\u_{mass}\end{bmatrix}_{\infty}=\begin{bmatrix}\frac{2000}{3}\\\frac{1000}{3}\end{bmatrix}$$。注意到特征值為$1$的特征向量元素皆為正。

為了求每一步的結果，我們必須解出所有特征向量。帶入$\lambda_2=0.7$求$A-0.7I$的零空間有$$\begin{bmatrix}0.2&0.2\\0.1&0.1\end{bmatrix}$$，則$$x_2=\begin{bmatrix}-1\\1\end{bmatrix}$$。

通過$u_0$解出$c_1, c_2$，$$u_k=c_11^k\begin{bmatrix}2\\1\end{bmatrix}+c_20.7^k\begin{bmatrix}-1\\1\end{bmatrix}$$，帶入$k=0$得$$u_0=\begin{bmatrix}0\\1000\end{bmatrix}=c_1\begin{bmatrix}2\\1\end{bmatrix}+c_2\begin{bmatrix}-1\\1\end{bmatrix}$$，解出$c_1=\frac{1000}{3}, c_2=\frac{2000}{3}$。

另外，有時人們更喜歡用列向量，此時將要使用列向量乘以矩陣，其行向量各分量之和為$1$。

## 傅里葉級數

在介紹傅里葉級數（Fourier series）之前，先來回顧一下投影。

設$q_1,q_2,\cdots q_n$為一組標準正交基，則向量$v$在該標準正交基上的展開為$v=x_1q_1+x_2q_2+\cdots+x_nq_n$，此時我們想要得到各系數$x_i$的值。比如求$x_1$的值，我們自然想要消掉除$x_1q_1$外的其他項，這時只需要等式兩邊同乘以$q_1^T$，因為的$q_i$向量相互正交且長度為$1$，則$q_i^Tq_j=0, q_i^2=1$所以原式變為$q_1^Tv=x_1$。

寫為矩陣形式有$$\Bigg[q_1\ q_2\ \cdots\ q_n\Bigg]\begin{bmatrix}x_1\\x_2\\\vdots\\x_n\end{bmatrix}=v$$，即$Qx=v$。所以有$x=Q^{-1}v$，而在第十七講我們了解到標準正交基有$Q^T=Q^{-1}$，所以我們不需要計算逆矩陣可直接得出$x=Q^Tv$。此時對於$x$的每一個分量有$x_i=q_i^Tv$。

接下來介紹傅里葉級數。先寫出傅里葉級數的展開式：

$$
f(x)=a_0+a_1\cos x+b_1\sin x+a_2\cos 2x+b_2\sin 2x+\cdots
$$

傅里葉发現，如同將向量$v$展開（投影）到向量空間的一組標準正交基中，在函數空間中，我們也可以做類似的展開。將函數$f(x)$投影在一系列相互正交的函數中。函數空間中的$f(x)$就是向量空間中的$v$；函數空間中的$1,\cos x,\sin x,\cos 2x,\sin 2x,\cdots$就是向量空間中的$q_1,q_2,\cdots,q_n$；不同的是，函數空間是無限維的而我們以前接觸到的向量空間通常是有限維的。

再來介紹何為“函數正交”。對於向量正交我們通常使用兩向量內積（點乘）為零判斷。我們知道對於向量$v,w$的內積為$v^Tw=v_1w_1+v_2w_2+\cdots+v_nw_n=0$，也就是向量的每個分量之積再求和。而對於函數$f(x)\cdot g(x)$內積，同樣的，我們需要計算兩個函數的每個值之積而後求和，由於函數取值是連續的，所以函數內積為：

$$f^Tg=\int f(x)g(x)\mathrm{d}x$$

在本例中，由於傅里葉級數使用正余弦函數，它們的周期都可以算作$2\pi$，所以本例的函數點積可以寫作$f^Tg=\int_0^{2\pi}f(x)g(x)\mathrm{d}x$。我來檢驗一個內積$\int_0^{2\pi}\sin{x}\cos{x}\mathrm{d}x=\left.\frac{1}{2}\sin^2x\right\|_0^{2\pi}=0$，其余的三角函數族正交性結果可以參考[傅里葉級數](https://zh.wikipedia.org/wiki/%E5%82%85%E9%87%8C%E5%8F%B6%E7%BA%A7%E6%95%B0)的“希爾伯特空間的解讀”一節。

最後我們來看$\cos x$項的系數是多少（$a_0$是$f(x)$的平均值）。同向量空間中的情形一樣，我們在等式兩邊同時做$\cos x$的內積，原式變為$\int_0^{2\pi}f(x)\cos x\mathrm{d}x=a_1\int_0^{2\pi}\cos^2x\mathrm{d}x$，因為正交性等式右邊僅有$\cos x$項不為零。進一步化簡得$a_1\pi=\int_0^{2\pi}f(x)\cos x\mathrm{d}x\rightarrow a_1=\frac{1}{\pi}\int_0^{2\pi}f(x)\cos x\mathrm{d}x$。

於是，我們把函數$f(x)$展開到了函數空間的一組標準正交基上。
