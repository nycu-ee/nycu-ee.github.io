---
layout: post
title: Git tutorial
categories: Dev
tags: [beginner]
---

author: Anderson

透過此篇教學，你可以學到從特地資源庫建立分支，並在編輯後對原資料庫提交PR。

## Git 介紹

Git 是由 Linux 核心的作者 Linus Torvalds 在 2005 年為了管理 Linux 核心程式碼，僅花了 10 天所開發出來的，至目前已有十幾年的歷史了。除了可免費使用外，整個 Git 的原始程式碼也可在網路上取得（當然 Git 的原始程式碼也是用 Git 在做版本控制的）。

**那Github是什麼?**

Git 是一款版本控制軟體，而 GitHub 是一個商業網站，GitHub 的本體是一個 Git 伺服器，但這個網站上的應用程式讓大家可以透過 Web 介面來操作一些原本需要複雜的 Git 指令才能做到的事。因為圖形介面操作起來較為容易，因此接下來的操作都是以Github Desktop進行操作，請大家先去下載並安裝，此外慶建立一個自己的Github帳號，以便後續操作。

Download: [Github Desktop](https://desktop.github.com/)

<!-- more -->

## Git 操作

由於Git操作指令的文章已經有很多了，因此附上[相關連結](https://dzone.com/articles/top-20-git-commands-with-examples)

接下來，假設你已開啟Github Desktop並登入帳號，請到[這個連結](https://github.com/nycu-ee/nycu-ee.github.io)點擊Fork

![](/public/img/git-tutorial/fork.png)

接著到自己Fork過來的資料庫**(注意:要確定是自己的)**依照以下圖片進行操作

![](/public/img/git-tutorial/open-with-desktop.png)

點擊Open with Github Desktop

![](/public/img/git-tutorial/clone-button.png)

點擊Clone

接下來，請在Clone下來的資料夾中找到**_post資料夾**，接下來請至[Typora教學](https://nycu-ee.github.io/dev/2021/01/31/typora-tutorial/)，完成第二項任務

## 完成第二項任務後

請確認檔案已放入**_post資料夾**且檔名無誤後，打開Github Desktop 在找到剛剛Clone下來的目錄

點擊左下角藍色的Commit**(注意:需要在按鈕上方的Summary打入簡短的敘述，才可進行Commit)**

完成Commit之後，在上方的黑色按鍵列點擊Push origin

## 發 PR 給原作者

回到自己的專案頁面，可以找到一個「New pull request」的按鈕

![](/public/img/git-tutorial/pr1.png)

按下「Create pull request」後，可開始填寫 PR 的相關資訊，讓作者知道你這個 PR 大概做了什麼事

![](/public/img/git-tutorial/pr2.png)

填寫完畢後，按下「Create pull request」按鈕後，即算完成送出 PR：

![](/public/img/git-tutorial/pr3.png)

## 如果有問題的話

在Clone部份的問題，可以參考[這個](https://gitbook.tw/chapters/github/clone-repository.html)

在PR部份的問題，可以參考[這個](https://gitbook.tw/chapters/github/pull-request.html)