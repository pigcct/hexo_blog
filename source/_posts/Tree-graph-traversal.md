---
title: 树和图的遍历
author: 苦逼小码农
tags:
  - 树
  - 图
categories:
  - 算法
mathjax: true
date: 2023-05-15 20:37:59
---

# 树与图的遍历

### 1. 树与图的存储

```cpp
**树与图的存储**
树是一种特殊的图，与图的存储方式相同。
对于无向图中的边ab，存储两条有向边a->b, b->a。
因此我们可以只考虑有向图的存储。

(1) 邻接矩阵：g[a][b] 存储边a->b

(2) 邻接表： h[0] -> a -> b -> c -> d -> null
					  h[1] -> a -> b -> null
						h[2] -> a -> null
						h[3] -> null

// 对于每个点k，开一个单链表，存储k所有可以走到的点。h[k]存储这个单链表的头结点
int h[N], e[N], ne[N], idx;

// 添加一条边a->b
void add(int a, int b)
{
    e[idx] = b, ne[idx] = h[a], h[a] = idx ++ ;
}

// 初始化
idx = 0;
memset(h, -1, sizeof h);
树与图的遍历
时间复杂度 O(n+m)O(n+m), nn 表示点数，mm 表示边数
```

## 2. 树的深度优先遍历

### 2.1 树的深度优先遍历的算法思想：

{% asset_img 1.gif %}

树的深度优先遍历，（既一条道走到黑），先从第一个点开始往下遍历，依次遍历以下的每一个点，直到遍历到最后的点为止。

### 2.2 代码模板：

```cpp
深度优先遍历 —— 模板题 AcWing 846. 树的重心

int dfs(int u)
{
    st[u] = true; // st[u] 表示点u已经被遍历过

    for (int i = h[u]; i != -1; i = ne[i])
    {
        int j = e[i];
        if (!st[j]) dfs(j);
    }
}

int dfs(int u)
{
    st[u] = true;
    
    int sum = 1, res = 0;
    for(int i = h[u]; i != -1; i = ne[i])
    {
        int j = e[i];
        if(!st[j])
        {
            int s = dfs(j);
            res = max(res, s);
            sum += s;
        }
    }
    res = max(res, n - sum);
    
    ans = min(ans, res);
    
    return sum;
}
```

## 3. 树的宽度优先遍历

### 3.1 树的宽度优先遍历的算法思想：

树的宽度优先遍历，既按层级从上层到下层依次遍历，比如说从第一个点开始，1号点可以拓展到它周围的所有邻点，每次只向下拓展一次，每次拓展的数都属于同一层级。

### 3.2 代码模板：

```cpp
宽度优先遍历 —— 模板题 AcWing 847. 图中点的层次

queue<int> q;
st[1] = true; // 表示1号点已经被遍历过
q.push(1);

while (q.size())
{
    int t = q.front();
    q.pop();

    for (int i = h[t]; i != -1; i = ne[i])
    {
        int j = e[i];
        if (!st[j])
        {
            st[j] = true; // 表示点j已经被遍历过
            q.push(j);
        }
    }
}

int bfs()
{
    int hh = 0, tt = 0;
    q[0] = 1;//q[0]为1号点，此题强制q[0]为1
    
    memset(d, -1, sizeof d);
    
    d[1] = 0;//表示1号点到1号点的距离为0
    
    while(hh <= tt)
    {
        int t = q[hh ++ ];//去除队头
        
        for(int i = h[t]; i != -1; i = ne[i])
        {
            int j = e[i];//用j记录当前的点
            if(d[j] == -1)//如果该点没有被扩展过
            {
                d[j] = d[t] + 1;
                q[ ++ tt] = j;
            }
        }
    }
    
    return d[n];
}
```

