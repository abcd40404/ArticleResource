---
title: 李代數 SO(3), SE(3) 微分推導
date: 2018-09-15 22:03:57
tags: Lie Algebra
categories: [學習札記, 視覺SLAM]
---
當我們考慮到無限小的運動時
就會需要到微分
對於旋轉矩陣 R(t)
我們知道:
{%math%}R(t)R^{T}(t) = I{%endmath%}
事實上旋轉矩陣的反矩陣, 即為他的轉置矩陣
接著我們對這個式子兩邊做微分:
{%math%}\frac{d}{dt}(RR^{T}) = \dot{R}R^{T} + R\dot{R^{T}} = 0{%endmath%}
移項後得到:
{%math}\dot{R}R^{T} = -(\dot{R}R^{T})^{T}{%endmath%}
此時可以發現到 {%math%} \dot{R}R^{T} {%endmath%} 就是斜對稱矩陣！
令 {%math%} \hat{w}(t) = -(\dot{R}R^{T})^{T} {%endmath%}
右乘 {%math%} R(t) {%endmath%} 得到:
{%math%}\dot{R}(t) = \hat(w)R(t){%endmath%}
如此就得到 R 微分的關係式

