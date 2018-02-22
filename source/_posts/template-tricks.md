---
title: 常用技巧篇
date: 2018-02-20 13:32:22
tags:
categories: [解題區, Template, 其他]
---
## 列舉因數

## 判斷後綴字串
a 是否為 b 的後綴字串
```cpp
bool Suf(string a, string b){
    if(a.length() > b.length()) return false;
    return a == b.substr(b.length() - a.length(), a.length());
}
```

## 分堆

## 離散化

## 平移視窗

## 浮點數
