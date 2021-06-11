---
layout: post
title: 線性代數筆記-35
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=36&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第三十五講：期末複習

依然是從以往的試題入手複習知識點。

1. *已知$$m\times n$$矩陣$$A$$，有$$Ax=\begin{bmatrix}1\\0\\0\end{bmatrix}$$無解；$$Ax=\begin{bmatrix}0\\1\\0\end{bmatrix}$$僅有唯一解，求關於$$m,n,rank(A)$$的信息。*

    首先，最容易判斷的是$$m=3$$；而根據第一個條件可知，矩陣不滿秩，有$$r<m$$；根據第二個條件可知，零空間僅有零向量，也就是矩陣消元後沒有自由變量，行向量線性無關，所以有$$r=n$$。
    
    綜上，有$$m=3>n=r$$。
    
    *根據所求寫出一個矩陣$$A$$的特例*：$$A=\begin{bmatrix}0&0\\1&0\\0&1\end{bmatrix}$$。
    
    *$$\det A^TA\stackrel{?}{=}\det AA^T$$*：不相等，因為$$A^TA$$可逆而$$AA^T$$不可逆，所以行列式不相等。（但是對於方陣，$$\det AB=\det BA$$恒成立。）
    
    *$$A^TA$$可逆嗎？*是，因為$$r=n$$，矩陣行向量線性無關，即行滿秩。
    
    *$$AA^T$$正定嗎？*否，因為$$AA^T$$是$$3\times n$$矩陣與$$n\times 3$$矩陣之積，是一個三階方陣，而$$AA^T$$秩為$$2$$，所以不是正定矩陣。（不過$$AA^T$$一定是半正定矩陣。）
    
    *求證$$A^Ty=c$$至少有一個解*：因為$$A$$的行向量線性無關，所以$$A^T$$的列向量線性無關，消元後每行都有主元，且總有自由變量，所以零空間中有非零向量，零空間維數是$$m-r$$（可以直接從$$\dim N\left(A^T\right)=m-r$$得到結論）。

2. *設$$A=\Bigg[v_1\ v_2\ v_3\Bigg]$$，對於$$Ax=v_1-v_2+v_3$$，求$$x$$。*
   
    按行計算矩陣相乘，有$$x=\begin{bmatrix}1\\-1\\1\end{bmatrix}$$。
    
    *若Ax=v_1-v_2+v_3=0，則解是唯一的嗎？為什麽。*如果解釋唯一的，則零空間中只有零向量，而在此例中$$x=\begin{bmatrix}1\\-1\\1\end{bmatrix}$$就在零空間中，所以解不唯一。
    
    *若$$v_1,v_2,v_3$$是標準正交向量，那麽怎樣的線性組合$$c_1v_1+c_2v_2$$能夠最接近$$v_3$$？*此問是考察投影概念，由於是正交向量，所以只有$$0$$向量最接近$$v_3$$。
    
3. *矩陣$$A=\begin{bmatrix}.2&.4&.3\\.4&.2&.3\\.4&.4&.4\end{bmatrix}$$，求穩態。*

    這是個馬爾科夫矩陣，前兩行之和為第三行的兩倍，奇異矩陣總有一個特征值為$$0$$，而馬爾科夫矩陣總有一個特征值為$$1$$，剩下一個特征值從矩陣的跡得知為$$-.2$$。
    
    再看馬爾科夫過程，設從$$u(0)$$開始，$$u_k=A^ku_0, u_0=\begin{bmatrix}0\\10\\0\end{bmatrix}$$。先代入特征值$$\lambda_1=0,\ \lambda_2=1,\ \lambda_3=-.2$$查看穩態$$u_k=c_1\lambda_1^kx_1+c_2\lambda_2^kx_2+c_3\lambda_3^kx_3$$，當$$k\to\infty$$，第一項與第三項都會消失，剩下$$u_\infty=c_2x_2$$。
    
    到這里我們只需求出$$\lambda_2$$對應的特征向量即可，帶入特征值求解$$(A-I)x=0$$，有$$\begin{bmatrix}-.8&.4&.3\\.4&-.8&.3\\.4&.4&-.6\end{bmatrix}\begin{bmatrix}?\\?\\?\end{bmatrix}=\begin{bmatrix}0\\0\\0\end{bmatrix}$$，可以消元得，也可以直接觀察得到$$x_2=\begin{bmatrix}3\\3\\4\end{bmatrix}$$。
    
    剩下就是求$$c_2$$了，可以通過$$u_0$$一一解出每個係數，但是這就需要解出每一個特征值。另一種方法，我們可以通過馬爾科夫矩陣的特性知道，對於馬爾科夫過程的每一個$$u_k$$都有其分量之和與初始值分量之和相等，所以對於$$x_2=\begin{bmatrix}3\\3\\4\end{bmatrix}$$，有$$c_2=1$$。所以最終結果是$$u_\infty=\begin{bmatrix}3\\3\\4\end{bmatrix}$$。

