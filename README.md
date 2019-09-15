# 数据结构复习笔记

## 数组
由相同类型的元素的集合所组成的数据结构，分配一块连续的内存来存储，利用元素的索引可以计算出该元素对应的存储地址。
1. 一维数组（向量）
1. 二维数组（矩阵）：行列数相等的矩阵称为方阵；元素大部分为零的矩阵称为稀疏矩阵；元素大部分非零的矩阵称为稠密矩阵。
1. 高维数组（张量）：存储方式有两种，从最左下标开始计数存储，和从最右下标开始计数存储。

## 顺序表
在计算机内存中以数组的形式保存的线性表，是指用一组地址连续的存储单元依次存储数据元素的线性结构。

## 链
1. 单链表：链表的链接方向是单向的，对链表的访问要通过从头部开始，依序往下读取。
1. 双链表：每个数据结点中都有两个指针，分别指向直接后继和直接前驱。
1. 循环链表：最后一个结点指向头结点，形成一个环。
1. 块状链表：每一个块状链表的节点，也就是顺序表，可以被叫做一个块。
1. 异或链表：通过异或操作（这里用⊕表示）把前一个结点的地址和后一个结点的地址变成一个地址。
1. 跳表：底层是一个普通的有序链表。每个更高层都充当下面列表的“快速通道”，这里在第 i 层中的元素按某个固定的概率 p（通常为1/2或1/4）出现在第 i+1 层，每个元素平均出现在 1/（1-p）个列表中。

## 字符串
由零个或多个字符组成的有限序列。通常以串的整体作为操作对象。\
字符串的长度是在字符串中字符的数目，空串是长度为0的字符串。\
字符串串接是结合性的，但非交换性运算，空串充当单比特。\
字符串s被称为是字符串t的子串，如果存在（可能为空）字符串 u 和 v 使得 t = usv。

### 字符编码
* Unicode：使用 16 位的编码空间，也就是每个字符占用 2 个字节。理论上一共最多可以表示 2^16（即 65536）个字符。
  * UTF-8：一种针对Unicode的可变长度字符编码，也是一种前缀码。它可以用来表示Unicode标准中的任何字符，且其编码中的第一个字节仍与ASCII兼容。
  * UTF-16：把Unicode字符集的抽象码位映射为16位长的整数的序列，用于数据存储或传递。
* ASCII：只能显示26个基本拉丁字母、阿拉伯数字和英式标点符号。
* GBK：字符有一字节和双字节编码，00–7F范围内是第一个字节，和ASCII保持一致。之后的双字节中，前一字节是双字节的第一位。总体上说第一字节的范围是81–FE，第二字节的一部分领域在40–7E，其他领域在80–FE。
* GB 18030：采用变长多字节编码，每个字可以由1个、2个或4个字节组成。编码空间庞大，最多可定义161万个字符。

## 散列表
根据键直接访问在内存存储位置的数据结构。通过计算一个关于键值的函数，将所需查询的数据映射到表中一个位置来访问记录。

### 散列函数
* 直接定址法：取关键字或关键字的某个线性函数值为散列地址。例：hash（k）= k，hash（k）= a * k + b
* 数字分析法：假设关键字是以r为基的数，并且哈希表中可能出现的关键字都是事先知道的，则可取关键字的若干数位组成哈希地址。
* 除留余数法：取关键字被某个不大于散列表表长 m 的数 p 除后所得的余数为散列地址。例：hash（k）= k mod p，p <= m
* 平方取中法：取关键字平方后的中间几位为哈希地址。通常在选定哈希函数时不一定能知道关键字的全部情况，取其中的哪几位也不一定合适，而一个数平方后的中间几位数和数的每一位都相关，由此使随机分布的关键字得到的哈希地址也是随机的。取的位数由表长决定。
* 折叠法：将关键字分割成位数相同的几部分，然后取这几部分的叠加和（舍去进位）作为哈希地址。例：字符串取所有字符异或
* 随机数法

### 冲突处理
* 开放定址法：所有输入的元素全部存放在哈希表里。逐个（线性、平方或伪随机）探测存放地址的表，直到查找到一个空单元，把散列地址存放在该空单元。
* 拉链法：将散列到同一个存储位置的所有元素保存在一个链表中。
* 再散列：在上次散列计算发生冲突时，利用该次冲突的散列函数地址产生新的散列函数地址，直到冲突不再发生。

## 队列
先进先出的线性表，通常用链表或数组来实现。队列只允许在后端进行插入操作，在前端进行删除操作。
1. 单链队列：使用链表作为基本数据结构，所以不存在伪溢出的问题，队列长度也没有限制。
1. 循环队列：防止伪溢出的发生，但队列大小是固定的。
1. 阵列队列：使用数组作为基本数据结构，队列大小是固定的。

## 栈
后进先出的线性表，通常用链表或数组来实现。栈只允许在有序的线性数据集合的一端进行加入数据和移除数据的运算。
1. 数组堆栈：预先分配一个大小固定且较合适的数组空间。
1. 串列堆栈：以连结串列的形式完成。
* 基本操作：
  * 推入：将数据放入堆栈顶端，堆栈顶端移到新放入的数据。
  * 弹出：将堆栈顶端数据移除，堆栈顶端移到移除后的下一笔数据。

## 树

## 堆

## 并查集

## 图
