---
title: TODO
date: 2019-11-13 23:30:43
tags: 技术
keywords:
description:
---

网上得来的知识点，一点点突破



<!--more-->



- [ ] Hashmap 源码级掌握，扩容，红黑树，最小树化容量，hash 冲突解决，有些面试官会提出发自灵魂的审问，比如为什么是红黑树，别的树不可以吗；为什么 8 的时候树化，4 不可以吗，等等 
- [ ] concureentHashMap，段锁，如何分段，和 hashmap 在 hash 上的区别，性能，等等
- [ ] HashTable，同步锁，这块可能会问你 synchronized 关键字 1.6 之后提升了什么，怎么提升的这些
  ArrayList 优势，扩容，什么时候用
- [ ] LinkedList 优势，什么时候用，和 arraylist 的区别 等等
- [ ] 基本类型和包装类型的区别，涉及自动装箱和拆箱，怎么做的，原理
- [ ] String，StringBuffer，StringBuilder 哪个是安全的
- [ ] 字符串编码的区别
- [ ] 什么是泛型，怎么用泛型
- [ ] static 能不能修饰 threadLocal，为什么
- [ ] Comparable 和 Comparator 接口是干什么的，其区别
- [ ] 多态的原理是什么
- [ ] 接口和抽象类，面试官问我是怎么理解的，我说接口对应功能，抽象类对应属性，然后面试官给我说了他的看法，说抽象类更偏向于一种模板~ 然后又交流了一下各自的想法
- [ ] 如何通过反射和设置对象私有字段的值
- [ ] 快速失败(fail-fast)和安全失败(fail-safe)的区别是什么
- [ ] synchronized 的实现原理以及锁优化？
- [ ] volatile 的实现原理？
- [ ] Java 的信号灯？
- [ ] synchronized 在静态方法和普通方法的区别？
- [ ] 怎么实现所有线程在等待某个事件的发生才会去执行？
- [ ] CAS ？ CAS 有什么缺陷，如何解决？
- [ ] synchronized 和 lock 有什么区别？
- [ ] Hashtable 是怎么加锁的 ？
- [ ] List，Map，Set 接口在取元素师，各有什么特点
- [ ] 如何线程安全的实现一个计数器
- [ ] 生产者消费者模式，要求手写过代码，还是要知道的
- [ ] 单例模式，饿汉式，懒汉式，线程安全的做法，两次判断 instance 是否为空，每次判断的作用是什么
- [ ] 线程池，这个还是很重要的，在生产中用的挺多，四个线程池类型，其参数，参数的理解很重要，corepoolSize 怎么设置，maxpoolsize 怎么设置，keep-alive 各种的，和美团面试官探讨过阻塞队列在生产中的设置，他说他一般设置为 0，防止用户阻塞
- [ ] cyclicbarrier 和 countdownlatch 的区别，个人理解 赛马和点火箭
- [ ] 线程回调，这块 被问过让我设计一个 RPC，怎么实现，其实用到了回调这块的东西
- [ ] sleep 和 yeild 方法有什么区别
- [ ] volatile 关键字，可见性。
- [ ] 乐观锁和悲观锁的使用场景
- [ ] 悲观锁的常见实现方式：lock synchronized retreentlock
- [ ] 乐观锁：CAS MVCC
- [ ] 读写锁的实现方式，16 位 int 的前八位和后八位分别作为读锁和写锁的标志位
- [ ] 死锁的条件，怎么解除死锁，怎么观测死锁。
- [ ] 希望大家能够好好看一下反射的原理，怎么确定类，怎么调方法
- [ ] RPC 框架，同步异步，响应时间，这些都被问到过，还让设计过同步，异步，阻塞，非阻塞 在深信服的面试中遇到过，最好再找一些应用场景加以理解



## JAVA 基础
- [ ] HashMap 的源码，实现原理； JDK8 做了什么优化
- [ ] HashMap 扩容机制，为什么都是 2 的 N 次幂
- [ ] ArrayList 和 Vector 的区别，扩容机制等
- [ ] CopyOnWriteArrayList 原理
- [ ] HashSet 和 TreeSet 原理
- [ ] ArrayBlockingQueue 和 LinkedBlockingQueue 区别
- [ ] 集合迭代器的原理
- [ ] 传值和传引用的区别
- [ ] 动态代理
- [ ] JDK8 Concurrent HashMap 的原理

## 多线程
- [ ] 创建多线程的方式，以及线程的状态转换
- [ ] 线程的中断机制
- [ ] ThreadPoolExecutor 初始化参数； Executors 静态方法
- [ ] synchronized 的使用方式及原理
- [ ] 偏向锁、轻量级锁、自旋锁等优化
- [ ] ReentrantLock 的特点及 AQS 原理
- [ ] Semaphore、CountDownLatch、CyclicBarrier 等使用
- [ ] ThreadLocal 的原理、与 Thread 类的关系、以及内存泄漏问题
- [ ] volatile 的原理及内存屏障相关
- [ ] Lock 接口有哪些实现类，使用场景是什么
- [ ] 悲观锁，乐观锁，优缺点，CAS 有什么缺陷，该如何解决

