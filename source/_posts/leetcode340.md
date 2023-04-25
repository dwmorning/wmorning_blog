---
title: 340. 至多包含 K 个不同字符的最长子串
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
date: 2023-04-25 13:59:19
keywords: 哈希表，字符串，滑动窗口
cover: https://w.wallhaven.cc/full/gj/wallhaven-gj968l.jpg
toc: false
---
> [尊享面试 100 题](https://dwmorning.github.io/leetcodeVipInterview)是Leetcode会员专享题单
## 340. 至多包含 K 个不同字符的最长子串
[力扣题目链接](https://leetcode.cn/problems/longest-substring-with-at-most-k-distinct-characters/)
给你一个字符串 s 和一个整数 k ，请你找出 至多 包含 k 个 不同 字符的最长子串，并返回该子串的长度。 

#### **示例 1：**
```
输入：s = "eceba", k = 2
输出：3
解释：满足题目要求的子串是 "ece" ，长度为 3 。
```
#### **示例 2：**
```
输入：s = "aa", k = 1
输出：2
解释：满足题目要求的子串是 "aa" ，长度为 2 。
```

**提示：**
* 1 <= s.length <= 5 * 10<sup>4</sup>
* 0 <= k <= 50

### 思路：

```javascript
/**
 * @param {string} s
 * @param {number} k
 * @return {number}
 */
var lengthOfLongestSubstringKDistinct = function(s, k) {
    let n = s.length
    if(s.length < k) return n
    let left = 0, right = 0, max= 0
    let map = new Map()
    while(right < n){
        if(map.size<k+1) map.set(s[right],right++)
        if(map.size === k + 1){
            let minKey, minValue = Infinity
            for(let [key,value] of map.entries()){
                if(minValue>value){
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