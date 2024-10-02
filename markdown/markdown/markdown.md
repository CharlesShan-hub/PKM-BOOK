---
description: 本文收集 markdown 的有趣的冷门的语法
---

# Markdown

## Syntax

### 标题

标题除了`#`的写法，也可以用横线，但是不推荐使用。

```markdown
Heading level 1
===============
Heading level 2
---------------
```

### 换行

换行的三种方式：

* `<br>`
* 直接回车
* 行末两个空格：不推荐

### 强调

* 加粗或斜体：推荐用下划线而不是星号
  * `Love__is__bold`：不起作用！
  * `Love**is**bold`：这样才行！
* 下划线：`<u>下划线文本</u>`
* 删除：`~~世界是平坦的。~~`

### 列表

有序列表，序号可以不真的按序号，只要是数字就行

```
列表可以不真正的排序
1. First item
1. Second item
1. Third item
1. Fourth item

甚至可以是错的
1. First item
8. Second item
3. Third item
5. Fourth item
```

无需列表可以用`+`，`-`，`*`

```markdown
可以用-
- First item
- Second item
- Third item

也可以用*
* First item
* Second item
* Third item

或者*
+ First item
+ Second item
+ Third item
```

### 代码

除了三个撇号，也可以用缩进来表示一个

```
```

### 分割线

```markdown
分割横线（注意前后要有空行）

***

---

_________________
```

### 各种链接

```markdown
图片
![Tux, the Linux mascot](/assets/images/tux.png)
![The San Juan Mountains are beautiful!](/assets/images/san-juan-mountains.jpg "San Juan Mountains")

超链接
My favorite search engine is [Google](https://www.google.com/，"Goto google").

带有链接的图片
[![An old rock in the desert](/assets/images/shiprock.jpg "Shiprock, New Mexico by Beau Rogers")](https://www.flickr.com/photos/beaurogers/31833779864/in/photolist-Qv3rFw-34mt9F-a9Cmfy-5Ha3Zi-9msKdv-o3hgjr-hWpUte-4WMsJ1-KUQ8N-deshUb-vssBD-6CQci6-8AFCiD-zsJWT-nNfsgB-dPDwZJ-bn9JGn-5HtSXY-6CUhAL-a4UTXB-ugPum-KUPSo-fBLNm-6CUmpy-4WMsc9-8a7D3T-83KJev-6CQ2bK-nNusHJ-a78rQH-nw3NvT-7aq2qf-8wwBso-3nNceh-ugSKP-4mh4kh-bbeeqH-a7biME-q3PtTf-brFpgb-cg38zw-bXMZc-nJPELD-f58Lmo-bXMYG-bz8AAi-bxNtNT-bXMYi-bXMY6-bXMYv)

URL 和 邮箱
<https://www.markdownguide.org>
<fake@example.com>
```

### 转义

```
如果要显示*，需要
\* 
其他的需要转义的符号：\`*_{}[]<>()#*+-/!|
```

***

## Reference

\[1] [https://www.markdownguide.org/basic-syntax/](https://www.markdownguide.org/basic-syntax/)
