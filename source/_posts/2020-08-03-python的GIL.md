---
title: python的GIL
date: 2020-08-03
tags: 
- python
- 多线程
description: 全局解释器锁(Global Interpreter Lock)简称GIL，它是c实现的python多线程的核心，不过它却限制了python利用多线程运行多核cpu，为什么要这样呢？GIL是如何实现的？
---





GIL实现细节：https://cyrusin.github.io/2016/04/27/python-gil-implementaion/