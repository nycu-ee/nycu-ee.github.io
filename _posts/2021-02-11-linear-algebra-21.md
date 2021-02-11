---
layout: post
title: 線性代數筆記-21
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=22&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第二十一講：特征值和特征向量

## 特征值、特征向量的由來

給定矩陣$A$，矩陣$A$乘以向量$x$，就像是使用矩陣$A$作用在向量$x$上，最後得到新的向量$Ax$。在這里，矩陣$A$就像是一個函數，接受一個向量$x$作為輸入，給出向量$Ax$作為輸出。

在這一過程中，我們對一些特殊的向量很感興趣，他們在輸入($x$)輸出($Ax$)的過程中始終保持同一個方向，這是比較特殊的，因為在大多情況下，$Ax$與$x$指向不同的方向。在這種特殊的情況下，$Ax$平行於$x$，我們把滿足這個條件的$x$成為特征向量（Eigen vector）。這個平行條件用方程表示就是：

$$Ax=\lambda x\tag{1}$$

* 對這個式子，我們試著計算特征值為$0$的特征向量，此時有$Ax=0$，也就是特征值為$0$的特征向量應該位於$A$的零空間中。
  
    也就是說，如果矩陣是奇異的，那麽它將有一個特征值為$\lambda = 0$。

* 我們再來看投影矩陣$P=A(A^TA)^{-1}A^T$的特征值和特征向量。用向量$b$乘以投影矩陣$P$得到投影向量$Pb$，在這個過程中，只有當$b$已經處於投影平面（即$A$的列空間）中時，$Pb$與$b$才是同向的，此時$b$投影前後不變（$Pb=1\cdot b$）。
  
    即在投影平面中的所有向量都是投影矩陣的特征向量，而他們的特征值均為$1$。
    
    再來觀察投影平面的法向量，也就是投影一講中的$e$向量。我們知道對於投影，因為$e\bot C(A)$，所以$Pe=0e$，即特征向量$e$的特征值為$0$。
    
    於是，投影矩陣的特征值為$\lambda=1, 0$。

* 再多講一個例子，二階置換矩陣$$A=\begin{bmatrix}0&1\\1&0\end{bmatrix}$$，經過這個矩陣處理的向量，其元素會互相交換。
  
    那麽特征值為$1$的特征向量（即經過矩陣交換元素前後仍然不變）應該型為$$\begin{bmatrix}1\\1\end{bmatrix}$$。
    
    特征值為$-1$的特征向量（即經過矩陣交換元素前後方向相反）應該型為$$\begin{bmatrix}1\\-1\end{bmatrix}$$。

再提前透露一個特征值的性質：對於一個$n\times n$的矩陣，將會有$n$個特征值，而這些特征值的和與該矩陣對角線元素的和相同，因此我們把矩陣對角線元素稱為矩陣的跡（trace）。$$\sum_{i=1}^n \lambda_i=\sum_{i=1}^n a_{ii}$$

在上面二階轉置矩陣的例子中，如果我們求得了一個特征值$1$，那麽利用跡的性質，我們就可以直接推出另一個特征值是$-1$。

## 求解$Ax=\lambda x$

對於方程$Ax=\lambda x$，有兩個未知數，我們需要利用一些技巧從這一個方程中一次解出兩個未知數，先移項得$(A-\lambda I)x=0$。

觀察$(A-\lambda I)x=0$，右邊的矩陣相當於將$A$矩陣平移了$\lambda$個單位，而如果方程有解，則這個平移後的矩陣$(A-\lambda I)$一定是奇異矩陣。根據前面學到的行列式的性質，則有$$\det{(A-\lambda{I})}=0\tag{2}$$

這樣一來，方程中就沒有$x$了，這個方程也叫作特征方程（characteristic equation）。有了特征值，代回$(A-\lambda I)x=0$，繼續求$(A-\lambda I)$的零空間即可。

