---
layout: post
title:  "Numpy备忘录"
date:   2018-09-12 19:54:42 +0800
excerpt: 矩阵创建、操作、运算
categories: 
   - Data-Science
tags: numpy
# toc: true
image: assets/images/data-science.jpeg
# header:
#    overlay_image: /assets/images/data-science.jpeg
#    overlay_filter: 0.4
---

### 一、矩阵创建

#### 1. 从python list创建：

   ```python
>>> import numpy as np 
>>> np.array([1,2,3])
array([1, 2, 3])
   ```

#### 2. 创建指定维度的矩阵

   ```python
>>> np.ndarray([3,3])
array([[6.91547902e-310, 6.91547902e-310, 3.24515130e-109],
       [1.33360310e+241, 1.84714205e+241, 3.50129306e-311],
       [1.93049258e+241, 3.50129306e-311, 1.97869600e-293]])
   ```

   注意到此时的矩阵元素并没有被初始化为0，如果想要全0的矩阵，可以使用zeros函数

   ```python
>>> np.zeros([3,3])
array([[0., 0., 0.],
       [0., 0., 0.],
       [0., 0., 0.]])
   ```

   类似的，还可以创建全1的矩阵

   ```python
>>> np.ones([3,3])
array([[1., 1., 1.],
       [1., 1., 1.],
       [1., 1., 1.]])
   ```

   numpy矩阵默认数据类型为float64， 可以指定为其他类型

   ```python
>>> np.ndarray([3,3]).dtype
dtype('float64')
>>> np.ones([3,3], dtype=int)
array([[1, 1, 1],
       [1, 1, 1],
       [1, 1, 1]])
   ```

#### 3. 单位矩阵

   ```python
>>> np.eye(3,3)
array([[1., 0., 0.],
       [0., 1., 0.],
       [0., 0., 1.]])
   ```

#### 4. 指定元素范围

   ```python
>>> np.arange(1,10)
array([1, 2, 3, 4, 5, 6, 7, 8, 9])
   ```

#### 5. 随机数矩阵

   ```python
>>> np.random.random([3,3])
array([[0.87405393, 0.10697372, 0.76971393],
       [0.40052012, 0.61633898, 0.38150143],
       [0.68392246, 0.92883538, 0.16442259]])
   ```

   

### 二、矩阵操作

#### 1. reshape

   ```python
>>> np.arange(1,10).reshape([3,3])
array([[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]])
   ```

#### 2. 合并

```python
>>> a = np.arange(1,4)
>>> a
array([1, 2, 3])
>>> b = np.arange(4,7)
>>> b
array([4, 5, 6])
>>> np.stack((a, b))	# 注意参数是一个元组 默认为按行堆叠 即axis=0
array([[1, 2, 3],
       [4, 5, 6]])
>>> np.stack((a, b), axis=1)	#按列堆叠
array([[1, 4],
       [2, 5],
       [3, 6]])
>>> np.vstack((a,b))
array([[1, 2, 3],
       [4, 5, 6]])
>>> np.hstack((a,b))
array([1, 2, 3, 4, 5, 6])
```

 

### 三、矩阵运算

#### 1. 最大值、最小值、求和

   ```python
>>> A = np.arange(1,10).reshape([3,3])
>>> A
array([[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]])
>>> A.max()
9
>>> A.min()
1
>>> A.sum()
45
   ```

   注意默认情况下求的是整个矩阵的最大最小值以及和，可以指定axis按行或列计算

   ```python
>>> a.max(axis=0)	# 求每一列的最大值
array([7, 8, 9])
>>> a.min(axis=1)	# 求每一行的最小值
array([1, 4, 7])
   ```

#### 2. 矩阵加法

   ```python
>>> a = np.arange(5)
>>> a
array([0, 1, 2, 3, 4])
>>> b = np.arange(5,10)
>>> b
array([5, 6, 7, 8, 9])
>>> a + b
array([ 5,  7,  9, 11, 13])
>>> np.add(a, b)
array([ 5,  7,  9, 11, 13])
   ```

#### 3. 矩阵乘法

   ```python
>>> A = np.arange(1,10).reshape([3,3])
>>> A
array([[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]])
>>> I = np.eye(3,3)
>>> I
array([[1., 0., 0.],
       [0., 1., 0.],
       [0., 0., 1.]])
>>> A.dot(I)
array([[1., 2., 3.],
       [4., 5., 6.],
       [7., 8., 9.]])
>>> np.dot(A,I)
array([[1., 2., 3.],
       [4., 5., 6.],
       [7., 8., 9.]])
   ```

   element-wise 乘法

   ```python
>>> A * I
array([[1., 0., 0.],
       [0., 5., 0.],
       [0., 0., 9.]])
   ```

#### 4. broadcast

   ```python
>>> a = np.arange(5)
>>> a
array([0, 1, 2, 3, 4])
>>> a + 1
array([1, 2, 3, 4, 5])
>>> a * 10
array([ 0, 10, 20, 30, 40])
   ```

#### 5. 转置

   ```python
>>> A = np.arange(1,10).reshape([3,3])
>>> A
array([[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]])
>>> A.T
array([[1, 4, 7],
       [2, 5, 8],
       [3, 6, 9]])
   ```

#### 6. 逆矩阵

   ```python
>>> A = np.arange(1,5).reshape([2,2])
>>> A
array([[1, 2],
       [3, 4]])
>>> np.linalg.inv(A)
array([[-2. ,  1. ],
       [ 1.5, -0.5]])
   ```

#### 7. 行列式

   ```python
>>> A
array([[1, 2],
       [3, 4]])
>>> np.linalg.det(A)
-2.0000000000000004
   ```

   