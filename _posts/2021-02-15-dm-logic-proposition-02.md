---
layout: post
title: 離散數學-邏輯與命題-推廣
categories: Mathematic
tags: [Discrete Mathematic]
---

author: [o-jules](https://github.com/o-jules)

> Description:
>
> 這是關於離散數學的相關筆記，本篇介紹論證	

<!-- more -->

## 論證

論證是一個斷言，是從稱為**前提**的給定命題集合 $P_1, P_2, ..., P_n$推出稱為*結論*的另一個命題$Q$的過程。
這樣的論證記作：
$$
P_1, P_2, ..., P_n \vdash Q
$$

**定義4.4** 有效論證

一個論證$P_1，P_2，...，P_n \vdash Q$ 稱為有效的，如果前提 $P_1，P_2，...，P_n$ 為真則 $Q$ 為真。

無效的論證稱為*謬誤*。

**拆分律**

$$
p, p \implies q \vdash q
$$

**定理4.3** 論證 $(P_1, P_2, ..., P_n)\vdash Q$ 有效當且僅當命題 $(P_1, P_2, ..., P_n) \implies Q$ 是一個永真命題。

### 三段論律

$$
p \implies q, q \implies r \vdash p \implies r
$$

即
$$
[(p \implies q) \land (q \implies r)] \implies (p \implies r)
$$
是一個永真命題。

## 邏輯蘊含

稱命題 $P(p, q, ...)$ 邏輯蘊含命題$Q(p, q, ...)$記作

$$
P(p, q, ...) \implies Q(p, q, ...)
$$

即若 $P(p, q, ...)$為真，必有 $Q(p, q, ...)$為真。

**定理4.4** 對論任意的命題$P(p, q, ...)$與$Q(p, q, ...)$下列三個陳述等價：
  1. $P(p, q, ...)$邏輯蘊含 $Q(p, q, ...)$
  2. 論證 $P(p, q, ...) \vdash Q(p, q, ...)$有效
  3. 命題$P(p, q, ...) \implies Q(p, q, ...)$ 是一個永真命題

## 命題函數，量詞

設A為一個給定集合，定義於$A$上的一個命題函數（或稱為*開放語句*或*開放條件*）是一個表達式

$$
p(x)
$$

滿足對每個$a \in A$，$p(a)$ 為真或為假，即以俚語的$a \in A$ 向$x$賦值時，$p(x)$都成為一個陳述（具有其真值）。

集合$A$稱為$p(x)$的定義域，而$A$中所有使得$p(a)$為真的元素的集合$T_p$稱為$p(x)$的真集。換句話說，

$$
T_p = \{x: x \in A, p(x) 為真\} 或 T_p = \{x: p(x)\}
$$

當$A$為數的集合時，條件$p(x)$通常是一個關於變量$x$的等式或不等式方程。


### 全稱量詞

設$p(x)$為定義於集合$A$上的命題函數，考慮表達式：
$$
(\forall x \in A) p(x)
$$

讀作“對$A$中的每個$x$，$p(x)$為真語句”。

符號$\forall$ 讀作“對所有”或“對每個”，稱為**全稱量詞**。
以上表達式等價於：
$$
T_p = \{x: x \in A, p(x) \} = A
$$

即 $p(x)$ 的真集是整個$A$。

### 存在量詞

設$p(x)$為定義於集合$A$上的一個命題函數，考慮表達式

$$
(\exists x \in A)p(x)
$$

讀作“在$A$中存在$x$使得$p(x)$為真語句”。

記號$\exists$ 讀作“存在”，或“對某個”，或“對於至少一個”。叫做**存在量詞**。

以上陳述等價於：

$$
T_p = \{x: x \in A, p(x)\} \neq \emptyset
$$

即$p(x)$的真集非空。特別地：

  $Q_2$: 如果${x: p(x)} \neq \emptyset$，則$ \exists x, p(x)$為真；否則$\exists x, p(x)$為假。

## 量詞語句的否定

**定理4.5（DeMorgan）**
$$
\lnot (\forall x \in A)p(x) \equiv (\exists x \in A)\lnot p(x)
$$
即以下兩個語句等價：
  1. 對所有的$a \in A，p(a)$為真是不對的。
  2. 存在 $a \in A$，使得$p(a)$為假。

**定理4.6（DeMorgan）**
$$
\lnot(\exists x \in A)p(x) \equiv (\forall x \in A) \lnot p(x)
$$
即以下兩個語句等價：
  1. 對某個$a \in A$，$p(a)$為真 是不對的
  2. 所有$a \in A$，$p(a)$為假

**反例**

存在元素 $x_0$，使得$p(x_0)$為假，$x_0$ 稱為 $\forall x, p(x)$的一個反例。

### 含有多個變量的命題函數

**基本原理** 對其每個變量冠以量詞後的命題函數為一個語句並且具有真值。

$$
\forall x \exists y, p(x,y)
$$

或

$$
\exists x \exists y \exists z, p(x, y, z)
$$
為具有真值的語句。

### 多變量的否定量詞語句

獲得多變量否定量詞語句的具體做法是：

將否定符號從左向右移動，同時將每個$\forall$ 換成$\exists$ 而將每個$\exists$ 換成 $\forall$。
