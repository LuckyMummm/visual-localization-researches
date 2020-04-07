## Image-based camera localization: an overview

## 背景 && TL;DR

- **作者：**[Yihong Wu](https://arxiv.org/search/cs?searchtype=author&query=Wu%2C+Y), [Fulin Tang](https://arxiv.org/search/cs?searchtype=author&query=Tang%2C+F), [Heping Li](https://arxiv.org/search/cs?searchtype=author&query=Li%2C+H) （自动化所）
- **会议/期刊：**Visual Computing for Industry, Biomedicine, and Art, 2018

- **TL;DR：**分已知环境和未知环境分别总结了基于图片输入的重定位算法。（我比较关心已知环境）



## 核心算法

#### 已知环境

这篇文章直接将这种场景定义为perspective-n-point problem，也就是PnP问题。并且讨论了当点对n>=6时，PnP是一个线性问题；当n=3，4，5时，PnP是一个非线性问题。**（这个怎么理解？）**

一般情况而言，n=3，4，5的情况在实际中比较少见，大多是大于等于6的情况：

- 算法效率上的研究（单个算法）
  - EPnP O(n)复杂度的算法，用作BA的初始值，是ETH在2008年提出的；
  - ...
- 大场景下localization（先查询在求位姿这种pipeline）
  - **（这里文章很多，大部分很有参考价值，就不一一列举了，后面再细看）**

#### 未知环境

其实也就主要是slam的方法，这里作者讨论各种slam方法，参考意义不大。



## 展望

**relocalization：**深度学习相关工作逐渐火起来，但是实际系统还是用的传统方法为主。

**冷门研究：**小场景的PnP；几何学的SfM（应该是已经做得差不多了）

**有价值的研究：**大场景下的PnP（可能通过多传感器融合）；几何和深度学习结合；多特征融合...



