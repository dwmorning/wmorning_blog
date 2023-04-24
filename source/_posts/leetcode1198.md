---
title: 1198. 找出所有行中最小公共元素
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
date: 2023-04-24 15:44:11
keywords: 数组, 二分查找, 哈希表, 计数矩阵
cover: https://w.wallhaven.cc/full/od/wallhaven-od95m7.jpg 
toc: false
---


## 1198. 找出所有行中最小公共元素
> [尊享面试 100 题](https://dwmorning.github.io/leetcodeVipInterview)是Leetcode会员专享题单

[力扣题目链接](https://leetcode.cn/problems/find-smallest-common-element-in-all-rows/)
给你一个 m x n 的矩阵 mat，其中每一行的元素均符合 严格递增 。请返回 所有行中的 最小公共元素 。
如果矩阵中没有这样的公共元素，就请返回 -1。

#### **示例 1：**
```
输入：mat = [[1,2,3,4,5],[2,4,5,8,10],[3,5,7,9,11],[1,3,5,7,9]]
输出：5
```
#### **示例 2：**
```
输入：mat = [[1,2,3],[2,3,4],[2,3,5]]
输出： 2
``` 

**提示：**
* m == mat.length
* n == mat[i].length
* 1 <= m, n <= 500
* 1 <= mat[i][j] <= 104
* mat[i] 已按严格递增顺序排列。

### 思路
#### 暴力解法
```javascript
/**
 * @param {number[][]} mat
 * @return {number}
 */
var smallestCommonElement = function(mat) {
    let map = new Map()
    let m = mat.length, n = mat[0].length
    for(let i = 0;i<m;i++){
        for(let j = 0; j< n;j++){
            if(i === 0){
                map.set(mat[i][j],1)
            }else{
                if(map.has(mat[i][j])){
                    map.set(mat[i][j],map.get(mat[i][j]) + 1)
                }
            }
        }
    }
    for(let [key,value] of map.entries()){
        if(value === m){
            return key
        }
    }
    return -1
};
```