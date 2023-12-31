---
title: DFS
author: 苦逼小码农
tags:
  - DFS
categories:
  - 算法
mathjax: true
date: 2023-05-15 19:59:15
---

# DFS——深度优先搜索

>  💡 DFS：深度优先搜索算法（Depth-First-Search）是一种用于**遍历**或**搜索树**或**图**的算法.沿着树的**深度遍历**树的节点，尽可能深的搜索树的分支。当节点v的所在边都己被探寻过，搜索将**回溯**到发现节点v的那条边的起始节点。这一过程一直进行到已发现从源节点可达的所有节点为止。如果还存在未被发现的节点，则选择其中一个作为源节点并重复以上过程，整个进程反复进行**直到所有节点都被访问为止**。



## 1. DFS算法思想：

>  💡 **DFS：stack（栈）**   时间复杂度：$O（N）$



DFS既深度优先搜索，通过从上到下每一层依次往深处搜索，（顺序为从上到下，从左到右），搜到最低处输出，然后回溯到相应的位置（回溯要恢复原来的数据），然后依稀按照之前的方式搜索。

{% asset_img 1.gif %}



## 2. DFS算法的实现方式：

**树的深度优先搜索（对树上的每一个节点都要进行搜索一遍）**

- 首先以数的头结点为第0层，即 U= 0（往下依次增加一层）
- 依次对从上到下，从左到右的每一条路径上的每一个节点进行搜索，直到搜到底未知
- 若搜索到了底部的叶子节点，开始回溯，直到找到他的父节点有其他子节点的点继续往下搜索
- 递归上面的方式，依次搜索每一个节点

{% asset_img 2.png %}

## 3. DFS代码模板：

```cpp
// DFS—— 模板题 AcWing 842. 排列数字
    
int n;  //n为输入的数字的个数
int path[N]; //path存储树的值
bool st[N];  //判断当前的数是否已经被使用，false为未使用，true为已使用

void dfs(int u)
{
    if(u == n)//如果当前的路已经走到了最后，输出路径上的所有值
    {
        for(int i = 0; i < n; i ++) cout << path[i] <<" ";
        puts("");
        return ;
    }
    
    for(int i = 1; i <= n; i ++)
    {
        if(!st[i]) //判断当前的数还未使用
        {
            path[u] = i;  //给当前的数赋值
            st[i] = true; //标记当前数已被使用
            dfs(u + 1);   //递归下一个数
            st[i] = false;//回溯，恢复原来的数据
        }
    }
}
```

