---
title: Hexo 顯示文章數量修改
date: 2017-03-07 11:09:19
tags: Hexo
categories: [學習札記, 網頁設計]
---

Hexo 在各個頁面預設的顯示文章數量為 10 個
如果想要修改
需要去 \_config.yml 裡的 per_page 更改

但是這會修改到全部頁面(Category, Archive...)的預設數量
如果想要各別修改, 可以在設定檔裏面
添加：
```
category_generator:
  per_page: 20
```
這樣就會針對 Category 頁面, 修改預設文章顯示數量。
