---
layout:     post
title:      "Leetcode 242 Valid Anagram "
subtitle:   "力扣242笔记：有效的字母异位词"
date:       2020-01-04
author:     "Eryn"
tags:
    - Java
    - Java Basics
    - Hash Table
    - Data Structure
---

作为hash table的方法之一，什么是ASCII？
为什么 ```int[] hashtable = new int[128]/[256] then hashtable[某些char```



##### 242. Valid Anagram   
**Given two strings s and t , write a function to determine if t is an anagram of s**   
approach 1: sorting   
approach 2: hash table (implemented by int[])   

Sorting: 
```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) {
        return false;
    }
    char[] str1 = s.toCharArray();
    char[] str2 = t.toCharArray();
    Arrays.sort(str1);
    Arrays.sort(str2);
    return Arrays.equals(str1, str2);
}
```
Time complexity : O(n \log n)O(nlogn). Assume that nn is the length of ss, sorting costs O(n \log n)O(nlogn) and comparing two strings costs O(n)O(n). Sorting time dominates and the overall time complexity is O(n \log n)O(nlogn).   

Space complexity : O(1)O(1). Space depends on the sorting implementation which, usually, costs O(1)O(1) auxiliary space if heapsort is used. Note that in Java, toCharArray() makes a copy of the string so it costs O(n)O(n) extra space, but we ignore this for complexity analysis because:   
* It is a language dependent detail.<font color = red>??????????</font>
* It depends on how the function is designed. For example, the function parameter types can be changed to char[].   
Hash table   
```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) {
        return false;
    }
    int[] counter = new int[26];
    for (int i = 0; i < s.length(); i++) {
        counter[s.charAt(i) - 'a']++;
        counter[t.charAt(i) - 'a']--;
    }
    for (int count : counter) {
        if (count != 0) {
            return false;
        }
    }
    return true;
```
time: O(n)   
space: O(1) Although we do use extra space, the space complexity is O(1)O(1) because the table's size stays constant no matter how large nn is.   

####



### Tips
* to traverse each character of a string   
```java
for (char i : S.toCharArray())
```
* to take digits off the number one by one until none remain     
e.g. 求某个数字的每一位digit的平方和，27-> 4+49 = 53    
```java
 private int getNext(int n) {
        int totalSum = 0;
        while (n > 0) {
            int d = n % 10; //得到最右一位/个位数
            n = n / 10;  // 去掉最右一位/百位变十位/十位变个位
            totalSum += d * d;
        }
        return totalSum;

time complexity: O(logn)
```
* anagram   
相同字母异序词   
e.g. cat - act   

* removeAll(collection) 会去除所有有交集的元素   
* 从string中取出空格隔开的数据   
```java
String str = "dog cat mouse";
String[] s = str.split(" ");
```
