---
layout:     post
title:      "CNN Deep Learning Notes"
subtitle:   "卷积神经网络学习笔记"
date:       2020-04-25
author:     "Eryn"
tags:
    - Machine Learning
    - CNN
    - Neural Network
---
### Covolutinal Neural Network
1. 数据量降维
2. 有效保留图片特征，有效表示出spatial structure

### Before CNN, problem of applying Fully NN to Image Data:
* Too many parameters require a lot of data
* Does not capture the spatial structure

### 数据量大
图像由像素构成，每个像素由颜色构成。    
假设一张1kx1k像素的图片，每个像素有RGB三个参数表示颜色信息    
处理该图片需要处理3百万个像素

### 基本原理
典型的CNN由三部分组成：    
1. 卷积层
2. 池化层
3. 全连接层
   
简单描述功能：    
卷积层负责提取图像中的局部特征；池化层用来大幅降低参数量级(降维)；全连接层类似传统神经网络的部分，用来输出想要的结果    

### 卷积：提取特征
#### image -> Convolved feature
用一个过滤器过滤图像的各个子区域，从而得到子区域特征值    
每个过滤器代表一种图像模式。如果卷积值较大，则认为此图像块十分接近于此卷积核（过滤器）。    
如果设计了100个过滤器，可以理解成：我们认为这个图像由100钟底层纹理模式。用100种模式能够描绘一幅图像。   

#### Feature Map
每种滤波器去卷积图像就得到对图像的不同特征的放映，我们称之为Feature Map。所以100种卷积核就有100个Feature Map。这100个Feature Map就组成了一层神经元。    

### 共享参数
每一个卷积核共享一个参数。每一层神经元的参数个数等于卷积核的种类乘以每种卷积核的参数。每种卷积核的参数等于感受野的大小x深度（RGB就是3）+1


### 池化层（下采样）：数据降维，避免过拟合
#### Convolved feature -> Pooled feature
池化的过程是非重叠的


References：
1. https://easyai.tech/ai-definition/cnn/