4. *對於二階方陣，回答以下問題：*
   
    *求投影在直線$$a=\begin{bmatrix}4\\-3\end{bmatrix}$$上的投影矩陣*：應為$$P=\frac{aa^T}{a^Ta}$$。
    
    *已知特征值$$\lambda_1=2,\ x_1=\begin{bmatrix}1\\2\end{bmatrix}\quad \lambda_2=3,\ x_2=\begin{bmatrix}2\\1\end{bmatrix}$$求原矩陣$$A$$*：從對角化公式得$$A=S\Lambda S^{-1}=\begin{bmatrix}1&2\\2&1\end{bmatrix}\begin{bmatrix}0&0\\0&3\end{bmatrix}\begin{bmatrix}1&2\\2&1\end{bmatrix}^{-1}$$，解之即可。
    
    *$$A$$是一個實矩陣，且對任意矩陣$$B$$，$$A$$都不能分解成$$A=B^TB$$，給出$$A$$的一個例子*：我們知道$$B^TB$$是對稱的，所以給出一個非對稱矩陣即可。
    *矩陣$$A$$有正交的特征向量，但不是對稱的，給出一個$$A$$的例子*：我們在三十三講提到過，反對稱矩陣，因為滿足$$AA^T=A^TA$$而同樣具有正交的特征向量，所以有$$A=\begin{bmatrix}0&1\\-1&0\end{bmatrix}$$或旋轉矩陣$$\begin{bmatrix}\cos\theta&-\sin\theta\\\sin\theta&\cos\theta\end{bmatrix}$$，這些矩陣都具有複數域上的正交特征向量組。
    
5. *最小二乘問題，因為時間的關係直接寫出計算式和答案，$$\begin{bmatrix}1&0\\1&1\\1&2\end{bmatrix}\begin{bmatrix}C\\D\end{bmatrix}=\begin{bmatrix}3\\4\\1\end{bmatrix}(Ax=b)$$，解得$$\begin{bmatrix}\hat C\\\hat D\end{bmatrix}=\begin{bmatrix}\frac{11}{3}\\-1\end{bmatrix}$$。*

    *求投影後的向量$$p$$*：向量$$p$$就是向量$$b$$在矩陣$$A$$行空間中的投影，所以$$p=\begin{bmatrix}p_1\\p_2\\p_3\end{bmatrix}=\begin{bmatrix}1&0\\1&1\\1&2\end{bmatrix}\begin{bmatrix}\hat C\\\hat D\end{bmatrix}$$。
    
    *求擬合直線的圖像*：$$x=0,1,2$$時$$y=p_1,p_2,p_2$$所在的直線的圖像，$$y=\hat C+\hat Dx$$即$$y=\frac{11}{3}-x$$。


```python
%matplotlib inline
import matplotlib.pyplot as plt
from sklearn import linear_model
import numpy as np
import pandas as pd
import seaborn as sns

x = np.array([0, 1, 2]).reshape((-1,1))
y = np.array([3, 4, 1]).reshape((-1,1))
predict_line = np.array([-1, 4]).reshape((-1,1))

regr = linear_model.LinearRegression()
regr.fit(x, y)
ey = regr.predict(x)

fig = plt.figure()
plt.axis('equal')
plt.axhline(y=0, c='black')
plt.axvline(x=0, c='black')

plt.scatter(x, y, c='r')
plt.scatter(x, regr.predict(x), s=20, c='b')
plt.plot(predict_line, regr.predict(predict_line), c='g', lw='1')
[ plt.plot([x[i], x[i]], [y[i], ey[i]], 'r', lw='1') for i in range(len(x))]

plt.draw()
```


![png](/public/img/linear-algebra-31/output_1_0.png)



```python
plt.close(fig)
```

* 接上面的題目

    *求一個向量$$b$$使得最小二乘求得的$$\begin{bmatrix}\hat C\\\hat D\end{bmatrix}=\begin{bmatrix}0\\0\end{bmatrix}$$*：我們知道最小二乘求出的向量$$\begin{bmatrix}\hat C\\\hat D\end{bmatrix}$$使得$$A$$行向量的線性組合最接近$$b$$向量（即$$b$$在$$A$$行空間中的投影），如果這個線性組合為$$0$$向量（即投影為$$0$$），則$$b$$向量與$$A$$的行空間正交，所以可以取$$b=\begin{bmatrix}1\\-2\\1\end{bmatrix}$$同時正交於$$A$$的兩個行向量。

# MIT線性代數的全部課程到此結束