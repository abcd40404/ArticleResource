---
title: 雙連通單元 BCC
date: 2018-03-04 19:30:28
tags:
categories: [解題區, Template, Graph]
---
在一個無向圖中
若任兩點, 存在"兩條點不重複路徑", 則稱此圖為 點-雙連通
而點-雙連通內部沒有割點
若任兩點, 存在"兩條邊不重複路徑", 則稱此圖為 邊-雙連通

點-雙連通的最大子圖稱為雙連通單元(分量)


## Code
```cpp
// 割點的 bccid 沒有意義
const int MAX_V = ...;
int V, E;
vector <int> g[MAX_V], bcc[MAX_V];
int dfn[MAX_V], low[MAX_V], tot, bccid[MAX_V], bcc_cnt;
bool cut[MAX_V];
stack <int> S;

void dfs(int x, int fa){
    int child = 0;
    dfn[x] = low[x] = ++tot;
    S.push(x);
    for(int i = 0; i < sz(g[x]); i++){
        int v = g[x][i];
        if(!dfn[v]){
            dfs(v, x);
            child++;
            low[x] = min(low[x], low[v]);
            if(low[v] >= dfn[x]){
                cut[x] = true;
                bcc[bcc_cnt].clear();
                while(1){
                    int u = S.top(); S.pop();
                    bccid[u] = bcc_cnt;
                    bcc[bcc_cnt].pb(u);
                    if(u == v) break;
                }
                bccid[x] = bcc_cnt; // 沒有意義
                bcc[bcc_cnt].pb(x);
                bcc_cnt++;
            }
        }
        else if(dfn[v] < dfn[x] && v != fa){ // 反向邊
            low[x] = min(low[x], dfn[v]);
        }
    }
    // 樹根
    if(fa == -1 && child < 2) cut[x] = false;
}

void bcc_tarjan(){
    bcc_cnt = 0;
    for(int i = 0; i < V; i++){
        if(!dfn[i]) dfs(i, -1);
    }
}
```
