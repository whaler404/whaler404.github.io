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

- Linux 下网络编程核心的包括系统编程和网络 IO 两个部分：
    - 进程间通信方式： 信号量、管道、共享内存、socket 等
    - 多线程编程：互斥锁、条件变量、读写锁、线程池等
    - 五大 IO 模型：同步、异步、阻塞、非阻塞、信号驱动
    - 高性能 IO 两种模式：Reactor 和 Proactor（ 但是 Linux 下由于缺少异步 IO 支持，基本没有 ProactorIO 
    - 复用机制：epoll、select、poll（破解 C10K 问题的利器）

- 多线程编程
    - 工具库：linux下使用pthread，c++11封装了跨平台的thread库

- 进程通信编程
# 相关博客

- [TinyWebServer——从0到服务器开发！](https://zhuanlan.zhihu.com/p/364044293)
- [c++经验之谈一：RAII原理介绍](https://zhuanlan.zhihu.com/p/34660259)
- [Linux下的I/O复用与epoll详解](https://www.cnblogs.com/lojunren/p/3856290.html)
- [回调函数（callback）是什么](https://www.zhihu.com/question/19801131)
- pthread库
    - [POSIX Threads Programming](https://hpc-tutorials.llnl.gov/posix/)
    - [POSIX thread (pthread) libraries (CMU)](https://www.cs.cmu.edu/afs/cs/academic/class/15492-f07/www/pthreads.html)
    - [yolinux: your linux tutorials](http://www.yolinux.com/TUTORIALS/)
    - [pthread的各种同步机制](https://casatwy.com/pthreadde-ge-chong-tong-bu-ji-zhi.html)