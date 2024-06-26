---
title: graph network
date: 2024-04-21 12:00:00 +/-TTTT
categories: [AI,model]
tags: [AI,paper-learing,graph  ]  # TAG names should always be lowercase
---

## GraphNetwork
### https://distill.pub/2021/gnn-intro/
### 数据表示
* 对图片，每个像素点都是一个节点通过邻接矩阵来表示像素的相邻关系
* 对文本，对每一个token抽象成节点，使用有向边表示文本序列
* 构建分子图 原子为节点 键为边
* 社交网络 
* 引用图 CitationNetwork

### 不同层面的问题
* 图层面
* 点层面 分类 点的属性判断
* 边层面 关系 边的属性判断
### 特性
* 假设：图的对称性
* 邻接矩阵过大 采用邻接列表的形式存储 
* 通过变换 改变边 顶点 全局信息；但是不改变连接性
* 通过多层感知机 来更新 边的向量、点的向量、全局向量；共三个
* pooling 
    * 对未知向量的点进行预测 **通过汇聚全局向量和连接的边向量** 进入全连接层 得到顶点向量
    * 对未知向量的边进行预测 **通过汇聚全局向量和连接的点向量** 进入全连接层 得到边向量
    * 对未知全局向量进行预测 **通过汇聚点向量** 进入全连接层 得到全局向量

* 信息传递
   * 在顶点进入MLP时 汇聚相近的顶点向量
   * 类似attention的机制，将所有接近内容都拿过来
   * 相连的顶点汇聚到边 邻近的边传递到顶点 再做更新
      * 先后顺序影响结果 采取两次的汇聚 两种顺序都做
    * 全局信息向量：虚拟节点和所有顶点和所有边都相连，用于较远信息的传递；
### 超参数
* 参数个数变多 准确度上升
* 三个向量长度 越长精度会更高 但不明显
* 不同 pooling 结果相近
* 信息传递机制 传递的消息越多 效果越好；边的传递的效果比较不明显
  
### addition
* 多层图
* 多种边的图

### 采样子图
*  在采样子图上做pooling 避免后期汇聚结果计算梯度时需要记录全图的信息

### 并行性


### 对偶