# Aliyun LOG Java Producer

[![Build Status](https://travis-ci.org/aliyun/aliyun-log-producer.svg?branch=master)](https://travis-ci.org/aliyun/aliyun-log-producer-java)
[![License](https://img.shields.io/badge/license-Apache2.0-blue.svg)](/LICENSE)

Aliyun LOG Java Producer 是一个易于使用且高度可配置的 Java 类库，专门为运行在大数据、高并发场景下的 Java 应用量身打造。

## 功能特点
1. 线程安全 - producer 接口暴露的所有方法都是线程安全的。
2. 异步发送 - 调用 producer 的发送接口通常能够立即返回。Producer 内部会缓存并合并发送数据，然后批量发送以提高吞吐量。
3. 自动重试 - 对可重试的异常，producer 会根据用户配置的最大重试次数和重试退避时间进行重试。
4. 行为追溯 - 用户通过 callback 或 future 不仅能获取当前数据是否发送成功的信息，还可以获得该数据每次被尝试发送的信息，有利于问题追溯和行为决策。
5. 上下文还原 - 同一个 producer 实例产生的日志在同一上下文中，在服务端可以查看某条日志前后相关的日志。
6. 优雅关闭 - 保证 close 方法退时，producer 缓存的所有数据都能被处理，用户也能得到相应的通知。

## 功能优势

使用 producer 相对于直接通过 API 或 SDK 向 LogHub 写数据会有如下优势。

### 高性能
在海量数据、资源有限的前提下，写入端要达到目标吞吐量需要实现复杂的控制逻辑，包括多线程、缓存策略、批量发送等，另外还要充分考虑失败重试的场景。Producer 实现了上述功能，在为您带来性能优势的同时简化了程序开发步骤。

### 异步非阻塞
在可用内存充足的前提下，producer 会对发往 LogHub 的数据进行缓存，因此用户调用 send 方法时能够立即返回，不会阻塞，达到计算与 I/O 逻辑分离的目的。稍后，用户可以通过返回的 future 对象或传入的 callback 获得数据发送的结果。

### 资源可控制
可以通过参数控制 producer 用于缓存待发送数据的内存大小，同时还可以配置用于执行数据发送任务的线程数量。这样做一方面避免了 producer 无限制地消耗资源，另一方面可以让您根据实际情况平衡资源消耗和写入吞吐量。

## 安装
在 Maven 工程中使用 Aliyun LOG Java Producer 只需在 pom.xml 中加入相应依赖即可。以 0.0.5 版本为例，在 <dependencies> 内加入如下内容：

```
<dependency>
    <groupId>com.aliyun.openservices</groupId>
    <artifactId>aliyun-log-producer</artifactId>
    <version>0.0.5</version>
</dependency>
<dependency>
    <groupId>com.aliyun.openservices</groupId>
    <artifactId>aliyun-log</artifactId>
    <version>0.6.28</version>
</dependency>
<dependency>
    <groupId>com.google.protobuf</groupId>
    <artifactId>protobuf-java</artifactId>
    <version>2.5.0</version>
</dependency>
```

## 快速入门

参考教程 [Aliyun LOG Java Producer 快速入门]()。

## 原理剖析

参考文章 [Aliyun LOG Java Producer 原理剖析]()。

## 问题反馈
如果您在使用过程中遇到了问题，可以创建 [GitHub Issue](https://github.com/aliyun/aliyun-log-producer/issues) 或者前往阿里云支持中心[提交工单](https://workorder.console.aliyun.com/#/ticket/createIndex)。
