---
title: 卡塔蘭數 Catalan number
date: 2018-02-10 00:02:58
tags:
categories: [解題區, Template, DP]
---

一般式: {%math%} C_{n} = \dfrac {1}{n+1}\binom{2n}{n} = \dfrac {\left( 2n\right) !}{\left( n+1\right) !n!} {%endmath%}
可用於 二元樹種類個數...等問題

## Code
```cpp
big fac[MAX_N * 2];
big res = fac[2 * n] / fac[n + 1] / fac[n];
```

## 例題
1. Uva 10007
