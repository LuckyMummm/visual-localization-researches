# Fast image-based localization using direct 2D to 3D matching

## 背景 && TL;DR

- **作者：**Torsten Sattler, Bastian Leibe, Leif Kobbelt
- **会议/期刊**：ICCV 2011
- **TL;DR：** 提出了一种直接找2d-3d的匹配方法，用来替代之前的image retrieval。



## 核心算法

- 出发点

  基于image retrieval的方法能检测出很多特征点，但是inlier点的数量只占特征点数量的很少一部分，所有浪费了特别多匹配时间。那能不能快速找到那些存在对应3D的2D点呢？

- 这篇文章就提出了一个Direct 2D-3D的匹配方法，如下图所示。所谓direct的方式就是不通过中间结构（比如说image retrieval），直接拿有descriptor信息的2D特征点和有descriptor信息的3D特征点做匹配。

  ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gdrxjlijucj30te07ewhy.jpg)



- 详细：
  - 3D point representation 描述符的选取提供了两种思路
  - Prioritized search 选描述子比较小的选匹配**（这里没搞明白？）**
  - RANSAC设置一个拒绝时间，跑太慢意味着跑不出来、拒绝，这个思路很有参考意义。



## 实验效果

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gdrxv1oydwj30ua0690ud.jpg)



## 展望

#### **Reference**

**这篇文章主要参考了两篇文献，对于retrieval还有挺有参考价值**

  - A. Irschara, C. Zach, J.-M. Frahm, and H. Bischof. From structure-from-motion point clouds to fast location recognition. In CVPR, 2009、

  - Y. Li, N. Snavely, and D. P. Huttenlocher. Location recognition using prioritized feature matching. In ECCV, 2010

    这篇介绍的说核心思想是在2D-3D匹配之后，做pose estimation的时候对3D点排列一个优先级，共识图越多的3D点就认为优先级越高，然后 按照优先级选取一定数量的点就好了。