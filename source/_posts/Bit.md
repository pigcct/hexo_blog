---
title: 位运算
author: 苦逼小码农
tags:
  - 位运算
categories:
  - 算法
mathjax: true
date: 2023-05-23 20:50:48
---

# 位运算（二进制运算）



## 1. 基础知识

### 1.1 原码，反码，补码

#### 1.1.1 原码

将一个整数转换成二进制形式，就是其原码。例如a = 6; a 的原码就是`0000 0000 0000 0110`；更改 a 的值a = -18; 此时 a 的原码就是`1000 0000 0001 0010`。**注意**`二进制最高位中1代表负数，0代表正数。`

#### 1.1.2 反码

对于正数，它的反码就是其原码（原码和反码相同）；**正数的反码是它本身，负数的反码是将原码中除`符号位`以外的所有位（数值位）取反**，也就是 0 变成 1，1 变成 0。例如a = 6; a 的原码和反码都是`0000 0000 0000 0110`；更改 a 的值a = -18; 此时 a 的反码是`1111 1111 1110 1101`。

#### 1.1.3 补码

对于正数，它的补码就是其原码（***正数的原码、反码、补码都相同***）；**负数的补码是其反码加 1**。例如a = 6; a 的原码、反码、补码都是`0000 0000 0000 0110`；更改 a 的值a = -18; a 的反码是`1111 1111 1110 1101`，此时 a 的补码是`1111 1111 1110 1110`。

{% asset_img 1.png %}





### 2. 逻辑符号

> 在C++中，8位二进制对应的char类型，范围为-128~127

在 m位二进制数中，为方便起见，通常称**最低位为第0位，从右到左依此类推，最高位为第m-1位。**本书默认使用这种表示方法来指明二进制数以及整数在二进制表示下的位数。

|      | 与   | 或   | 非   | 异或 |
| ---- | ---- | ---- | ---- | ---- |
| 语句 | and  | or   | not  | xor  |
| 符号 | &    | \|   | ~    | ^    |

位运算是指直接对整数在二进制形式下进行操作的运算。它包括了按位与运算、按位或运算、按位异或运算、左移运算和右移运算等。以下是位运算的一些知识点总结：

1. 按位与运算（&）：对两个数的每一位进行与操作，只有两个数的对应位都为 1 的时候，结果的对应位才为 1。例如，3 & 5 的结果为 1。（3的二进制为`0011`, 5的二进制为`0101` 3 & 5 = 1 即`0011 & 0101 = 0001`）

2. 按位或运算（|）：对两个数的每一位进行或操作，只有两个数的对应位其中一个为 1 的时候，结果的对应位就为 1。例如，3 | 5 的结果为 7。（3的二进制为`0011`, 5的二进制为`0101` 3 | 5 = 7 即`0011 | 0101 = 0111`）
3. 按位异或运算（^）：对两个数的每一位进行异或操作，两个数的对应位相同为0，不同为1。例如，3 ^ 5 的结果为 6。（3的二进制为`0011`, 5的二进制为`0101` 3 ^ 5 = 6 即`0011 ^ 0101 = 0110`）
4. 左移运算（<<）：把一个数的二进制码向左移动指定的位数，左移时低位补 0。例如，3 << 2 的结果是 12，即 1100。（3的二进制为`0011`,  3 << 2 = 12 即`0011 << 2 = 1100`）
5. 右移运算（>>）：把一个数的二进制码向右移动指定的位数，右移时高位补 0 或 1（取决于该数原来的符号位），右移一位相当于除以 2。例如，3 >> 1 的结果是 1，即 01。（3的二进制为`0011` ，3 >> 1 = 1 即`0011 >> 1 = 0001`）
6. 位取反运算（~）：对一个数的每一位按位取反（0 变为 1，1 变为 0）。例如，3取反的结果是 -4。（3的二进制为`0011`, 4的二进制为`0100` ~3 = -4 即`0011 = 1100`）
7. lowbit 函数：lowbit(n) 表示 n 在二进制下的最后一个 1 所代表的数值。lowbit(6) 的结果为 2，即`lowbit(0110) = 10 => 2`。





## 3. Lowbit算法



### 3.1 Lowbit算法思想：

{% asset_img 2.png %}



### 3.2 算法描述:

- 例如，求**a = 6**的 **二进制为 0 1 1 0**

- lowbit(6) = `0 1 1 0`中最后一位1的值

- 即：输出为 0 1 `1` 0中最后一位1的值为`2`

  

### 3.3 代码模板：

```cpp
// 返回n的最后一位1的值
int lowbit(int n)
{
	// n & -n 等价于 n & (~n + 1)
    return n & -n;
    //return n & (~n + 1);
}
```





## 4. 移位运算

> **求n的第k位数字: n >> k & 1**



### 4.1 左移

在二进制表示下把数字同时向左移动，低位以0填充，高位越界后舍弃。

**既	1 << n = $2^n$, 	n << 1 = 2n**



### 4.2 算数右移

在二进制补码表示下把数字同时向右移动，高位以符号位填充，低位越界后舍弃。

**既	n >> 1 = $\lfloor n/2.0 \rfloor$**



### 4.3 逻辑右移

在二进制补码表示下把数字同时向右移动，高位以0填充，低位越界后舍弃。
