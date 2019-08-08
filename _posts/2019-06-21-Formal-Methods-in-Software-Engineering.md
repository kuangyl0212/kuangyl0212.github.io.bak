---
layout: post
title: 软件工程中的形式化方法小结
date: 2019-06-13 17:18 +0800 
categories: 
    - Software-Engineering
tags: 
    - "Formal Methods"
image: assets/images/4.jpg
---

## 什么是形式化方法？

形式化方法企图以数学的方式来描述软件系统，从而保证软件的正确性。

> 数学是准确的建模媒体，能够对现象、对象、动作等进行简洁、准确的描述；数学支持抽象，它使得规格的本质可以被展示出来，并且还可以以一种有组织的方式来表示系统规格中的抽象层次；数学提供了高层确认的手段，可以使用数学证明来揭示规格中的矛盾性和不完整性、以及用来展示设计和规格之间的一致情况。

形式化方法包括三个方面的活动：形式化规格、形式化验证以及程序求精（refinement）或转换。

1. **形式化规格**

    基于严格的数学（具有严格的语法和语义定义，可以准确的描述系统模型）来描述用户的需求、软件系统的功能以及各种性质。

2. **形式化验证**

    主要包括模型检验和定理证明：

    - **模型检验**： 基于有限状态模型并检验该模型的期望特性。(存在“状态爆炸问题”)
    - **定理证明**： 采用逻辑公式来规格系统及其性质。

3. **程序求精**

    又称程序变换，是将自动推理和形式化方法相结合而形成的一门新技术，它研究从抽象的形式规格推演出具体的面向计算机的程序代码的全过程。

## 典型的形式化方法

