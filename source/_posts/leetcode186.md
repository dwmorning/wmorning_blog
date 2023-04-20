---
title: 186. 反转字符串中的单词 II
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
date: 2023-04-20 15:44:58
keywords: 双指针, 字符串
cover: https://w.wallhaven.cc/full/r7/wallhaven-r71zwq.jpg
toc: false
---
> [尊享面试 100 题](https://dwmorning.github.io/leetcodeVipInterview)是Leetcode会员专享题单

## 186. 反转字符串中的单词 II
[力扣题目链接](https://leetcode.cn/problems/reverse-words-in-a-string-ii/?envType=study-plan-v2&id=premium-algo-100)

给你一个字符数组 s ，反转其中 单词 的顺序。
单词 的定义为：单词是一个由非空格字符组成的序列。s 中的单词将会由单个空格分隔。
必须设计并实现 原地 解法来解决此问题，即不分配额外的空间。


#### **示例 1：**
```
输入：s = ["t","h","e"," ","s","k","y"," ","i","s"," ","b","l","u","e"]
输出：["b","l","u","e"," ","i","s"," ","s","k","y"," ","t","h","e"]
```
#### **示例 2：**
```
输入：s = ["a"]
输出：["a"]
```

**提示：**
* 1 <= s.length <= 105
* s[i] 可以是一个英文字母（大写或小写）、数字、或是空格 ' ' 。
* s 中至少存在一个单词
* s 不含前导或尾随空格
* 题目数据保证：s 中的每个单词都由单个空格分隔

### 思路：
本来想直接一行实现，但是需要在原地实现如下：

```javascript
var reverseWords = function(s) {
    return s.join('').split(' ').reverse().join(' ').split('')
};
```
那么则先将数组整体反转，再将单词反转即可
```javascript
/**
 * @param {character[]} s
 * @return {void} Do not return anything, modify s in-place instead.
 */
var reverseWords = function(s) {
    // return s.join('').split(' ').reverse().join(' ').split('')
    s.reverse()
    const reverseFun = (left,right)=>{
        while(left < right){
            [s[left],s[right]] = [s[right],s[left]]
            left++
            right--
        }
    }
    let start = 0
    for(let i = 0; i<= s.length;i++){
        if(s[i] === ' ' || i === s.length){
            reverseFun(start,i-1)
            start = i + 1
        }
    }
};
```