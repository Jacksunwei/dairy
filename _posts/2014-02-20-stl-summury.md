---
layout: post
title: STL 常用知识
description: STL 常用知识
modified: 2014-02-20
tags: [leetcode, STL, 技巧]
image:
  feature: abstract-6.jpg
comments: true
share: true
---

*这篇文档用来记录STL中的常用知识*

基本操作
-----------

算法
----

* STL二分搜索(binary_search)，执行一下操作是都要假定范围内已按顺序排好序 

    * `lower_bound(first, last, &val)` - 返回[first, last)中第一个不比`val`值小的迭代器
    * `upper_bound(first, last, &val)` - 返回[first, last)中第一个比`val`值大的迭代器 
    * `binary_search(first, last, &val)` - 在[first, last)区间内，二分查找`val`值，找到返回`true`，否则返回`false`

* `lower_bound(first, last, &val)`的实现：

{% highlight cpp %}
template <class ForwardIterator, class T>
  ForwardIterator lower_bound (ForwardIterator first, ForwardIterator last,
                               const T& val) 
{
    while (first != last) {
        auto mid = next(first, distance(first, last) / 2);
        if (*mid < val) first = ++mid; // 这里是++mid
        else last = mid;
    }
    return first;
}
{% endhighlight %}

* `upper_bound(first, last, &val)`的实现

{% highlight cpp %}
template <class ForwardIterator, class T>
  ForwardIterator upper_bound (ForwardIterator first, ForwardIterator last,
                               const T& val) 
{
    while (first != last) {
        auto mid = next(first, distance(first, last) / 2);
        if (*mid <= val) first = ++mid; // 只有这里与lower_bound不同
        else last = mid;
    }
    return first;
}
{% endhighlight %}


迭代器
-----

* 迭代器的操作：

    * `void advance (InputIterator& it, Distance n)`将`it`向前迭代`n`步
    * `iterator prev(itr, step = 1)`和`iterator next(itr, step = 1)`，向前或向后迭代`step`步，并返回一个更新的迭代器。

容器
----

* 常用的容器：

    * `vector` - 动态数组
    * `list` - 双向链表
    * `map` - 有序映射
    * `unordered_map` - hash map

* 常用容器的常用方法：

    * `push_back(const value_type& val)`, `pop_back()`
    * `std::list::push_front(const value_type& val)`, `std::list::pop_front()`
    * `remove()`和`erase()`方法的区别，`remove()`方法接受值类型，`erase()`方法接受迭代器类型，而且`erase()`方法更为普遍。(参见`map::erase()`和`list::remove()`)
    * *to be continued...*

* [unordered_map](http://www.cplusplus.com/reference/unordered_map/unordered_map/) 要点如下：
    
    * `find(key)` - 返回`unordered_map::iterator`; 没有返回`unordered_map::end()`
    * `map`和`unordered_map`的迭代器通过`itr->first`来访问`key`，通过`itr->second`来访问`value`
    * `operator[]` - 如果没有，会自动增加元素
    * `at(key)` - 如果没有，会抛异常

