---
title: 1027. 最长等差数列
author: 菜鸟书生
banner:
  type: img
  bgurl: https://pic1.zhimg.com/v2-b3c2c6745b9421a13a3c4706b19223b3_r.jpg
  bannerText: 每日一题
categories:
  - leetcode
tags:
  - 每日一题
  - leetcode
date: 2023-04-22 16:32:58
keywords: 数组, 哈希表, 二分查找, 动态规划
# cover: https://w.wallhaven.cc/full/yj/wallhaven-yj7wqk.jpg
toc: false
---

## 1043. 分隔数组以得到最大和
[力扣题目链接](https://leetcode.cn/problems/longest-arithmetic-subsequence/)

给你一个整数数组 nums，返回 nums 中最长等差子序列的长度。

回想一下，nums 的子序列是一个列表 nums[i1], nums[i2], ..., nums[ik] ，且 0 <= i1 < i2 < ... < ik <= nums.length - 1。并且如果 seq[i+1] - seq[i]( 0 <= i < seq.length - 1) 的值都相同，那么序列 seq 是等差的。

#### **示例 1：**

```
输入：nums = [3,6,9,12]
输出：4
解释： 
整个数组是公差为 3 的等差数列。
```

#### **示例 2：**

```
输入：nums = [9,4,7,2,10]
输出：3
解释：
最长的等差子序列是 [4,7,10]。
```

#### **示例 3：**

```
输入：nums = [20,1,15,3,10,5,8]
输出：4
解释：
最长的等差子序列是 [20,15,10,5]。
```

**提示：**

* `2 <= nums.length <= 1000`
* `0 <= nums[i] <= 500`

### 思路：

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var longestArithSeqLength = function(nums) {
    let n = nums.length
    let dp = Array(n).fill(0).map(()=>new Map())
    let res = 0
    for(let i = 1; i<n;i++){
        for(let j = 0; j<i;j++){
            let seq = nums[i] - nums[j]
            let count = dp[j].get(seq) || 1
            dp[i].set(seq,count+1)
            res = Math.max(res,count+1)
        }
    }
    return res

};
```
