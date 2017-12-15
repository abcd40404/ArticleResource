---
title: 大數運算 模版
date: 2017-10-24 23:31:43
tags:
categories: [解題區, Template, 其他]
---
第三次寫大數了
在比賽裡面因為 JAVA 有內建大數
所以此類題目比較少出
不過刷題的時候還是會遇到

```cpp
struct big{
    vector <int> digit;

    big(){

    }

    big(string s){
        int len = s.length();
        for(int i = 0; len - 1 - i >= 0; i++){
            digit.push_back(s[len - 1 - i] - '0');
        }
    }

    big operator +(const big& obj)const{
        int carry = 0;
        int maxSize = max(digit.size(), obj.digit.size()), minSize = min(digit.size(), obj.digit.size());
        big res;
        for(int i = 0; i < minSize; i++){
            int num = digit[i] + obj.digit[i] + carry;
            carry = num / 10;
            num %= 10;
            res.digit.push_back(num);
        }
        for(int i = minSize; i < maxSize; i++){
            int num;
            if(digit.size() > minSize)
                num = digit[i] + carry;
            else
                num = obj.digit[i] + carry;
            carry = num / 10;
            num %= 10;
            res.digit.push_back(num);
        }
        if(carry){
            res.digit.push_back(carry);
            carry = 0;
        }
        return res;
    }

    void print(){
        for(int i = (int)digit.size() - 1; i >= 0; i--){
            printf("%d", digit[i]);
        }
        puts("");
    }
};
```