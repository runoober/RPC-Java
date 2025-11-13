# Java项目推荐：手撕RPC项目（第六版） | 代码随想录知识星球

> **本项目目前只在[知识星球](https://programmercarl.com/other/kstar.html)答疑并维护**。

Java RPC项目是 24年初发布的第一版，24年底发布了第五版：[手撕RPC框架（第五版）（Java）](https://mp.weixin.qq.com/s/oPw1jN2noz3ew6eqqdhf-Q)

目前 已经优化到第六版了。

## 项目特色

本项目不是一口作气就带大家做一个完善的RPC，而是通过四个实现版本循序渐进带大家逐步完善RPC

### 版本一

实现一个最简单可以用的RPC：

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20240722195214.png' width=500 alt=''></img></div>

### 版本二

添加netty自定义编码器，解码器和序列化器，创建缓存：

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20240722195256.png' width=500 alt=''></img></div>

### 版本三

添加负载均衡、超时重试 &白名单：

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20240722195341.png' width=500 alt=''></img></div>

### 版本四

服务-限流、熔断：

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20240722195428.png' width=500 alt=''></img></div>

### 版本五

增加了更多的序列化方式、配置顶、SPI 机制等

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20250311114755.png' width=500 alt=''></img></div>

补充了经典 RPC 框架的介绍及优缺点，并在对应下面提供了，文档地址和源码链接。

如 gRPC、Dubbo。 分析这些框架的好处在于，能够学习成熟的设计理念，深入理解核心模式和技术难点。

同时通过对比性能、扩展性和适用场景，帮助选择更优的方案。此外，这种分析还能避免重复造轮子，将精力聚焦于创新与优化，提升技术积累与实践能力。



### 版本六

1. 实现分布式日志链路追踪，集成Zipkin实现链路可视化
2. 优化 优雅关闭，netty新增 心跳检测功能 动态维护channel资源
3. 细化重试粒度，由接口改为方法；使用注解实现白名单注册

架构图：

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20250311105047.png' width=500 alt=''></img></div>

## 项目背景与简单介绍

### 项目背景

随着业务不断升级，系统规模不断扩大， 单体架构会产生越来越多的问题，需要引入微服务将原先架构解耦为一个个模块。

每个服务模块放在不同的服务器上，能够保证系统在高并发环境下的正常运转。

各个服务模块之间如何相互调用，就使用到了RPC协议的思想（远程调用）。

### RPC介绍

#### 概念

1. RPC（Remote Procedure Call Protocol） 远程过程调用协议。
2. RPC是一种通过网络从远程计算机程序上请求服务，不需要了解底层网络技术的协议。
3. RPC主要作用就是不同的服务间方法调用就像本地调用一样便捷。

#### 常用RPC技术或框架

* 应用级的服务框架：阿里的 Dubbo/Dubbox、Google gRPC、Spring Boot/Spring Cloud。
* 远程通信协议：RMI、Socket、SOAP(HTTP XML)、REST(HTTP JSON)。
* 通信框架：MINA 和 Netty

#### 为什么要有RPC？

1. 服务化：微服务化，跨平台的服务之间远程调用；
2. 分布式系统架构：分布式服务跨机器进行远程调用；
3. 服务可重用：开发一个公共能力服务，供多个服务远程调用。
4. 系统间交互调用：两台服务器A、B，服务器A上的应用a需要调用服务器B上的应用b提供的方法，而应用a和应用b不在一个内存空间，不能直接调用，此时，需要通过网络传输来表达需要调用的语义及传输调用的数据。

### 技术栈

- fastjson和protobuf等主流数据序列化方式
- 高性能网络框架netty
- 分布式协调应用zookeeper
- 负载均衡算法实现
- 限流算法实现
- 重试任务和定时任务在项目场景下的运用

## RPC项目专栏

本项目专栏只分享在[知识星球](https://programmercarl.com/other/kstar.html)里。

在RPC项目专栏 会给出本项目的参考简历写法，为了不让 这些写法重复率太高，所以公众号上是打码的。

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20250311105841.png' width=500 alt=''></img></div>


同时项目专栏也会针对本项目的常见面试问题，经行归类总结，并持续更新

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20250311105908.png' width=500 alt=''></img></div>

以上仅仅是一部分截图，**除了常见问题，还给出基于本项目场景题的案例**：

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20250311105931.png' width=500 alt=''></img></div>

专栏中的项目面试题都掌握的话，这个项目在面试中基本没问题。

很多录友在做项目的时候，把项目运行起来 就是第一大难点！

做这个项目需要的前置知识：

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20250311110346.png' width=500 alt=''></img></div>


关于RPC的设计思路：

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20250311110452.png' width=500 alt=''></img></div>

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20250311110522.png' width=500 alt=''></img></div>

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20250311110552.png' width=500 alt=''></img></div>

六个RPC版本详细讲解：

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20250311110651.png' width=500 alt=''></img></div>

经典RPC框架拆解：

<div align="center"><img src='https://file1.kamacoder.com/i/algo/20250311110719.png' width=500 alt=''></img></div>

## 答疑

本项目在[知识星球](https://programmercarl.com/other/kstar.html)里为 文字专栏形式，大家不用担心，看不懂，星球里每个项目有专属答疑群，任何问题都可以在群里问，都会得到解答：

![](https://file1.kamacoder.com/i/web/2025-09-26_11-30-13.jpg)



## 获取本项目专栏

**本文档仅为星球内部专享，大家可以加入[知识星球](https://programmercarl.com/other/kstar.html)里获取，在星球置顶一**

