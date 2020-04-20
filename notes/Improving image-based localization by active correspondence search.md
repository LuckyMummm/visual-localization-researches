## TL;DR

是Fast image-based localization using direct 2D to-3D matching这篇文章的改进版本，主要是在效果方面的改进。



## Related work

**一个经典的方法：**

- Irschara, A., Zach, C., Frahm, J.M., Bischof, H.: From structure-from-motion point clouds to fast location recognition. In: CVPR. (2009)

**延伸做法，将3D点云重投影出更多的virtual图像用来做检索：**

- Wendel, A., Irschara, A., Bischof, H.: Natural landmark-based monocular localization for mavs. In: ICRA. (2011)

**提出一个metric，根据query image以及rough pose estimate来预测哪些3D点是匹配上的：**

- Alcantarilla, P.F., Ni, K., Bergasa, L.M., Dellaert, F.: Visibility learning in largescale urban environment. In: ICRA. (2011)

**用到重建images的共识图关系来提升3D-2D匹配：**

- Li, Y., Snavely, N., Huttenlocher, D.P.: Location recognition using prioritized feature matching. In Daniilidis, K., Maragos, P., Paragios, P., eds.: ECCV 2010, Part II. LNCS, vol. 6312, Springer, Heidelberg (2010) 

**vocabulary based的方法丢失了一定的精度，为何丢失的以及如何提升**

- Philbin, J., Chum, O., Isard, M., Sivic, J., Zisserman, A.: Lost in quantization: Improving particular object retrieval in large scale image databases. In: CVPR. (2008)



## 算法

这篇文章号称结合了2D-3D以及3D-2D的优点，首先2D-3D的优点是准但是慢，3D-2D当然就是快。

（3D-2D指的是给单个点，去queryimage中找最相似的feature；2D-3D就是给一个feature去找点）

方法是首先相对于每一个point都对应到word，然后图片的每一个feature也对应到word，然后找feature有公共单词的point。这步骤叫做2D-3D，思路和作者前面那篇fast 2d-3d一样。然后利用了一个信息，就是point周围的点匹配的概率更大，于是在这里可以维护一个优先队列，把这个point周围的点按一定的优先级送进去做，然后遍历这个队列做3D-2D匹配。（所以是仅仅在初始化的时候做了一个2D-3D的匹配）

#### 一些加速手段

- 2D-3D匹配激活activative search之后，通过共识图关系，把最开始找到那个点周围没有共识图关系的点全部都移除队列
- 在RANSAC之前移除一些不属于子图的点（视为outliers），具体操作得看paper





