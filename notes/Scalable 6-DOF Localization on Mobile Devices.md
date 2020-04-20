## TL; DR

结合了local tracking和global localization的mobile应用，特点是drift-free并且不需要处理loop-closures了。



## Related Work

**用于室外location recognition的工作**

- Li, Y., Snavely, N., Huttenlocher, D., Fua, P.: Worldwide Pose Estimation Using 3D Point Clouds. In: ECCV (2012)

**导航**

- Irschara, A., Zach, C., Frahm, J.M., Bischof, H.: From Structure-from-Motion Point Clouds to Fast Location Recognition. In: CVPR (2009)

- 针对这个任务提了一些优化策略：simpler descriptor等等

  Lim, H., Sinha, S.N., Cohen, M.F., Uyttendaele, M.: Real-Time Image-Based 6-DOF Localization in Large-Scale Environments. In: CVPR (2012)

  

**大场景下的定位**（每8m * 5m地图大小增加100M）

- Lhuillier, M.: Fusion of GPS and Structure-from-Motion Using Constrained Bundle Adjustments. In: CVPR (2011)
- Ventura, J., Hollerer, T.: Wide-Area Scene Mapping for Mobile Visual Tracking. In: ISMAR (2012)



## 算法

**Local Pose Tracking using SLAM**

这个不多说，就是slam那一套

**Server-based Global Localization**

找2D-3D匹配使用的这篇文章的方法：Improving Image-Based Localization by Active Correspondence Search.

然后pose estimate用的是RANSAC.

**融合（本文最核心的点）**

这个融合和一般的融合不太一样，不只有两个坐标系对齐的问题，是真的在做融合。

不一样的点是这里融合的出发点是local tracking是可调的，借助global localization的方法实现精度更高的local tracking。

反投影误差：

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ge0mf137luj30r804kgm0.jpg)

- 策略一：Alignment Using the Global Keyframe Positions

  对于local tracking，一个反投影误差再加上一个和global localization的位姿差的二范数一起去优化。

  ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ge0mfgtxqgj30f404i3yn.jpg)

- 策略二：Alignmnet Using the Global 2D-3D Matches

  作者认为有时候global给出的pose不一定准确，比如说当pose estimation选得点比较集中的时候；所以这里对于local tracking，优化的目标就是一个反投影误差再加上一个2D-3D匹配，不同的是这个3D点是global坐标系下的3D坐标。

  ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ge0mfts6m6j30r0048dg9.jpg)

## 实验

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ge0m9swgmej31ka0s415t.jpg)

三条轨迹从左到右对应的三种融合方式

- 一次对齐
- 上述第一种融合
- 上述第二种融合

**误差指标**

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ge0mmg83olj31gg070abq.jpg)



## 借鉴意义

如果slam和localization都可调的话，这篇paper里面提到的方式肯定是极好的。

