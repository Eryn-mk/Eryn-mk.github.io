---
layout:     post
title:      "Binary Search Problems"
subtitle:   "二分搜索法和题目总结"
date:       2019-11-23
author:     "Eryn"
tags:
    - Leetcode
    - Binary Search
    - Algorithm
---

## Binary Search
-------------

### Last Position of Target

leetcode 34 Find first and last position of element in sorted array       
* find first 一直往左靠，向头部靠，当```nums[mid]==target```时```right = mid```
* find last 一直往右靠，末尾靠，当```nums[mid]==target```时```left = mid```
* 这个方法```while(start + 1 < end)```保证永远不会错
* 该方法最后的缺点是：只知道最后结果在end与start这两个index中，但不知道是哪一个，所以if一下，如果都不在就```return -1；```


### Find Peak Element
* array不为空
* 中间找不到peak时，最后会走向array的两个端点，其中一个成为peak
* mid只与前一位比较，不用和后面的比较

### First Bad Version


### Search in Rotated Sorted Array (no duplicates)
### Search in Rotated Sorted ArrayII (with duplicates)
* 和上一题相比， 会出现```nums[l] == nums[r] == nums[mid]```
* target = 3时会出现```[1,1,3,1] or [1,3,1,1] or [1,3,1,1,1]```
* 单独要讨论```nums[mid] == nums[l]```情况，这个情况下```l++```

### pow(x,n)    
* 取绝对值计算，然后如果n是负数，最后```return 1 / result```
* 因为```Integer.MIN_VALUE```最小值的绝对值比最大值大1，所以int要转换成long，```long longN = Math.abs((long)n);```
* 每次```longN >>= 1```右移一位，效果约等于除以2
* 如果不处理n是负数的情况，就会死循环，while loop会超时，递归写法会爆栈

### Search in a 2D matrix
每一行的后一个比前一个大，下一行的第一个比上一行的最后一个大，所以整个matrix可以看成是从第一行第一个到最后一行最后一个的排序序列。在这种条件下:    
* ```end = matrix.length * matrix[0].length - 1```
* 求了mid之后，这个mid是相对于整条序列而言，那么mid的位置表示为```row = mid / matrix[0].length; col = mid % matrix[0].length;```
* 最后验证l和r是否是target的时候，因为l和r都是相对于整条序列的index，所以求row和col的方法同上
### Maximum Number in Mountain Sequence

### Find K Closest Elements

### Search in a Big Sorted Array

### Fast Power
