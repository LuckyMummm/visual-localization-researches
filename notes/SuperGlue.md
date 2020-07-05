# SuperGlue

## Info

* **Archive:** Image Matching
* **Paper link:** https://arxiv.org/pdf/1911.11763.pdf
* **Conference:** CVPR 2020
* **Publish date:** 2020
* **Code:** https://github.com/magicleap/SuperGluePretrainedNetwork
* **Author:**
  * Paul-Edouard Sarlin1(ETH&Magic Leap)
  * ......



## TL; DR (summarize this paper in one sentence or two)

**Build a learning middle-end of SLAM system by using DL methods to match local features between two images. It's performance surpass other traditional method.**



## Contribution

- A SLAM system can be decomposed into **front-end**(feature extration), **back-end**(bundle adjustment). However we usually ignore the **middle-end** by using a naive way to tackle it. This paper present a novel and learnable feature matching method.

- learnable architecture which combine graph network and transformer(amazing!)

### Architecture:  Graph Network + Transformer

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggg9sds0kwj31po0g4wlq.jpg)

See the forward way:

**Step1.** Given two images with their local features(descriptors and positions)

**Step2.** **Keypoint encoder:** "x" is a intermediate representation for local feature.

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggg9uex9uxj30fm02qt8t.jpg)

**Step3. Multiplex Graph Neural Network** (connect the ervery two nodes by self-edge and cross-edge)

**The forward path of GNN:**

- between layers:

  - "m" means edges, $`\varepsilon`$ = $`\varepsilon_{self}`$ when layer is odd and   $`\varepsilon`$ = $`\varepsilon_{cross}`$ when layer is even.

  ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggga0e6gipj30p003o74j.jpg)

- between nodes(aggreate attention):

  ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggga8auoygj30hy056mxf.jpg)

  - Given a local feature in image Q and a local feature in image S. We have the formulation below. The motivation is key, query and value in tranformer.

    ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gggad7h4nij30m60803z9.jpg)

  - Then $`\alpha_{ij}=Softmax_j(q_i^T k_j)`$ . Just like using key to query a database.

  By using the forward path above, we can get the representation of local feature at a certain layer, called $`f_i`$.

- **Step4.** **Optimal matching layer**

  - Once we got the representation vector of local feature, we can build a score matrix by inner product.
  - Because there are still some contraines in graph matching like one node just match one. So we need to find a assignment $`P`$ to let $`\sum_{i,j}S_{i,j}P_{i,j}`$ achieve largest. This is equivalent to solving a linear assignment problem. (classical bipartite matching problem)
  - By using a differential method which called Sinkhorn Algorithm, we can achieve that.
  - (another trick is dustbin row and column to collect those local features which can't find proper matching node)

**The backward path of GNN:**

  - loss function

    ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gggavywx6pj30nk07e3z2.jpg)

    - $`M`$ is set of groud truth matches
    - $`I`$ and $`J`$ are set of unmatched local feature



## Experiment

### Inference Time

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gggazm6l8sj30ey07yt9i.jpg)

### Homography estimation

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gggb0ixu95j30en058dgc.jpg)

The SuperGlue with DLT performs better than RANSAC. Very convinced.(means the mismatches are few)



### Indoor estimation

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gggb2w8z1bj30gb0a575t.jpg)

### Outdoor estimation

~

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gggb52dok1j30v70u0qv5.jpg)



## Thoughts

思路非常新颖和make sense，效果看上去也是特别感人。之前一直说由于在slam领域有比较完备的几何学知识在，所以深度学习不太能颠覆这个方向。与之前那些end-end做pose estimation的文章不一样，这篇文章选择的方向特别好，就是把几何学擅长的地方保留还是用几何学方法，把深度学习擅长地地方统统用深度学习替换掉。

这个方法值得实测一下，说不定能对现有slam系统或者重定位的recall有大幅度的提升。


