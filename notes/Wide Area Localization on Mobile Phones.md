## Wide area localization on mobile phones

## 背景 && TL;DR

- **作者：**Arth C, Wagner D, Klopschitz M, Irschara A, Schmalstieg D
- **会议/期刊**：ISMAR, 2009
- **TL;DR：** 先重建再对输入图片位姿估计，并且重建的数据存储采用了PVS(potentially visible sets)。（应该是第一篇在wide area做重定位思路的文章）



## 核心算法

### 算法Pipeline

![](https://tva1.sinaimg.cn/large/00831rSTgy1gdm9cbslilj30de0fygmy.jpg)

### 重建

- Global Registration
  - 就是通过一对无序的图片得到每张图片的全局位姿
- PVS(potentially visible sets)
  - "we propose a method for dividing large 3D reconstructions into serveral smaller parts that can be compactly represented and allow for building a highly scalabel system."

### 重定位

- feature extraction and description
  - 这里看作者的意思是它们重建的时候拿SIFT重建，但是在重定位的时候是采用的一个更快速的自己实现版本去做的重定位（比SURF和GPU-SIFT还快好几倍）。**这也侧面提供了一个思路，就是重定位的特征提取器不一定需要和重建的保持一致。**
- Feature matching, optional voting, outilier removal
  - Way-1：直接拿输入图片在当前PVS的所有图片里面去找匹配，然后传给下一步；
  - Way-2：vocabulary tree voting scheme
    - 先找到那些和输入图片匹配点比较多的图片，再传给下一步；
  - 但是仅有上面两步，并不能解决误匹配的问题（文章这里把误匹配定义为outliers），于是这里加入了一个RANSAC。**（具体的算法没有阐述，还得细看参考文献）**
- pose estimation
  - EPnP是在2008年才提出来，所以作者在这里也没有提EPnP而是直接做了一个优化问题求解。



## 实验效果

- 作者这里评估精度的方法是用的Reprojection Error有点意外

![](https://tva1.sinaimg.cn/large/00831rSTgy1gdm9t4shfjj30d30afq35.jpg)

- 时间

  ![](https://tva1.sinaimg.cn/large/00831rSTgy1gdm9ui44lej30fx0c1mz4.jpg)



## 展望

这篇文章提供的思路很好，其中重定位的第二步很有借鉴意义，可以细看如何去掉误匹配点。

