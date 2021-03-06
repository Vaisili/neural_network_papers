# 论文阅读笔记

**记录一些读过的论文，给出个人对论文的评分情况并简述论文insight**

**评分细节：** 

- 5分：值得反复阅读的论文，非常具有启发性

- 4分：值得精读的论文，具有一定的启发性

- 3分：值得粗略阅读的论文，了解论文大概思想后会有一定收获

- 2分：价值不大的论文，读完基本没有收获

- 1分：粗制滥造的论文

> 论文将按照年份/评分依次排序，绝大多数论文将会给出[arXiv](https://arxiv.org/)的链接.


# Table of contents

- [论文阅读笔记](#论文阅读笔记)
- [Table of Contents](#table-of-contents)
- [Semi-supervised](#semi-supervised)

# Semi-supervised

> 半监督学习。

- [ReMixMatch: Semi-Supervised Learning with Distribution Alignment and Augmentation Anchoring](https://arxiv.org/abs/1911.09785) (ICLR2020)
    - 4分
    - 对MixMatch做了两点改进。
    - 1.distribution alignment:鼓励模型在期望意义下的输出分布逼近p(y)。将每个伪标签后处理，对齐有标记数据的p(y)分布，隐式地实现上述目标(就像MixMatch中用sharpen隐式地实现熵最小原则一样)。
    - 2.augmentation anchor: 类似AutoAugment的一种更强的数据增强。notice:将一致性正则中常用的平方损失换成了交叉熵。
    - 还加上了自监督里比较经典的Rotation Loss。

- [FixMatch: Simplifying Semi-Supervised Learning with Consistency and Confidence](https://arxiv.org/abs/2001.07685) (NIPS2020)
    - 4分
    - 相对于ReMixMatch来说更加简单直观。相比MixMatch的改进主要在于一致性正则的一些不同:
    - 1.平方差异损失改为了交叉熵损失(一定好吗?原文并没有讨论。)
    - 2.sharpen label改为带threshold的one-hot label。ablation study中认为前者需要多一个超参但并没有带来明显提升。
    - 3.MixMatch:原样本输出分布去逼近aug样本输出分布。FixMatch:weak aug样本的输出分布去逼近strong aug样本的输出分布。这里本质上还是strong aug带来的提升。

- [Self-training with Noisy Student improves ImageNet classification](https://arxiv.org/abs/1911.04252) (CVPR2020)
    - 4分
    - 与传统self-training或者KD的区别在于两点：Our  key  improvements  lie  in  adding  noise  to  the  student and using student models that are not smaller than the teacher.
    - When applied to unlabeled data, noise has an important benefit of enforcing invariances in the decision function on both labeled and unlabeled data.

- [Temporal Ensembling for Semi-Supervised Learning](https://arxiv.org/abs/1610.02242) (ICLR2017)
- [Virtual Adversarial Training: A Regularization Method for Supervised and Semi-Supervised Learning](https://arxiv.org/abs/1704.03976) (TPAMI2018)
- [Mean teachers are better role models: Weight-averaged consistency targets improve semi-supervised deep learning results](https://arxiv.org/abs/1703.01780) (NIPS2017)
- [MixMatch: A Holistic Approach to Semi-Supervised Learning](https://arxiv.org/abs/1905.02249) (NIPS2019)
    - 5分
    - semi-supervised learning必读经典，基本都包括了两个重要原则:
    - 1.一致性正则:相同的输入应该产生相同的输出。通常采用原样本与aug样本两者输出的平方差异损失。
    - 2.最小熵准则:分类面应该穿过低密度区域，即对样本输出的置信度较高，即输出分布的熵最小。通常采用样本输出与伪标签之间的交叉熵来实现。因为不管是转化为one-hot还是sharpen后的伪标签(sharpen相当于是soft版本的ont-hot)，都相较于输出分布有着更小的熵。



