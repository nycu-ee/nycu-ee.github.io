---
layout: post
title: Markdown and Typora tutorial
categories: Dev
tags: [beginner]
---

author: Andreson

Typora是一款Markdown編輯器，本篇文章將帶你完成第一篇Markdown自我介紹文章。

Download: [Typora](https://typora.io/)

<!-- more -->

## Markdown是什麼?

Markdown是一種輕量級標記式語言，創始人為約翰·格魯伯。它允許人們使用易讀易寫的純文字格式編寫文件，然後轉換成有效的XHTML（或者HTML）文件。這種語言吸收了很多在電子郵件中已有的純文字標記的特性。

由於Markdown的輕量化、易讀易寫特性，並且對於圖片，圖表、數學式都有支援，目前許多網站都廣泛使用Markdown來撰寫說明文件或是用於論壇上發表訊息。如GitHub、Reddit、Diaspora、Stack Exchange、OpenStreetMap 、SourceForge、簡書等，甚至還能被用來撰寫電子書。

詳細語法在[這裡](https://markdown.tw/)，但是用Typora就不用特別記語法了。

## 編寫自我介紹

請開啟Typora

先儲存並將檔案命名為:**YYYY-MM-DD-你在本網站想使用的作者名-introduction.md**

並在檔案中加入以下程式碼

```markdown
---
layout: post
title: 你的作者名的自我介紹
categories: self-intro
tags: [self-introduction]
---

author: 你的作者名

<!-- more -->
## 你的作者名的自我介紹

```

### 自我介紹建議內容

1. 你的作者名
2. 你的學校和科系
3. 你的興趣
4. 你希望別人透過什麼管道認識你(如IG、Facebook)
5. 其他你想分享給我們的資訊

## 完成自我介紹之後

1. 請檢查檔案名稱是否正確
2. 接著請至[這裡](https://nycu-ee.github.io/dev/2021/01/31/git-tutorial/)完成PR的部分
3. 創作文章的相關規範可以參考[這裡](https://nycu-ee.github.io/dev/2021/01/31/example-article/)
