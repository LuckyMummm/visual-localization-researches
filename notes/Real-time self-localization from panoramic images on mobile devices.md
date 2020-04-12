

# Real-time self-localization from panoramic images on mobile devices

## 背景 && TL;DR

- **作者：** Arth C, etc.
- **会议/期刊**：ISMAR, 2011
- **TL;DR：** 针对室外场景，比室外场景多一个合成全景图片再做定位的操作。



## 核心算法

大的系统和室内的流程一致，多了一个用image stiching得到全景图的操作。文中也并没有过多得介绍这个全景图到底采用的哪个算法。



## 实验部分

- 文中提到pose estimation用到的inliers大概占匹配到的features的5%-10%，占检测到的features的1%-2%。说明它的pose estimation算法的稳定性，很值得参考。
- 在全景下的误差大概达到84%落在1m内，88%落在5°内；


  ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gdrel57w44j30w509gq82.jpg)

- 再看FoV带来的影响，非常明显

  ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gdremrrucxj30we0ao168.jpg)

## 展望

- **有一个问题，没有看明白这篇文章里面的GT是怎么得到的？**
- 因为系统的重定位流程是incremental的，所以这里做全景也是增量处理的，从这里延伸去联想一下，所以对于大图片其实是可以做并行提取特征的。