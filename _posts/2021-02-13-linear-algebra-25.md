---
layout: post
title: 線性代數筆記-25
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=26&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第二十五講：複習二

* 我們學習了正交性，有矩陣$Q=\Bigg[q_1\ q_2\ \cdots\ q_n\Bigg]$，若其行向量相互正交，則該矩陣滿足$Q^TQ=I$。
* 進一步研究投影，我們了解了Gram-Schmidt正交化法，核心思想是求法向量，即從原向量中減去投影向量$E=b-P, P=Ax=\frac{A^Tb}{A^TA}\cdot A$。
* 接著學習了行列式，根據行列式的前三條性質，我們拓展出了性質4-10。
* 我們繼續推導出了一個利用代數余子式求行列式的公式。
* 又利用代數余子式推導出了一個求逆矩陣的公式。
* 接下來我們學習了特征值與特征向量的意義：$Ax=\lambda x$，進而了解了通過$\det(A-\lambda I)=0$求特征值、特征向量的方法。
* 有了特征值與特征向量，我們掌握了通過公式$AS=\Lambda S$對角化矩陣，同時掌握了求矩陣的冪$A^k=S\Lambda^kS^{-1}$。

微分方程不在本講的範圍內。下面通過往年例題複習上面的知識。

1. *求$$a=\begin{bmatrix}2\\1\\2\end{bmatrix}$$的投影矩陣$P$*：$\Bigg($由$a\bot(b-p)\rightarrow A^T(b-A\hat x)=0$得到$\hat x=\left(A^TA\right)^{-1}A^Tb$，求得$p=A\hat x=A\left(A^TA\right)^{-1}A^Tb=Pb$最終得到$$P\Bigg)$$ $$\underline{P=A\left(A^TA\right)^{-1}A^T}\stackrel{a}=\frac{aa^T}{a^Ta}=\frac{1}{9}\begin{bmatrix}4&2&4\\2&1&2\\4&2&4\end{bmatrix}$$。
   
    *求$P$矩陣的特征值*：觀察矩陣易知矩陣奇異，且為秩一矩陣，則其零空間為$2$維，所以由$Px=0x$得出矩陣的兩個特征向量為$\lambda_1=\lambda_2=0$；而從矩陣的跡得知$trace(P)=1=\lambda_1+\lambda_2+\lambda_3=0+0+1$，則第三個特征向量為$\lambda_3=1$。
    
    *求$\lambda_3=1$的特征向量*：由$Px=x$我們知道經其意義為，$x$過矩陣$P$變換後不變，又有$P$是向量$a$的投影矩陣，所以任何向量經過$P$變換都會落在$a$的行空間中，則只有已經在$a$的行空間中的向量經過$P$的變換後保持不變，即其特征向量為$$x=a=\begin{bmatrix}2\\1\\2\end{bmatrix}$$，也就是$Pa=a$。
    
    *有差分方程$$u_{k+1}=Pu_k,\ u_0=\begin{bmatrix}9\\9\\0\end{bmatrix}$$，求解$u_k$*：我們先不急於解出特征值、特征向量，因為矩陣很特殊（投影矩陣）。首先觀察$u_1=Pu_0$，式子相當於將$u_0$投影在了$a$的行空間中，計算得$$u_1=a\frac{a^Tu_0}{a^Ta}=3a=\begin{bmatrix}6\\3\\6\end{bmatrix}$$（這里的$3$相當於做投影時的系數$\hat x$），其意義為$u_1$在$a$上且距離$u_0$最近。再來看看$u_2=Pu_1$，這個式子將$u_1$再次投影到$a$的列空間中，但是此時的$u_1$已經在該列空間中了，再次投影仍不變，所以有$$u_k=P^ku_0=Pu_0=\begin{bmatrix}6\\3\\6\end{bmatrix}$$。
    
    上面的解法利用了投影矩陣的特殊性質，如果在一般情況下，我們需要使用$AS=S\Lambda\rightarrow A=S\Lambda S^{-1} \rightarrow u_{k+1}=Au_k=A^{k+1}u_0, u_0=Sc\rightarrow u_{k+1}=S\Lambda^{k+1}S^{-1}Sc=S\Lambda^{k+1}c$，最終得到公式$A^ku_0=c_1\lambda_1^kx_1+c_2\lambda_2^kx_2+\cdots+c_n\lambda_n^kx_n$。題中$P$的特殊性在於它的兩個“零特征值”及一個“一特征值”使得式子變為$A^ku_0=c_3x_3$，所以得到了上面結構特殊的解。
    
2. *將點$(1,4),\ (2,5),\ (3,8)$擬合到一條過零點的直線上*：設直線為$y=Dt$，寫成矩陣形式為$$\begin{bmatrix}1\\2\\3\end{bmatrix}D=\begin{bmatrix}4\\5\\8\end{bmatrix}$$，即$AD=b$，很明顯$D$不存在。利用公式$A^TA\hat D=A^Tb$得到$$14D=38,\ \hat D=\frac{38}{14}$$，即最佳直線為$y=\frac{38}{14}t$。這個近似的意義是將$b$投影在了$A$的行空間中。