* 現在計算一個簡單的例子，$$A=\begin{bmatrix}3&1\\1&3\end{bmatrix}$$，再來說一點題外話，這是一個對稱矩陣，我們將得到實特征值，前面還有置換矩陣、投影矩陣，矩陣越特殊，則我們得到的特征值與特征向量也越特殊。看置換矩陣中的特征值，兩個實數$1, -1$，而且它們的特征向量是正交的。

    回到例題，計算$$\det{(A-\lambda{I})}=\begin{vmatrix}3-\lambda&1\\1&3-\lambda\end{vmatrix}$$，也就是對角矩陣平移再取行列式。原式繼續化簡得$(3-\lambda)^2-1=\lambda^2-6\lambda+8=0, \lambda_1=4,\lambda_2=2$。可以看到一次項系數$-6$與矩陣的跡有關，常數項與矩陣的行列式有關。

    繼續計算特征向量，$$A-4I=\begin{bmatrix}-1&1\\1&-1\end{bmatrix}$$，顯然矩陣是奇異的（如果是非奇異說明特征值計算有誤），解出矩陣的零空間$$x_1=\begin{bmatrix}1\\1\end{bmatrix}$$；同理計算另一個特征向量，$$A-2I=\begin{bmatrix}1&1\\1&1\end{bmatrix}$$，解出矩陣的零空間$$x_2=\begin{bmatrix}1\\-1\end{bmatrix}$$。

    回顧前面轉置矩陣的例子，對矩陣$$A'=\begin{bmatrix}0&1\\1&0\end{bmatrix}$$有$$\lambda_1=1, x_1=\begin{bmatrix}1\\1\end{bmatrix}, \lambda_2=-1, x_2=\begin{bmatrix}-1\\1\end{bmatrix}$$。看轉置矩陣$A'$與本例中的對稱矩陣$A$有什麽聯系。

    易得$A=A'+3I$，兩個矩陣特征值相同，而其特征值剛好相差$3$。也就是如果給一個矩陣加上$3I$，則它的特征值會加$3$，而特征向量不變。這也很容易證明，如果$Ax=\lambda x$，則$(A+3I)x=\lambda x+3x=(\lambda+3)x$，所以$x$還是原來的$x$，而$\lambda$變為$\lambda+3$。

接下來，看一個關於特征向量認識的誤區：已知$Ax=\lambda x, Bx=\alpha x$，則有$(A+B)x=(\lambda+\alpha)x$，當$B=3I$時，在上例中我們看到，確實成立，但是如果$B$為任意矩陣，則推論**不成立**，因為這兩個式子中的特征向量$x$並不一定相同，所以兩個式子的通常情況是$Ax=\lambda x, By=\alpha y$，它們也就無從相加了。

* 再來看旋轉矩陣的例子，旋轉$90^\circ$的矩陣$$Q=\begin{bmatrix}\cos 90&-\sin 90\\\sin 90&\cos 90\end{bmatrix}=\begin{bmatrix}0&-1\\1&0\end{bmatrix}$$（將每個向量旋轉$90^\circ$，用$Q$表示因為旋轉矩陣是正交矩陣中很重要的例子）。

    上面提到特征值的一個性質：特征值之和等於矩陣的跡；現在有另一個性質：特征值之積等於矩陣的行列式。$$\prod_{i=1}^n\lambda_i=\det A$$
    
    對於$Q$矩陣，有$$\begin{cases}\lambda_1+\lambda_2&=0\\\lambda_1\cdot\lambda_2&=1\end{cases}$$，再來思考特征值與特征向量的由來，哪些向量旋轉$90^\circ$後與自己平行，於是遇到了麻煩，並沒有這種向量，也沒有這樣的特征值來滿足前面的方程組。
    
    我們來按部就班的計算，$$\det(Q-\lambda I)=\begin{vmatrix}\lambda&-1\\1&\lambda\end{vmatrix}=\lambda^2+1=0$$，於是特征值為$\lambda_1=i, \lambda_2=-i$，我們看到這兩個值滿足跡與行列式的方程組，即使矩陣全是實數，其特征值也可能不是實數。本例中即出現了一對共軛負數，我們可以說，如果矩陣越接近對稱，那麽特征值就是實數。如果矩陣越不對稱，就像本例，$Q^T=-Q$，這是一個反對稱的矩陣，於是我得到了純虛的特征值，這是極端情況，通常我們見到的矩陣是介於對稱與反對稱之間的。
    
    於是我們看到，對於好的矩陣（置換矩陣）有實特征值及正交的特征向量，對於不好的矩陣（$90^\circ$旋轉矩陣）有純虛的特征值。
    
* 再來看一個更糟的情況，$$A=\begin{bmatrix}3&1\\0&3\end{bmatrix}$$，這是一個三角矩陣，我們可以直接得出其特征值，即對角線元素。來看如何得到這一結論的：$$\det(A-\lambda I)=\begin{vmatrix}3-\lambda&1\\0&3-\lambda\end{vmatrix}=(3-\lambda)^2=0$$，於是$\lambda_1=3, \lambda_2=3$。而我們說這是一個糟糕的狀況，在於它的特征向量。

    帶入特征值計算特征向量，帶入$\lambda_1=3$得$$(A-\lambda I)x=\begin{bmatrix}0&1\\0&0\end{bmatrix}\begin{bmatrix}x_1\\x_2\end{bmatrix}=\begin{bmatrix}0\\0\end{bmatrix}$$，算出一個特征值$$x_1=\begin{bmatrix}1\\0\end{bmatrix}$$，當我們帶入第二個特征值$\lambda_1=3$時，我們無法得到另一個與$x_1$線性無關的特征向量了。
    
    而本例中的矩陣$A$是一個退化矩陣（degenerate matrix），重覆的特征值在特殊情況下可能導致特征向量的短缺。
    

這一講我們看到了足夠多的“不好”的矩陣，下一講會介紹一般情況下的特征值與特征向量。
