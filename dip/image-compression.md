---
icon: '7'
description: 图像压缩
---

# Image Compression

## Overview

<img alt="" class="gitbook-drawing">

***

## 熵编码

> 熵编码或统计编码属于无损编码，给出现概率较大的符号赋予一个短码字，给出现概率较小的符号赋予一个长码字，从而使最终的平均码长很小。主要的熵编码方法包括哈夫曼编码、香农编码、算术编码等。

### 哈夫曼编码

扫描各种颜色的像素出现的概率，然后按照概率大小组成哈夫曼编码。（个人感觉意义不大）

<figure><img src="../.gitbook/assets/image (39).png" alt="" width="563"><figcaption></figcaption></figure>

<details>

<summary>Demo(他给的代码其实有问题)</summary>

```
2 
4 1
0 011
1 010
3 00
```

```python
import numpy as np
import queue
"""
定义需要进行编码的图像
"""
image = np.array(
    [
        [3,1,2,4],
        [2,4,0,2],
        [2,2,3,3],
        [2,4,4,2]
    ]
)
"""
计算每种元素出现的概率
"""
hist = np.bincount(image.ravel(), minlength=5)
probabilities = hist / np.sum(hist)
"""
找出数据中的最小元素
"""
def get2smallest(data):
    first = second = 1;
    fid = sid = 0
    for idx, element in enumerate(data):
        if (element < first):
            second = first
            sid = fid
            first = element
            fid = idx
        elif (element < second and element != first):
            second = element
    return fid, first, sid, second
""""
定义哈夫曼树节点
"""
class Node:
    def __init__(self):
        self.prob = None
        self.code = None
        self.data = None
        self.left = None
        self.right = None      # 元素值存储在叶节点
    def __lt__(self, other):
        if (self.prob < other.prob):  # 定义优先树中排序规则
            return 1
        else:
            return 0
    def __ge__(self, other):
        if (self.prob > other.prob):
            return 1
        else:
            return 0
"""
构建哈夫曼树
"""
def tree(probabilities):
    prq = queue.PriorityQueue()
    for color, probability in enumerate(probabilities):
        leaf = Node()
        leaf.data = color
        leaf.prob = probability
        prq.put(leaf)
    while (prq.qsize() > 1):
        newnode = Node()    #  创建新节点
        l = prq.get()
        r = prq.get()    #  找出叶节点中概率最小的两个
        # 移除最小的两个节点
        newnode.left = l    # 左侧是较小的
        newnode.right = r
        newprob = l.prob + r.prob   # 新的概率是两个小概率相加
        newnode.prob = newprob
        prq.put(newnode)    #  插入新节点，替代原有的两个节点
    return prq.get()     # 返回根节点，完成树的构建
"""
对哈夫曼树进行遍历，得出编码
"""
def huffman_traversal(root_node, tmp_array, f):
    if (root_node.left is not None):
        tmp_array[huffman_traversal.count] = 1
        huffman_traversal.count += 1
        huffman_traversal(root_node.left, tmp_array, f)
        huffman_traversal.count -= 1
    if (root_node.right is not None):
        tmp_array[huffman_traversal.count] = 0
        huffman_traversal.count += 1
        huffman_traversal(root_node.right, tmp_array, f)
        huffman_traversal.count -= 1
    else:
        huffman_traversal.output_bits[
            root_node.data] = huffman_traversal.count  # 得出每个元素的编码值
        bitstream = ''.join(str(cell) for cell in tmp_array [1:huffman_traversal.count])
        color = str(root_node.data)
        wr_str = color + ' ' + bitstream + '\n'
        f.write(wr_str)  #  保存到文件中
    return
root_node = tree(probabilities)
tmp_array = np.ones([4], dtype=int)
huffman_traversal.output_bits = np.empty(5, dtype=int)
huffman_traversal.count = 0
f = open('codes.txt', 'w')
huffman_traversal(root_node, tmp_array, f)  # 遍历树结构，给出编码
```

</details>

### 算术编码

> 个人觉得也意义不大，跳过吧

<details>

<summary>解释</summary>

算术编码的算法思想如下。

1. 对一组信源符号按照符号的概率从大到小排序，将\[0,1)设为当前分析区间。按信源符号的概率序列在当前分析区间划分比例间隔。
2. 检索“输入消息序列”​，锁定当前消息符号（初次检索的话就是第一个消息符号）​。找到当前符号在当前分析区间的比例间隔，将此间隔作为新的当前分析区间，并把当前分析区间的起点（即左端点）指示的数“补加”到编码输出数里。当前消息符号指针后移。
3. 仍然按照信源符号的概率序列在当前分析区间划分比例间隔。然后重复第二步，直到“输入消息序列”检索完毕为止。
4. 最后的编码输出数就是编码好的数据。