3. *求$$a_1=\begin{bmatrix}1\\2\\3\end{bmatrix}\ a_2=\begin{bmatrix}1\\1\\1\end{bmatrix}$$的正交向量*：找到平面$A=\Bigg[a_1,a_2\Bigg]$的正交基，使用Gram-Schmidt法，以$a_1$為基準，正交化$a_2$，也就是將$a_2$中平行於$a_1$的分量去除，即$$a_2-xa_1=a_2-\frac{a_1^Ta_2}{a_1^Ta_1}a_1=\begin{bmatrix}1\\1\\1\end{bmatrix}-\frac{6}{14}\begin{bmatrix}1\\2\\3\end{bmatrix}$$。

4. *有$4\times 4$矩陣$A$，其特征值為$\lambda_1,\lambda_2,\lambda_3,\lambda_4$，則矩陣可逆的條件是什麽*：矩陣可逆，則零空間中只有零向量，即$Ax=0x$沒有非零解，則零不是矩陣的特征值。

    *$\det A^{-1}$是什麽*：$\det A^{-1}=\frac{1}{\det A}$，而$\det A=\lambda_1\lambda_2\lambda_3\lambda_4$，所以有$\det A^{-1}=\frac{1}{\lambda_1\lambda_2\lambda_3\lambda_4}$。
    
    *$trace(A+I)$的跡是什麽*：我們知道$trace(A)=a_{11}+a_{22}+a_{33}+a_{44}=\lambda_1+\lambda_2+\lambda_3+\lambda_4$，所以有$trace(A+I)=a_{11}+1+a_{22}+1+a_{33}+1+a_{44}+1=\lambda_1+\lambda_2+\lambda_3+\lambda_4+4$。
    
5. *有矩陣$$A_4=\begin{bmatrix}1&1&0&0\\1&1&1&0\\0&1&1&1\\0&0&1&1\end{bmatrix}$$，求$D_n=?D_{n-1}+?D_{n-2}$*：求遞歸式的系數，使用代數余子式將矩陣安第一行展開得$$\det A_4=1\cdot\begin{vmatrix}1&1&0\\1&1&1\\0&1&1\end{vmatrix}-1\cdot\begin{vmatrix}1&1&0\\0&1&1\\0&1&1\end{vmatrix}=1\cdot\begin{vmatrix}1&1&0\\1&1&1\\0&1&1\end{vmatrix}-1\cdot\begin{vmatrix}1&1\\1&1\end{vmatrix}=\det A_3-\det A_2$$。則可以看出有規律$D_n=D_{n-1}-D_{n-2}, D_1=1, D_2=0$。

    使用我們在差分方程中的知識構建方程組$\begin{cases}D_n&=D_{n-1}-D_{n-2}\\D_{n-1}&=D_{n-1}\end{cases}$，用矩陣表達有$$\begin{bmatrix}D_n\\D_{n-1}\end{bmatrix}=\begin{bmatrix}1&-1\\1&0\end{bmatrix}\begin{bmatrix}D_{n-1}\\D_{n-2}\end{bmatrix}$$。計算系數矩陣$A_c$的特征值，$$\begin{vmatrix}1-\lambda&1\\1&-\lambda\end{vmatrix}=\lambda^2-\lambda+1=0$$，解得$\lambda_1=\frac{1+\sqrt{3}i}{2},\lambda_2=\frac{1-\sqrt{3}i}{2}$，特征值為一對共軛複數。
    
    要判斷遞歸式是否收斂，需要計算特征值的模，即實部平方與虛部平方之和$\frac{1}{4}+\frac{3}{4}=1$。它們是位於單位圓$e^{i\theta}$上的點，即$\cos\theta+i\sin\theta$，從本例中可以計算出$\theta=60^\circ$，也就是可以將特征值寫作$\lambda_1=e^{i\pi/3},\lambda_2=e^{-i\pi/3}$。注意，從複平面單位圓上可以看出，這些特征值的六次方將等於一：$e^{2\pi i}=e^{2\pi i}=1$。繼續深入觀察這一特性對矩陣的影響，$\lambda_1^6=\lambda^6=1$，則對系數矩陣有$A_c^6=I$。則系數矩陣$A_c$服從周期變化，既不发散也不收斂。 

6. *有這樣一類矩陣$$A_4=\begin{bmatrix}0&1&0&0\\1&0&2&0\\0&2&0&3\\0&0&3&0\end{bmatrix}$$，求投影到$A_3$行空間的投影矩陣*：有$$A_3=\begin{bmatrix}0&1&0\\1&0&2\\0&2&0\end{bmatrix}$$，按照通常的方法求$P=A\left(A^TA\right)A^T$即可，但是這樣很麻煩。我們可以考察這個矩陣是否可逆，因為如果可逆的話，$\mathbb{R}^4$空間中的任何向量都會位於$A_4$的行空間，其投影不變，則投影矩陣為單位矩陣$I$。所以按行展開求行列式$\det A_4=-1\cdot-1\cdot-3\cdot-3=9$，所以矩陣可逆，則$P=I$。

    *求$A_3$的特征值及特征向量*：$\left\|A_3-\lambda I\right\|=\begin{vmatrix}-\lambda&1&0\\\\1&-\lambda&2\\\\0&2&-\lambda\end{vmatrix}=-\lambda^3+5\lambda=0$，解得$\lambda_1=0,\lambda_2=\sqrt 5,\lambda_3=-\sqrt 5$。
    
    我們可以猜測這一類矩陣的規律：奇數階奇異，偶數階可逆。
