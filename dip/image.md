---
icon: '1'
description: 图像的基本概念
---

# Image

> 1. Image：图像
> 2. Sampling：采样
> 3. Quantization：量化
> 4. Neighbor and Distance：邻域与距离

***

## Image

图像就是数组，每个像素点的颜色是响应值。

<figure><img src="../.gitbook/assets/tmp1irw0f42.jpg" alt="宇航员的图片" width="256"><figcaption></figcaption></figure>

<details>

<summary>Code</summary>

```python
import skimage.data as data
from PIL import Image

image = Image.fromarray(data.astronaut())

image.show()
```

</details>

{% hint style="info" %}
skimage.data模块有很多demo 图片python

<pre class="language-python"><code class="lang-python"><strong>print(data.__all__)
</strong><strong>['astronaut', 'binary_blobs', 'brain', 'brick', 'camera', 'cat', 'cell', 'cells3d', 'checkerboard', 'chelsea', 'clock', 'coffee', 'coins', 'colorwheel', 'data_dir', 'download_all', 'eagle', 'file_hash', 'grass', 'gravel', 'horse', 'hubble_deep_field', 'human_mitosis', 'immunohistochemistry', 'kidney', 'lbp_frontal_face_cascade_filename', 'lfw_subset', 'lily', 'logo', 'microaneurysms', 'moon', 'nickel_solidification', 'page', 'palisades_of_vogt', 'protein_transport', 'retina', 'rocket', 'shepp_logan_phantom', 'skin', 'stereo_motorcycle', 'text', 'vortex']
</strong></code></pre>
{% endhint %}

***

## Sampling

采样：从连续信号到离散信号。

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>Code</summary>

```python
import numpy as np
import matplotlib.pyplot as plt

def generate_image(width, height):
    I = np.zeros((width, height))
    for x in range(width):
        for y in range(height):
            I[x, y] = np.cos(x/width*2*np.pi) * np.cos(y/height*2*np.pi) * 255
    return I

def plot(index,n):
    plt.subplot(1,4,index+1)
    plt.imshow(generate_image(n, n), cmap='gray')
    plt.title(f"{n}x{n}")
    plt.axis('off')
for i,n in enumerate([5,15,50,1000]):
    plot(i,n)
plt.show()
```

</details>

***

## Quantization

量化：用多少比特代表每个像素的颜色。

<figure><img src="../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>Code</summary>

```python
import numpy as np
import matplotlib.pyplot as plt

def generate_image(level):
    I = np.zeros((16,256))
    for x in range(256):
        n = 2**level         # 一共多少个格子
        length = int(256/n)  # 每个格子有多大
        I[:, x] = int(x/length) / n
    return I/np.max(I)

def plot(index,level):
    plt.subplot(4,1,index+1)
    plt.imshow(generate_image(level), cmap='gray', vmax=1, vmin=0)
    plt.title(f"level = {level}")
    plt.axis('off')
for index,level in enumerate([1,2,4,8]):
    plot(index,level)
plt.show()
```

</details>

***

## Neighbor and Distance

1. 邻域：4 邻域(上下左右)，D 邻域(四个角)，8 邻域(4+D)
2. 欧氏距离：$$D_e = \sqrt{(x-s)^2+(x-t)^2}$$
3. $$D_4$$距离：$$D_4 = |x-s|+|y-t|$$
4. $$D_8$$距离：$$D_8 = \max(|x-s|+|y-t|)$$

