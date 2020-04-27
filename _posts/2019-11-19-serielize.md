---
layout:     post
title:      "'Serialize' in Java"
subtitle:   "理解Java中的序列化和反序列化"
date:       2019-11-19
author:     "Eryn"
tags:
    - Leetcode
    - Serialization
    - Algorithm
---


## Serialize and Deserialize 
### encode and decode 

------------------------
### Serialize and Deserialize Binary Tree
**Serialize**     
* 全局变量```String result = ""``` & ```int id = 0```
* 只要root不是null，每一次call serialwork就```id++```，然后把值赋给nowId，即当前树的id
* 每个树节点的“4-len“信息包括：val，id，leftid，rightid，用逗号分隔
* 如果树节点为null，id返回-1 （特别是在leaf时，左右子树的id都会时-1）
* 整棵树组成一整个String，组与组用分号```;```隔开，四点信息为一组，每组代表一个节点    
* 递归得到leftid和rightid，然后写进root的”4-len“信息里
注意： 这个serial function是helper function，修改了全局变量result，但返回int id，所以在主方法中可以随便declare一个rootid去call这个方法，把root node放进去，然后在这个方法执行的过程中result（全局）就被修改了。return result即可。而这个rootId其实在后面也不一定会被用到。      

**Deserialize**      
* 将result这整个String分隔成多个String，放在array中。这个方法要用```String[] nodes = result.split(";")``` ，注意split方法返回的是```String[]```
* ```Map<Integer, Treenode>```将每一组id和node存进去
* 左子树和右子树分别通过map去get出来
* 注意这个方法是bottom up pre-order，所以会先从leaf开始deserialize，等到了parent时，child（leaf with two null children）已经在map里面了，此时要做的是连接起来他们的父子关系



---------------------------
## 构树

### Construct Binary Tree from Preorder-and-inorder/PostOrder-and-inorder
**DFS**dfs的顺序分为了in/pre/post-order，而bfs只是层级遍历。所以当我们讨论in/pre/post我们指的是dfs。      
**postorder & inorder / preorder & inorder**     
* postorder的作用是找到root，每个子树的root
* inorder的作用是划分左右子树
* 比如取出postorder的最后一位元素，它就是原树的root，这个元素再inorder array中的位置，左边皆为左子树，右边皆为右子树。以此类推。
* 用map存好所有的inorder：key：元素；value：index
* 关于index的左右子树的关系（关系到dfs的参数）

**具体方法**
* edge cases是两个array至少一个为空
* hashmap储存inorder
* dfs返回的是树节点，**注意不是void**
* dfs，```if (instart > inend || poststart > postend) return null```就是leaf的左右子树
* 找到当前树root（即post的最后一个）的inorder index；
* 得到左子树的节点数量```left count = rootindex - instart```
* 分别dfs左子树和右子树。

* 无论是pre&in/post&in，最好的方法是画一颗普通的树，写出两个遍历，标明index，找出左子树/右子树的index关系。dfs本身的模板是一样的。
![postorder and inorder](https://img-blog.csdn.net/20161218205159542?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZGluZ2NoZW54aXhp/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)     

**pre-order & post-order**
* 道理本质同上，但不完全一样
* ```pre[0]```和```post[length - 1]```是当前数的root.val
* 如果本树传进来的节点数```N == 1```直接返回root，说明这就一个，是个leaf
* 如果大于1，就正常找左右子树的分界，分别递归
* 为了方便可以将pre[]和post[]都变成global 变量
* helper用的param分别为pre_start_index, post_start_index,number_nodes


------------------------
### Construct binary tree from String
* 格式是```"4(2(3)(1))(6(5))"```左子树优先，也就是说5是6的左子树，6右子树为null
* 用stack方法，preorder的顺序，dfs的思想
* 建立stack
* i遍历整个字符串
* 如果是右括号，pop，这就好比dfs里面的remove(size()-1)
* 如果在0到9之间```else if (char >= '0' && c <='9')```， 以这个数字建立新树节点
* 如果当前char是‘-’，说明接下来这个val是个负数，所以要while到数字部分，substring，再
* 如果stack不为空，则peek一下，peek到的就是父节点，如果父节点的左不为null，就将当前节点添加到父节点的right，否则left。
* 最后将当前节点push进去
* 总的最后，在stack不为空也就是root不为null的情况下，stack.peek()返回root

--------------------
### Unique binary search trees
* 给n，从1到n这n个数额能组成多少个不同的**BST**
* DP
* G(n)=∑ i=1 n G(i−1)⋅G(n−i)
* G(n) is the number of unique BST with n-len sequence, F(i,n) is the number of unique BST when i is the root
```java
public class Solution {
  public int numTrees(int n) {
    int[] G = new int[n + 1];
    G[0] = 1;
    G[1] = 1;

    for (int i = 2; i <= n; ++i) {      // G(n)=∑i=1 n F(i,n)
      for (int j = 1; j <= i; ++j) {    // F(i,n)=G(i−1)⋅G(n−i)
        G[i] += G[j - 1] * G[i - j];
      }
    }
    return G[n];
  }
}
```
