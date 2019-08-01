---
layout: post
title:  "《计算机网络--自顶向下方法》读书笔记--第一章 计算机网络和因特网"
date:   2018-06-28 09:54:42 +0800
categories: 
    - "Computer-Networks"
image: assets/images/2.jpg
---

#### 前言
1. 什么是自顶下下方法？
    - 从应用层开始向下一直讲到物理层

### 第一章 计算机网络和因特网

#### 1.1 什么是因特网

从两个方面来描述：
1. 描述因特网的具体构成
2. 根据分布式应用提供服务的网络基础设施来描述

##### 1.1.1 具体构成描述
一些术语：
- 主机（host）/端系统（end system）
- 通信链路（communication link）--通信的物理媒体，包括：
    - 同轴电缆
    - 铜线
    - 光纤
    - 无线电频谱
- 分组交换机（packet switch）
- 分组（packet）--将数据分段，并为每段加上首部字节
- 路径（route/path）--一个分组从发送端系统到接收端系统所经过的一系列通信链路和分组交换机
- 因特网服务提供商（Internet Service Provider， ISP）--端系统通过ISP接入因特网，ISP上运行IP协议
- 协议（protocol），最重要的两个协议：
    - TCP（Transmission Control Protocol），传输控制协议
    - IP（Internet Protocol），网际网协议
- 因特网标准（Internet Standard）：由IETF（Internet Engineering Task Force，因特网工程任务组）研发
- RFC（Request For Comment，请求评论），IETF的标准文件
- 内联网（intranet）：与Internet相对

##### 1.1.2 服务描述
- 分布式应用程序（distributed application）：诸如电子邮件、往上冲浪、即时讯息等等
- 应用程序编程接口（Application Programming Interfa， API）：规定一个端系统上的软件请求因特网基础设施上运行的另一个端系统上特定的软件交付数据的方式（因特网是一种基础设施）

##### 1.1.3 协议
- 定义：两个或多个通信实体之间交换的报文格式和次序，以及报文传输和/或接收或其他时间方面所采取的动作
