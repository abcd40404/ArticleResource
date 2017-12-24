---
title: 小東西筆記
date: 2017-12-24 11:08:38
tags:
categories: [解題區, Template, 其他]
---

## Operator
1. ~n == (-n - 1) <=> ~n + 1 == -n
~ 是做 1's complement, 而負數就是 2's complement == 1's complement + 1
2. 取得二進制的最後一個 1
n & -n 或是 n & (n - 1)
3. AND bit 0: 把該 bit 關閉
   OR  bit 1: 把該 bit 打開
   AND bit 1 和 OR bit 0: 皆保持原樣, 無作用
