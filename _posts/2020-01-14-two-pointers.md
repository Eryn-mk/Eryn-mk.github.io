---
layout:     post
title:      "Two-Pointers Problems"
subtitle:   "双指针题型总结“
date:       2020-01-14
author:     "Eryn"
tags:
    - Java
    - Leetcode
    - Two Pointers
    - Algorithm
---
# Two References
---
### <font face="微软雅黑">同向指针</font> 
两个指针从头到尾或从尾到头遍历  
第一个指针用于遍历  
第二个指针在满足一定掉条件移动    
sliding window   
### Problems
##### 1. 283 Move Zeroes (easy)  
**Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements**   
_fast pointer_: processing new elements  
_slow pointer_: the position of last found non-0 element  
find new non-0 elements and overwrite them at 'lastNonZero + 1'index  
fill all the rest indexes after 'lastNonZero' with 0s  
``` java  
space complexity: O(1) 
time complexity: O(n)     

        public void moveZeroes(int[] n) {
            int lastNonZero = 0;
            for (int j=0;j<n.length;j++) {
                if(n[j] != 0)
                    n[lastNonZero++] = n[j];
            }
            for (int j=lastNonZero;j<n.length;j++)
                n[j] = 0;
        }
```
_pointer1_: lastNonZero   
_pointer2_: processing   
if pointer2 is non-zero, swap, advance both   
all elements between 1 and 2 are zeroes  
``` java
space complexity: O(1)
time complexity: O(k)   
    k is the number of non-0 elements  
    so works better than last method when lots of zeroes
    works the same as O(n) when all elements are non-zero, k=n
    
        if (n[j] != 0) 
            swap(n[lastNonZero++],n[j]);
    
```
##### 2. 26 Removed Duplicates from Sorted Array (easy)   
**Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length**   
```java
        if (n[lastNonDup] != n[j])
            n[++lastNonDup] = n[j]];
```
##### 3. 80 Remove Duplicates from Sorted Array II (medium)   
**Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most *twice* and return the new length**   
pointer 1: next overwrittenable location   
pointer 2: processing, here as j  
var count: count of occurance of one element - min always be 1   
```java
space complexity: O(1)
time complexity: O(n) process each element once

    /*  i = 0;
        for j from 1 to length
        if n[j] == n[j-1], also count > 2, i keep still 
        if n[j] != n[j-1]  move element from j to ++i, count=1*/
        
        public int removeDuplicates(int[] n) {
            int i = 0      // ++i = ready be overwritten
            int count = 1  // minimum = 1
            for (int j=1; j<n.length; j++) {
                count = n[j]==n[j-1] ? count+1:1;
                if (count <=2)
                    n[++i] = n[j];
            }
            return i+1;
        }

```
##### 4. 349 Intersection of Two Arrays (easy)
**Given two arrays, write a function to compute their intersection**   
if two arrays are assumed sorted, can use two pointers   
if not, HashSet is easier
```java
        FAKE CODE
        use Arrays.sort(n1); Arrays.sort(n2);
        i for n1, j for n2
        if n1[i] == n2[j] list.add(this element) 
            then i++ j++;
        if n1[i] < n2[j] i++;
        if n1[2] > n2[j] j++;
```
##### 5. 350 Intersection of Two Arrays II (easy)
##### 6. 925 Long Pressed Name (easy) (String manipulation)  
Input: name = "alex", typed = "aaleex" || Output: true   
Input: name = "saeed", typed = "ssaa**e**dd" || Output: false
##### 7. 88 Merge Sorted Array (easy)
**Merged array nums2 to nums1 (both sorted, assume nums1 have enough space, m and n are the numbers of elements given)**   
"place" pointer starts from the end of nums1   
pointer i starts from m-1   
pointer j starts from n-1   
``` java
        while (i>=0 && j>=0) {...}
        System.arraycopy(nums1, 0, nums2, 0, j+1);
```
After while loop only to copy from nums2 to nums1, if all the rest smaller are in nums1, then nothing will be copied from nums2 **(those smaller already in place!!)**; otherwise all the rest smaller are in nums2 and then copied.
##### 844 Backspace String Compare (easy)   

##### 86 Partition List (medium)
play with reference; first time did O(N) space complexity, second time did O(1) space complexity. The difference is to add "after_tail.next = null" to get rid of whatever after the tail, otherwise out of time limit

##### 986 Interval List Intersections (medium)
**Given two lists of closed intervals, each list of intervals is pairwise disjoint and in sorted order. Return the intersection of these two interval lists.**

techniques: intersect of each interval    
Do not traverse all of the numbers in all intervals (time limit exceeded)

##### 209 Minimum Size Subarray Sum    
**Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ s. If there isn't one, return 0 instead.**  

##### 713 Subarray Product Less Than K (medium)   
**Given an array of positive integers nums.Count and print the number of (contiguous) subarrays where the product of all the elements in the subarray is less than k.**   

