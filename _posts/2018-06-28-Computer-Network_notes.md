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

#### 1.2 网络边缘

##### 1.2.1 客户机-服务器

- 客户机程序(client program)/服务器程序(server program)

    分布式应用程序的分布式即是指客户机程序和服务器程序运行在不同的计算机上。
    除了客户-机服务器模式意外还有对等模式(P2P)，用户端系统既是客户机程序，也是服务器程序，用户端系统接收数据时是客户机，发送数据时是服务器。

##### 1.2.2 接入网(access network)

- 接入网是指将端系统连接到其他边缘路由器的物理链路，可分为：

   1. 住宅接入(residential access)
   2. 公司接入(company access)
   3. 无线接入(wireless access)

   住宅接入有拨号调制解调器(dial-up modem)，先将数字信号调制成m模拟信号，经由模拟电话线(通常是双绞铜线，即电话线)传输到目的端，目的端将模拟信号解调为数字信号。缺点是： 1. 速度太慢，峰值为56kbps，而且由于双绞线质量低，实际速率远低于峰值；2. 占用电话线，也就是说上网的时候不能打电话，打电话的时候不能上网。

   除拨号调制解调器以外，住宅接入主要有DSL(Digital Subscriber Line, 数字用户线)和HFC(Hybrid Fiber-coaxial cable，混合光纤同轴电缆)。DSL概念上类似于拨号调制解调器(且同样使用电话线)，但是，通过限制是用户和ISP的距离提高了速率，另外，下行速度快上行速度慢。DSL划分了3个不重叠的频段(频分多路复用)：
   
   1. 高速下行信道，50kHz~1MHz;
   2. 中速上行信道，4kHz~50kHz;
   3. 普通双向电话信道, 0~4kHz
   
   HFC扩展了用户广播电缆电视的电缆网络, HFC需要特殊的调制解调器,称为电缆调制解调器(cable modem), HFC的一大特点是共享广播媒体, 因此会出现资源争用. (而DSL则是用户和ISP之间的点对点专用通道). 和DSL一样,也是下行速率快, 上行慢. 

   DSL, HFC和卫星接入的一个共同点是always on. 

    公司接入: 局域网(LAN), 以太网为主流,速率100Mbps或1Gbps甚至10Gbps. 使用双绞线或同轴电缆.

    无线接入: 两大类:

     - 无线局域网(wireless LAN) IEEE 802.11
     - 广域无线接入网(wide-area wireless access network)
    
##### 1.2.3 物理媒介

 1. 双绞铜线(就是平常所见的网线)
 2. 同轴电缆(电视信号线)
 3. 光缆
 4. 陆地无线电信道
 5. 卫星无线电信道
   
#### 1.3 网络核心

##### 1.3.1 电路交换(circuit switching)和分组交换(packet switching)

- 电话网络是电路交换的例子,而因特网则是分组交换的典范.
- 电路交换
  - 当两台主机要通信时,需要在两者之间创建一条端到端连接(end-to-end connection)
  - 多路复用: 频分多路复用(Frequency-Division Multiplexing, FDM)和时分多路复用(Time-Division Multiplexing)
  - 电路交换效率低,静默期(silent period)专用电路空闲
  - 创建端到端电路和预留端到端带宽很复杂,需要复杂的心灵软件来协调沿端到端路径的交换机的操作.
  - 电路交换的传输时间与链路数量无关,也就是说无法通过增加链路数量来提高传输速率
- 分组交换