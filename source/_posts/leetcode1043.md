---
title: 1043. 分隔数组以得到最大和
author: 菜鸟书生
cover: https://w.wallhaven.cc/full/01/wallhaven-01mj83.jpg
banner:
  type: img
  bgurl: https://pic1.zhimg.com/v2-b3c2c6745b9421a13a3c4706b19223b3_r.jpg
  bannerText: 每日一题 04-19
categories:
  - leetcode
tags:
  - 每日一题
  - leetcode
date: 2023-04-19 09:52:31
keywords: 数组, 动态规划
toc: false
---
## 1043. 分隔数组以得到最大和

给你一个整数数组 `arr`，请你将该数组分隔为长度 **最多 **为 k 的一些（连续）子数组。分隔完成后，每个子数组的中的所有值都会变为该子数组中的最大值。

返回将数组分隔变换后能够得到的元素最大和。本题所用到的测试用例会确保答案是一个 32 位整数。

#### **示例 1：**

```
输入：arr = [1,15,7,9,2,5,10], k = 3
输出：84
解释：数组变为 [15,15,15,9,10,10,10]
```

#### **示例 2：**

```
输入：arr = [1,4,1,5,7,3,6,1,9,9,3], k = 4
输出：83
```

#### **示例 3：**

```
输入：arr = [1], k = 1
输出：1
```

**提示：**

* 1 <= arr.length <= 500
* 0 <= arr[i] <= 10 `<sup>`9 `</sup>`
* 1 <= k <= arr.length

### 思路：

```javascript
/**
 * @param {number[]} arr
 * @param {number} k
 * @return {number}
 */
var maxSumAfterPartitioning = function(arr, k) {
    let len = arr.length
    if(len <= k) return Math.max(...arr) * len
    let dp = Array(len+1).fill(0)
    for(let i = 1; i <= len; i++){
        let max = 0
        for(let j = i - 1; j >= Math.max(0, i - k); j--){
            max = Math.max(max,arr[j])
            dp[i] = Math.max(dp[i], dp[j] + max * (i - j)) 
        }
    }
    return dp[len]
};
```
