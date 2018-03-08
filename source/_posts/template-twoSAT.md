---
title: 2-SAT
date: 2018-03-08 12:02:50
tags:
categories: [解題區, Template, Graph]
---


## Code
```cpp
const int MAX_V = ...;

struct TwoSAT{
    int V, E;
    vector <int> g[MAX_V * 2];
    int dfn[MAX_V * 2], low[MAX_V * 2], sccid[MAX_V * 2], tot, scc_cnt;
    stack <int> S;
    bool in_stack[MAX_V * 2];

    void init(int n){
        this->V = n * 2;
        for(int i = 0; i < V; i++) g[i].clear();
        memset(dfn, 0, sizeof(dfn));
        memset(low, 0, sizeof(low));
        memset(sccid, 0, sizeof(sccid));
        tot = 0;
    }

    void addClause(int x, int xflag, int y, int yflag){
        x = x * 2 + xflag;
        y = y * 2 + yflag;
        if(x == y) g[x ^ 1].pb(y);
        else{
            g[x ^ 1].pb(y);
            g[y ^ 1].pb(x);
        }
    }

    void dfs(int x){
        dfn[x] = low[x] = ++tot;
        in_stack[x] = true;
        S.push(x);
        for(int i = 0; i < sz(g[x]); i++){
            int v = g[x][i];
            if(!dfn[v]){
                dfs(v);
                low[x] = min(low[x], low[v]);
            }
            else if(in_stack[v]){
                low[x] = min(low[x], dfn[v]);
            }
        }
        if(dfn[x] == low[x]){
            while(1){
                int v = S.top(); S.pop();
                in_stack[v] = false;
                sccid[v] = scc_cnt;
                if(v == x) break;
            }
            scc_cnt++;
        }
    }
    
    void tarjan(){
        scc_cnt = 0;
        for(int i = 0; i < V; i++){
            if(!dfn[i]) dfs(i);
        }
    }

    bool solve(){
        tarjan();
        for(int i = 0; i < V; i += 2){
            if(sccid[i] == sccid[i ^ 1]) return false;
        }
        return true;
    }
}solver;
```

# 例題
1. Uva 10319
