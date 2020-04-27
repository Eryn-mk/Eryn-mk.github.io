---
layout:     post
title:      "Default Interview Problems"
subtitle:   "常见技术面试题目总结"
date:       2019-11-26
author:     "Eryn"
tags:
    - Leetcode
    - Coding Interview
    - Algorithm
    - Data Structure
---

### longest palindrome
            
* 创建array存放所有的char，所以注意标注array的大小```int[] count = new int[256]```   
* 统计String中每一个char出现的次数```for (char c : s.toCharArray()) count[c]++;```
* 偶数可以全用上```total += even_number```
* 奇数中的偶数次可以用上```total += odd_number - 1```，odd=1，最后只能有```single one 1```个奇数字母
* ```return total + odd``` 就是把一个字母放在正中间 

--------------------
### implement strStr()
Return the index of the first occurrence of needle in haystack（草垛）, or -1 if needle is not part of haystack.    
<font color = red>应该问面试官·：如果needle是empty string应该返回什么？</font>         


-----------------------
### valid palindrome
* 应该考虑的问题是：case sensitive？ 
* alphaNumeric value可以自己写一个方法辨别，也可以用现成的```Character.isLetterOrDigit(char)```
```java
        private boolean isAlphaNumeric(char c) {
            return (c >= '0' && c<= '9') || (c >= 'a' && c <= 'z') || c >= 'A' && c <= 'Z');
        }
```
* case insensitive 时，将char换成小写用```Character.toLowerCase(char)```  


----------------------
### longest palindromic substring
* 中心扩散法，选定一个数当中心，向两边扩散开，对称地对比是否相同
* 注意以某个数为中心，有两种palindrome，都要approach，一个是奇数形式（中心只此一个），一个是偶数形式（所有都是两两成对）
* 对比长度，保留长的；注意用一个global String保留该子串，或者global int记录start index & end index，最后用于返回

    <font color = red>注意：</font>    
* 应该考虑一些题目没有明确的问题：
    1. case sensitive？
    2. 数字或者符号会出现吗？数字算吗？
    3. 返回的type是什么？如果是String，那么```input == String || input.length() == 0```时返回空字符串吗？    
    
* 应该test的情况：
    1. ```s.length() == 1 即 s = "a"```
    2. ```s = "aa"```

------------------------
### LRU
#### 常规写法
#### LinkedHashMap

------------------------

### LFU (Least Frequency Used)
当容量满了换出使用频率最少的那个，有tie再进一步取least recent，采用每个页使用的次数作为判断依据。进阶是O(1)时间复杂度，一般会考虑map     

实现get和put     
* ```get(key)```：返回指定key对应的value，如果指定key在cache中不存在，返回-1
* ```put(key, value)```：设置指定key的value，如果key不存在，则插入该key-value对。如果cache空间已满，则将最少使用的key-value对移除，如果存在多个key-value对的使用次数相同，则将上次访问时间最早的key-value对移除。

**思路：**       
* map1储存key - value
* map2储存key - frequency
* map3储存frequency - set of keys
* class中两个field: capacity，minFrequency

**get(int key)**
* 用map1查看key-value是否存在，不存在返回-1
* 得到key对应的freq，并得到freq对应的set，set里面删掉这个key（因为这个key的freq升级了！不能呆在这了，被get一次freq就+1）
* 如果原本这个freq是minFreq，而这个set删除后就空了，那么说明这个曾经的最小的freq后继无人-> 更新minFreq （会不会remove了freq = 1，但是下一个明明是3，可是freq++只到2）
* 再把这个key放到合适的位置去，该更新map2和map3，如果这个fre set还没有，就创建新的。可以用```frequencies.computeIfAbsent(frequency, k -> new LinkedHashSet<>()).add(key)```
    * computeIfAbsent & getOrDefault的区别是，前者已经modify map，后者返回了你给的default值，但如果要modify map，自己要put一次                

                                  
   **put(int key, int value)**
* 如果已经存在，overwrite map，然后用get方法更新即可（get更新的对象是map2和map3，不涉及第一个map）
* 如果不存在，要检验capacity是否满了，这一步在添加之后，因为判断删除的条件是size() > capacity. 为不是size() == capacity, 这是为了防止capacity = 0的现象出现（？？？）。记得用minFreq去删除（这是添加之前的minFreq）      
（奇怪的是LRU也会出现这个问题，但是LRU的case里面没有capacity = 0， 所以就能accept）       
* 添加完新的后，minFreq更新成1，因为新添加的元素频率都是1           

tips：
* LinkedHashSet里面是doubly linked list，insertion-order
* 为什么要用LinkedHashSet？当最后删除的时候，要选择同一个freq里面least recenly used这个用linked结构可以理解，但为什么要用set？会存在储存重复的情况吗？不可以用linkedlist吗

-------------------------
### Count primes

**埃拉托色筛选法**
1. 先把1删除（现今数学界1既不是质数也不是合数）
2. 读取队列中当前最小的数2，然后把2的倍数删去
3. 读取队列中当前最小的数3，然后把3的倍数删去
4. 读取队列中当前最小的数5，然后把5的倍数删去
5. 读取队列中当前最小的数7，然后把7的倍数删去
6. 如上所述直到需求的范围内所有的数均删除或读取



-------------------------
