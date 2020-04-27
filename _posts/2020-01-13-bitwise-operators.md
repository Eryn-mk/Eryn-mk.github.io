---
layout:     post
title:      "Bitwise Operators"
subtitle:   "位运算笔记"
date:       2020-01-13
author:     "Eryn"
tags:
    - Coding Interview
    - Computer Science
    - Leetcode
    - Algorithm
---
# Bitwise Operators
----
used to perform manipulation of individual bits of a number   
can be used with any of the integral types (char, short, int, etc).   
used when performing update and query operations of Binary indexed tree.

#### OR (|)
binary operator    
if either bit is 1, then 1, else 0   
#### AND (&)   
binary operator   
if both bit are 1, then 1, else 0   
#### XOR (^)   
binary operator   
if bits are different, then 1, else 0   
#### Complement (~)   
unary operator
makes every 0 to 1, every 1 to 0    
compiler will give 2's complement of that number, i.e., input 10, output -6   
    
## Shift Operators
----
#### Signed Right Shift (>>)   
Shifts the bits of the number to the right and fills 0 on voids left as a result. The leftmost bit depends on the sign of initial number.   
**preserve the sign bit**   

#### Unsigned Right Shift (>>>)   
Shifts the bits of the number to the right and fills 0 on voids left as a result. The leftmost bit is set to 0.   
**DOES NOT preserve the sign bit**   

#### Signed Left Shift (<<)   
there is no <<< in java, because the logical << and arithmetic left-shift <<< operations are identical

##### 136. Single Number   
**Given a non-empty array of integers, every element appears twice except for one. Find that single one.**   
If we take XOR of zero and some bit, it will return that bit   
* a⊕0=a
If we take XOR of two same bits, it will return 0   
* a⊕a=0
* a⊕b⊕a=(a⊕a)⊕b=0⊕b=b
So we can XOR all bits together to find the unique number.   
```java
class Solution {
    public int singleNumber(int[] nums) {
        int a = 0;
        for (int i : nums) {a ^= i;}
        return a;
```