Solution: Sliding Window   
understand why result += right- left + 1   
每当右边到一个新的数，通过while调整左边，判断最大的区间, 然后计算包含最右这个数的所有子集, 即它自己, 它+前一个, 它+前一个+前前一个..., 所以数量=该区间元素数量=left-right+1   
```java
        class Solution {
            public int numSubarrayProd(int[] nums, int k) {
                if (k <= 1) return 0;
                int prod = 1, ans = 0, left = 0;
                for (int right = 0; right < nums.length; right++) {
                    prod *= nums[right];
                    while (prod >= k) prod /= nums[left++];
                    ans += right - left + 1;
                }
                return ans;
            }
        }
```

##### 826 Most Profit Assigning Work (medium)   

##### 930 Binary Subarrays With Sum (medium)   
**In an array A of 0s and 1s, how many non-empty subarrays have sum S?**    
同上，但是最后要看左边有多少个0，0不影响总和，却代表了不同的子集   
```java
        for (int i = left; sum==S && A[i] == 0 && i < right; i++)
                        result++;
```
##### 838 Push Dominoes (medium, low frequency)

---
### <font face="微软雅黑">快慢指针</font>    
若双指针以固定步长移动，如果第一个指针移动两步，第二个指针移动一步，成为快慢指针。   
常用于   
* 单向链表(Cycle): 如果有闭环，速度不一样的两个指针早晚会相遇   
* Loop判断

##### 26. Remove Duplicates from Sorted Array
##### 19. Remove Nth Node From End of List (medium)   
**Given a linked list, remove the n-th node from the end of list and return its head.**   
be aware of the conditon that [1,2] n=2, 就是返回结果是要删除第一个节点，此时用if直接head = head.next   

##### 141. Linked List Cycle (easy)   
**Given a linked list, determine if it has a cycle in it.To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.**   

Approach 1: HashTable, time O(N), space O(N)  
record each node's reference one by one in a hash table. If the current node is null means no cycle. If current node's reference is in the hash table, exist cycle.   
```java
        public boolean hasCycle(ListNode head) {
            Set<ListNode> nodesSeen = new HashSet<>();
            while (head != null) {
                if (nodesSeen.contains(head)) {
                    return true;
                } else {
                    nodesSeen.add(head);
                }
                head = head.next;
            }
            return false;
        }
```
Approach 2: Fast & Slow Pointers, time O(N+K), space O(1)   
if cyclic, 2 pointers eventually meet; if not cyclic, the fast pointer eventually reaches the end, and we return false.   
```java
        public boolean hasCycle(ListNode head) {
                ListNode fast = head;
                ListNode slow = head;

                while (fast != null && fast.next != null) {
                    fast = fast.next.next;
                    slow = slow.next;
                    if (fast == slow ) return true;
                }
                return false;
            }
```

##### 142. Linked List Cycle II (medium)   
**Given a linked list, return the node where the cycle begins. If there is no cycle, return null. To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.Do not modify the linked list.**     
Approach 1: hashtable, O(n), O(n)   
Approach 2: <font color = RED>Floyd's Tortoise and Hare,time O(n), space O(1)</font>   


##### 234. Palindrome Linked List (easy)   
**Given a singly linked list, determine if it is a palindrome.**   
Approach 1: deque, time O(n), space O(n)    
Approach 2: reverse second half in-space, time O(n), space O(1)   
Approach 3: copy to an ArrayList and 双向指针, O(n), O(n)   
Approach 4: <font color = RED>recursive (advanced), O(n), O(n)</font>
```java
        Approach 2 reverse second half in-space
        public boolean isPalindrome(ListNode head) {
            // Trivial case
            if(head == null || head.next == null) 
                return true;

            ListNode start = new ListNode(0);
            start.next = head;
            ListNode firstHalfStart = head;
            ListNode secondHalfStart = head;
            ListNode fast = head;

            /* Traverse to mid node and Reverse the First half 
            of the LinkedList in the same run*/
            while(fast.next != null && fast.next.next != null) {
                fast = fast.next.next;

                start.next = secondHalfStart.next;
                secondHalfStart.next = secondHalfStart.next.next;
                start.next.next = firstHalfStart;

                firstHalfStart = start.next;
            }

            /*Offset for odd number of elements
            As the mid node is common to both halves, 
            this should be skipped*/
            if(fast.next == null) {
                firstHalfStart = firstHalfStart.next;
            }

            /* At the end of the previous loop, 
             SecondHalfStart pointer is still stuck 
             on the end of the first half
             Shift it by one to take it to the start of the SecondHalf*/
            secondHalfStart = secondHalfStart.next;

            while(secondHalfStart != null) {
                if(firstHalfStart.val != secondHalfStart.val) 
                    return false;
                secondHalfStart = secondHalfStart.next;
                firstHalfStart = firstHalfStart.next;
            }
            return true;
        }
```
```java
        Approach 4 recursive   
        class Solution {

            private ListNode frontPointer;

            private boolean recursivelyCheck(ListNode currentNode) {
                if (currentNode != null) {
                    if (!recursivelyCheck(currentNode.next)) return false;
                    if (currentNode.val != frontPointer.val) return false;
                    frontPointer = frontPointer.next;
                }
                return true;
            }

            public boolean isPalindrome(ListNode head) {
                frontPointer = head;
                return recursivelyCheck(head);
            }
        }
```

