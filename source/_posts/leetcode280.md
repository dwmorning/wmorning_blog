---
title: 280. 摆动排序
author: 菜鸟书生
banner:
  type: img
  bgurl: https://pic1.zhimg.com/v2-b3c2c6745b9421a13a3c4706b19223b3_r.jpg
  bannerText: 尊享面试 100 题
categories:
  - leetcode
tags:
  - leetcode
  - 尊享面试 100 题
date: 2023-04-20 14:32:16
keywords: 贪心, 数组, 排序
cover: https://w.wallhaven.cc/full/we/wallhaven-we61wq.jpg
toc: false
---
> [尊享面试 100 题](https://dwmorning.github.io/leetcodeVipInterview)是Leetcode会员专享题单

## 280. 摆动排序
[力扣题目链接](https://leetcode.cn/problems/wiggle-sort/?envType=study-plan-v2&id=premium-algo-100)
给你一个的整数数组 nums, 将该数组重新排序后使 nums[0] <= nums[1] >= nums[2] <= nums[3]... 
输入数组总是有一个有效的答案。

#### **示例 1：**
```
输入：nums = [3,5,2,1,6,4]
输出：[3,5,1,6,2,4]
解释：[1,6,2,5,3,4]也是有效的答案
```
#### **示例 2：**
```
输入：nums = [6,6,5,6,3,8]
输出：[6,6,5,6,3,8]
```

**提示：**
* 1 <= nums.length <= 5 * 10<sup>4</sup>
* 0 <= nums[i] <= 10<sup>4</sup>
* 输入的 nums 保证至少有一个答案。

### 思路：
先排序，再两两交换

```javascript
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var wiggleSort = function(nums) {
    nums = nums.sort((a,b)=>a-b)
    let n = nums.length
    for(let i = 2; i< n;i += 2){
        [nums[i],nums[i-1]] = [nums[i-1],nums[i]]
    }
    // return nums
};
```