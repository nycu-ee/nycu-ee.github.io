---
layout: post
title: 線性代數筆記-32
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=33&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第三十二講：基變換和圖像壓縮

## 圖像壓縮

本講我們介紹一種圖片有損壓縮的一種方法：JPEG。

假設我們有一張圖片，長寬皆為$$512$$個像素，我們用$$x_i$$來表示第$$i$$個像素，如果是灰度照片，通常$$x_i$$可以在$$[0,255]$$上取值，也就是8 bits。對於這承載這張圖片信息的向量$$x$$來說，有$$x\in\mathbb{R}^n, n=512^2$$。而如果是彩色照片，通常需要三個量來表示一個像素，則向量長度也會變為現在的三倍。

如此大的數據不經過壓縮很難廣泛傳播。教學錄像采用的壓縮方法就是JPEG（Joint Photographic Expert Group，聯合圖像專家組），該方法采用的就是基變換的方式壓縮圖像。比如說一塊乾凈的黑白，其附近的像素值應該非常接近，此時如果一個像素一個像素的描述黑白灰度值就太浪費空間了，所以標準基在這種情況下並不能很好的利用圖片的特性。

我們知道，標準基是 $$\begin{bmatrix}1\\0\\\vdots\\0\end{bmatrix}\begin{bmatrix}0\\1\\\vdots\\0\end{bmatrix}\cdots\begin{bmatrix}0\\0\\\vdots\\1\end{bmatrix}$$，我們想尋找一個更好的基。

我們試試使用別的基描述圖片，比如：

* 基中含有的一個向量 $$\begin{bmatrix}1&1&\cdots&1\end{bmatrix}^T$$，即分量全為$$1$$的向量，一個向量就可以完整的給出所有“像素一致圖像”的信息；
* 另一個向量 $$\begin{bmatrix}1&-1&\cdots&1&-1\end{bmatrix}^T$$，正負交替出現，比如描述國際象棋棋盤；
* 第三個個向量 $$\begin{bmatrix}1&1&\cdots&-1&-1\end{bmatrix}^T$$，一半正一半負，比如描述一半亮一半暗的圖片；

### 傅里葉基

現在我們來介紹傅里葉基，以$$8\times 8$$傅里葉基為例（這表示我們每次只處理$$8\times 8$$像素的一小塊圖像）：

$$F_n=\begin{bmatrix}1&1&1&\cdots&1\\1&w&w^2&\cdots&w^{n-1}\\1&w^2&w^4&\cdots&w^{2(n-1)}\\\vdots&\vdots&\vdots&\ddots&\vdots\\1&w^{n-1}&w^{2(n-1)}&\cdots&w^{(n-1)^2}\end{bmatrix},\ w=e^{i2\pi/n},\ n=8$$，我們不需要深入$$8$$階傅里葉基的細節，先看看使用傅里葉基的思路是怎樣的。

每次處理$$8\times 8$$的一小塊時，會遇到$$64$$個像素，也就是$$64$$個基向量，$$64$$個係數，在$$64$$維空間中利用傅里葉向量做基變換：

* 輸入信號$$x$$為$$64$$維向量$$\xrightarrow{基變換}$$輸出信號$$c$$為$$x$$在傅里葉基下的$$64$$個係數。

    注意前面做的都是無損的步驟，我們只是選了$$\mathbb{R}^64$$的一組基，接著把信號用這組基表達出來。
    
    接下來的步驟就涉及到壓縮和損失了：
    
* 一種方法是扔掉較小的係數，這叫做閾值量化（thresholding），我們設定一個閾值，任何不在閾值範圍內的基向量、係數都將丟棄，雖然有信息損失，但是只要閾值設置合理，肉眼幾乎無法區別壓縮前後的圖片。經由此步處理，向量$$c$$變為$$\hat c$$，而$$\hat c$$將有很多$$0$$。
  
    通常$$\begin{bmatrix}1&1&\cdots&1\end{bmatrix}^T$$向量很難被丟棄，它通常具有較大的係數。但是$$\begin{bmatrix}1&-1&\cdots&1&-1\end{bmatrix}^T$$向量在平滑信號中的可能性就很小了。前一個的向量稱作低頻信號，頻率為$$0$$，後一個向量稱作高頻信號，也是我們能夠得到的最高頻率的信號，如果是噪音或抖動輸出的就是它。
    
    比如講課的視頻圖像信號，這種平滑的情形下輸出的大多是低頻信號，很少出現噪音。
    
* 接著我們用這些係數$$\hat c$$來重構信號，用這些係數乘以對應的基向量$$\hat x=\sum \hat{c}_iv_i$$，但是這個求和不再是$$64$$項求和了，因為壓縮後的係數中有很多零存在，比如說我們壓縮後$$\hat c$$中僅有三個非零項，那麽壓縮比將近達到$$21:1$$。

我們再來提一下視頻壓縮：視頻是一系列連續圖像，且相近的幀非常接近，而我們的壓縮算法就需要利用這個相近性質。在實際生活中，從時間與空間的角度講，事物不會瞬間改變。

### 小波基

接下來介紹另一組基，它是傅里葉基的競爭對手，名為小波（wavelets），同樣以$$8\times 8$$為例：
$$\begin{bmatrix}1\\1\\1\\1\\1\\1\\1\\1\end{bmatrix}
\begin{bmatrix}1\\1\\1\\1\\-1\\-1\\-1\\-1\end{bmatrix}
\begin{bmatrix}1\\1\\-1\\-1\\0\\0\\0\\0\end{bmatrix}
\begin{bmatrix}0\\0\\0\\0\\1\\1\\-1\\-1\end{bmatrix}
\begin{bmatrix}1\\-1\\0\\0\\0\\0\\0\\0\end{bmatrix}
\begin{bmatrix}0\\0\\1\\-1\\0\\0\\0\\0\end{bmatrix}
\begin{bmatrix}0\\0\\0\\0\\1\\-1\\0\\0\end{bmatrix}
\begin{bmatrix}0\\0\\0\\0\\0\\0\\1\\-1\end{bmatrix}$$。

