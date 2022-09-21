---
layout: post
title: 離散數學-邏輯與命題-基本概念
categories: Mathematic
tags: [Discrete Mathematic]
---

author: [o-jules](https://github.com/o-jules)

> Description:
>
> 這是關於離散數學的相關筆記，本篇介紹命題和複合命題	

<!-- more -->

## 命題與複合命題

### 命題

**命題**（或**陳述**）是一個說明性語句，它只能是真或假，不可能兩者同時成立。

## 複合命題

**複合命題** 由**子命題**及它們之間的各種聯系組成的命題稱為複合命題。

**原子命題** 不能被分解為更簡單的命題（非複合命題）稱為原子命題

## 基本邏輯運算

**合取聯結**

任何兩個命題可以用術語“與”聯合而成一個複合命題，叫做這兩個原始命題的合取聯結。記作：

$$
p \land q
$$

讀作“$p$與$q$”，表示$p$與$q$的合取聯結。

**定義4.1** 如果$p$與$q$均為真，則$p \land q$ 為真；否則$ p \land q$為假。

**析取聯結**

任何兩個命題可以用術語“或”聯合而成一個複合命題，叫做這兩個原始命題的析取聯結。記作：

$$
p \lor q
$$

讀作“$p$ 或 $q$”，表示$p$ 與 $q$的析取聯結。

**定義4.2** 如果$p$與$q$均為假，則 $p \lor q$ 為假；否則$p \lor q$為真。

### 否定聯結, $\lnot p$

給定任一命題$p$，都可以通過在$p$前面添加“不是”或“假”或在$p$前面插入“非”，得到另一個命題，稱為$p$的否定聯結，記作：

$$
\lnot p
$$

讀作“非$p$”，表示$p$的否定聯結。

**定義4.3** 如果$p$為真，則 $\lnot p$ 為假；如果$p$為假，則 $\lnot p$ 為真。

## 命題與真值表

**命題表達式**

設 $P(p, q, ...)$為一個由取值為真(T)或假(F)的邏輯變量$p$, $q$, ... 以及邏輯聯結 $\land$, $\lor$, $\lnot$ 構成的表達式。
這樣的表達式$P(p, q, ...)$稱為一個命題。

**邏輯聯結的規定優先級** 規定：

$$
\lnot 優先於 \land 優先於 \lor
$$

### 構造真值表的另一種方法

## 永真命題與永假命題

**永真命題** 對於變量的任意值，都為真的命題。

**永假命題** 對於變量的任意做，都為假的命題。

**定理4.1（代入原理）** 若$P(p, q, ...)$是永真命題，
則對任意命題$P_1, P_2, ...,$ 命題$P(P_1, P_2, ...)$仍然是永真命題。

## 邏輯等價

兩個命題$P(p, q, ...)$ 與 $Q(p, q, ...)$如果具有*相同的真值表*，則稱為*邏輯等價*的，或簡稱為*等價*或*相等*，記作：

$$
P(p, q, ...) \equiv Q(p, q, ..)
$$

例如：
$$
\lnot (p \land q) \equiv \lnot p \land \lnot q
$$

## 命題代數

**定理4.2** 命題滿足如下定律：

    1. 冪等律

$$
  p \lor p \equiv p
$$

$$
  p \land p \equiv p
$$

    2. 結合律

$$
  (p \lor q) \lor r \equiv p lor (q \lor r)
$$

$$
  (p \land q) \land r \equiv p \land (q \land r)
$$

    3. 交換律

$$
  p \lor q \equiv q \lor p
$$

$$
  p \land q \equiv q \land p
$$

    4. 分配律

$$
  p \lor (q \land r) \equiv (p \lor q) \land (p \lor r)
$$

$$
  p \land (q \lor r) \equiv (p \land q) \lor (p \land r)
$$

    5. 同一律

$$
  p \land T \equiv p, p \lor F \equiv p
$$

$$
  p \lor T \equiv T, p \land F \equiv F
$$

    6. 互補律

$$
  p \lor \lnot p \equiv T, p \land \lnot p \equiv F
$$

$$
  \lnot T \equiv F, \lnot F \equiv T
$$

    7. 對合律

$$
  \lnot \lnot p \equiv p
$$

    8. DeMorgan律

$$
  \lnot(p \lor q) \equiv \lnot p \land \lnot q
$$

$$
  \lnot(p \land q) \equiv \lnot p \lor \lnot q
$$

## 條件語句與雙條件語句

**條件語句** 具有形式“如果p則q”的語句稱為條件語句。記作：

$$
p \implies q
$$

常讀作“p蘊含q”或者“僅當q時有p”。

**真值表**

| p    | q    |$p \implies q$|
| ---- | ---- | ------------ |
| T    | T    | T            |
| T    | F    | F            |
| F    | T    | T            |
| F    | F    | T            |

（為何 (F, F) = T ？）

**雙條件語句** 具有形式“p當且僅當q”的語句稱為雙條件語句。記作：
$$
p \iff q
$$

| p    | q    |$p \iff q$|
| ---- | ---- | -------- |
| T    | T    | T        |
| T    | F    | F        |
| F    | T    | F        |
| F    | F    | T        |
