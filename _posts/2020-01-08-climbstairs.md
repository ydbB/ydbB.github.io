---
layout: post
title: 爬楼梯
---
假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数

### 题解
这个问题比较简单
写最简单的一种：
``` java
public int climbStairs(int n) {
    int f1 = 1, f2 = 1, f3;
    for (int i = 2; i <= n; ++ i) {
       f3 = f1 + f2;
       f1 = f2;
       f2 = f3;
   }
    return f2;
}
```  
