---
title: 1100. 长度为 K 的无重复字符子串
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
date: 2023-04-24 15:27:27
keywords: 哈希表, 字符串, 滑动窗口
cover: https://w.wallhaven.cc/full/3z/wallhaven-3zkold.jpg
toc: false
---

## 1100. 长度为 K 的无重复字符子串
> [尊享面试 100 题](https://dwmorning.github.io/leetcodeVipInterview)是Leetcode会员专享题单

[力扣题目链接](https://leetcode.cn/problems/find-k-length-substrings-with-no-repeated-characters/?envType=study-plan-v2&id=premium-algo-100)
给你一个字符串 S，找出所有长度为 K 且不含重复字符的子串，请你返回全部满足要求的子串的 数目。

#### **示例 1：**
```
输入：S = "havefunonleetcode", K = 5
输出：6
解释：
这里有 6 个满足题意的子串，分别是：'havef','avefu','vefun','efuno','etcod','tcode'。
```
#### **示例 2：**
```
输入：S = "home", K = 5
输出：0
解释：
注意：K 可能会大于 S 的长度。在这种情况下，就无法找到任何长度为 K 的子串。
``` 

**提示：**
* 1 <= S.length <= 10^4
* S 中的所有字符均为小写英文字母
* 1 <= K <= 10^4

### 思路
#### 暴力解法
```javascript
/**
 * @param {string} s
 * @param {number} k
 * @return {number}
 */
var numKLenSubstrNoRepeats = function(s, k) {
    if(s.length<k) return 0
    let arr = []
    for(let i = k-1; i<s.length;i++){
        let str = s.slice(i-k+1,i+1)
        let set = new Set(str.split(''))
        if(set.size === k){
            arr.push(str)
        }
    }
    return arr.length
};
```
#### 滑动窗口
```javascript
/**
 * @param {string} s
 * @param {number} k
 * @return {number}
 */
var numKLenSubstrNoRepeats = function(s, k) {
    if(s.length<k) return 0
    let right = 0
    let arr = [], res = 0
    while(right<s.length){
        arr.push(s[right])
        while(arr.indexOf(s[right]) !== arr.length-1){
            arr.shift()
        }
        if(arr.length>=k){
            res++
        }
        right++
    }
    return res
};
```