##### 457. Circular Array Loop (medium)   
**given a circular array nums of positive and negative integers. Determine if there is a loop (or a cycle) in nums.**   


##### 287. Find the Duplicate Number    

---
### <font face="微软雅黑">反向指针</font>   
双指针其中一个从头、另一个从尾，两者往中间遍历。   

##### 344. Reverse String (easy)   
**Write a function that reverses a string. The input string is given as an array of characters char[].(in-place)**   
Approach 1: recursion   
Noted that recursion is not 'constant-space' due to the use of stack, but recursion is 'in-place'   
<font color = BLUE>**in place**: by definition, an in-place algorithm which transforms input **using no auxiliary data structure**.(but the space used by other actors other than data structures still means 'in-place')</font>    

Approach 2: Two pointers iteration: time O(n), space O(1)   

##### 125. Valid Palindrome   
**Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases. Define empty string as vaid palindrome**   

```java
string.toLowerCase();   
Character.idDigit(string.charAt(index));
Character.isLetter(string.charAt(index));
//Use Apache Commons Lang
StringUtils.isAlphanumeric(string);
Character.isLetterOrDigit(char);
```
##### 345. Reverse Vowels of a String (easy)   
**Write a function that takes a string as input and reverse only the vowels of a string.**    
vowel: 元音     
to check if a char is a vowel:   
```java
        public boolean isVowel(char c) {
          return "AEIOUaeiou".indexOf(c) != -1;
        }
````
to tranform a taken String into an Array
```java
        char[] c = s.toCharArray();
```

##### 61. Rotate List (medium)   
**Given a linked list, rotate the list to the right by k places, where k is non-negative.**    
Set a head and a tail, connect them: tail.next = head;   
new head's position: n - n%k   
new tail's position: n - n%k - 1   
so new_tail.next = new_head; only need to traverse n - n%k - 1 to find new_tail   

##### 75. Sort Colors (medium)   
**Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red(0), white(1) and blue(2).**   
Approach 1: two pass: two-pass algorithm using counting sort. First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's     
Approach 2: Move curr pointer along the array, if nums[curr] = 0 then swap it with nums[p0], if nums[curr] = 2 then swap it with nums[p2].    
both time O(N) space O(1)

##### 1093. Statistics from a Large Sample 
##### 11. Container With Most Water (medium & high frequency)   
**array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49 (7x7)**   
my approach: brute forth, time O(n^2), space O(1)   
one-pass: 反向指针, time O(n), space O(1)   
Clarify: If we move the larger one, we cannot increase the height because we are always limited by the shortest, and we would be decreasing j-i, the width as well. 所以移动高的，一定不会增大面积；所以我们保留高的，移动低的。
```java
         int maxarea = 0, l = 0, r = height.length - 1;
                while (l < r) {
                    maxarea = Math.max(maxarea, Math.min(height[l], height[r]) * (r - l));
                    if (height[l] < height[r]) {l++;}
                    else {r--;}
```

##### 42. Trapping Rain Water (hard) 

---


### Two Sum & Three Sum
-----
#### 1. two sum   
**Given an array of integers, return indices of the two numbers such that they add up to a specific target.You may assume that each input would have exactly one solution, and you may not use the same element twice.**   
```java
one-pass hash table
        public int[] twoSum(int[] nums, int target) {
            Map<Integer, Integer> map = new HashMap<>();
            for (int i = 0; i < nums.length; i++) {
                int complement = target - nums[i];
                if (map.containsKey(complement)) {
                    return new int[] { map.get(complement), i };
                }
                map.put(nums[i], i);
            }
            throw new IllegalArgumentException("No two sum solution");
        }
```
#### 15. three Sum
**Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.**   

```java
        public List<List<Integer>> threeSum(int[] num) {
            Arrays.sort(num);
            List<List<Integer>> res = new LinkedList<>(); 
            for (int i = 0; i < num.length-2; i++) {
                if (i == 0 || (i > 0 && num[i] != num[i-1])) {
                    int lo = i+1, hi = num.length-1, sum = 0 - num[i];
                    while (lo < hi) {
                        if (num[lo] + num[hi] == sum) {
                            res.add(Arrays.asList(num[i], num[lo], num[hi]));
                            while (lo < hi && num[lo] == num[lo+1]) lo++;
                            while (lo < hi && num[hi] == num[hi-1]) hi--;
                            lo++; hi--;
                        } else if (num[lo] + num[hi] < sum) lo++;
                        else hi--;
                   }
                }
            }
            return res;
        }
```

#### 16. three sum closest   
**Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.**   
