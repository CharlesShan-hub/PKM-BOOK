---
icon: '3'
description: >-
  第3章处理数据:C++提供了内置类型来存储两种数据:整数(没有小数的数字)和浮点数(带小数的数字)。为满足程序员的各种需求，C++为每一种数据都提供了几个类型。本章将要讨论这些类型，包括创建变量和编写各种类型的常量。另外，还将讨论C++是
  如何处理不同类型之间的隐式和显式转换的。
---

# 处理数据

### 3.1 简单变量

#### 3.1.1 变量名

* 在名称中只能使用字母字符、数字和下划线 ( \_ )；
* 名称的第一个字符不能是数字；
* 区分大写字符与小写字符；
* 不能将C++关键字用作名称；
* <mark style="color:orange;">以</mark>_<mark style="color:orange;">两个下划线</mark>_ <mark style="color:orange;"></mark><mark style="color:orange;">或</mark> <mark style="color:orange;"></mark>_<mark style="color:orange;">下划线+大写字母</mark>_ <mark style="color:orange;"></mark><mark style="color:orange;">打头的名称被保留给实现（编译器及其使用的资源）使用</mark>；
* <mark style="color:orange;">以</mark> <mark style="color:orange;"></mark>_<mark style="color:orange;">一个下划线</mark>_ <mark style="color:orange;"></mark><mark style="color:orange;">开头的名称被保留给实现，用作全局标识符</mark>；
* C++对于名称的长度没有限制，名称中所有的字符都有意义，但有些平台有长度限制。

{% hint style="info" %}
倒数第二三点与前面几点有些不同，因为使用像 <mark style="color:orange;">\_\_time\_stop</mark> 或 <mark style="color:orange;">\_Donut</mark> 这样的名称不会导致编译器错误，而会导致行为的不确定性。换句话说，不知道结果将是什么。不出现编译器错误的原因是，这样的名称不 是非法的，但要留给实现使用。
{% endhint %}

{% hint style="warning" %}
TODO

命名风格
{% endhint %}

#### 3.1.2 整型

整数无限大，每一种 C++的整形只是数学上的整数的一部分。

#### 3.1.3 short、int、long、long long

1. 用 [climits.md](library/climits.md "mention") 来确定各种整形的最大最小值
2.

***

### 3.2 const 限定符







***

### 3.3 浮点数





***

### 3.4 C++算术运算符











