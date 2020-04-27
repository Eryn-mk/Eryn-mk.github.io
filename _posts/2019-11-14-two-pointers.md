---
layout:     post
title:      "'LinkedList' in Java"
subtitle:   "理解Java中的链表“
date:       2019-11-14
author:     "Eryn"
tags:
    - Java
    - Leetcode
    - Java Basics
    - LinkedList
    - Data Structure
---

## LinkedList
### LinkedList cycle
**检测链表中是否有环/环的入口**    
![LinkedList Cycle](https://img-blog.csdn.net/20160107192700740)
* 第一次快指针（一次两步）和慢指针（一次一步）一起从头开始走
* 第一次相遇的点Pos意义：快指针走的路程是慢指针的两倍 
> 快指针路程 (LenA + x + y + x) = 2 * (LenA + x) 慢指针路程     
> 所以得到：y + x = LenA + x 所以 y = LenA
    * 
  ``` java
    ListNode fast = head;
    ListNode slow = head;
    while (fast != null && fast.next != null) {
        fast = fast.next.next;
        slow = slow.next;
    }
  ```
* 快指针回到原点，慢指针留在Pos
* 两个指针都（一次一步）走，直到相遇Join点
* 第二次相遇的点Join意义：环的入口
> 因为 y = LenA， 所以同样速度的两个指针必然在Join相遇
    * 
  ```java
    fast = head;
    while (fast != slow) {
        fast = fast.next;
        slow = slow.next;
    }
  ```


-------------------
## Two Pointers
--------------------
### Middle of Linked List
* return slow pounter

### Two Sum III - Data structure design
* 实现两个方法void add(bumber)和boolean find(targetSum)
* 因为第二个方法是在存了的数字中找到两个数字，其数字之和等于target；可用到头尾指针
* 头尾指针遍历：两指针之和 > target就right--; 之和 < target就left++；
* 因为上述遍历方式，储存时要保持一个sorted状态（比如sorted array）

----------------------
### Move Zeroes

-------------------------
### Remove Duplicate Numbers in Array
* p1 的意义：左边和自己都没有duplicates
* p2 的意义：去找unique

-------------------------
### Sort Colors II
* 用extra space：bucket sort。建立一个array，index分别是0，1，2；然后遍历一次，遇到哪个就相应++；最后重新遍历，根据你新array的计数赋值
* 然后constant space: pointers，一个头，一个尾，一个从头到尾traverse，**重点在于traversal的指针什么时候++？**
    * 和红色（0）swap时，都++；
    * 和蓝色（2）swap时，只有蓝色指针--；
    * 如果值为1，就单纯++；不管红蓝色指针的事情
* 可以不用else，三种情况都用if，但是一定要记得continue，不然swap之后值就变了，如果进入到下面的if就乱了。每一次loop只操作一个颜色。
* 朝纲：rainbow sort

-----------------------
### Longest Substring Without Repeating Characters I
* Hash table || two pointers || sliding window
* 建一个char array作为hash table，关于size，如果是ASCII就是128， 如果是ASCII extend就是256

核心：
* ```pointer i & pointer j``` j跑在前面，所以```while (j < s.length())``` j遍历并在array中储存该char出现的次数
* 判断char出现的次数有没有超过要求？```if valid```就计算这个substring length 且更新maxlength；```j++```
* 如果次数超过要求```if not valid```，移动pointer i，```while(i < j)```i遍历的char在array中的次数相应减一，如果当前遍历到的是j停留的那个超出要求次数的char，说明此时整个substring已经valid，```i++; j++``` 然后break
* 后面这个while loop记得i++；毕竟外循环是移动i，也就是左边界
* 最后return maxLen

### 变形：Longest Substring with at most two distinct characters
---------------
### Sort Integers II
### Two Sum II - Input array is sorted

### 3Sum
### Partition Array
### Kth Largest Element
-------------------------
### Majority Element
* 题目定义majority element是指数量大于```size / 2```
* 题目假定input有效不为空，且majority element一定有
* 注意：**一定只有一个** 因为n个元素，有一种的数量大于一半，就再也不会有第二种的数量更多。最多只能是刚好小于一半。

* 如果sort，直接```return nums[nums.length / 2]```因为不管这个数字本身排序第几，因为它是majority，排序后一定在```length / 2```的位置上。极端情况是0和length-1，也依然可以擦这边排在该位置。所以不会错。
    * 这个方法前提是‘majority element always exist’！ 否则n为偶数时，正好等于n/2也会在这个位置
* 不sort，可用类似**消元**的概念，for loop从1开始，count从1开始
    * 如果count = 0 （说明上一个循环里减掉了，前一个majority没有经历住考研），那么```majority = nums[i]``` ，count = 1， continue到下一次循环。
    * 如果当前仍然是majority，count++； 否则count--；
    * 为什么不一样时要count--？因为如果这个是我们要找的majority，那他遇到不一样的元素而全部消耗完异类的数量，他也会至少留count = 1，他本身的总数是大于length/2的，大于其他异类的总数之和 
* 最后返回majority

**Boyer–Moore majority vote algorithm**

-------------------------
### Majority Element II
* 题目条件变为```length / 3```且要求linear time和constant space
* 注意；**最多只有两个** 因为数量**多于三分之一**，那三个majority总数就会**超过n**
* 设两个major对象，以及两个count分别记录；如果```nums[i]不等于任何一个，两个count都--```
* 有一个trick，用Integer作为两个major对象，没有赋值时为null，有赋值时可以和int直接比较。机智！！！

```java
  // using Moore majority voting algorithm
  for (int i = 0; i < n; i++) {
    if (m1 != null && a[i] == m1)      { c1++; } 
    else if (m2 != null && a[i] == m2) { c2++; }
    else if (c1 == 0)                  { m1 = a[i]; c1 = 1; }
    else if (c2 == 0)                  { m2 = a[i]; c2 = 1; } 
    else                               { c1--; c2--; }
  }
```
* 最后需要double check，重新遍历，计算c1，c2，是为了防止该数组**只有两种数字**的情况
* 最后在list中加入```count > n / 3```的major object，返回list
