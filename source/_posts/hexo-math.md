---
title: 在 Hexo 顯示數學式
date: 2017-10-28 12:36:31
tags: Hexo
categories: [學習札記, 網頁設計]
---

試了幾個小時 終於成功了
首先安裝
```
npm install hexo-math --save
```
裝好之後
來個簡單的測試
```
Simple inline $a = b + c$
```
應該要正常顯示 a = b + c 的式子
但是問題來了QQ
網頁上根本沒渲染
查了好幾個網頁
每個都說要在 **_config.yml** 加東加西的
但完全沒用啊！

最後找到一篇文章說, 安裝
```
npm install hexo-renderer-mathjax --save
```
果然成功渲染了！

此外好像還有 latex 語法加底線, 會被 markdown 當成斜體的問題
不過還沒用到那些數學式, 之後再研究

2018/1/24 更新:
回到家之後, 筆電也不能正常顯示QQ
於是在 **_config.yml** 加了就可以了
```
math:
  engine: 'mathjax' # or 'katex'
  mathjax:
    src: custom_mathjax_source
    config:
      # MathJax config
  katex:
    css: custom_css_source
    js: custom_js_source # not used
    config:
      # KaTeX config
```

參考：
https://github.com/hexojs/hexo-math/issues/26
