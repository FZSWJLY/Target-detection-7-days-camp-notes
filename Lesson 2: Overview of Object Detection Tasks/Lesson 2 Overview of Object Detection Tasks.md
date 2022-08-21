### 1.2 目标检测算法基础知识

#### 传统目标检测算法

![在这里插入图片描述](https://img-blog.csdnimg.cn/3b70b884a28640e3bf9b2e7fb02da186.png#pic_center)


- 滑动窗口

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/1a125cf6919c4d1b8f88bd8d61a630b6.png#pic_center)


  **候选区域（Proposal Region）**：每个AiBj所代表的矩形框，也被称为**感兴趣区域**（Region of Interest，RoI）

- SIFT、HOG

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/3cf742a07a62463f8d8b102ba39a4884.png#pic_center)


- SVM、Adaboost

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/cd1d0b3d8f4a41558f1cb2141387860b.png#pic_center)


- NMS：过滤框

#### 深度学习的优势

![在这里插入图片描述](https://img-blog.csdnimg.cn/287410e6a24c44fba7080583b141252d.png#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/940fb0d09c82438d82809582c39ef1a4.png#pic_center)


#### 两阶段之RCNN：深度学习方法提取特征

![在这里插入图片描述](https://img-blog.csdnimg.cn/30258717d17648b49b4865453aba21bd.png#pic_center)


#### 两阶段之Fast/Faster-RCNN

![在这里插入图片描述](https://img-blog.csdnimg.cn/0102f1e0e4da475b9beb5698b44a8efc.png#pic_center)


- 引入RoI Pooling操作，解决重复特征提取问题
- 将**分类和回归**损失统一在同一个框架中
- 通过SS（selective search)提取候选框，速度慢，不是端到端

![在这里插入图片描述](https://img-blog.csdnimg.cn/de8acd867213496b8d64f4de8659bb5f.png#pic_center)


- 通过RPN（Region proposal network)学习候选区域
- 提高了精度，速度快

#### Anchor和Anchor-Based方法

- **Anchor（锚框）：**
  - **预先**设定好**比例**的一组**候选框**集合
  - 滑动窗口提取
- **Anchor Based Methods：**
  - 使用Anchor提取候选目标框
  - 在特征图上的每一个点，对Anchor进行**分类和回归**

![在这里插入图片描述](https://img-blog.csdnimg.cn/cce3869783ee415c9b49fc8b4ee2f0f9.png#pic_center)


#### Anchor-Based方法：两阶段

![在这里插入图片描述](https://img-blog.csdnimg.cn/1280ac8c8b514ba29c2434b473b1d440.png#pic_center)


- **两阶段方法：**
  - 先使用anchor回归候选目标框，划分**前景和背景**
  - 使用候选目标框进一步进行**回归和分类**，输出最终目标框和对应的类别
  - R-CNN系列
    - RCNN、Fast-RCNN、FasterRCNN
    - FPN、CascadeRCNN、LibraRCNN，...

#### Anchor-Based方法：一阶段

![在这里插入图片描述](https://img-blog.csdnimg.cn/41cf02a56171464b8422e720d5824e27.png#pic_center)


- **一阶段方法：**
  - 直接对anchor回归和分类最终目标框和类别
  - 算法：
    - YOLOv2 YOLOv3
    - SSD、RetinaNet

#### Anchor缺点

![在这里插入图片描述](https://img-blog.csdnimg.cn/d49fb337a0eb419db469914fdad26ad9.png#pic_center)


#### Anchor-Free方法

![在这里插入图片描述](https://img-blog.csdnimg.cn/5f783c5eb6704d13bed0cd49dd64fe04.png#pic_center)


- 不再使用预先设定的anchor，通常通过预测目标的中心或者角点，对目标进行检测
- 基于**多关键点联合表达**的方法：
  - CornerNet/CornerNet-lite
  - CornerNet:Keypoint Triplets for Object Detection
  - RepPoints
- 基于**中心区域**预测的方法：
  - FCOS
  - CornerNet:Object as Points

#### 深度学习算法小结

![在这里插入图片描述](https://img-blog.csdnimg.cn/12805cf211dc483eb7c2123375084569.png#pic_center)


#### 三类算法对比

|          | Anchor-Based单阶段 | Anchor-Based两阶段 | Anchor-Free |
| -------- | ------------------ | ------------------ | ----------- |
| 网络结构 | 简单               | 复杂               | 简单        |
| 精度     | 优                 | 更优               | 较优        |
| 预测速度 | 快                 | 稍慢               | 快          |
| 超参数   | 较多               | 多                 | 相对少      |
| 扩展性   | 一般               | 一般               | 较好        |

#### 基础概念

- BBox：Bounding Box，边界框
  - 绿色为人工标注的groud-truth，红色为预测结果
  - xyxy：左上＋右下
  - xywh：左上＋宽高

![在这里插入图片描述](https://img-blog.csdnimg.cn/60fdef69a134486eb66d6f6d0fe0987d.png#pic_center)


- Anchor：锚框
  - 人为设定不同长宽比、面积的先验框
  - 在单阶段SSD检测算法中也称Prior box

![在这里插入图片描述](https://img-blog.csdnimg.cn/eee3b203d9704b4bb49db16ddbfeb24e.png#pic_center)


- RoI：Region of Interest

  - 特定的感兴趣区域

- Region Proposal

  - 候选区域/框

- RPN：Region Proposal Network

  - Anchor-based的两阶段提取候选框的网络

- IoU：Intersaction over Union

  - 评价预测框的质量，IoU越大则预测框与标注越接近

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/0dc2053cdc894feb98a4267d5f95e664.png#pic_center)


- mAP

  - TP：IoU>=阈值（如0.3）检测框数量

  - FP：IoU<阈值（如0.3）检测框数量

  - FN：没有检测到的GT数量

  - 举例：

    输入样本：某个类别10个框

    预测结果：预测到8个框，6个正确，2个错误

    Precision：6 / 8 = 0.75

    Recall：6 / 10 = 0.6

    ![在这里插入图片描述](https://img-blog.csdnimg.cn/c65daa7235154a9396d47ae6f05f1833.png#pic_center)


  - P-R曲线：以Precision、Recall为纵、横坐标的曲线。

  - AP（Average Precision）：某一类P-R曲线下的面积

  - mAP（mean Average Precision）：所有类别AP平均

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/86c673bec4d642ef9d769605fc4546dc.png#pic_center)


- **NMS：非极大值抑制，Non-Maximum Suppression**

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/8e1924a434774edf9c7f3ff8ca7c6b10.png#pic_center)


  ```python
  def nms(dets, thresh):
      # boxes位置
      x1 = dets[:, 0]
      y1 = dets[:, 1]
      x2 = dets[:, 2]
      y2 = dets[:, 3]
      # boxes scores
      scores = dets[:, 4]
      
      areas = (x2 - x1 + 1) * (y2 - y1 + 1) # 各box的面积
      order = scores.argsort()[:: -1] # boxes按照score排序
      
      keep = [] # 记录保留下的boxes
      while order.size > 0;
      	i = order[0] # score最大的box对应的index
          keep.append(i) # 将本轮score最大的box的index保留
          
          # 计算剩余boxes与当前box的重叠程度IoU
          xx1 = np.maximum(x1[i], x1[order[1:]])
          yy1 = np.maximum(y1[i], y1[order[1:]])
          xx2 = np.maximum(x2[i], x2[order[1:]])
          yy2 = np.maximum(y2[i], y2[order[1:]])
          
          w = np.maximum(0.0, xx2 - xx1 + 1)
          h = np.maximum(0.0, yy2 - yy1 + 1)
          inter = w * h
          # IoU
          ovr = inter / (area[i] + area[order[1: ]] - inter)
          
          # 保留IoU小于设定阈值的boxes
          inds = np.where(ovr <= thresh)[0]
          order = order[inds + 1]
      return keep
  ```

#### 常用开源数据集

| 数据集          | 类别数 | train图片数，box数 | val图片数，box数 | boxes/Image |
| --------------- | ------ | ------------------ | ---------------- | ----------- |
| Pascal VOC-2012 | 20     | 5717，1.3万+       | 5823，1.3万+     | 2.4         |
| COCO            | 80     | 118287,4万+        | 5000，3.6万+     | 7.3         |
| Object365       | 365    | 600k，9623k        | 38k，479k        | 16          |
| OpenImages18    | 500    | 1643042，86万+     | 100000，69.6万+  | 7.0         |

- 驱动算法发展
- 业务场景提供预训练
- **PaddleDetection提供676类预训练，包含大多数物体，直接使用 或 作为预训练提升业务精度**

[https://github.com/rafaelpadilla/Object-Detection-Metics](https://github.com/rafaelpadilla/Object-Detection-Metics)

### 1.3 PaddleDetection

#### PaddleDetection端到端开发套件

![在这里插入图片描述](https://img-blog.csdnimg.cn/4794b3ac70fb4358800ea50ffad2a761.png#pic_center)


- **自由切换骨干网络、损失函数等，来大幅提升网络性能**
- **预置有效优化策略，用户可直接快速试用**

![在这里插入图片描述](https://img-blog.csdnimg.cn/113bbb6d5177443896baf2631a70719d.png#pic_center)


#### PaddleDetection主要特点

![在这里插入图片描述](https://img-blog.csdnimg.cn/47a94e4c6dd243adbcf86fcc6bac6bea.png#pic_center)


#### 模块化设计

![在这里插入图片描述](https://img-blog.csdnimg.cn/c94ccb911b9940ad8df0b9243b377b14.png#pic_center)


#### 丰富模型库

![在这里插入图片描述](https://img-blog.csdnimg.cn/118f744932614fc8a8c36f44a8126234.png#pic_center)


#### 主要模型效果一览

![在这里插入图片描述](https://img-blog.csdnimg.cn/836030ffff2b49abb31762aa75426dc7.png#pic_center)


#### 其他特色模型

![在这里插入图片描述](https://img-blog.csdnimg.cn/de7b742f96a6421bb3e573aaf71f89ae.png#pic_center)


#### 端到端的能力

![在这里插入图片描述](https://img-blog.csdnimg.cn/5854168f17814de6964209a5b05ad1f4.png#pic_center)


#### 支持VisualDL辅助模型优化

- 可视化训练过程中的指标，如Loss和mAP，实时监控模型训练过程。

![在这里插入图片描述](https://img-blog.csdnimg.cn/77814d57e8a14eb2851aa3d43fb82f9e.png#pic_center)


#### 支持模型压缩

[https://github.com/PaddlePaddle/PaddleSlim](https://github.com/PaddlePaddle/PaddleSlim)

![在这里插入图片描述](https://img-blog.csdnimg.cn/c37d4f515135496d8d9477708cbd8e8a.png#pic_center)


#### 支持移动端部署

![在这里插入图片描述](https://img-blog.csdnimg.cn/054e0ebba48243adbc777f1c16ec8e64.png#pic_center)


#### 支持服务部署

![在这里插入图片描述](https://img-blog.csdnimg.cn/a3d1945c11a1440782a7e48c730bb32e.png#pic_center)



