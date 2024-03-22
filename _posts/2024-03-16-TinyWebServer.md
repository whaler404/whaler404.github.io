---
layout: post
title:  TinyWebserver 项目讲解
# subtitle: 
date:   2024-03-16
author: whaler404
header-img: img/post-bg-playphone.jpg
categories: post csdiy cpp project
catalog: true
tags:
    - blog
    - cpp
    - project
---

# 项目介绍

- Linux C++开发的轻量Web服务器，主要涉及
  - 使用**线程池+非阻塞socket+epoll+事件处理**的并发模型
  - 使用**状态机**解析HTTP请求报文，支持Post和Get的解析
  - 访问**服务器数据库**实现web端用户注册、登录功能，可以请求视频和文件
  - 实现**同步/异步日志系统**，可以记录服务器运行状态
  - 通过了**Webbench**压力测试，可以实现上万的并发连接数据交换

- 主流的webserver有apache、nginx，

# linux网络编程核心技术

## Linux 网络编程核心
- Linux 下网络编程核心的包括系统编程和网络 IO 两个部分：
    - 进程间通信方式： 信号量、管道、共享内存、socket 等
    - 多线程编程：互斥锁、条件变量、读写锁、线程池等
    - 五大 IO 模型：同步、异步、阻塞、非阻塞、信号驱动
    - 高性能 IO 两种模式：Reactor 和 Proactor（ 但是 Linux 下由于缺少异步 IO 支持，基本没有 ProactorIO 
    - 复用机制：epoll、select、poll（破解 C10K 问题的利器）

## Linux C++ 中的系统函数：
- 文件和I/O操作：
    - open()、close()：打开和关闭文件。
    - read()、write()：从文件中读取数据和向文件写入数据。
    - lseek()：设置文件偏移量。
    - fcntl()：文件控制。
    - ioctl()：设备控制。
- 进程和线程管理：
    - fork()、exec()、wait()、waitpid()：创建新进程、执行新程序、等待子进程结束。
    - exit()、_exit()：正常和非正常退出进程。
    - getpid()、getppid()：获取进程ID和父进程ID。
    - pthread_create()、pthread_join()、pthread_exit()：创建线程、等待线程结束、线程退出。
- 内存管理：
    - malloc()、calloc()、realloc()、free()：动态内存分配和释放。
    - mmap()、munmap()：文件映射到内存。
    - brk()、sbrk()：调整进程的数据段和堆。
- 进程间通信（IPC）：
    - pipe()、mkfifo()：创建管道。
    - msgget()、msgsnd()、msgrcv()：消息队列。
    - semget()、semop()、semctl()：信号量。
    - shmget()、shmat()、shmdt()、shmctl()：共享内存。
- 网络通信：
    - socket()、bind()、listen()、accept()：创建套接字、绑定、监听和接受连接。
    - connect()、send()、recv()：连接到远程套接字、发送和接收数据。
    - getaddrinfo()、gethostbyname()、gethostbyaddr()：获取地址信息和主机信息。
- 时间和日期：
    - time()、clock_gettime()、gettimeofday()：获取当前时间。
    - ctime()、strftime()：时间格式化。
- 信号处理：
    - signal()、sigaction()、kill()：信号处理。
- 系统调用和系统信息：
    - syscall()：调用内核系统调用。
    - getuid()、getgid()、getpid()、getppid()：获取用户ID、组ID、进程ID、父进程ID等。

- 多线程编程
    - 工具库：linux下使用pthread，c++11封装了跨平台的thread库

- 进程通信编程
# 相关博客

- [TinyWebServer讲解——两猿社](https://2yuan.club/categories/TinyWebServer/)
- [TinyWebServer——从0到服务器开发！](https://zhuanlan.zhihu.com/p/364044293)
- [Linux高性能服务器编程-pdf](https://dark-wind.github.io/books/Linux%E9%AB%98%E6%80%A7%E8%83%BD%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BC%96%E7%A8%8B.pdf)
- [c++经验之谈一：RAII原理介绍](https://zhuanlan.zhihu.com/p/34660259)
- [Linux下的I/O复用与epoll详解](https://www.cnblogs.com/lojunren/p/3856290.html)
- [回调函数（callback）是什么](https://www.zhihu.com/question/19801131)
- [c++标准](https://docs.oldtimes.me/c.biancheng.net/cplus/index.html)
- [如何在 Linux 系统中结束进程或是中止程序](https://zhuanlan.zhihu.com/p/37702619)

- pthread库
    - [POSIX thread (pthread) libraries (CMU)](https://www.cs.cmu.edu/afs/cs/academic/class/15492-f07/www/pthreads.html)
    - [yolinux: your linux tutorials](http://www.yolinux.com/TUTORIALS/)
    - [pthread的各种同步机制](https://casatwy.com/pthreadde-ge-chong-tong-bu-ji-zhi.html)
    - [为什么 pthread 条件变量(condition variable)函数要用到 mutex ](https://feng-qi.github.io/2017/05/08/Why-do-pthreads-condition-variable-functions-require-a-mutex/)
    - [pthread 读写锁](https://www.cnblogs.com/sinkinben/p/14272921.html)
    - [Linux系统编程-(pthread)线程通信(自旋锁)](https://cloud.tencent.com/developer/article/1944273)
    - [pthread使用barrier栅栏方式同步](https://langzi989.github.io/2018/07/05/pthread%E4%BD%BF%E7%94%A8barrier%E6%A0%85%E6%A0%8F%E6%96%B9%E5%BC%8F%E5%90%8C%E6%AD%A5/)
    
- semaphore库
    - [被"抛弃"的同步模型 - 信号量Semaphores](https://dengzuoheng.github.io/cpp-concurency-pattern-3-semaphore)

- 跨进程通信
    - [Linux C 中的 fork()、vfork()、exec*()、system() 等进程函数](https://learnku.com/articles/69324)
    - [C/C++ 进程间通信 管道](https://www.cnblogs.com/dk666/p/7412527.html)
    - [Signal Handling in C++](https://www.geeksforgeeks.org/signal-handling-in-cpp/)
    - [一文看懂 Linux 信号处理原理与实现](https://www.51cto.com/article/675743.html)
    - [IPC using Message Queues](https://www.geeksforgeeks.org/ipc-using-message-queues/)
    - [IPC through shared memory](https://www.geeksforgeeks.org/ipc-shared-memory/)

- IO
    - [fcntl函数的用法总结](https://www.cnblogs.com/zxc2man/p/7649240.html)
    - [《UNIXLinux程序设计教程》一3.6　文件控制函数fcntl()](https://developer.aliyun.com/article/175396)
    - [c++标准文件操作](https://docs.oldtimes.me/c.biancheng.net/cplus/60/index.html)

- IO多路复用
    - [Select、Poll、Epoll简单入门](https://zhuanlan.zhihu.com/p/373835207)
    - [Epoll的理解](https://blog.csdn.net/weixin_43326322/article/details/108276554)
    - [句柄是什么？](https://www.zhihu.com/question/27656256)

- HTTP
    - [HTTP请求报文和HTTP响应报文](https://www.cnblogs.com/biyeymyhjob/archive/2012/07/28/2612910.html)
