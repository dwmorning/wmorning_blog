---
title: 487. 最大连续1的个数 II
author: 菜鸟书生
banner:
  type: img
  bgurl: https://pic1.zhimg.com/v2-b3c2c6745b9421a13a3c4706b19223b3_r.jpg
  bannerText: 尊享面试 100 题
categories:
  - leetcode
tags:
  - 尊享面试 100 题
  - leetcode
date: 2023-04-25 13:59:05
keywords: 数组，动态规划，滑动窗口
cover: https://w.wallhaven.cc/full/qz/wallhaven-qzdxd5.jpg
toc: false
---

> [尊享面试 100 题](https://dwmorning.github.io/leetcodeVipInterview)是Leetcode会员专享题单
## 487. 最大连续1的个数 II
[力扣题目链接](https://leetcode.cn/problems/max-consecutive-ones-ii/)
给定一个二进制数组 nums ，如果最多可以翻转一个 0 ，则返回数组中连续 1 的最大个数。

#### **示例 1：**
```
输入：nums = [1,0,1,1,0]
输出：4
解释：翻转第一个 0 可以得到最长的连续 1。
     当翻转以后，最大连续 1 的个数为 4。
```
#### **示例 2：**
```
输入：nums = [1,0,1,1,0,1]
输出：4
```

**提示：**
* 1 <= nums.length <= 10<sup>5</sup>
* nums[i] 不是 0 就是 1.

### 思路：

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var findMaxConsecutiveOnes = function(nums) {
    let res = 0, dp0 = 0, dp1 = 0
    for(let i = 0; i < nums.length; i++){
        if(nums[i]){
            dp0++
            dp1++
        }else{
            dp1 =  dp0 + 1
            dp0 = 0
        }
        res = Math.max(res,Math.max(dp0,dp1))
    }
    return res
};
```