可以看出傅里葉基中頻率最高的向量為小波後四個基向量之和。

在標準基下的一組（按八個一組計算，$$P\in\mathbb{R}^8$$）像素$$P=\begin{bmatrix}p_1\\p_2\\\vdots\\p_8\end{bmatrix}=c_1w_1+c_2w_2+\cdots+c_nw_n=\Bigg[w_1\ w_2\ \cdots\ w_n\Bigg]\begin{bmatrix}c_1\\c_2\\\vdots\\c_n\end{bmatrix}$$，即$$P=WC$$，我們需要計算像素向量在另一組基下係數，所以有$$C=W^{-1}P$$。

此時我們发現，如果選取“好的基”會使得逆矩陣的求解過程變簡單，所謂“好的基”：

* 計算快；
  
    我們需要大量使用$$P=WC$$來計算整幅圖在另一個基下的表達，在傅里葉變換中我們學習了快速傅里葉變換（FFT），同樣的在小波變換中也有快速小波變換（FWT）；
    
    另外的，我們需要計算其逆矩陣，所以這個逆矩陣計算也必須快，觀察小波基不難发現基向量相互正交，假設我們已經對小波基做了標準化處理，則小波基是一組標準正交基，所以有$$W^{-1}=W^T$$。
    
* 僅需少量向量即可最大限度的重現圖像。
  
    因為在圖像壓縮時，我們會舍棄較小的係數，比如$$c_5,c_6,c_7,c_8$$，所以後四個的基向量都會被舍棄，重現圖像時僅使用前四個基向量的線性組合，而好的基選取會在使用較少基的前提下保證圖像質量不會有較大損失。
    
    題外話：JPEG2000標準會將小波基納入壓縮算法。我們上面介紹的是最簡單的一組小波基，而FBI的指紋識別或JPEG2000的壓縮算法納入的是更加平滑的小波基，不會使用像上面介紹的那種直接從$$1$$變為$$-1$$的基。

要想繼續了解小波基，可以參考一篇非常精彩的文章[能不能通俗的講解下傅立葉分析和小波分析之間的關系？——“咚懂咚懂咚“的答案](https://www.zhihu.com/question/22864189/answer/40772083)

## 基變換

前面介紹小波基的時候我們就已經做了一次基變換。

將目標基的向量按行組成矩陣$$W$$，則基變換就是$$\Bigg[x\Bigg]\xrightarrow{x=Wc}\Bigg[c\Bigg]$$。

看一個例子，有線性變換$$T:\mathbb{R}^8\to\mathbb{R}^8$$，在第一組基$$v_1,v_2,\cdots,v_8$$上計算得到矩陣$$A$$，在第二組基$$w_1,w_2,\cdots,w_n$$上計算得到矩陣$$B$$。先說結論，矩陣$$A,B$$是相似的，也就是有$$B=M^{-1}AM$$，而$$M$$就是基變換矩陣。

進行基變換時會发生兩件事：
1. 每個向量都會有一組新的坐標，而$$x=Wc$$就是新舊坐標的關系；
2. 每個線性變換都會有一個新的矩陣，而$$B=M^{-1}AM$$就是新舊矩陣的關系。

    再來看什麽是$$A$$矩陣？
    
    對於第一組基$$v_1,v_2,\cdots,v_8$$，要完全了解線性變換$$T$$，只需要知道$$T$$作用在基的每一個向量上會產生什麽結果即可。因為在這個基下的每一個向量都可以寫成$$x=c_1v_1+c_2v_2+\cdots+c_8v_8$$的形式，所以$$T(x)=c_1T(v_1)+c_2T(v_2)+\cdots+c_8T(v_8)$$。
    
    而且$$T(v_1)=a_{11}v_1+a_{21}v_2+\cdots+a_{81}v_8,\ T(v_2)=a_{12}v_1+a_{22}v_2+\cdots+a_{82}v_8,\ \cdots$$，則矩陣$$\begin{bmatrix}A\end{bmatrix}=\left[\begin{array}{c\|c\|c\|c}a_{11}&a_{12}&\cdots&a_{1n}\\a_{21}&a_{22}&\cdots&a_{2n}\\\vdots&\vdots&\ddots&\vdots\\a_{m1}&a_{m2}&\cdots&a_{mn}\\\end{array}\right]$$
    
    這些都是上一講結尾所涉及的知識。

最後我們以一個更加特殊的基收場，設$$v_1,v_2,\cdots,v_n$$是一組特征向量，也就是$$T(v_i)=\lambda_1v_i$$，那麽問題就是矩陣$$A$$是什麽？

繼續使用線性變換中學到的，輸入的第一個向量$$v_1$$經由$$T$$加工後得到$$\lambda_1v_1$$，第二個向量$$v_2\xrightarrow{T}\lambda_2v_2$$，繼續做下去，最終有$$v_n=v_n\xrightarrow{T}\lambda_nv_n$$。除了$$\lambda_iv_i$$外的其他基向量都變為$$0$$，那麽矩陣$$A=\begin{bmatrix}\lambda_1&&&\\&\lambda_2&&\\&&\ddots&\\&&&\lambda_n\end{bmatrix}$$。

這是一個非常完美的基，我們在圖像處理中最想要的就是這種基，但是找出像素矩陣的特征向量代價太大，所以我們找了一些代價小同時效果也不錯的基，比如小波基、傅里葉基等等。