在算术编码中需要注意3个问题。

1. 由于实际计算机的精度不可能无限长，运算中出现溢出是一个明显的问题，但多数计算机都有16位，32位或者64位的精度，因此这个问题可以使用比例缩放方法解决。
2. 算术编码器对整个消息只产生一个码字，这个码字是在间隔\[0,1)中的一个实数，因此译码器在接收到表示这个实数的所有位之前不能进行译码。
3. 算术编码是一种对错误很敏感的编码方法，如果有一位发生错误，就会导致整个消息译错。

算术编码可以是静态的或者是自适应的。在静态算术编码中，信源符号的概率是固定的。在自适应算术编码中，信源符号的概率根据编码时符号出现的频率动态地修改，在编码期间估算信源符号概率的过程叫作建模。需要开发动态算术编码的原因是事前知道精确的信源概率是很难的，而且不切实际。当压缩消息时，不能期待一个算术编码器获得最大的效率，所能做的最有效的方法是在编码过程中估算概率。因此，动态建模就成为确定编码器压缩效率的关键。

</details>

### RLE编码

> 比较简单，也可以略

行程长度编码（Run- Length Encoding，RLE）压缩算法是Windows系统中使用的一种图像文件压缩方法

例如：RRRRRGGBBBBBB -> 5R2G6B

### LZW编码

> wiki\[1], 各种版本的 LZW 实现\[2], geeksforgeeks\[3]

* 数据流（CharStream）​：对象（文本文件的数据序列）
* 编码流（CodeStream）：输出对象（经过压缩运算的编码数据）​
* 编译表（String Table）​：编译表不是事先创建好的，而是根据原始文件数据动态创建的
* LZW压缩算法的基本原理：提取原始文本文件数据中的不同字符，基于这些字符创建一个编译表，然后用编译表中的字符的索引替代原始文本文件数据中的相应字符，减少原始数据大小。

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>[4] encoding <a href="https://www.bilibili.com/video/BV1rp4y117WB">https://www.bilibili.com/video/BV1rp4y117WB</a></p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>[5] <a href="https://www.bilibili.com/video/BV15p4y1C71G">https://www.bilibili.com/video/BV15p4y1C71G</a></p></figcaption></figure>

详细过程感觉并不好记，使用时随时翻阅资料吧

***

## 预测编码

> 基于图像数据的空间或时间冗余特性，用相邻的已知像素（或像素块）预测当前像素（或像素块）的取值，然后再对预测误差进行量化和编码，包括脉冲编码调制（PCM）​、差分脉冲编码调制（DPCM）等。

### DM 编码

