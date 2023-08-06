---
title: 最短路
author: 苦逼小码农
tags:
  - 最短路
categories:
  - 算法
mathjax: true
date: 2023-05-15 20:40:14
---

# 最短路(Dijkstra, Bellman-ford, SPFA, Floyd)

{% asset_img 1.png %}

## 1. Dijsttra

### 1.1 素版Dijkstra算法（稠密图——邻接矩阵）

> 💡时间复杂度：$O(N^2)$

#### 1.1.1 朴素版Dijkstra算法思想：

迪杰斯特拉（dijkstra）算法是一种求单源最短路的算法，假若从一个点a出发，终点是s，dijkstra算法可以求出从a到达s的最短路径（所有边权都是正数）。

{% asset_img 1.gif %}

#### 1.1.2 朴素版Dijkstra算法实现方式：

- 初始化距离**dist[1] = 0 , dist[i] = 无穷** （表示起点到i点的距离）
- 循环n次
  - 将已确定的最短距离的点存放到数组**dist**中
  - 找到不在**dist**中且距离最近的点—>**t**
  - 将 **t** 加到**dist**中，用 **t** 更新其它点的距离
  - 判断**dist[x] > dist[t] + w**

#### 1.1.3 朴素版Dijkstra算法代码模板：

```cpp
朴素dijkstra算法 —— 模板题 AcWing 849. Dijkstra求最短路 I
时间复杂是 O(n2+m)O(n2+m), nn 表示点数，mm 表示边数
int g[N][N];  // 存储每条边
int dist[N];  // 存储1号点到每个点的最短距离
bool st[N];   // 存储每个点的最短路是否已经确定

// 求1号点到n号点的最短路，如果不存在则返回-1
int dijkstra()
{
    memset(dist, 0x3f, sizeof dist);//将所有点的距离都初始化为无穷大
    dist[1] = 0;//初始化距离，这里表示第一个点的距离为0

    for (int i = 0; i < n - 1; i ++ )
    {
        int t = -1;     // 在还未确定最短路的点中，寻找距离最小的点
        for (int j = 1; j <= n; j ++ )
            if (!st[j] && (t == -1 || dist[t] > dist[j]))
                t = j;

        // 用t更新其他点的距离
        for (int j = 1; j <= n; j ++ )
            dist[j] = min(dist[j], dist[t] + g[t][j]);

        st[t] = true;
    }

    if (dist[n] == 0x3f3f3f3f) return -1;
    return dist[n];
}
```





### 1.2 堆优化版Dijkstra算法（稀疏图——邻接表）

> 💡 **时间复杂度：**$O(M*log N)$



#### 1.2.1 堆优化版Dijkstra算法思想：

| 方法 | 描述         | 示例            | 时间复杂度 |
| ---- | ------------ | --------------- | ---------- |
| push | 将元素插入堆 | q.push(x)       | O(log n)   |
| pop  | 删除堆顶元素 | q.pop()         | O(long n)  |
| top  | 查询堆顶元素 | int x = q.top() | O（1）     |

{% asset_img 2.png %}

#### 1.2.2 堆优化版Dijkstra算法实现方式：

- 初始化距离**dist[1] = 0 , dist[i] = 无穷** （表示起点到i点的距离）
- 循环n次（dist为已经确定最短距离的点）
  - 找到不在**dist**中且离起点最近的点，赋值**→t**（优化：小根堆）
  - 将 **t 加入**如到**dist**中
  - 用 **t** 更新所有点的距离（优化：用堆更新了每个点的时间复杂度为O（log n））

#### 1.2.3 堆优化版的Dijkstra算法代码模板：

```cpp
堆优化版dijkstra —— 模板题 AcWing 850. Dijkstra求最短路 II
时间复杂度 O(mlogn)O(mlogn), nn 表示点数，mm 表示边数
typedef pair<int, int> PII;

int n;      // 点的数量
int h[N], w[N], e[N], ne[N], idx;       // 邻接表存储所有边
int dist[N];        // 存储所有点到1号点的距离
bool st[N];     // 存储每个点的最短距离是否已确定

// 求1号点到n号点的最短距离，如果不存在，则返回-1
int dijkstra()
{
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;
    priority_queue<PII, vector<PII>, greater<PII>> heap;
    heap.push({0, 1});      // first存储距离，second存储节点编号

    while (heap.size())
    {
        auto t = heap.top();
        heap.pop();

        int ver = t.second, distance = t.first;

        if (st[ver]) continue;
        st[ver] = true;

        for (int i = h[ver]; i != -1; i = ne[i])
        {
            int j = e[i];
            if (dist[j] > dist[ver] + w[i])
            {
                dist[j] = dist[ver] + w[i];
                heap.push({dist[j], j});
            }
        }
    }

    if (dist[n] == 0x3f3f3f3f) return -1;
    return dist[n];
}
```





