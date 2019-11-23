---
layout: post
title: Java中的volatile
subtitle: 🙈🙊🙉
date: 2019-02-19
author: 华仔
header-img: img/post-bg-debug.png
catalog: false
tags:
    - Java
---

```
volatile :	/'vɑlətl/
adj. [化学] 挥发性的；不稳定的；爆炸性的；反复无常的
n. 挥发物；有翅的动物
n. (Volatile)人名；(意)沃拉蒂莱
```

### volatile介绍

​	volatile作为java中的关键词之一，用以声明变量的值可能随时会被别的线程修改，使用volatile修饰的变量会强制将修改的值立即写入主内存，主内存中值的更新会使缓存中的值失效(非volatile变量不具备这样的特性，非volatile变量的值会被缓存，线程A更新了这个值，线程B读取这个变量的值时可能读到的并不是线程A更新后的值)。==**volatile会禁止指令重排。**==**被volatile修饰的变量能够保证每个线程能够获取该变量的最新值，从而避免出现数据脏读的现象。**



### volatile特性

**volatile具有可见性、有序性，不具备原子性。**

注意，volatile不具备原子性，这是volatile与java中的synchronized、java.util.concurrent.locks.Lock最大的功能差异，这一点在面试中也是非常容易问到的点。



### 原子性，可见性，有序性介绍

- 原子性：原子性是指**一个操作是不可中断的，要么全部执行成功要么全部执行失败，有着“同生共死”的感觉**。及时在多个线程一起执行的时候，一个操作一旦开始，就不会被其他线程所干扰。
- 可见性：当多个线程访问同一个变量x时，线程1修改了变量x的值，线程1、线程2...线程n能够立即读取到线程1修改后的值。（可见性是指当一个线程修改了共享变量后，其他线程能够立即得知这个修改。）
- 有序性：即程序执行时按照代码书写的先后顺序执行。在Java内存模型中，允许编译器和处理器对指令进行重排序，但是重排序过程不会影响到单线程程序的执行，却会影响到多线程并发执行的正确性。(本文不对指令重排作介绍，但不代表它不重要，它是理解JAVA并发原理时非常重要的一个概念)。



### synchronized和volatile的三条性质区别

```
synchronized: 具有原子性，有序性和可见性
volatile：具有有序性和可见性
```

|  | 原子性 | 有序性 | 可见性 |
| :-: | :----: | :----: | :----: |
| synchronized |   √    |   √    |   √    |
| volatile     |   ×    |   √    |   √    |




> [三大性质总结：原子性，有序性，可见性](https://www.jianshu.com/p/cf57726e77f2)

> [让你彻底理解volatile](https://www.jianshu.com/p/157279e6efdb)

