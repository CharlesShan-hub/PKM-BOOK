---
icon: '2'
description: 颜色空间
---

# Color

Overview

<img src="../.gitbook/assets/file.excalidraw.svg" alt="" class="gitbook-drawing">



LMS(Long, Medium, Short)就是运用这一原理的色彩模式。



### Color Space

#### LMS

光是电磁波，按照频率可以绘制出光谱。人眼的三种视锥细胞分别可以吸收三种频率的光。自然界各种频率的光，对于人眼而言，只要转换成三种细胞的吸收情况就可以了。&#x20;

<figure><img src="../.gitbook/assets/image (1).png" alt="https://upload.wikimedia.org/wikipedia/commons/d/d1/Cone_spectral_sensitivities.png"><figcaption><p>LMS Response over the light wavelength (from Wikipedia). L is roughly centered on red, M on green and S on blue. Note that the responses overlap significantly, especially for the L and M cones.[1]</p></figcaption></figure>

人眼的三种视锥细胞对光的响应值的公式如下\[3]，视锥响应函数![{\displaystyle {\bar {l\}}(\lambda ),{\bar {m\}}(\lambda ),{\bar {s\}}(\lambda )}](https://wikimedia.org/api/rest\_v1/media/math/render/svg/1b09aeb060e8ce50c6fcaa63ca4e6ee62ed0f10a) 是LMS颜色空间的颜色匹配函数：

<figure><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/a0f66c09f32a2db12739fe49d7ce13f13c36b031" alt=""><figcaption></figcaption></figure>

<figure><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/8bf4b90785233c594e12ac69e4aad251fb41abfd" alt=""><figcaption></figcaption></figure>

<figure><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/0a45c5b2f886a77529cd13f9bff0c8104e1c7a8a" alt=""><figcaption></figcaption></figure>

建立了一个坐标系，坐标轴是三种细胞对某种光刺激的响应值。然后扫描光谱，把不同频率的光对应的响应值绘制在坐标系中。

<figure><img src="../.gitbook/assets/image.png" alt="https://commons.wikimedia.org/wiki/File:3D_Graph_of_LMS_Color_Space.png"><figcaption><p><a href="https://commons.wikimedia.org/wiki/File:3D_Graph_of_LMS_Color_Space.png">https://commons.wikimedia.org/wiki/File:3D_Graph_of_LMS_Color_Space.png</a> [2]</p></figcaption></figure>

上图的边缘就代表了所有的纯色。利用这些纯色相互组合，就可以构造出所有的人可以看到的颜色。提现在图中，就是上图中的任意两点，连成一条线，这条线就是可以被这两个纯色插值出来的所有颜色。

<figure><img src="../.gitbook/assets/image (2).png" alt="" width="375"><figcaption><p>https://www.bilibili.com/video/BV1U34y1G7wa/?t=1673</p></figcaption></figure>

以上我们就得到了所有的人眼可见的颜色。但是注意，还有好多人眼不可见的区域也在这个正方体中。比如“超绿色”，这是人们不能看到的，因为人的视锥细胞对某个频率会两种细胞都刺激到而并不会只刺激到一种。比如频率为 550Hz 的光，红色和绿色的视锥细胞都会有反应值。

<figure><img src="../.gitbook/assets/image (3).png" alt="【C02.02 Imaging - Colorspace】 【精准空降到 30:51】 https://www.bilibili.com/video/BV1U34y1G7wa/?share_source=copy_web&#x26;vd_source=0470ad56f59229195a0a7f79ab37cb27&#x26;t=1851" width="400"><figcaption><p>https://www.bilibili.com/video/BV1U34y1G7wa/?t=1851</p></figcaption></figure>

下面我们就只考虑人眼可见的颜色了。我们把取过坐标轴的三个顶点的平面，这就是

### Awesome Resources

{% embed url="https://www.bilibili.com/video/BV1U34y1G7wa" %}

{% embed url="https://www.youtube.com/watch?v=nJlZT5AE9zY" %}

### Reference

> \[1] [https://daltonlens.org/opensource-cvd-simulation/](https://daltonlens.org/opensource-cvd-simulation/)
>
> \[2] [https://upload.wikimedia.org/wikipedia/commons/5/5d/3D\_Graph\_of\_LMS\_Color\_Space.png](https://upload.wikimedia.org/wikipedia/commons/5/5d/3D\_Graph\_of\_LMS\_Color\_Space.png)
>
> \[3] [https://en.wikipedia.org/wiki/LMS\_color\_space](https://en.wikipedia.org/wiki/LMS\_color\_space)
