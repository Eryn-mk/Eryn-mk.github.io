---
layout:     post
title:      "Back Tracking & DFS"
subtitle:   "回溯法总结"
date:       2020-01-05
author:     "Eryn"
tags:
    - Java
    - Leetcode
    - DFS
    - Back Tracking
    - Algorithm
---

### BackTracking

**弱点：找不准dfs return的条件**
```java
class Solution {
    /**
     * @param S: A set of numbers.
     * @return: A list of lists. All valid subsets.
     */
    public ArrayList<ArrayList<Integer>> subsets(int[] nums) { 
        if(nums==null||nums.length==0) return null;
        ArrayList<ArrayList<Integer>> results = new ArrayList<>();
        //把空集开头的所有集合放入result
        dfsHelper(nums,0,new ArrayList<Integer>(), results);
        return results;
    }

    private void dfsHelper(int[] nums, 
                            int startIndex, 
                            ArrayList<Integer> subset, 
                            ArrayList<ArrayList<Integer>> results){
        //deep copy,否则后面操作subset，subset的内容就改变了
        results.add(new ArrayList<Integer>(subset));
        for(int i = startIndex; i<nums.length;i++){
            subset.add(nums[i]);
            dfsHelper(nums,i+1,subset,results);
            subset.remove(subset.size()-1);
        }   
    }
}
```
* 库函数 Arrays.sort()是用的quick sort实现，可以认为是nlogn的复杂度
* 这里不可以用results.addAll(xxx) ，因为addAll 表示，把xxx中的元素都加入到results中，我们是需要加入list，而不是list中的元素
* 为什么result.add 在for循环前面？因为答案不仅仅只存在于搜索树的叶子节点，每一个节点都是一个答案，所以进入这个搜索节点 就要add一下
* 要记得递归完成后subset.remove(subset.size() - 1)，这就是BackTracking，把刚才加进去的那一个清除掉（add--remove） ，回到上一步，再继续向后进行，刚才添加进去的那个就是idx=subset.size() - 1，因为我们是往list添加元素，那么当前元素就是添加在list后面，我们回溯是一层一层上来，就是从后一层一层把元素remove掉，当前就remove目前的最后的元素

##### 22. Generate Parentheses      
##### 51. N-Queens
##### 52. N-Queens II
##### 39. Combination Sum
##### 40. Combination Sum II
##### 216. Combination Sum III
##### 46. Permutations
##### 47. Permutations II
##### 78. Subsets
##### 90. Subsets II
##### 131. Palindrome Partitioning

#####
##### 
#####
#####
##### 
#####
#####
##### 
#####
#####
##### 
#####
#####
##### 
#####
#####
