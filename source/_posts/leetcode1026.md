---
title: 1026. 节点与其祖先之间的最大差值 - 每日一题0418
cover: https://w.wallhaven.cc/full/0j/wallhaven-0jlz9p.jpg
banner:
  type: img
  bgurl: https://pic1.zhimg.com/v2-b3c2c6745b9421a13a3c4706b19223b3_r.jpg
  bannerText: 每日一题 04-18
categories:
  - leetcode
tags:
  - leetcode
  - 每日一题
date: 2023-04-18 14:23:40
author: 菜鸟书生
keywords: 数,深度优先搜索,二叉树
toc: false
---
[力扣题目链接](https://leetcode.cn/problems/maximum-difference-between-node-and-ancestor/)

**给定二叉树的根节点 root，找出存在于 不同 节点 A 和 B 之间的最大值 V，其中 V = |A.val - B.val|，且 A 是 B 的祖先。**

**（如果 A 的任何子节点之一为 B，或者 A 的任何子节点是 B 的祖先，那么我们认为 A 是 B 的祖先）**

#### 示例1：

![1681810158883](image/leetcode1026/1681810158883.png)

```
输入：root = [8,3,10,1,6,null,14,null,null,4,7,13]
输出：7
解释： 
我们有大量的节点与其祖先的差值，其中一些如下：
|8 - 3| = 5
|3 - 7| = 4
|8 - 1| = 7
|10 - 13| = 3
在所有可能的差值中，最大值 7 由 |8 - 1| = 7 得出。
```

#### 示例2：

![1681810167515](image/leetcode1026/1681810167515.png)

```
输入：root = [1,null,2,null,0,3]
输出：3
```

#### 提示：

* 树中的节点数在 `2` 到 `5000` 之间。
* `0 <= Node.val <= 10<sup>5</sup>`

### 思路：

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxAncestorDiff = function(root) {
    let diff = 0
    const diffData = (node,min,max) =>{
        if(!node) return 0
        diff = Math.max(Math.abs(node.val-min),Math.abs(node.val-max))
        min = Math.min(min,node.val)
        max = Math.max(max,node.val)
        diff = Math.max(diff,diffData(node.left,min,max)) 
        diff = Math.max(diff,diffData(node.right,min,max)) 
        return diff
    }
  
    return diffData(root,root.val,root.val)
};
```

### 总结：

#### 复杂度

- 时间复杂度
- 时间复杂度：O(n)，其中n 是二叉树的节点数目。遍历二叉树的所有节点需要O(n)。
- 空间复杂度：O(n)。最坏情况下，二叉树退化为链表，递归栈的空间为O(n)。
