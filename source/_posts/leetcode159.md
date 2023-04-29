---
title: 159. 至多包含两个不同字符的最长子串
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
date: 2023-04-24 14:47:10
keywords: 哈希表, 字符串, 滑动窗口
# cover: https://w.wallhaven.cc/full/3l/wallhaven-3l9zy3.jpg
toc: false
---
## 159. 至多包含两个不同字符的最长子串
> [尊享面试 100 题](https://dwmorning.github.io/leetcodeVipInterview)是Leetcode会员专享题单

[力扣题目链接](https://leetcode.cn/problems/longest-substring-with-at-most-two-distinct-characters/)
给你一个字符串 s ，请你找出 至多 包含 两个不同字符 的最长子串，并返回该子串的长度。

#### **示例 1：**
```
输入：s = "eceba"
输出：3
解释：满足题目要求的子串是 "ece" ，长度为 3 。
```
#### **示例 2：**
```
输入：s = "ccaabbb"
输出：5
解释：满足题目要求的子串是 "aabbb" ，长度为 5 。
``` 

**提示：**
* 1 <= s.length <= 10<sup>5</sup>
* s 由英文字母组成

### 思路
```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstringTwoDistinct = function(s) {
    let n = s.length
    if(n < 3) return n
    let left = 0, right = 0, max = 2
    let map = new Map()
    while(right < n){
        if(map.size < 3) map.set(s[right],right++)
        if(map.size === 3){
            let minKey,minValue = Infinity
            for(let [key,value] of map.entries()){
                if(minValue > value){
                    minValue = value
                    minKey = key
                }
            }
            map.delete(minKey)
            left = minValue + 1
        }
        max = Math.max(max,right-left)
    }
    return max
};
```