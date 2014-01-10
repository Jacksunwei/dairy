---
layout: post
title: Leetcode 技巧总结
description: "Leetcode 手记"
modified: 2014-01-05
tags: [leetcode, 技巧]
image:
  feature: abstract-6.jpg
comments: true
share: true
---

*这篇文档用来记录代码中的易错点和小技巧*

## 犯过的错误 ##
1. 使用指针时，应该用`->`，却用`.`访问方法
2. 准备弹栈时，用了`stack::top()`，却忘记`stack::pop()`
3. 没有画图，就想当然开始写代码，大忌！！！[Binary Tree Zigzag Level Order Traversal](http://oj.leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)


## 小技巧 ##
1. 互换元素不要用指针，而用STL模板`swap(&a, &b)`这样既清晰又不容易错

## 线性表类问题思路 ##
1. O(n)算法一般通过两边扫描可以实现
2. O(n<sup>2</sup>)及以上算法，可以先排序来简化问题。

## 位运算 ##
1. 异或 `^`

## 链表 ##
1. 为了使代码结构统一，链表一般要使用**头结点**，即`ListNode *head`


## STL 技巧 ##

* 迭代器操作

    * `prev(itr, step = 1)`和`next(itr, step = 1)`，向前或向后迭代`step`步

* STL二分搜索(binary_search)，执行一下操作是都要假定范围内已按顺序排好序 

    * `upper_bound(first, last, &val)` - 返回[first, last)中第一个比`val`值大的迭代器 (类似的有`lower_bound`)

    * `binary_search(first, last, &val)` - 在[first, last)区间内，二分查找`val`值，找到返回`true`，否则返回`false`

* [unordered_map](http://www.cplusplus.com/reference/unordered_map/unordered_map/) 要点如下：
    
    * `find(key)` - 返回`unordered_map::iterator`; 没有返回`unordered_map::end()`
    * `operator[]` - 如果没有，会自动增加元素
    * `at(key)` - 如果没有，会抛异常
