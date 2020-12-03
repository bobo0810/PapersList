# 论文清单

相关代码收录于[PytorchNetHub](https://github.com/bobo0810/PytorchNetHub)

[TOC]

## 网络结构

### HS-ResNet: Hierarchical-Split Block on Convolutional Neural Network

- **问题**

  视觉任务重，多尺度特征极其重要。三个目标如下：

  （1）减少特征图的冗余信息（2） 避免复杂计算下提高特征表达能力（3）保持速度和精度

- **创新点**
  1. 提出HS-Block(Hierarchical-Split)，并构建HS-ResNet。

- **原理**

  1. 将ResNet-Bottleneck的Conv3x3替换为HS-Block，其包含众多通道级别Split和Concat（维护特征表达   sum破坏特征表达）。
  2. HS-Block将特征图分为S组，每组卷积拆分两份，一份恒等映射，一份接入下一组卷积捕获更精细特征。
  3. 引入超参 分组数S：S越大，多尺度能力越强，速度相应变慢。
  4. 影响速度的两个因素：（1）特征图串行处理 （2）Split操作耗时

- **好处**

  同一层融合多尺度特征（类似Res2Net）

### TARGETDROP: A TARGETED REGULARIZATION METHOD FOR CONVOLUTIONAL NEURAL NETWORKS

- **问题**

  Dropout随机丢弃特征：由于空间相关特征允许丢弃信息在网络内流动，故对网络影响较小。

- **创新点**

  提出正则化TargetDrop，基于注意力机制针对性删除判别特征，迫使网络学习更多可区分特征。

- **原理**

  1. 通过通道注意力SE模块 提取 重要程度较大的特征图。
  2. 对于提取的特征图，以图中最高激活值为中心生成矩形块，以屏蔽高响应区域。

- **好处**

  训练启用，预测关闭。通用性强。

### Attentional Feature Fusion

​	WACV2021	

- **问题**

  当前未关注过多尺度通道注意力融合。

- **创新点**

  1. 统一特征融合方式，包括 同一层、短连接、长连接的sum/concat操作。

  2. 单特征通道加权：提出MS-CAM 多尺度通道注意力模块，纠正不同尺度的特征不一致，作用类似SE模块。
  3. 多特征融合：提出AFF、iAFF，解决初始特征聚合的问题。

- **原理**

  1. 通过结合通道注意力和空间注意力，以融合特征。
  2. 由于初始聚合特征影响最终特征，iAFF用迭代方式缓解。

- **好处**

  即插即用，统一特征融合方式。

## 轻量级网络

- TODO

## 损失函数

### A Discriminative Feature Learning Approach for Deep Face Recognition

​	ECCV2016

- **问题**

  Softmax只促进特征可分离性，对人脸识别（类内紧凑，类间区隔）并不有效。

- **创新点**
  1. 针对人脸识别，为加强特征可区分能力，提出Center-Loss
- **原理**
  1. 基于mini-batch更新类中心。
  2. 为避免少量错误标记造成较大扰动，使用α控制学习率。
- **好处**
  1. 学习类中心，惩罚类间距离。
  2. 易于训练、优化。

### NormFace: L2 Hypersphere Embedding for Face Verification

- TODO

### SphereFace: Deep Hypersphere Embedding for Face Recognition

​	CVPR2017

- TODO

### Additive Margin Softmax for Face Verification

- TODO

### ArcFace: Additive Angular Margin Loss for Deep Face Recognition

​	CVPR2019

- TODO

### Circle Loss: A Unified Perspective of Pair Similarity Optimization

​	CVPR2020

- TODO

### DiscFace: Minimum Discrepancy Learning for Deep Face Recognition

​	ACCV2020  

- **问题**

  基于Softmax方法：训练过程中，类中心周围的样本特征虽然与类中心接近，但各自方向不同，彼此间隔较大 。这种方向性的差异将导致评估性能下降。

  > 注：训练阶段优化样本特征与类中心距离，评估阶段衡量样本对之间角距离。

- **创新点**

  1. 第一个提出 “解决过程差异”问题。

  2. 提出正则化方法“最小偏差学习”：通过一个可学习偏差 迫使类内样本特征朝向最优方向。

  3. 可学习偏差  有助于从样本特征中分离出“类不变向量”。

- **原理**

  - 论文 Algorithm 1

- **好处**

  - 适用于 “类别不平衡” 及 “类别数量大，类内样本少”  的数据集。
  - 容易嵌入CosFace\ArcFace等基于Softmax的分类器中。



## 激活函数

### Funnel Activation for Visual Recognition

​	ECCV2020	

- **问题**

  当前激活函数没有专为视觉任务设计，激活过程中的空间不敏感性阻碍识别。

- **创新点** 

  提出FReLU，将ReLU扩展到二维（1）像素级别建模（2）通过规则卷积捕获视觉布局（3）将感受野引入非线性激活层

- **原理**

  用卷积操作替代ReLU的下限0。

- **好处**

  简单高效且易于迁移各种视觉任务。

### Dynamic ReLU

​	ECCV2020	

- **问题** 

  当前ReLU及变种都是固定参数，对所有输入执行相同操作。

- **创新点**

  1. 提出动态Dy-ReLU，通过汇总空间及通道维度信息去自适应激活函数。
  2. 统一现有的多数激活函数。

- **原理**

  Dy-ReLU将全局信息编码为超函数，并相应调整分段线性激活函数，以增强表达能力。

- **好处**

  即插即用，统一多数激活函数。

  

## 训练策略

### BroadFace: Looking at Tens of Thousands of People at Once for Face Recognition

​	ECCV2020   

- **问题** 
  常规方法每次只取min-ibatch，无法反映 整个数据集分布。

- **创新点**
  提出BroadFace，在训练阶段增加实例的补偿方法，能够考虑到大量身份数据。
- **原理**
  1. 通过 当前类中心与过去类中心的差值，将 队列内过去特征 补偿近似为 当前特征。
  2. mini-batch的梯度更新卷积层，mini-batch和队列concat的梯度更新分类器。
  3. 更好的分类器训练出更好的卷积层。

- **好处**
  由于队列，故用于fintuning阶段。

### Semi-Siamese Training for Shallow Face Learning

​	ECCV2020  

- **问题**

  1. 每个类别id对应图像过少，仅包含注册照和生活照两张，称为浅层人脸学习。

  2. 缺乏类内多样性，导致特征维度崩溃、网络极易退化或过拟合。

- **创新点**

  1. 提出Semi-Siamese Training (SST)训练策略，采用两个孪生网络，两者结构相同，参数接近但不同，保证类内差异。
  2. 第一个网络提取注册集特征作为类中心，抛弃分类器；第二个网络提取生活照训练分类层。

- **原理**

  1. 正确更新Wy和Xi：损失更新探测集网络，滑动平均更新注册集网络。SGD更新一个网络，用滑动均值更新另一个
  2. 保持Wy的项远离0：用注册集网络的输出代替类中心权重

- **好处**

  浅层人脸学习是痛点，但所提方法未像BroadFace进行特征补偿，效果存疑。

### Partial FC: Training 10 Million Identities on a Single Machine

​	AAAI2021

- **问题**
  1. 类别过多，导致分类器GPU占用过大 ，故采用模型并行。
  2. 当类别持续增大（亿级），模型并行时单个GPU占用也持续增大，导致无法训练更大规模id分类。

- **创新点**
  1. 提出大规模id分类的训练策略,成功训练亿级目标。
  2. 提出softmax近似算法，仅用10%类中心仍保持准确率。
  3. 提供Glint360K数据集

* **原理**
		提出softmax近似算法，用PPRN（正类全采样，负类随机采10%）来近似softmax
* **好处**
		解决“能否”训练亿级类别问题，并非持续提升。





