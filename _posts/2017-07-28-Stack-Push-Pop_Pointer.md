---
layout: post
title: "入栈出栈时栈顶指针移动顺序问题"
date: 2017-07-28 13:23:07 +0800

categories: 
    - Data Structure
tags: 
    - Stack
image: assets/images/8.jpg
---

所谓栈顶指针移动顺序问题，就是指针移动在前还是入栈出栈的操作在前的问题。

### 首先，栈顶指针有两种形式：
1. 指向栈顶元素
2. 指向栈顶元素的下一个位置

那么指针移动的顺序也分这两种情况来讨论，（注意：这里的栈的存储结构为顺序栈）
### 指向栈顶元素的栈顶指针
1. 入栈时先移动指针，再入栈这是因为栈顶指针指向栈顶元素，入栈时需要为新的栈顶元素腾出位置
``` c
Status Push(SqStack &s, ElemType x) {
	if (s.top == MaxSize - 1) { // 栈满
		return ERROR;
	}
	s.data[++s.top] = x; // 先移指针，再入栈
	return OK;
}
```
2. 出栈，先弹出栈顶元素，再移动指针
``` c
Status Pop(SqStack &s, ElemType &x) {
	if (s.top == -1) { // 栈空
		return ERROR;
	}
	x = s.data[s.top--]; // 先出栈，再移指针
	return OK;
}
```
### 指向栈顶元素下一个位置的栈顶指针
1. 入栈时不需要先移动指针，因为栈顶元素的下一个位置早已虚位以待了
``` c
Status Push(SqStack &s, ElemType x) {
	if (s.top == MaxSize) { // 栈满
		return ERROR;
	}
	s.data[s.top++] = x; // 先入栈，再移指针
	return OK;
}
```
2. 出栈时需要先下移栈顶指针才能取得栈顶元素
``` c
Status Pop(SqStack &s, ElemType &x) {
	if (s.top == 0) { // 栈空
		return ERROR;
	}
	x = s.data[--s.top]; // 先移指针，再出栈
	return OK;
}
```

### 总结
以上是教材上的做法，笔者以为不必如此拘泥，说到底指针移动的顺序其实不影响，这样写唯一的好处在于代码变得简洁优雅了一丢丢而已
以指向栈顶元素的栈顶指针的入栈操作为例，如果先入栈再移动指针，那么代码应该是这样
``` c
Status Push(SqStack &s, ElemType x) {
	if (s.top == MaxSize - 1) { // 栈满
		return ERROR;
	}
	s.data[s.top + 1] = x;
	s.top++;
	return OK;
}
```
只不过是对同一个操作的不同封装罢了
当然，如果是链栈，那又不一样了
