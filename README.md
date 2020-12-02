# PapersList

## 新结构

- TODO

## 轻量级结构

- TODO



## 损失函数

### DiscFace: Minimum Discrepancy Learning for Deep Face Recognition

ACCV2020  

- 问题

  基于Softmax方法：训练过程中，类中心周围的样本特征尽管方向不同，但仍受到惩罚。这种方向性的差异将导致评估性能下降。

- 创新点

  提出 最小偏差学习：使用一个可学习偏差 迫使类内样本特征朝向最优方向。

 





## 训练策略

### BroadFace: Looking at Tens of Thousands of People at Once for Face Recognition

ECCV2020    [复现](https://github.com/bobo0810/BroadFace)

- 问题 
  常规方法每次只取min-ibatch，无法反映 整个数据集分布。

- 创新点
  提出BroadFace，在训练阶段增加实例的补偿方法，能够考虑到大量身份数据。
- 原理
  1. 通过 当前类中心与过去类中心的差值，将 队列内过去特征 补偿近似为 当前特征。
  2. mini-batch的梯度更新卷积层，mini-batch和队列concat的梯度更新分类器。
  3. 更好的分类器训练出更好的卷积层。

- 好处
  由于队列，故用于fintuning阶段。

### Semi-Siamese Training for Shallow Face Learning

ECCV2020   [项目注释](https://github.com/bobo0810/Semi-Siamese-Training)

- 问题

  1. 每个类别id对应图像过少，仅包含注册照和生活照两张，称为浅层人脸学习。

  2. 缺乏类内多样性，导致特征维度崩溃、网络极易退化或过拟合。

- 创新点

  1. 提出Semi-Siamese Training (SST)训练策略，采用两个孪生网络，两者结构相同，参数接近但不同，保证类内差异。
  2. 第一个网络提取注册集特征作为类中心，抛弃分类器；第二个网络提取生活照训练分类层。

- 创新点

  1. 正确更新Wy和Xi：损失更新探测集网络，滑动平均更新注册集网络。SGD更新一个网络，用滑动均值更新另一个
  2. 保持Wy的项远离0：用注册集网络的输出代替 类中心权重

- 好处

  浅层人脸学习是痛点，但所提方法未像BroadFace进行特征补偿，效果存疑。

