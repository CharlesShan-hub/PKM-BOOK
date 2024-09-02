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

### 行程编码

行程长度编码（Run- Length Encoding，RLE）压缩算法是Windows系统中使用的一种图像文件压缩方法

例如：RRRRRGGBBBBBB -> 5R2G6B

### LZW编码



***

## 预测编码

> 基于图像数据的空间或时间冗余特性，用相邻的已知像素（或像素块）预测当前像素（或像素块）的取值，然后再对预测误差进行量化和编码，包括脉冲编码调制（PCM）​、差分脉冲编码调制（DPCM）等。

### DM 编码





### DPCM 编码







***

## 变换编码

> 将空域上的图像变换到另一变换域上，变换后图像的大部分能量只集中到少数几个变换系数上，采用适当的量化和熵编码就可以有效地压缩图像。

### K-L 变换





### DCT 变换





***

## 混合编码

> 混合编码是综合了熵编码、变换编码或预测编码的编码方法，如JPEG标准和MPEG标准。

### JPEG



***

## Reference

