---
title: 求取循環節長度
date: 2017-10-28 11:01:11
tags: BSGS Algorithm
categories: [學習札記, 數論]
mathjax: true
---

任何有理數 p / q 皆可以用循環小數來表示
像是 
1 / 3 = 0.33333...
1 / 4 = 0.25000...

以下介紹一些定理以及方法
來求取 非循環節 以及 循環節

## 定理

1. 不循環節長度 - 2 / 5 定理：
分母拆解成 2 和 5 的乘積, 長度 = max(num_2, num_5);

2. 循環節長度: 如果 a 沒有 2 or 5 的質因數, 且 a, b 互質
則 b / a 的循環節長度為: {% math %} \min \{ e\in N,10^{e}\equiv 1(mod\ a) \} {% endmath %}
然後我們就可以用 [BSGS 演算法](http://abcd40404.github.io/2017/10/28/BSGS-Algorithm/)來求出 e


