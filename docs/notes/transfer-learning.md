# 迁移学习

- 在机器学习、深度学习和数据挖掘的大多数任务中，我们都会假设training和inference时，采用的数据服从相同的分布（distribution）、来源于相同的特征空间（feature space）。但在现实应用中，这个假设很难成立，往往遇到一些

  问题：

  - 1、**带标记的训练样本数量有限**。比如，处理A领域（target domain）的分类问题时，缺少足够的训练样本。同时，与A领域相关的B（source domain）领域，拥有大量的训练样本，但B领域与A领域处于不同的特征空间或样本服从不同的分布。
  - 2、**数据分布会发生变化**。比如，数据分布与时间、地点或其他动态因素相关。随着动态因素的变化，数据分布会发生变化，以前收集的数据已经过时，需要重新收集数据，重建模型。

- 这时，知识迁移（knowledge transfer）是一个不错的选择，即把B领域中的知识迁移到A领域中来，提高A领域分类效果，**不需要花大量时间**去标注A领域数据。迁移学习，做为一种新的学习范式，被提出用于解决这个问题。

## Fine-tuning

- 任务描述
  - 目标数据：很少
  - 源数据：很多
- 例子：语言辨识
  - 目标数据：少量音频数据和特定用户（例如：中文）
  - 源数据：大量音频数据和特定用户（例如：英文）
- 处理方式：通过源数据训练模型，当作初始值，然后训练目标数据
  - 挑战：因为目标数据少，所以小心防止过拟合

### 防止过拟合技巧

**Conservarive Traing**（保守学习？）：训练目标数据的时候，训练完成后新model和旧model相差不大

- 加一种regularization：新model和旧model在看到同一笔data的时候他们的output越接近越好
- 新model和旧model的L2 norm差距越小越好

**Layer Transfer**：只训练某几层的参数，其余参数迁移冻结

- 那些层的参数可以被迁移
  - 语音：通常迁移最后几层（语音可以看成：声音讯号->发音方式->辨识结果；通常声音讯号->发音方式人和人不一样，发音方式->辨识结果跟人无关。）
  - 图像：通常迁移前面几层（前几层通常检测最简单的图案，比如检测直线、横线或者简单的几何图形；最后几层学习到比较抽象无法迁移。）

## Multitask Learning

> 同时在源数据领域和目标数据领域的效果好。

**几乎所有的语言都可以迁移。**

## Domain-adversarial training

- 任务描述
  - 目标数据： 测试数据
  - 源数据：训练数据
  - 目标数据和源数据非常不匹配
- 例子：图像辨识
  - 目标数据：MNIST-M（无标签）
  - 源数据：MNIST

`通常网络模型的前面几层可以看作是在抽feature，后面几层可以看作是在做classification，把feature做可视化，发现不同领域的数据，他们的feature完全不一样。`

- 处理方式：抽特征时，消除领域特性（不同领域的feature不应该明显分开，应该混合在一起）
  - 在feature extractor后面接一个domian classfier，区分抽取的特征属于哪一个领域（消除领域特性：不管看到那个特征都视为同一领域）
  - feature extractor输出的feature需要同时骗过domian classfier还要让label predictor做的好

## Zero-shot Learning

- 任务描述
  - 目标数据： 测试数据
  - 源数据： 训练数据
  - 目标数据和源数据是不同的任务
- 例子：图像辨识
  - 目标数据：其他动物（无标签）
  - 源数据：猫狗
- 语音处理方式：（不可能在训练集上有所有的单词数据）
  - 解决方法：不直接辨识那一段声音属于哪一个word，辨识声音属于哪一个phoneme（音标），再做一个phoneme跟table之间对应关系的表（lexicon：词典），辨识的时候只需要辨识出phoneme，再根据phoneme查表找到对应word。
- 图像处理方式：
  - 解决方法：class（类别）用attributes（特征）表示；辨识图像具备怎样的attributes，然后查表看与那个类别的attributes最接近就属于哪一类。
  - 对应表：可以将每个类的word2vec后的向量作为该类别的attributes。

- Attribute embedding：attribute的dimension很大，做降维。
- 方法：
  - 相同类别的内积大于该类别与不同类别的最大内积，而且要大于一个边界（margin：k）；把相同类别的距离拉近，把不同类别的距离扩大。
  - Convex Combination of Semantic Embedding

## Self-taught Clustering

- 任务描述
  - 目标数据：测试数据
  - 源数据：训练数据
- 从源数据中学习一个好的特征表示模型（feature extractor）。
- 用这个feature extractor在目标数据上抽feature。
