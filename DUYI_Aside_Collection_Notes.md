# 集合Collection

### 集合的分类：

1. **Collection**：以value形式存储
   1. **List** - 有序可重复
   2. **Queue** - 有序可重复 - **队列特点：先进先出**
   3. **Set** - 无序不重复
2. **Map**：以Key-Value形式存储
   * Key无序不重复，value无序可重复

### List : Vector, ArrayList, Stack

**Vector** ---> **ArrayList** (早-->晚)：底层实现都是动态数组

<---**Stack**(栈) extends Vector : 因此底层也是数组，但拥有自己的**栈的特点：后进先出**

**LinkedList**：底层是链表。依赖Node类。

### 集合的学习

1. 集合的应用

   集合就是一个小容器，应用主要是：增删改查

2. 集合使用的情景：各自集合的特点

   集合有很多分支，考虑用数组还是集合？数组长度固定，集合长度可变。集合有很多分支，有的适合遍历(ArrayList)，有的适合添加删除(LinkedList)，有的先入先出，有的先入后出。

3. 每一个集合底层的原理：数据结构的存储方式。为什么它们有自己的特点？
4. 自己尝试实现

### List下的应用：

List家族中都有的方法：

* add()    remove()    set()    get()   size()  ---> 增删改查+size

Stack中还要的，自己的方法：

* push()   pop()   peek()

Queue中自己的方法：

* offer()   poll()   peek()



