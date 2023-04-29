---
title: 1031. 两个非重叠子数组的最大和
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
date: 2023-04-26 16:31:57
keywords: 数组, 动态规划, 滑动窗口
# cover: https://w.wallhaven.cc/full/5g/wallhaven-5gwp58.jpg
toc: false
---

## 1031. 两个非重叠子数组的最大和
[力扣题目链接](https://leetcode.cn/problems/maximum-sum-of-two-non-overlapping-subarrays/)

给你一个整数数组 nums 和两个整数 firstLen 和 secondLen，请你找出并返回两个非重叠 子数组 中元素的最大和，长度分别为 firstLen 和 secondLen 。

长度为 firstLen 的子数组可以出现在长为 secondLen 的子数组之前或之后，但二者必须是不重叠的。

子数组是数组的一个 连续 部分。


#### **示例 1：**
```
输入：nums = [0,6,5,2,2,5,1,9,4], firstLen = 1, secondLen = 2
输出：20
解释：子数组的一种选择中，[9] 长度为 1，[6,5] 长度为 2。
```
#### **示例 2：**
```
输入：nums = [3,8,1,3,2,1,8,9,0], firstLen = 3, secondLen = 2
输出：29
解释：子数组的一种选择中，[3,8,1] 长度为 3，[8,9] 长度为 2。
```
#### **示例 3：**
```
输入：nums = [2,1,5,6,0,9,5,0,3,8], firstLen = 4, secondLen = 3
输出：31
解释：子数组的一种选择中，[5,6,0,9] 长度为 4，[0,3,8] 长度为 3。
```

**提示：**
* 1 <= firstLen, secondLen <= 1000
* 2 <= firstLen + secondLen <= 1000
* firstLen + secondLen <= nums.length <= 1000
* 0 <= nums[i] <= 1000

### 思路：

```javascript
/**
 * @param {number[]} nums
 * @param {number} firstLen
 * @param {number} secondLen
 * @return {number}
 */
var maxSumTwoNoOverlap = function(nums, firstLen, secondLen) {
    let res = 0, n = nums.length
    let arr = Array(n+1).fill(0)
    for(let i = 0; i<n;i++){
        arr[i+1] = arr[i] + nums[i]
    }
    for(let i = firstLen, t = 0; i + secondLen - 1 < n; i++){
        t = Math.max(t,arr[i] - arr[i-firstLen])
        res = Math.max(res, t + arr[i+secondLen] - arr[i])
    }
    for(let i = secondLen, t = 0; i + firstLen - 1 < n; i++){
        t = Math.max(t,arr[i] - arr[i-secondLen])
        res = Math.max(res, t + arr[i+firstLen] - arr[i])
    }
    return res
};
```

