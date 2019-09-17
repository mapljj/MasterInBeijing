## Detection Survey

大佬们表示通用物体检测有如下困难：

![屏幕快照 2019-07-05 下午4.11.09.png](https://upload-images.jianshu.io/upload_images/13965778-34167cdba9814454.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###框架：two stage/one stage

1. 早期Region Based方法是image上选择候选区域，CNN提取特征，构建分类器(SVM等)

   - Baseline-**RCNN** including: 

     1. Region proposal computation(using selective search): Crop Region  from the image and warp into the same size

     2. Finetuned CNN model: AlexNet from ImageNet extract the fixed length features from original region

     3. Class specific SVM classifiers: Region 分类

     4. Class specific bounding box regressors：Region 回归

        ![屏幕快照 2019-07-05 下午4.44.00.png](https://upload-images.jianshu.io/upload_images/13965778-9f756dc4947d7302.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   - **SPPNet**：为了减少Region进入CNN带来的开销，引入了SPP层，使得不同大小的区域的特征长度一致。

     ![屏幕快照 2019-07-05 下午4.42.03.png](https://upload-images.jianshu.io/upload_images/13965778-669943a7cd667e80.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     ![屏幕快照 2019-07-05 下午4.42.44.png](https://upload-images.jianshu.io/upload_images/13965778-f2f35a215ee70765.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. Two Stage方法：

   - Baseline—**Fast RCNN**: 

     1. BackBone: Finetuned CNN extract Feature Map from original Image
     2. ROI pooling: 在Feature Map上划分Interst region，并抽取fixed shape feature
     3. 二阶段：细分类和框回归

     引入了ROI(Region of Interest)pooling，multi-task loss(Classification and Regressor),实现了end-2-end的pipeline。

     ![屏幕快照 2019-07-05 下午4.55.38.png](https://upload-images.jianshu.io/upload_images/13965778-29be3af60f5df746.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   - **Faster RCNN**：Propose RPN(region proposal net) to generate region proposals; Anchor 真香 以及真正地有了两次的框回归和分类。

     **Acnhor的数值，效果需要again**，太熟悉了被干的彻彻底底

     ![屏幕快照 2019-07-05 下午5.04.27.png](https://upload-images.jianshu.io/upload_images/13965778-30c6e0c5d4124dc7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     

   - **RFCN**: using Fully Convolutional Network(花里胡哨不常用)

     全程使用CNN，没有FC也就没有了ROI pooling等后续操作。从而使得二阶段的分类和回归也是roi 共享的。

     **Key**：深层的CNN对**category semantic**敏感而对**translation**不敏感导致直接使用CNN预测框回归效果较差。所以添加了Conv分支，如下：

     ![屏幕快照 2019-07-05 下午5.25.23.png](https://upload-images.jianshu.io/upload_images/13965778-fed303fd73b9a168.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   - **Mask RCNN**: 解决pixelwise object instance segmentation， propose **RoIAlign**解决量化误差，在二阶段添加FCN分支预测mask，如下：

     ![屏幕快照 2019-07-05 下午5.31.58.png](https://upload-images.jianshu.io/upload_images/13965778-60053eaf8961133f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     

   - **Cascade RCNN**: The essence of **cascade** is to learn more discriminative classifiers by using multistage classifiers. 

     > Two-stage object detection can be considered as cascade of two object detectors, the first object detector removes large amount of background regions and the second stage classifying the remaining regions

     所以Cascade RCNN的本质是一个IOU选择的问题，核心就是利用不断提高的阈值，在保证样本数不减少的情况下训练出高质量的检测器。(效果很惊艳)

     > **只有proposal自身的阈值和训练器训练用的阈值较为接近的时候，训练器的性能才最好**

     ![屏幕快照 2019-07-05 下午5.45.44.png](https://upload-images.jianshu.io/upload_images/13965778-8a2fac80bae37046.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     ![屏幕快照 2019-07-05 下午5.52.12.png](https://upload-images.jianshu.io/upload_images/13965778-0ed0b4c0a35e662e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. One Stage:

   - **DetectorNet:** 早期的废弃想法

   - **OverFeat**：OverFeat performs object detection in a **multiscale sliding window fashion** via a **single forward** pass through the fully convolutional layers in the network，其pipeline如下：

     1. Generate object candidates by performing object classification
        via a **sliding window fashion on multiscale images**.

     2. Increase the number of predictions by **offset max pooling**

     3. Bounding box regression and Combine predictions.

        ![屏幕快照 2019-07-05 下午6.09.49.png](https://upload-images.jianshu.io/upload_images/13965778-03bb2c0c657e69a7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   - **YOLO**：将original Image分成了S\*S的网格，然后每个网格预测类别和Box的回归量，那么最后得到了S\*S个候选框。

     > a unified detector casting object detection as a regression
     > problem from image pixels to spatially separated bounding boxes
     > and associated class probabilities.

     YOLO快但是效果一般，并且由于网格设置，对小物体检测结果相当差。

     改进版本：**YOLOv2** /**YOLO9000**，**YOLOv3**

     YOLOv2: Trick真香以及Anchor真香。

     ![屏幕快照 2019-07-05 下午6.22.46.png](https://upload-images.jianshu.io/upload_images/13965778-5485cf6c09edc4c5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     ![屏幕快照 2019-07-05 下午6.25.25.png](https://upload-images.jianshu.io/upload_images/13965778-105240d7c56a4817.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     YOLOv3: 引入多尺度，同时使用更好的BackBone，具体而言有：

     - 多个二分类取代Softmax
     - 每种尺度预测3个box, anchor的设计方式仍然使用聚类,得到9个聚类中心,将其按照大小均分给3中尺度.
     - 尺度1: 在基础网络之后添加一些卷积层再输出box信息 ；尺度2: 从尺度1中的倒数第二层的卷积层上采样(x2)再与最后一个16x16大小的特征图相加,再次通过多个卷积后输出box信息.相比尺度1变大两倍；尺度3: 与尺度2类似,使用了32x32大小的特征图.

   - **SSD**：一开始就使用多尺度预测方法：结合Anchor先验框；利用卷积进行检测。

      在VGG的基础上增加更深的卷积层获得更多更大的语义信息；

     - [ ] 预测Proposal时的encode/decode问题(与Faster RCNN的应该有点区别)。

     ![屏幕快照 2019-07-05 下午6.34.16.png](https://upload-images.jianshu.io/upload_images/13965778-42c60af862a561f8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     SSD改进的方法有：

   - **CornerNet**:(基于Key Point 的detection方法) 使用左上角/右下角的一组点来表示Detection Box；提出Corner Pooling，获得角点信息；同时使用Hourglass Network；
   
  类似的改进有：
   
  1. Center Net：each object as a triplet of keypoint,使用角点检测，中心点过滤;
     2. Extreme Net: 检测四个极值点和中心点；暴力枚举，基于几何方式组合得到检测框；
     3. FCOS: 使用FPN类似的多尺度预测；预测点到四个边的距离；提出centerNes用于使预测点接近box的中心同时过滤无关的预测点；
     4. Center Net：object as a point；检测中心点
   

4. **BackBone**(Object Representation): 

   -  Only CNN Arch: (e.g. Hourglass, Dilated Residual Networks, Xception, DetNet,Dual Path Networks(DPN), FishNet, GLoRe)

     ![屏幕快照 2019-07-08 上午11.08.15.png](https://upload-images.jianshu.io/upload_images/13965778-898592fab5f2d983.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   - **Multi-Scale Object**: 

     核心问题: CNN中底层feature 位置信息丰富而语义信息缺失；高层语义信息丰富而缺乏位置信息；单层feature不可能适合检测所有的物体；

     - [ ] **combined features** of multiple CNN layers: 

       using **Concat** combine feature and increased computational complexity.

       ![屏幕快照 2019-07-08 上午11.34.20.png](https://upload-images.jianshu.io/upload_images/13965778-0f3341ba0a24ce30.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 

       ![image.png](https://upload-images.jianshu.io/upload_images/13965778-ac8df4de8ea81f61.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     - [ ] Detecting at **multiple CNN layers**: SSD/MSCNN/RBF/DSOD

       **SSD**: using **multi scale Anchor** on **multiple conv layers**

       **RFBNet**: imporve the SSD where the later conv layers are replaced with a Receptive Field Block(RFB), which **inception** and **dilated convolution**

       ![屏幕快照 2019-07-08 上午11.47.14.png](https://upload-images.jianshu.io/upload_images/13965778-854efc6c0faa4583.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

       **MSCNN**:  applies **deconvolution**

       **TridentNet** ：好像很有效，建议下午看一看。

       ![屏幕快照 2019-07-08 上午11.42.24.png](https://upload-images.jianshu.io/upload_images/13965778-ce489d9277565307.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     - [ ] Combination of two method: (lots of method and effecive)

       FPN/DSSD/TDM/ZIP/RON/RefineDet: construct the feature pyramid according to the **inherent multiscale** pyramidal architecture of the backbone, including: **top-down** network and **lateral features**

       主要的区别是: **Feature Fusion Block**的不同以及Pyramid策略。

       ![屏幕快照 2019-07-08 下午12.10.09.png](https://upload-images.jianshu.io/upload_images/13965778-c2ad36762f7c45e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

       PANet/FPR/DetNet/M2Det: 基本结构没有变化，只是显得复杂了许多

       **PANet**:adding **another bottom-up path** with clean **lateral connections** from the low level to top ones; an adaptive feature
       pooling was proposed to aggregate features from all feature levels
       for each proposal

       ![屏幕快照 2019-07-08 下午7.04.18.png](https://upload-images.jianshu.io/upload_images/13965778-3301323620daf1fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

       **FPR**(花里胡哨，没有奶子用):explicitly reformulating the feature pyramid construction process;  **extracts features** from multiple layers in the backbone network by **adaptive concatenation** and then designs a more complex FFB module

       ![屏幕快照 2019-07-08 下午7.38.55.png](https://upload-images.jianshu.io/upload_images/13965778-874cfc47c5de2781.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

       **DeNet**: introducing **dilated convolutions** to the later layers of the backbone network in order to maintain high spatial resolution in deeper layers.

       ![屏幕快照 2019-07-08 下午7.44.31.png](https://upload-images.jianshu.io/upload_images/13965778-8045b479813952fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

       **MLFPN**: much more complex for different scales

       ![屏幕快照 2019-07-08 下午7.50.57.png](https://upload-images.jianshu.io/upload_images/13965778-c97a43974f223936.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

       Table:

       ![image.png](https://upload-images.jianshu.io/upload_images/13965778-a99fdb0a05d8fd25.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   - IntraClass Variations, including: 

     1. **Geometric transformations in object scale, pose, rotation, viewpoint and part deformations;**(caused by the lack ability of be spatially invariant to the geometric transformations of the input data for CNN)

        Methods: Spatial Transformer Networks (**STN**) in text/face detection ;Deformable Part based Models(**DPMs**) in deep learning ;

        - DeepIDNet:  **a deformation constrained pooling layer** to replace a regular max pooling layer

        - Deformable Convolutional Networks(**DCN**): a deformable convolution and RoI pooling layer, both of which are based on the idea of augmenting the regular grid sampling locations in the feature maps with **additional position offsets** 

        - **DPFCN**: proposed deformable part based RoI pooling layer which **selects discriminative parts** of objects around object proposals by simultaneously optimizing latent displacements of all parts

          ![屏幕快照 2019-07-08 下午8.14.58.png](https://upload-images.jianshu.io/upload_images/13965778-e494a3ad0dc554c6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     2. **Occlusions**: 遮挡问题现在主要是使用可形变卷积；Someone 尝试了**GAN**，也许是以后的趋势；
     3. **Image degradations, such as caused by illumination changes, blur, motion, low resolution, noise and weather conditions**：No dataset so not work focus on this

     

5. **Context**  Modeling: 一直是我关注的问题；Context can be grouped into: **Semantic context**: The likelihood of an object to be found in
   some scenes but not in others; **Spatial context**: The likelihood of finding an object in some position and not others with respect to other objects in the scene;**Scale context**: Objects have a limited set of sizes relative to
   other objects in the scene, so there are these methods:

   - **Global Context**:image or scene level context. **DeepIDNet** use the image classification scores; **ION ** use **spatial RNN** to explore contextual information across the entire image. 

   - **Local Context**: 这个我熟悉啊，全是VRD那边的方法。**relationship** among locally nearby objects, as well as the interactions between an object and its surrounding area. Spatial Memory Network(**SMN**): 就那个外置记忆模块的傻子玩意。 Object Relation Network(**ORN**): attention is all your need, 想当初我也这么搞过23333 。Structure Inference Network(**SIN**)：就那个贼唬人的关系图的那个。

   - **Local context via larger window**：normally by **enlarging the detection window size** to extract some form of local context：

     - **MRCNN**：Multi Region for object feature

       ![屏幕快照 2019-07-08 下午8.43.45.png](https://upload-images.jianshu.io/upload_images/13965778-a52ee2a30f1257ce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     - Gated BiDirectional CNN(**GBDNet**):

       **multiscale contextualized regions** surrounding an object proposal to improve detection performance and use gate to control the message.

       ![屏幕快照 2019-07-08 下午8.46.31.png](https://upload-images.jianshu.io/upload_images/13965778-799d23dd736b53f7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     - Attention to Context CNN(**ACCNN**)

       both global and local contextual information to facilitate object detection. **Multiscale Local Contextualized (MLC)** subnetwork was proposed to generates an attention map.

       ![屏幕快照 2019-07-08 下午8.49.10.png](https://upload-images.jianshu.io/upload_images/13965778-8005f2d6913f64d5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

     - **CoupleNet**:

       captures object information with position sensitive RoI pooling and added one branch to encode the global context information with RoI pooling.

       ![屏幕快照 2019-07-08 下午8.50.45.png](https://upload-images.jianshu.io/upload_images/13965778-d60cf1bd193a1e61.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   

6. **Other Special Issues**:

   - Data Augmentation:

   - **Novel Training Strategies**: **object scale**/**image resolution**/**Batch Size**

     Methods: SNIP/SNIPER/MegNet(这几个贼强)

   - Reducing Localization Error: noval **IOU loss**,  **Soft NMS**, **Cassade RCNN**.

   - Class **Imbalance**: **Focal Loss**, Online Hard Example Mining (**OHEM**) and Gradient Harmonizing Mechanism (**GHM**). 

     ![屏幕快照 2019-07-08 下午9.13.01.png](https://upload-images.jianshu.io/upload_images/13965778-ba7ccb4633a88bc2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



### 结论: 

1. two stage 比one stage 模型复杂度更高，精度也更优

2. one stage 比two stage 对BackBone更不敏感, e.g. res50=>res101的提升

3. 推断时BackBone耗时最为明显，并且通过降低候选proposal的个数可以明显提升two stage方法的速度

4. one stage 方法对于检测小物体(<32*32)效果不佳，但是对于大物体大家都是差不多的

5. 在detection的设计中，有如下趋势:**Fully convolutional pipeline** — simple, efficient, and elegant;**Exploring complementary information** from other correlated tasks ;**Sliding window** – making it easier to learn the classifier; **Fuse information** from different layers of the backbone Network.

   **Cascade, Anchor Free**可能是未来的重点

6. 现有detection 框架中各部分存在的问题

   - BackBone: 大多数模型明显受到BackBone的限制‘

   - Object Scale and Small Object: **Image Pyramids**/**feature from multi resolutions conv layers**/**Dilated conv**/**Multi Scale Anchor**

   - Deformation, occlusion, and other factors:  using **spatial transformer
     network** and based on **deformable part-based model**.

     **Rotation invariance may be attractive in certain applications such as detection from satellite image**, 比如之前做过的那个卫星云图，可能旋转不变形更重要一点。

7. Context Reason: Context information 对于小物体/遮挡物体应该会有所改善。

### 面试问题

数据集问题

并集， IOU的计算

mAP的计算

FPN, Guided Anchor, FCOS, CenterNet, 