## 2. Bellman-Ford

> 💡 **时间复杂度：**$O(N*M)$



### 2.1 Bellman-Ford算法思想：

Bellman_Ford算法的原理是对n条边进行n - 1次松弛操作，得到所有可能的最短路径。由于是有**步数限制和负数边**存在，我们不能使用Djkstra算法，但是Bellman_Ford算法的实现和Djkstra算法在思路上还是差不多。Ballman_Ford算法可以解决存在负权边的问题，对于一些有步数限制的问题只能使用Bellman_ford算法，但是其他的负权边问题用SPFA解决会更佳。

### 2.2 Bellman-Ford算法实现方式：

- 初始化距离**dist[1] = 0 , dist[i] = 无穷** （表示起点到i点的距离）
- **循环n次（外层）**
- 循环m次（内层）→遍历所有边
  - 每一次更新一个节点的最短距离（**dist[b] = dist[a] + w**(松弛操作)）
  - 循环n次后所有边都满足：**dist[b] = dist[a] + w**(三角不等式)

**迭代k次的意义：从1号点结果k条边到每一个点的最短距离。**

### 2.3 Bellman-Ford算法代码模板：

```cpp
Bellman-Ford算法 —— 模板题 AcWing 853. 有边数限制的最短路
时间复杂度 O(nm)O(nm), nn 表示点数，mm 表示边数
注意在模板题中需要对下面的模板稍作修改，加上备份数组，详情见模板题。

int n, m;       // n表示点数，m表示边数
int dist[N];        // dist[x]存储1到x的最短路距离

struct Edge     // 边，a表示出点，b表示入点，w表示边的权重
{
    int a, b, w;
}edges[M];

// 求1到n的最短路距离，如果无法从1走到n，则返回-1。
int bellman_ford()
{
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;

    // 如果第n次迭代仍然会松弛三角不等式，就说明存在一条长度是n+1的最短路径，由抽屉原理，路径中至少存在两个相同的点，说明图中存在负权回路。
    for (int i = 0; i < n; i ++ )
    {
        for (int j = 0; j < m; j ++ )
        {
            int a = edges[j].a, b = edges[j].b, w = edges[j].w;
            if (dist[b] > dist[a] + w)
                dist[b] = dist[a] + w;
        }
    }

    if (dist[n] > 0x3f3f3f3f / 2) return -1;
    return dist[n];
}
```





## 3. SPFA

> 💡 **时间复杂度：**$O(N)或(N * M)$



### 3.1 SPFA算法思想：

***代码跟堆优化版Dijkstra相似，只用更改一下spfa函数即可***

SPFA算法就是将bellman_ford算法加上了队列优化，在使用bellman_ford算法时**对每一条边都要进行遍历**，实际上是将每一个边都进行了n - 1 次松弛操作，实际上我们没必要松弛每一个点，那么我们希望去掉一些无用的松弛操作，这个时候我们用**队列**来维护哪些点可能会需要松弛操作，这样就能**只访问必要的边**，SPFA同样能处理负权回路的图。

### 3.2 SPFA算法实现方式：

- 初始化距离**dist[1] = 0 , dist[i] = 无穷** （表示起点到i点的距离）
- 将源点的队头元素入列给t， 然后弹出
- 队首 **t** 出队，**并将 t 标记为没有访问过**，方便下次入队(进行松弛操作)
- 遍历以队首为起点的所有边**（t, i)** ,如果 **dist[ i ] > dist [ t ] + w [ i ]** ,更新 **dist [ i ]**
- 如果 i不在队列中，则标记入队，一直循环到为空为止

### 3.3 SPFA代码模板：

```cpp
spfa 算法（队列优化的Bellman-Ford算法） —— 模板题 AcWing 851. spfa求最短路
时间复杂度 平均情况下 O(m)O(m)，最坏情况下 O(nm)O(nm), nn 表示点数，mm 表示边数
int n;      // 总点数
int h[N], w[N], e[N], ne[N], idx;       // 邻接表存储所有边
int dist[N];        // 存储每个点到1号点的最短距离
bool st[N];     // 存储每个点是否在队列中

// 求1号点到n号点的最短路距离，如果从1号点无法走到n号点则返回-1
int spfa()
{
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;

    queue<int> q;
    q.push(1);
    st[1] = true;

    while (q.size())
    {
        auto t = q.front();
        q.pop();

        st[t] = false;

        for (int i = h[t]; i != -1; i = ne[i])
        {
            int j = e[i];
            if (dist[j] > dist[t] + w[i])
            {
                dist[j] = dist[t] + w[i];
                if (!st[j])     // 如果队列中已存在j，则不需要将j重复插入
                {
                    q.push(j);
                    st[j] = true;
                }
            }
        }
    }

    return dist[n];
}
```