1. **有限状态机**

    FSM(Finite State Machine)，是关于存储量有限的计算机的基本模型，也是许多形式化方法规格和验证技术的基础模型。
   
    ![fsm]({{site.url}}/assets/images/fsm.png){: .align-center}

    有限状态机的形式化定义为一个五元组 $M = (Q, \Sigma, \delta, q_0, F)$，具体定义如下：
    1. $ Q = \\{ q_0, q_1,...,q_n \\} $, 有限状态集合。在任一确定时刻，FSM只能处于一个确定的状态$q_i$。
    2. $\Sigma = \\{\sigma_1, \sigma_2,...,\sigma_m\\}$, 有限输入字符集合。在任一确定的时刻，有限状态机只能接收一个确定的输入$\sigma_j$。
    3. $\delta: Q \times \Sigma \rightarrow Q$, 状态转移函数。如果在某一确定时刻，有限状态机处于某一状态$q_i \in Q$，并接收一个输入字符$\sigma_j \in \Sigma$，那么下一时刻处于一个确定的状态$q' = \delta(q_i, \sigma_j) \in Q$。规定$q = \sigma(q,\epsilon)$，即任何状态下读入空字符时不发生任何状态转换。
    4. $q_0 \in Q$，初始状态。
    5. $F \subseteq Q$，终结状态集合。注意这里的$F$是一个集合，也就是说可以有多个状态作为终结状态，即当FSM的状态到达$F$集合中某个状态时就不再接收输入。

    有限状态机的一个局限在于，仅有输入和状态转移，没有输出。对有限状态机进行扩展，引入输出可以得到Moore机和Mealy机。Moore机和Mealy机的不同主要在于：Moore机的输出仅与状态有关，二Mealy机的输出与状态和输入有关。

    - **Moore机**

        Moore机定义为六元组$M = (Q, \Sigma, \Delta, \delta, \lambda, q_0)$，其中：
        1. $Q = \\{q_0,q_1,...,q_n\\}$，有限状态集合；
        2. $\Sigma = \\{\sigma_1, \sigma_2,...,\sigma_m$，有限输入字符集合；
        3. $\Delta = \\{ a_1, a_2, ..., a_r$，有限输出字符集合；
        4. $\delta : Q \times \Sigma \rightarrow Q$，状态转移函数；
        5. $\lambda : Q \rightarrow \Delta$，输出函数；
        6. $q_0 \in Q$ 初始状态。

        注意，和FSM相比，除了定义了输出集合和输出函数意外，Moore机没有了终结状态，这就意味着Moore机不存在“接受”或“拒绝”一个输入的问题。l另外，也可以将FSM看做是Moore机的特例，其输出集合为$\Delta = \\{0,1\\}$， 其输出函数为$$\lambda (q) = \begin{cases} 1, & \text{if } q \in F; \\ 0, & \text{otherwise.} \end{cases}$$

    - **Mealy机**

        同样地，Mealy机也定义为六元组，和Moore机相比，仅输出函数定义不同。
        $\lambda : Q \times \Sigma \rightarrow \Delta$

2. **Petri网**

    Petri网是用来描述并发、异步、分布式软件系统的形式化方法。

    ![petri]({{site.url}}/assets/images/petri.png){: .align-center}

    Petri网，顾名思义是一种有向图。既是图，就有顶点和边。Petri网有两种顶点，位置（Place）和变迁（Transition），位置在上图中用圆圈表示，变迁则用竖线表示。Petri网的边只能连接两个不同的顶点，要么从位置到变迁，要么从变迁到位置，换言之，Petri网是一个二部图。另外，上图中位置圆圈内的点是（令牌）Token，表示资源。

    Petri网也可用代数表示，用一个五元组来描述$PN = (P,T, I, O, M_0)$，其中：
    1. $P = \\{p_1, p_2,...,p_m\\}$，有限位置的集合；
    2. $T = \\{t_1, t_2, ..., t_n\\}$，有限变迁的集合，$P \cap T = \emptyset$
    3. $I: P \times T \rightarrow \\{0, 1\\}$，输入函数（向前函数），对$\forall p \in P, \forall t \in T,$有$I(p, t) = 1 \Leftrightarrow p$到$t$有边
    4. $M_0 : P \rightarrow \\{0,1,2,...,w\\}，初始标示函数，$M_0(p) = k$表示$p$中有$k$个资源（token）。
    
    一个变迁$t$对于给定标示函数$M$是**可发射的**，当且仅当$\forall p \in P, M(p) - I(p, t) \geq 0$。（有资源才可发射）

    在标示函数$M_0下$，**变迁$t$的发射**是用一个新的标示函数$M_1$来代替$M_0$，记为$M_0 \stackrel{t}{\longrightarrow} M_1$，使得：对$\forall p \in P, M_1(p) = M_0(p) - I(p, t) + O(t, p)$，即$t$的发射使得$t$的每个输入位置令牌数减1，使每个输出位置的令牌数加1.

    **可达性**：若$M_0 \stackrel{t_1}{\longrightarrow}M_1\stackrel{t_2}{\longrightarrow}...\stackrel{t_k}{\longrightarrow}M_k = M$则称$M_k$是$M_0$可达的，记为$M_0 \stackrel{\pi}{\longrightarrow}M_k, \pi = t_1 t_2...t_k$

    下面是一个哲学家就餐的例子

    假设五位哲学家围坐在一张圆桌上，相邻哲学家共用一副筷子，如图所示
    ![table]({{site.url}}/assets/images/table.png){: .align-center}
    每位哲学家共有两种状态：think和eat，一位进餐时需要同时获取左右两边的筷子，那么一个哲学家的情况表示成Petri网具有4个位置（两种状态和两边的餐具）和2个变迁（获取筷子和释放筷子）
    ![one_philosopher]({{site.url}}/assets/images/one_philosopher.png){: .align-center}
    完整Petri网（初始状态，即五位哲学家均处于think状态）可表示为：
    ![philosophers]({{site.url}}/assets/images/philosophers.png){: .align-center}

3. **CSP**

    CSP, Communicating Sequential Processes, 即通信顺序进程。CSP是一种描述并发系统的形式化语言。

    **CSP 语法**
    * Assignment primitive
        - &lt;varible&gt; := &lt;expression&gt;
        - Ex: x := e {variable x takes on the value of expression e}
    * Output primitive
        - &lt;destination process&gt; ! &lt;expression&gt;
        - Ex: A ! e {output the value of expression e to process A}
    * Input primitive
        - &lt;source process&lt; ? &lt;variable&gt;
        - Ex: B ? x {from process B input to var x}
    * Concurrent excution
        - [&lt;process&gt; \|\| &lt;process&gt; &lt;\|\| &lt;process&gt; ... &gt;]
    * Iteration
        - *[...]
    * Dijkstra's Guarded Commands
        - &lt;guard&gt; -> &lt;commands&gt;
            * the guard may be a Boolean expression or a result of I/O.
            * commands is a list of commands to be executed if the guard is true
    * Conditional Commands
        - [ &lt;guarded commands&gt; [] &lt;guarded commands&gt; ... ]

    例子：生产者/消费者

    ```
    Producer::
        Buf ! P
    
    Consumer::
        Buf ! more();
        Buf ? P

    Buf::buffer:(0...9)
        in, out:integer;
        in := 0; out := 0;
        *[
            in < out + 10; Producer ? buffer(in mod 10) -> 
                    in := in + 1
         [] out < in; Consumer ? more() -> 
                    Consumer ! buffer(out mod 10) ->
                        out := out + 1
        ]
    ```
