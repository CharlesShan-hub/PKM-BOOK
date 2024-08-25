---
icon: '2'
description: 颜色空间
---

# Color

## Overview

<img src="../.gitbook/assets/file.excalidraw.svg" alt="" class="gitbook-drawing">

## Color Space

### LMS

光是电磁波，按照频率可以绘制出光谱。人眼的三种视锥细胞分别可以吸收三种频率的光。自然界各种频率的光，对于人眼而言，只要转换成三种细胞的吸收情况就可以了。&#x20;

<figure><img src="../.gitbook/assets/image (1) (1).png" alt="https://upload.wikimedia.org/wikipedia/commons/d/d1/Cone_spectral_sensitivities.png"><figcaption><p>LMS Response over the light wavelength (from Wikipedia). L is roughly centered on red, M on green and S on blue. Note that the responses overlap significantly, especially for the L and M cones.[1]</p></figcaption></figure>

人眼的三种视锥细胞对光的响应值的公式如下\[3]，视锥响应函数![{\displaystyle {\bar {l\}}(\lambda ),{\bar {m\}}(\lambda ),{\bar {s\}}(\lambda )}](https://wikimedia.org/api/rest\_v1/media/math/render/svg/1b09aeb060e8ce50c6fcaa63ca4e6ee62ed0f10a) 是LMS颜色空间的颜色匹配函数：

<figure><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/a0f66c09f32a2db12739fe49d7ce13f13c36b031" alt=""><figcaption></figcaption></figure>

<figure><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/8bf4b90785233c594e12ac69e4aad251fb41abfd" alt=""><figcaption></figcaption></figure>

<figure><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/0a45c5b2f886a77529cd13f9bff0c8104e1c7a8a" alt=""><figcaption></figcaption></figure>

LMS代表Long（长波长，对应红色）、Medium（中波长，对应绿色）和Short（短波长，对应蓝色）。建立一个坐标系，坐标轴是三种细胞对某种光刺激的响应值。然后扫描光谱，把不同频率的光对应的响应值绘制在坐标系中。

<figure><img src="../.gitbook/assets/image (4).png" alt="https://commons.wikimedia.org/wiki/File:3D_Graph_of_LMS_Color_Space.png"><figcaption><p><a href="https://commons.wikimedia.org/wiki/File:3D_Graph_of_LMS_Color_Space.png">https://commons.wikimedia.org/wiki/File:3D_Graph_of_LMS_Color_Space.png</a> [2]</p></figcaption></figure>

上图的边缘就代表了所有的纯色。利用这些纯色相互组合，就可以构造出所有的人可以看到的颜色。提现在图中，就是上图中的任意两点，连成一条线，这条线就是可以被这两个纯色插值出来的所有颜色。

<figure><img src="../.gitbook/assets/image (2) (1).png" alt="" width="375"><figcaption><p>https://www.bilibili.com/video/BV1U34y1G7wa/?t=1673</p></figcaption></figure>

以上我们就得到了所有的人眼可见的颜色。但是注意，还有好多人眼不可见的区域也在这个正方体中。比如“超绿色”，这是人们不能看到的，因为人的视锥细胞对某个频率会两种细胞都刺激到而并不会只刺激到一种。比如频率为 550Hz 的光，红色和绿色的视锥细胞都会有反应值。

<figure><img src="../.gitbook/assets/image (3) (1).png" alt="【C02.02 Imaging - Colorspace】 【精准空降到 30:51】 https://www.bilibili.com/video/BV1U34y1G7wa/?share_source=copy_web&#x26;vd_source=0470ad56f59229195a0a7f79ab37cb27&#x26;t=1851" width="400"><figcaption><p>https://www.bilibili.com/video/BV1U34y1G7wa/?t=1851</p></figcaption></figure>

### XYZ

LMS 中，人眼的三种视锥细胞的响应值是归一化过的。三种视锥细胞的真实的响应函数是这样的。

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>XYZ color matching functions, CIE 1931 and Stockman &#x26; Sharpe 2006.[4]</p></figcaption></figure>

可以看到，上图中的蓝色响应函数的最大值很大，如果它被标准化到 1，相比红色和绿色而言会有很多的颜色被压缩。所以 XYZ 把 LMS 的蓝色维度保持不变，保持了三种响应函数彼此的一个比例关系，从而让色彩空间看起来更加“舒展”，这样如果后续需要进行抽样，可以更均衡的表示各种颜色。

<figure><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/4a15573a77cd48decc68aada921e4ff01a6d24e2" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
其实 XYZ 的提出要早于 LMS！上面的内容其实是从实用主义的角度往回推导。从另一个角度想，其实 XYZ 也给 LMS 提供了科学依据，因为 LMS 从细胞的角度进行了精确的测量。
{% endhint %}

下面我们还是回到 LMS，想象由坐标轴三个顶点进行连线，将颜色空间切开。这个切面的三个点就是三个最极限的纯色，三角形内部的点就是三个顶点插值的结果。另外，三角形上任意一点与原点相连，可以提现亮度的变化（原点是黑色，三角形上一点是某一颜色的最亮）

<figure><img src="../.gitbook/assets/image (1).png" alt="" width="249"><figcaption><p>https://www.bilibili.com/video/BV1U34y1G7wa/?t=1973</p></figcaption></figure>

XYZ 其实就是 LMS 的线性变换，XYZ 保持了LMS 的很多性质，比如颜色由三色光组成。但是这个变换让上边的那个三角形扭曲了，得到了 XYZ 里边的三角形，但其原理不变：三维空间某个纯颜色在三角形上投影，这个投影的颜色绘制为这个纯颜色在二维上的表示。

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

得到了我们熟悉的 CIE颜色图（CIE chromaticity diagram）。

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>The Chromaticity Diagram[5]</p></figcaption></figure>

CIE颜色图中上半边曲线是所有频率颜色，也就是前边说的纯颜色，红橙黄绿青蓝紫。图中的下半边直线以及区域内部的点均是插值得到的结果！

{% hint style="info" %}
当然，这个切面肯定不是单纯把 LMS 的切面线性变换了一下这么简单。毕竟 LMS 是后来的理论，XYZ切的角度会不一样。
{% endhint %}

### RGB

上边的理论需要现代生物知识才能做到，RGB 模型诞生于二十世纪，那时的人们怎么确定的人眼对三原色的响应值呢。

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>A Beginner’s Guide to (CIE) Colorimetry[7]</p></figcaption></figure>







## Resources and Reference

{% embed url="https://www.bilibili.com/video/BV1U34y1G7wa" %}

{% embed url="https://www.youtube.com/watch?v=nJlZT5AE9zY" %}

> \[1] [https://daltonlens.org/opensource-cvd-simulation/](https://daltonlens.org/opensource-cvd-simulation/)
>
> \[2] [https://upload.wikimedia.org/wikipedia/commons/5/5d/3D\_Graph\_of\_LMS\_Color\_Space.png](https://upload.wikimedia.org/wikipedia/commons/5/5d/3D\_Graph\_of\_LMS\_Color\_Space.png)
>
> \[3] [https://en.wikipedia.org/wiki/LMS\_color\_space](https://en.wikipedia.org/wiki/LMS\_color\_space)
>
> \[4] [https://en.wikipedia.org/wiki/CIE\_1931\_color\_space](https://en.wikipedia.org/wiki/CIE\_1931\_color\_space)
>
> \[5] [https://www.youtube.com/watch?v=O0nYJ0Mjx10](https://www.youtube.com/watch?v=O0nYJ0Mjx10)
>
> \[6] [https://www.youtube.com/watch?v=AS1OHMW873s](https://www.youtube.com/watch?v=AS1OHMW873s)
>
> \[7] [https://medium.com/hipster-color-science/a-beginners-guide-to-colorimetry-401f1830b65a](https://medium.com/hipster-color-science/a-beginners-guide-to-colorimetry-401f1830b65a)
