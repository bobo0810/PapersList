## 损失函数

### A Discriminative Feature Learning Approach for Deep Face Recognition

ECCV2016

| 主题   | 描述                                                         |
| ------ | :----------------------------------------------------------- |
| 问题   | Softmax只促进特征可分离性，对人脸识别（类内紧凑，类间区隔）并不有效。 |
| 创新点 | 针对人脸识别，为加强特征可区分能力，提出Center-Loss。        |
| 原理   | 1. 基于mini-batch更新类中心。<br/>2. 为避免少量错误标记造成较大扰动，使用α控制学习率。 |
| 好处   | 1. 学习类中心，惩罚类间距离。<br/>2. 易于训练、优化。        |

### NormFace: L2 Hypersphere Embedding for Face Verification

- TODO

### SphereFace: Deep Hypersphere Embedding for Face Recognition

CVPR2017

- TODO

### Additive Margin Softmax for Face Verification

- TODO

### ArcFace: Additive Angular Margin Loss for Deep Face Recognition

CVPR2019

- TODO

### Circle Loss: A Unified Perspective of Pair Similarity Optimization

CVPR2020

- TODO

### DiscFace: Minimum Discrepancy Learning for Deep Face Recognition

ACCV2020  

| 主题   | 描述                                                         |
| ------ | :----------------------------------------------------------- |
| 问题   | 基于Softmax方法：训练过程中，类中心周围的样本特征虽然与类中心接近，但各自方向不同，彼此间隔较大 。这种方向性的差异将导致评估性能下降。<br/>注：训练阶段优化样本特征与类中心距离，评估阶段衡量样本对之间角距离。 |
| 创新点 | 1. 第一个提出 “解决过程差异”问题。<br/>2. 提出正则化方法“最小偏差学习”：通过一个可学习偏差 迫使类内样本特征朝向最优方向。<br/>3. 可学习偏差  有助于从样本特征中分离出“类不变向量”。 |
| 原理   | 论文 Algorithm 1                                             |
| 好处   | 1. 适用于 “类别不平衡” 及 “类别数量大，类内样本少”  的数据集。<br/>2. 容易嵌入CosFace\ArcFace等基于Softmax的分类器中。 |