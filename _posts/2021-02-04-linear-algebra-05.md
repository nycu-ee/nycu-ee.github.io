---
layout: post
title: 線性代數筆記-05
categories: Mathematic
tags: [linear algebra]
---

author: [zlotus](https://github.com/zlotus/notes-linear-algebra)

> Description:
>
> 這是MIT 18.06 Linear-Algebra 的學習筆記	

[Course video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=6&ab_channel=MITOpenCourseWare)

<!-- more -->

# 第五講：轉換、置換、向量空間R

## 置換矩陣（Permutation Matrix）

$P$為置換矩陣，對任意可逆矩陣$A$有：

$PA=LU$

$n$階方陣的置換矩陣$P$有$\binom{n}{1}=n!$個

對置換矩陣$P$，有$P^TP = I$

即$P^T = P^{-1}$
## 轉置矩陣（Transpose Matrix）

$A^T_{ij}=A_{ji}$

## 對稱矩陣（Symmetric Matrix）

$A^T$ = $A$

對任意矩陣$R$有$R^TR$為對稱矩陣：

$$
(R^TR)^T = (R)^T(R^T)^T = R^TR\\
\textrm{即}(R^TR)^T = R^TR
$$

## 向量空間（Vector Space）

所有向量空間都必須包含原點（Origin）；

向量空間中任意向量的數乘、求和運算得到的向量也在該空間中。
即向量空間要滿足加法封閉和數乘封閉。
