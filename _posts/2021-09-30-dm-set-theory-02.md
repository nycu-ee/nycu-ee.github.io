---
layout: post
title: 離散數學-集合論-集合運算
categories: Mathematic
tags: [Discrete Mathematic]
---

author: [o-jules](https://github.com/o-jules)

> Description:
>
> 這是關於離散數學的相關筆記，本篇介紹命題和複合命題	

<!-- more -->

# 集合的運算

## 集合的並與交

  - 屬於A或者屬於B的所有元素的集合，稱為集合$A$​和B的並集，記作：$A∪B$，即：

    $A∪B = \{x: x ∈ A 或 x ∈ B\}$

  - 屬於$A$並且屬於$B$的所有元素的集合，稱為集合$A$和$B$的交集，記作：$A∩B$，即：

    $A∩B = \{x: x ∈ A 且 x ∈ B\}$

    如果$A$和$B$沒有公共元素，則稱集合$A$和$B$是不交的， $A∩B = ∅$。
    此時，$A$與$B$的並集稱為 不交的並(disjoint union)。

### 定理1.2

下述語句等價：$A ⊆ B$，$A ∩ B = A$，$A ∪ B = B$。

## 集合的補

所有屬於全集$U$但不屬於$A$的元素構成的集合：

$$
A^c = \{x: x \in \mathbb{U}, x \not\in A \}。
$$

也記作 $\overline{A}$​或者 $A^c$​​​。

### 相對補\差

集合$B$​關於集合$A$​的相對補，或稱集合$A$​與集合$B$​的差，記作 $A \setminus B$​，是由所有屬於A但不屬於B的元素構成的集合，即：

$A\setminus B = \{x: x ∈ A, x ∉ B\}$​。

也記作：$A-B$ 或者 $A$~$B$。

（本質上：$A \setminus B = A ∩ \overline{B}$​。）

## 集合的基本積

對於 $n$ 個不同的集合 $A1, A2, ..., An$, 它們的基本積是以下形式的任一集合：
$A1* \cap A2* \cap ... \cap An* (Ai* = A 或 Ai* = A^c)$

## 對稱差

集合A和B的對稱差，記作
$$
A ⊕ B
$$
是所有屬於A或B但不同時屬於A和B的元素的集合。即：

$$
A \oplus B = \{x | (x \in A \land x \not\in B) \lor (x \in B \land x \not\in A)\}
$$

性質：
$$
A \oplus B = (A \cup B) \setminus (A \cap B) \\
A \oplus B = (A \setminus B) \cup (B \setminus A)
$$

## 集合的代數運算及對偶性

定理1.3，集合滿足以下表所列的規律：

### 對偶性

設$E$為集合代數運算的一個方程，則$E$的對偶$E$*是由將$E$中的並與交互換，全集與空集互換，得到的方程。
在集合的代數運算中，對偶原理成立。即如果一個方程$E$成立，則其對偶方程$E$*必定成立。

## 有限集及計數原理

一個集合稱為有限集，如果它恰好含有$m$個相異的元素，其中$m$為某非負整數；否則，稱集合為無限集。

用記號$n(A)$表示有限集$A$中元素的個數，也可以用 $\#(A)$，$|A|$ 或者 $card(n)$。

### 引理1.4

如果$A$，$B$為不交的有限集，則$A∪B$為有限集且

$n(A ∪ B) = n(A) + n(B)$。

### 定理1.5

如果$A$，$B$均為有限集，則$A ∪ B$和$A ∩ B$均為有限集，且

$n(A ∪ B) = n(A) + n(B) - n(A ∩ B)$。

### 推論1.6

如果$A$，$B$，$C$均為有限集，則$A ∪ B ∪ C$均為有限集，且

$n(A ∪ B ∪ B) = n(A) + n(B) + n(C) - n(A ∩ B) - n(A ∩ C) - n(B ∩ C) + n(A ∩ B ∩ C)$。
