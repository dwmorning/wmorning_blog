---
title: 2418. 按身高排序
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
date: 2023-04-25 09:51:30
keywords: 数组, 哈希表, 排序, 字符串
cover: https://w.wallhaven.cc/full/j8/wallhaven-j87ldq.jpg
toc: false
---

## 2418. 按身高排序
[力扣链接](https://leetcode.cn/problems/sort-the-people/)

给你一个字符串数组 names ，和一个由 互不相同 的正整数组成的数组 heights 。两个数组的长度均为 n 。
对于每个下标 i，names[i] 和 heights[i] 表示第 i 个人的名字和身高。
请按身高 降序 顺序返回对应的名字数组 names 。

 

#### **示例 1：**
```
输入：names = ["Mary","John","Emma"], heights = [180,165,170]
输出：["Mary","Emma","John"]
解释：Mary 最高，接着是 Emma 和 John 。
```
#### **示例 2：**
```
输入：names = ["Alice","Bob","Bob"], heights = [155,185,150]
输出：["Bob","Alice","Bob"]
解释：第一个 Bob 最高，然后是 Alice 和第二个 Bob 。
```

**提示：**
* n == names.length == heights.length
* 1 <= n <= 10<sup>3</sup>
* 1 <= names[i].length <= 20
* 1 <= heights[i] <= 10<sup>5</sup>
* names[i] 由大小写英文字母组成
* heights 中的所有值互不相同

### 思路
```javascript
/**
 * @param {string[]} names
 * @param {number[]} heights
 * @return {string[]}
 */
var sortPeople = function(names, heights) {
    let res = []
    let map = new Map()
    for(let i =0; i< names.length;i++){
        map.set(heights[i],names[i])
    }
    let arr = Array.from(map)
    arr.sort((a,b)=>b[0]-a[0])
    for(let [key,value] of arr.entries()){
        res.push(value[1])
    }
    return res
};
```