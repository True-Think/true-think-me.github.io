---
layout:     post
title:      "spark入门"
subtitle:   " \"spark基本概念\""
date:       2022-02-21 17:45:00 +0800
author:     "True-Think"
header-img: "img/new/mao_cow.jpg"
catalog: true
tags:
    - 技术
    - spark
---
# Spark入门

### Spark 概念

- 解决MapReduce计算慢的问题，接口简单编程不灵活，只能离线计算
- 基于内存分布式计算框架，速度快
- 只负责计算，不负责存储
- Spark离线计算功能类似于mapreduce
- Hadoop生态圈
  - 批处理：MapReduce、Hive、Pig
  - 流式计算：Storm
  - 交互式计算：Impala、presto
- Spark优势：
  - 运行速度快
  - 自身生态比较完善
    - Spark sql
    - Spark streaming
    - Spark mllib/Spark ML
  - api比较丰富

### 什么是RDD？

RDD(Resillient Distributed Dataset)叫做弹性分布式数据集，是

- Spark中最基本的数据抽象，是**<u>不可变、可分区、并行计算</u>**的。

- 所有Spark中对数据的操作最终都会转换成RDD操作：	
  - spark sql
  - spark streaming
  - spark ml、spark mllib

- 同hdfs分布式原理，
  - hdfs文件被切分为多个block存储在各个节点上，而RDD是被切分为多个partition。不同的partition可能在不同的节点上。
  - 读hdfs时，spark加载hdfs数据1个block对于的rdd的partition
  - 写数据时，spark 1个partition可能对于多个block
- 创建RDD
  - 内存方式
    - rdd1 = sc.parallelizel(data)
    - rdd1.mapreduce() 
  - 创建RDD时可以指定partition的数量（RDD会分成几份）一个partition会对应一个task,根据CPU的内核数来指定partition(1核对应2-4个partition)

