---
title: 2413. 最小偶倍数
author: 菜鸟书生
banner:
  type: img
  bgurl: https://pic1.zhimg.com/v2-b3c2c6745b9421a13a3c4706b19223b3_r.jpg
  bannerText: 每日一题
categories:
  - leetcode
tags:
  - leetcode
  - 每日一题
date: 2023-04-21 21:34:25
keywords: 数学, 数论
# cover: https://w.wallhaven.cc/full/o5/wallhaven-o5x3v7.jpg
toc: false
---

## 2413. 最小偶倍数

[力扣链接](https://leetcode.cn/problems/smallest-even-multiple/)

给你一个正整数 n ，返回 2 和 n 的最小公倍数（正整数）。

**#### \**示例 1：\****

```
输入：n = 5
输出：10
解释：5 和 2 的最小公倍数是 10 。
```

**#### \**示例 2：\****

```
输入：n = 6
输出：6
解释：6 和 2 的最小公倍数是 6 。注意数字会是它自身的倍数。
```

**提示：**

- 1 <= n <= 150

### 思路

一行实现

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var smallestEvenMultiple = function(n) {
    return n%2===1 ? 2*n : n
};
```

