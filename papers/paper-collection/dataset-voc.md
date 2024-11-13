# Dataset：VOC

## Overview

* 目标检测数据集PASCAL VOC简介：[https://arleyzhang.github.io/articles/1dc20586/](https://arleyzhang.github.io/articles/1dc20586/)

<table><thead><tr><th width="90">Year</th><th align="center">Statistics</th><th align="center">New developments</th><th align="center">Notes</th></tr></thead><tbody><tr><td>2005</td><td align="center"><ul><li>4类：摩托车、自行车、汽车、人</li><li>训练+验证+测试</li><li>1578 张图，2209 个物体</li></ul></td><td align="center"><ul><li>分类</li><li>检测</li></ul></td><td align="center"><ul><li>这些图片大部分都是从公开的数据集上截取的，并不像flickr图片那样具有挑战性。</li><li>此数据集已过时。</li></ul></td></tr><tr><td>2006</td><td align="center"><ul><li>10类：自行车，公共汽车，汽车，猫，牛，狗，马，摩托车，人，羊</li><li>训练+验证+测试</li><li>2618 张图，4754 个物体</li></ul></td><td align="center">图片来自Flickr和Microsoft Research Cambridge（MSRC）数据集</td><td align="center"><ul><li>MSRC图像比Flickr更容易，因为照片通常集中在感兴趣的对象上。</li><li>此数据集已过时。</li></ul></td></tr><tr><td>2007</td><td align="center"><p></p><ul><li><em>人：</em>人</li><li><em>动物：</em>鸟，猫，牛，狗，马，羊</li><li><em>交通工具：</em>飞机、自行车、船、公共汽车、汽车、摩托车、火车</li><li><em>室内：酒瓶、椅子、餐桌、盆栽、沙发、电视/显示器</em></li><li>训练+验证+测试</li><li>9936 张图，24640 个物体，20 种物体</li></ul></td><td align="center"></td><td align="center"></td></tr></tbody></table>





## VOC 2005

1. **Introduction**
   1. 往年的数据集（Caltech 5，UIUC）已经性能饱和。
   2. VOC 2005 加入了更多变异性。
2. **Challenge**
   1. 在真实场景中识别 4 种物体类别：摩托车、自行车、汽车和人。
   2. **分类**： 预测测试图像中是否存在特定类别的物体实例。
   3. **检测**： 预测测试图像中每个目标类别的物体实例的边界框和标签。
3. **Image Sets**
   1. 第一组：train、val、train+val、test1（简单版的测试集）
   2. 第二组：train、val、train+val、test2（更多遮挡、更多尺度变化和姿态变化）
   3. 删掉了太小的（像斑点一样大的车），太密集的（自行车架上的一排自行车）
   4. 加入了负样本（即不包含目标类别的图像）：没有汽车的道路图像；在汽车与非汽车的判断任务中，其他物体也可以成为负样本；汽车、摩托车、自行车和人都可能出现在街道场景中，这样的重用图像也会让任务更逼真。
   5.  数量统计（107 代表图片数量，109 代表物体数量，其他同理）



       <table><thead><tr><th width="101">类别</th><th>train</th><th>val</th><th>test1</th><th>test2</th></tr></thead><tbody><tr><td>摩托</td><td>107、109</td><td>107、108</td><td>216、220</td><td>179、202</td></tr><tr><td>自行车</td><td>57、63</td><td>57、60</td><td>114、123</td><td>241、342</td></tr><tr><td>人</td><td>42、81</td><td>42、71</td><td>84、149</td><td>441、874</td></tr><tr><td>车</td><td>136、159</td><td>131、161</td><td>275、341</td><td>211、295</td></tr></tbody></table>
   6.  test1 举例

       <figure><img src="../../.gitbook/assets/voc-2005-example.png" alt=""><figcaption></figcaption></figure>
   7.  test2 举例

       <figure><img src="../../.gitbook/assets/voc-2005-example2.png" alt=""><figcaption></figcaption></figure>
4.
5. 本章其余部分的结构如下。第2节描述了为挑战定义的各种比赛。第3节描述了为挑战赛参与者提供的培训和测试数据集。第4节定义了挑战赛的分类竞赛和评估方法，并讨论了用于分类的方法参与者的类型。第5节定义了挑战的检测竞争和评估方法，并讨论了用于检测的方法参与者的类型。第6节介绍了参与者提供的方法。第7节展示了分类竞赛的结果，第8节展示了检测竞赛的结果。第9节最后讨论了挑战结果、挑战研讨会参与者提出的挑战的各个方面以及未来挑战的前景。

**挑战目标**

* 在真实场景中识别 4 种物体类别：摩托车、自行车、汽车和人。P2
*

**挑战设置**

* **数据集**：
  * **第一组数据集**： 包含训练、验证和测试数据，用于训练和初步评估。P3
  * **第二组数据集（test2）**： 包含更具变异性（更多遮挡、更多尺度变化和姿态变化）的测试数据，用于更严格的评估。P6
  * **负样本**： 使用包含其他类别物体的图像作为负样本，以增加挑战难度。P7
* **竞赛**：
  * **分类**： 根据 training data 和 test data 的选择，分为 4 个竞赛。P9
  * **检测**： 根据 training data 和 test data 的选择，分为 4 个竞赛。P14

**参赛方法**

* **分类**：
  * **局部特征分布**： 使用 SIFT 描述符，并以“词袋”模型表示图像。P10
  * **单个局部特征**： 使用 SIFT 描述符和颜色特征，并为每个局部特征分配类别概率。
  * **分割区域**： 结合全局和局部特征，使用 SOM 进行分类。P11
  * **检测**： 使用检测器识别物体，并使用边界框或分割掩码进行训练。P11P12
* **检测**：
  * **局部特征配置**： 使用 SIFT 描述符，并以“词袋”模型表示图像，并考虑特征的空间配置。P15
  * **基于窗口的分类器**： 使用卷积神经网络或 HOG 描述符，并在图像窗口上运行分类器。P16
  * **基线方法**： 使用简单的基线方法，例如使用训练数据中的平均边界框或所有 Harris 点的边界框。P16

**结果**

* **分类**： INRIA-Jurie 和 INRIA-Zhang 方法在 EER 和 AUC 测量方面表现最佳。
* **检测**： Darmstadt 方法在摩托车类别上表现最佳，INRIA-Dalal 方法在自行车和汽车类别上表现最佳。P52P53
* **数据集难度**： test2 数据集比 test1 数据集更具挑战性，并且不同类别之间的性能差异较大。P54

**讨论**

* 数据集中的错误和标注问题需要改进。P60P61
* 训练数据量有限，需要更大规模的训练数据集。P61
* 数据集的难度与 test data 相比可能不足。P61
* 测试数据的发布可能会影响参赛者的方法优化。P61
* 评估方法需要进一步改进。P61P62
* 未来挑战可以考虑增加类别数量和提供更灵活的训练数据。P62

**总结**

PASCAL VOC 2005 物体识别挑战推动了物体识别领域的研究，并展示了各种方法的性能和局限性。未来挑战可以进一步改进数据集、评估方法和竞赛设置，以推动该领域的发展。