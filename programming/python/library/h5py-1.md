---
description: HDF5 二进制数据格式接口的库
---

# h5py

`h5py` 是一个为 Python 提供 HDF5 二进制数据格式接口的库。HDF5 是一种用于存储大量数值数据的文件格式，`h5py` 允许用户轻松地从 NumPy 中操作这些数据。例如，你可以像操作真正的 NumPy 数组一样切片硬盘上存储的多 TB 数据集。此外，成千上万个数据集可以存储在单个文件中，并且可以按照你想要的任何方式进行分类和标记。

#### 安装 `h5py`

你可以使用 `conda` 或 `pip` 来安装 `h5py`。如果你使用 Anaconda 或 Miniconda，可以使用以下命令安装：

```bash
conda install h5py
```

如果你平台的 (mac, linux, windows on x86) 有轮子 (wheel) 并且不需要 MPI，你也可以通过 `pip` 安装：

```bash
pip install h5py
```

#### 核心概念

HDF5 文件是两种对象类型的容器：数据集（dataset），这是类似数组的数据集合，以及组（group），这是类似文件夹的容器，可以包含数据集和其他组。使用 `h5py` 时，最基本的概念是：组就像字典，而数据集就像 NumPy 数组。

#### 文件对象

文件对象（`File object`）是你操作的起点。例如，假设有人给你一个 HDF5 文件 `mytestfile.hdf5`，你首先需要以读取模式打开这个文件：

```python
import h5py
f = h5py.File('mytestfile.hdf5', 'r')
```

然后，你可以检查文件中的键来了解其中存储了什么内容。

#### 高级 API 参考和高级主题

`h5py` 文档还提供了高级 API 参考和高级主题，包括配置 `h5py` 库、特殊类型、HDF5 中的字符串、对象和区域引用、并行 HDF5、单写多读（SWMR）以及虚拟数据集（VDS）等内容。 更多详细信息，你可以访问 `h5py` 的官方文档，了解安装指南、快速入门指南、高级主题等内容。`h5py` 是一个为 Python 提供 HDF5 二进制数据格式接口的库。HDF5 是一种用于存储大量数值数据的文件格式，`h5py` 允许用户轻松地从 NumPy 中操作这些数据。例如，你可以像操作真正的 NumPy 数组一样切片硬盘上存储的多 TB 数据集。此外，成千上万个数据集可以存储在单个文件中，并且可以按照你想要的任何方式进行分类和标记。

#### 安装 `h5py`

你可以使用 `conda` 或 `pip` 来安装 `h5py`。如果你使用 Anaconda 或 Miniconda，可以使用以下命令安装：

```bash
conda install h5py
```

如果你平台的 (mac, linux, windows on x86) 有轮子 (wheel) 并且不需要 MPI，你也可以通过 `pip` 安装：

```bash
pip install h5py
```

#### 核心概念

HDF5 文件是两种对象类型的容器：数据集（dataset），这是类似数组的数据集合，以及组（group），这是类似文件夹的容器，可以包含数据集和其他组。使用 `h5py` 时，最基本的概念是：组就像字典，而数据集就像 NumPy 数组。

#### 文件对象

文件对象（`File object`）是你操作的起点。例如，假设有人给你一个 HDF5 文件 `mytestfile.hdf5`，你首先需要以读取模式打开这个文件：

```python
import h5py
f = h5py.File('mytestfile.hdf5', 'r')
```

然后，你可以检查文件中的键来了解其中存储了什么内容。

#### 高级 API 参考和高级主题

`h5py` 文档还提供了高级 API 参考和高级主题，包括配置 `h5py` 库、特殊类型、HDF5 中的字符串、对象和区域引用、并行 HDF5、单写多读（SWMR）以及虚拟数据集（VDS）等内容。 更多详细信息，你可以访问 `h5py` 的官方文档，了解安装指南、快速入门指南、高级主题等内容。
