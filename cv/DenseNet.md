# Densely Connected Convolutional Networks

[paper](https://arxiv.org/abs/1608.06993)

## 1. abstract
- 本文的核心是提出了BC-cov-block，将当前层的feather map传入后续的所有层以增强特征表示，从而实现了密集连接

- 与resnet不同的是，resnet是在每一层的输出上进行跳跃连接，而本文是在每一层的输入上进行跳跃连接，而且是对其后所有层进行连接，相当于$\frac{L(L+1)/2}{L}$个连接

## 2. conclusion
404

## 3. Reading
- introduction（时间均为论文时间）
 - 指出cnn已经是20年前的研究产物，而现代的硬件刚可以训练更深层的网络
 - lenet5达到了5层，vgg达到了19层，去年的highway network和残差网络打破了100层的壁垒
 - 然后讲述为什么深层cnn难以训练，其实还是梯度消失/爆炸的问题，然后说一些模型的设计方案，缓解了这些问题
 - 综上，作者认为当前的结局方案都是创建短路径以连接前后层
 - 提出自己的方案，确保最大化的信息流入神经网络，然后就自前向后连接了全部层，把当前层的特征传给后续所有层
 - 并且这种反直觉的拥有更少的参数，因为无需再提取冗余的特征，传统前馈神经网络可以被视为一个状态算法，一层一层向后传递，近期的研究表明resnet一部分的层只贡献了很少的信息，甚至可以随机丢弃掉。（也就是层深了之后有混子），resnet就类似于展开的递归神经网络，但是参数却显著增加
 - 提出的Denset明确了保留的信息，只向网络的集体知识添加很小一部分特征，优势体现在优化了信息流，并且易于训练，每一层都可以直接访问后面的损失函数和原始输入信号，并且实验表明，densenet还有正则化效应
 - $ x_\ell = H_\ell(x_{\ell-1}) + x_{\ell-1} $ - 对前面所有层的feature map进行相加 ， $ x_{\ell} = H_{\ell}([x_0,x_1,...,x_{\ell-1}]) $
 - 这种计算方式同样没有增加参数，只是进行了过程和，没有增加计算复杂度，这点与resnet相似
 - 优点是，所有的信息可以完整的流通整个神经网络，这使得模型更容易被训练
 - 1980s的一个完全多层连接的概念给了他们启发(本段主要是对相关连接理念模型的介绍)
 - 

## 4. Try some work
### 4.1 what does the author try to accomplish?
- 作者在对前人中在网络中进行连接的方式进行考究后，创造了完全连接，即将前一层的feature map完整的传递给后面的每一层，以此来解决梯度消失的问题
### 4.2 what were the key element of the approach?
- 完全向后层的shortcut connection
### 4.3 what can you use in your work?
- 404
### 4.4 what other reference do you want to follow?
- [CVPR 2017] [ResNeXt](https://arxiv.org/abs/1611.05431): 结合ResNet与分组卷积的进化版本
- [CVPR 2018] [SENet](https://arxiv.org/abs/1709.01507): 引入通道注意力机制增强特征表示
- [CVPR 2018] [MobileNetV2](https://arxiv.org/abs/1801.04381): 轻量化网络设计范式（反向残差结构）
- [CVPR 2019] [DPN](https://arxiv.org/abs/1707.01629): 结合ResNet与DenseNet的双路径网络
- [NeurIPS 2019] [EfficientNet](https://arxiv.org/abs/1905.11946): 复合缩放理论的提出
- [CVPR 2020] [CSPNet](https://arxiv.org/abs/1911.11929): 跨阶段局部网络，解决DenseNet特征冗余问题
- [CVPR 2021] [DynamicDenseNet](https://arxiv.org/abs/2105.04618): 动态调整密集连接路径
- [TPAMI 2022] [ResNet-RS](https://arxiv.org/abs/2103.07579): 重新审视残差网络设计原则

推荐阅读路线：
1. 基础扩展：ResNeXt → SENet（理解现代网络基础组件）
2. 轻量化：MobileNetV2 → ShuffleNetV2 
3. 结构优化：DPN → CSPNet（DenseNet的改进方向）
4. 自动化设计：EfficientNet → RegNet
