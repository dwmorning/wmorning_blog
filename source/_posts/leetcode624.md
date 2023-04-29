---
title: 624. 数组列表中的最大距离
author: 菜鸟书生
# cover: https://w.wallhaven.cc/full/28/wallhaven-28pdry.jpg
banner:
  type: img
  bgurl: https://pic1.zhimg.com/v2-b3c2c6745b9421a13a3c4706b19223b3_r.jpg
  bannerText: 尊享面试 100 题
categories:
  - leetcode
tags:
  - leetcode
  - 尊享面试 100 题
date: 2023-04-19 11:04:56
keywords: 贪心, 数组
toc: false
---
> [尊享面试 100 题](https://dwmorning.github.io/leetcodeVipInterview)是Leetcode会员专享题单

## 624. 数组列表中的最大距离
[力扣题目链接](https://leetcode.cn/problems/maximum-distance-in-arrays/?envType=study-plan-v2&id=premium-algo-100)
给定 m 个数组，每个数组都已经按照升序排好序了。现在你需要从两个不同的数组中选择两个整数（每个数组选一个）并且计算它们的距离。两个整数 a 和 b 之间的距离定义为它们差的绝对值 |a-b| 。你的任务就是去找到最大距离

#### **示例 1：**

```
输入： 
[[1,2,3],
 [4,5],
 [1,2,3]]
输出： 4
解释：
一种得到答案 4 的方法是从第一个数组或者第三个数组中选择 1，同时从第二个数组中选择 5 。
```


**注意：**

* 每个给定数组至少会有 1 个数字。列表中至少有两个非空数组。
* 所有 m 个数组中的数字总数目在范围 [2, 10000] 内。
* m 个数组中所有整数的范围在 [-10000, 10000] 内。

### 思路：

```javascript
/**
 * @param {number[][]} arrays
 * @return {number}
 */
var maxDistance = function(arrays) {
    let res = 0, min = Infinity, max = -Infinity
    for(let i = 0; i < arrays.length; i++){
        let start = arrays[i][0]
        let end = arrays[i][arrays[i].length-1]
        res = Math.max(res,max-start,end-min)
        max = Math.max(max,end)
        min = Math.min(min,start)
    }
    return res
};
```