* wiki\[6]：[https://en.wikipedia.org/wiki/Delta\_modulation](https://en.wikipedia.org/wiki/Delta\_modulation)
* 精髓是用变换来保存序列。
* 做法是用上行和下行两种信号模拟一个连续信号，把连续信号转换成离散。
* 需要用过采样，即以比奈奎斯特速率高几倍的速率对模拟信号采样。
* DM 是 DPCM 的最简单形式。

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>Demo</summary>

比如对\[33, 35, 34, 36, 35]进行编码，步长为 4.5

![](<../.gitbook/assets/image (3).png>)

结果就是\[33, 1, 0, 1, 0]，其中 33 代表初始的位置，1 代表上升，0 代表下降。

</details>

### DPCM 编码

* wiki\[7]：[https://en.wikipedia.org/wiki/Differential\_pulse-code\_modulation](https://en.wikipedia.org/wiki/Differential\_pulse-code\_modulation)
* 精髓也是用变化代替绝对值。
  * 这个变化是用某个像素的一边（下例是 左，左上，上三个方向）来预测这个像素。然后用预测值与本像素相减，得到误差。
  * 这个误差会经过量化，这一步引入了误差，也达到了压缩的目的。

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>Demo</summary>



```python
import numpy as np
from skimage import data
from skimage import transform
from matplotlib import pyplot as plt

def quantize_error(error,level):
    max=255
    min=-255
    q=(max-min)/level
    i=1
    while(error>=min+q*i):
        i=i+1
    quantized_error=min+q*(i-1)+q/2
    return  quantized_error

def DPCM_encoder(img,level):
    N=img.shape[0]
    predictor=np.zeros(shape=(N,N))
    quantized_error=np.zeros(shape=(N,N))
    for i in range(N):
        for j in range(N):
            if i==0:
                if j==0:
                    predicted=0
                else:
                    predicted=0.95*predictor[i,j-1]
            else:predicted=0.95*predictor[i-1,j]+0.95*predictor[i,j-1]-0.95**2*predictor[i-1,j-1]
            error=img[i,j]-predicted
            quantized_error[i,j]=quantize_error(error,level)
            predictor[i,j]=predicted+quantized_error[i,j]
        for j in range(i,N):
            if i==0:
                predicted = 0.95 * predictor[j - 1, i]
            else:predicted=0.95*predictor[j-1,i]+0.95*predictor[j,i-1]-0.95**2*predictor[j-1,i-1]
            error=img[j,i]-predicted
            quantized_error[j,i]=quantize_error(error,level)
            predictor[j,i]=predicted+quantized_error[j,i]
    return quantized_error

def DPCM_decoder(error):
    N=error.shape[0]
    img=np.zeros(shape=(N,N))
    predictor=np.zeros(shape=(N,N))
    for i in range(N):
        for j in range(N):
            if i==0:
                if j==0:
                    predicted=0
                else:
                    predicted=0.95*predictor[i,j-1]
            else:
             predicted=0.95*predictor[i-1,j]+0.95*predictor[i,j-1]-0.95**2*predictor[i-1,j-1]
            img[i,j]=predicted+error[i,j]
            predictor[i,j]=predicted+error[i,j]
    return img

if __name__ == '__main__':
    levels=32
    img=data.coffee()
    img=transform.resize(img,(img.shape[0],img.shape[0],3), preserve_range=True)
    plt.subplot(1,3,1)
    plt.title("Original")
    plt.imshow(img/255.0)
    img_r=img[:,:,0]
    encoded_img_r=DPCM_encoder(img_r,levels)
    decoded_img_r=DPCM_decoder(encoded_img_r)
    decoded_img_r=decoded_img_r.reshape((decoded_img_r.shape[0], decoded_img_r.shape[1],1))
    img_g = img[:, :, 1]
    encoded_img_g = DPCM_encoder(img_g, levels)
    decoded_img_g = DPCM_decoder(encoded_img_g)
    decoded_img_g = decoded_img_g.reshape((decoded_img_g.shape[0],decoded_img_g.shape[1],1))
    img_b = img[:, :, 2]
    encoded_img_b = DPCM_encoder(img_b, levels)
    decoded_img_b = DPCM_decoder(encoded_img_b)
    decoded_img_b = decoded_img_b.reshape((decoded_img_b. shape[0],decoded_img_b.shape[1],1))
    decoded_img=np.concatenate([decoded_img_r,decoded_img_g, decoded_img_b],2)
    
    plt.subplot(1,3,2)
    plt.title("Reconstructed")
    plt.imshow(decoded_img/255.0)
    plt.subplot(1,3,3)
    plt.title("Error")
    error = np.abs((img-decoded_img))
    error/=np.max(error)
    plt.imshow(error*4,vmin=0, vmax=1)
    plt.show()
```

</details>

***

## 变换编码

> 将空域上的图像变换到另一变换域上，变换后图像的大部分能量只集中到少数几个变换系数上，采用适当的量化和熵编码就可以有效地压缩图像。
>
> 典型的准最佳变换有DCT（离散余弦变换）​、DFT（离散傅里叶变换）​、WHT（Walsh Hadama变换）​、HrT（Haar变换）等。

### K-L 变换

* K-L 变换又称 Hotelling 变换，特征向量变换或主分量方法（这个就是主成分分析法吧。。）





<details>

<summary>Demo</summary>



</details>

### DCT 变换





***

## 混合编码

> 混合编码是综合了熵编码、变换编码或预测编码的编码方法，如JPEG标准和MPEG标准。

### JPEG



***

## Reference

\[1] [https://en.wikipedia.org/wiki/Lempel%E2%80%93Ziv%E2%80%93Welch](https://en.wikipedia.org/wiki/Lempel%E2%80%93Ziv%E2%80%93Welch)

\[2] [https://rosettacode.org/wiki/LZW\_compression](https://rosettacode.org/wiki/LZW\_compression)

\[3] [https://www.geeksforgeeks.org/lzw-lempel-ziv-welch-compression-technique/](https://www.geeksforgeeks.org/lzw-lempel-ziv-welch-compression-technique/)

\[4] [https://www.bilibili.com/video/BV1rp4y117WB](https://www.bilibili.com/video/BV1rp4y117WB)

\[5] [https://www.bilibili.com/video/BV15p4y1C71G](https://www.bilibili.com/video/BV15p4y1C71G)

\[6] [https://en.wikipedia.org/wiki/Delta\_modulation](https://en.wikipedia.org/wiki/Delta\_modulation)

\[7] [https://en.wikipedia.org/wiki/Differential\_pulse-code\_modulation](https://en.wikipedia.org/wiki/Differential\_pulse-code\_modulation)

