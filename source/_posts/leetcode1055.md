---
title: 1055. 形成字符串的最短路径
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
date: 2023-04-23 14:24:06
keywords: 贪心，双指针，字符串
# cover: https://w.wallhaven.cc/full/45/wallhaven-45pe95.jpg
toc: false
---
> [尊享面试 100 题](https://dwmorning.github.io/leetcodeVipInterview)是Leetcode会员专享题单

## 1055. 形成字符串的最短路径
[力扣题目链接](https://leetcode.cn/problems/shortest-way-to-form-string)
对于任何字符串，我们可以通过删除其中一些字符（也可能不删除）来构造该字符串的 子序列 。(例如，“ace” 是 “abcde” 的子序列，而 “aec” 不是)。

给定源字符串 source 和目标字符串 target，返回 源字符串 source 中能通过串联形成目标字符串 target 的 子序列 的最小数量 。如果无法通过串联源字符串中的子序列来构造目标字符串，则返回 -1。

#### **示例 1：**
```
输入：source = "abc", target = "abcbc"
输出：2
解释：目标字符串 "abcbc" 可以由 "abc" 和 "bc" 形成，它们都是源字符串 "abc" 的子序列。
```
#### **示例 2：**
```
输入：source = "abc", target = "acdbc"
输出：-1
解释：由于目标字符串中包含字符 "d"，所以无法由源字符串的子序列构建目标字符串。
```
#### **示例 3：**
```
输入：source = "xyz", target = "xzyxz"
输出：3
解释：目标字符串可以按如下方式构建： "xz" + "y" + "xz"。
```

**提示：**
- 1 <= source.length, target.length <= 1000
- source 和 target 仅包含英文小写字母。

### 思路
```javascript
/**
 * @param {string} source
 * @param {string} target
 * @return {number}
 */
var shortestWay = function(source, target) {
    let res = 0, s = 0, t = 0
    while(t<target.length){
        if(source.indexOf(target[t]) === -1) return -1

        if(source[s] === target[t]){
            s++
            t++
        }else{
            s++
        }

        if(s>=source.length){
            res++
            s = 0
        }
    }
    if(t>=target.length && s!==0) res++
    return res
};
```
