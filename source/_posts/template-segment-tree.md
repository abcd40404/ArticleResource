---
title: 線段樹 Segment Tree
date: 2018-01-24 10:14:23
tags:
categories: [解題區, Template, Data Structure]
---
可做到:
1. 範圍更新
2. 範圍查詢
---

注意是: 0-based index

建樹就一邊 input, 一邊 update 就好
經過測試
update 的時候一定要 push 再 pull
query 可以只做 push 就好

## Code
```cpp
const int MAX_N = 100010;

int seg[MAX_N * 8];
int lazy[MAX_N * 8];
int SN;

void seg_init(int N){
    SN = 1;
    while(SN < N) SN <<= 1;
    memset(seg, 0, sizeof(seg));
    memset(lazy, 0, sizeof(lazy));
}

void seg_pull(int idx){
    seg[idx] = seg[idx * 2 + 1] + seg[idx * 2 + 2];
}

void seg_push(int idx, int l, int m, int r){
    if(lazy[idx]){
        seg[idx * 2 + 1] += lazy[idx] * (m - l);
        seg[idx * 2 + 2] += lazy[idx] * (r - m);
        lazy[idx * 2 + 1] += lazy[idx];
        lazy[idx * 2 + 2] += lazy[idx];
        lazy[idx] = 0;
    }
}

void seg_update(int a, int b, int x, int idx, int l, int r){
    if(r <= a || l >= b) return ;
    if(a <= l && r <= b){
        seg[idx] += x * (r - l);
        lazy[idx] += x;
        return ;
    }

    int m = (l + r) / 2;
    seg_push(idx, l, m, r);
    seg_update(a, b, x, idx * 2 + 1, l, m);
    seg_update(a, b, x, idx * 2 + 2, m, r);
    seg_pull(idx);
}

int seg_query(int a, int b, int idx, int l, int r){
    if(r <= a || l >= b) return 0;
    if(a <= l && r <= b) return seg[idx];

    int m = (l + r) / 2;
    seg_push(idx, l, m, r);
    int ans = 0;
    ans += seg_query(a, b, idx * 2 + 1, l, m);
    ans += seg_query(a, b, idx * 2 + 2, m, r);
    seg_pull(idx);
    return ans;
}
```

## 例題
1. POJ 3468
