---
title: 161. 相隔为 1 的编辑距离
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
date: 2023-04-23 14:00:05
keywords: 双指针, 字符串
cover: https://w.wallhaven.cc/full/4g/wallhaven-4gy2l7.jpg
toc: false
---
> [尊享面试 100 题](https://dwmorning.github.io/leetcodeVipInterview)是Leetcode会员专享题单

## 161. 相隔为 1 的编辑距离
[力扣题目链接](https://leetcode.cn/problems/one-edit-distance/)
给定两个字符串 s 和 t ，如果它们的编辑距离为 1 ，则返回 true ，否则返回 false 。
字符串 s 和字符串 t 之间满足编辑距离等于 1 有三种可能的情形：
- 往 s 中插入 恰好一个 字符得到 t
- 从 s 中删除 恰好一个 字符得到 t
- 在 s 中用 一个不同的字符 替换 恰好一个 字符得到 t

#### **示例 1：**
```
输入: s = "ab", t = "acb"
输出: true
解释: 可以将 'c' 插入字符串 s 来得到 t。
```
#### **示例 2：**
```
输入: s = "cab", t = "ad"
输出: false
解释: 无法通过 1 步操作使 s 变为 t。
```

**提示:**
- 0 <= s.length, t.length <= 10<sup>4</sup>
- s 和 t 由小写字母，大写字母和数字组成

### 思路
```javascript
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isOneEditDistance = function(s, t) {
    let slen = s.length
    let tlen = t.length
    if(Math.abs(slen - tlen) > 1) return false
    for(let i =0; i< Math.min(slen,tlen);i++){
        if(s[i] !== t[i]){
            if(slen < tlen){
                return s.substring(i) === t.substring(i+1)
            }else if(slen === tlen){
                return s.substring(i+1) === t.substring(i+1)
            }else{
                return s.substring(i+1) === t.substring(i)
            }
        }
    }
    return slen !== tlen
};
```