### 3.4 SPFA算法判断图中是否存在负环问题

**判断存在负环的思想：**

- dsit[ x ] 表示的是1号点到x号点的距离

- cnt[ x ]表示的是1号点到x号点的边的数量

- 判断负环是增加了更新的步骤

  - dist [x] = dist[t] + w[i]（这里是更新1号点到x号点的距离，用dist[t]更新）
  - cnt[x] = cnt[t] + 1（这里入下图所示，因为1号点到t号点的距离更新了，1号点到x号点的边数相对于1号点到t号点多了1，所以ccnt[x]就应该加上1）

  ```cpp
  spfa判断图中是否存在负环 —— 模板题 AcWing 852. spfa判断负环
  时间复杂度是 O(nm)O(nm), nn 表示点数，mm 表示边数
  int n;      // 总点数
  int h[N], w[N], e[N], ne[N], idx;       // 邻接表存储所有边
  int dist[N], cnt[N];        // dist[x]存储1号点到x的最短距离，cnt[x]存储1到x的最短路中经过的点数
  bool st[N];     // 存储每个点是否在队列中
  
  // 如果存在负环，则返回true，否则返回false。
  bool spfa()
  {
      // 不需要初始化dist数组
      // 原理：如果某条最短路径上有n个点（除了自己），那么加上自己之后一共有n+1个点，由抽屉原理一定有两个点相同，所以存在环。
  //*****************************************************
      queue<int> q;
      for (int i = 1; i <= n; i ++ )
      {
          q.push(i);
          st[i] = true;
      }
  //****************************************************
      while (q.size())
      {
          auto t = q.front();
          q.pop();
  
          st[t] = false;
  
          for (int i = h[t]; i != -1; i = ne[i])
          {
              int j = e[i];
              if (dist[j] > dist[t] + w[i])
              {
                  dist[j] = dist[t] + w[i];
                  cnt[j] = cnt[t] + 1;
                  if (cnt[j] >= n) return true;       // 如果从1号点到x的最短路中包含至少n个点（不包括自己），则说明存在环
                  if (!st[j])
                  {
                      q.push(j);
                      st[j] = true;
                  }
              }
          }
      }
  
      return false;
  }
  ```

  



## 4. Floyd

> 💡 **时间复杂度：**$O(N^3)$



### 4.1 Floyd算法思想：

Floyd算法又称为插点法，是一种利用动态规划的思想寻找给定的加权图中多源点之间最短路径的算法，算法的主要思想基于动态规划（Dp)。

### 4.2 Floyd算法实现方式：

- 邻接矩阵(二维数组)dist储存路径，数组中的值开始表示点点之间初始直接路径，最终是点点之间的最小路径，有两点需要注意的，第一是如果没有直接相连的两点那么默认为一个很大的值(不要因为计算溢出成负数)，第二是自己和自己的距离要为 0。
- 状态转移方程（其中**d[i][j]\**的意思可以理解为点a到点b的最短路径,所以\**d[i][k]\**的意思可以理解为\**i到k的最短路径d[k][j]\**的意思为\**k到j的最短路径.**）

```cpp
dp[i][j]=min(dp[i][j],dp[i][k]+dp[k][j])
```

- 从第1个到第n个点依次加入松弛计算，每个点加入进行试探枚举是否有路径长度被更改(自己能否更新路径)。顺序加入(k枚举)松弛的点时候，需要遍历图中每一个点对(i,j双重循环)，判断每一个点对距离是否因为加入的点而发生最小距离变化，如果发生改变(变小)，那么两点(i,j)距离就更改。
- 重复上述直到最后插点试探完成。

### 4.3 Floyd代码模板：

```cpp
floyd算法 —— 模板题 AcWing 854. Floyd求最短路
时间复杂度是 O(n3)O(n3), nn 表示点数
初始化：
    for (int i = 1; i <= n; i ++ )
        for (int j = 1; j <= n; j ++ )
            if (i == j) d[i][j] = 0;
            else d[i][j] = INF;

// 算法结束后，d[a][b]表示a到b的最短距离
void floyd()
{
    for (int k = 1; k <= n; k ++ )
        for (int i = 1; i <= n; i ++ )
            for (int j = 1; j <= n; j ++ )
                d[i][j] = min(d[i][j], d[i][k] + d[k][j]);
}
```



