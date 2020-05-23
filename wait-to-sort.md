# system

**一个经典的方法：**

- Irschara, A., Zach, C., Frahm, J.M., Bischof, H.: From structure-from-motion point clouds to fast location recognition. In: CVPR. (2009)

**比较老且不太相关的方法：**

- Pose Tracking from Natural Features on Mobile Phones. ISMAR 2008

  这个做的是用SIFT以及另外一个分类器来做平面的tracking

- Klein, G., Murray, D.: Parallel Tracking and Mapping for Small AR Workspaces. In: ISMAR (2007)

  Klein, G., Murray, D.: Parallel Tracking and Mapping on a Camera Phone. In: ISMAR (2009)

  这个是在还在3G时代的iPhone上做的一个slam系统的尝试，但是提出了一个比较有意义的结构，就是**PTAM**，就是说用两个线程分别来做帧间的tracking以及mapping。这一点可以参考orb-slam，估计后面的slam系统都沿用了这个设计。

**用于室外location recognition的工作**

Li, Y., Snavely, N., Huttenlocher, D., Fua, P.: Worldwide Pose Estimation Using 3D Point Clouds. In: ECCV (2012)


##### 针对这个任务提了一些优化策略：simpler descriptor等等，14年之前的SOTA模型

 Lim, H., Sinha, S.N., Cohen, M.F., Uyttendaele, M.: Real-Time Image-Based 6-DOF Localization in Large-Scale Environments. In: CVPR (2012)

**大场景下的定位**（每8m * 5m地图大小增加100M）

- Lhuillier, M.: Fusion of GPS and Structure-from-Motion Using Constrained Bundle Adjustments. In: CVPR (2011)
- Ventura, J., Hollerer, T.: Wide-Area Scene Mapping for Mobile Visual Tracking. In: ISMAR (2012)

##### 商场的重定位，不用SfM，而是使用商场平面图

通过单张图片和商场的平面图来实现定位，需要文字检测辅助以及标注数据，精度比较差...

Lost Shopping! Monocular Localization in Large Indoor Spaces Shenlong Wang, Sanja Fidler. ICCV Oral, 2015



# retrieval

**延伸做法，将3D点云重投影出更多的virtual图像用来做检索：**

Wendel, A., Irschara, A., Bischof, H.: Natural landmark-based monocular localization for mavs. In: ICRA. (2011)

**提出一个metric，根据query image以及rough pose estimate来预测哪些3D点是匹配上的：**

Alcantarilla, P.F., Ni, K., Bergasa, L.M., Dellaert, F.: Visibility learning in largescale urban environment. In: ICRA. (2011)

**用到重建images的共识图关系来提升3D-2D匹配：**

Li, Y., Snavely, N., Huttenlocher, D.P.: Location recognition using prioritized feature matching. In Daniilidis, K., Maragos, P., Paragios, P., eds.: ECCV 2010, Part II. LNCS, vol. 6312, Springer, Heidelberg (2010) 

**vocabulary based的方法丢失了一定的精度，为何丢失的以及如何提升**

Philbin, J., Chum, O., Isard, M., Sivic, J., Zisserman, A.: Lost in quantization: Improving particular object retrieval in large scale image databases. In: CVPR. (2008)