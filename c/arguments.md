---
description: 运算符，表达式和语句
icon: sliders-up
---

# Arguments

## Operater

### 基本运算符

* 赋值：=
  * 可以三重赋值：`int a,b,c; a = b = c = 1;`
  * 赋值的顺序是从右向左
* 加法：+
* 减法：-
* 符号：-与+（就是正负号，C90 才可以用）
* 乘法：\*
* 除法：/
  * 如果是整数除法会截断，浮点数除法得到浮点数
* 取模：%
  * 不能用于浮点数
  * 负数怎么办
* 递增运算符：++
  * 前缀模式，后缀模式
  * 优先级：括号 > 递增递减 > 其他
* 递减运算符：--

### 其他运算符

* <mark style="color:red;">sizeof</mark> 函数返回 <mark style="color:red;">size\_t</mark> 类型的值，这是个无符号整型。
* C99 可以用 <mark style="color:red;">%zd</mark> 对应 size\_t 类型的值，如果编译器支持也可以用 <mark style="color:red;">%u</mark> 或 <mark style="color:red;">%lu</mark>。

### 不要自作聪明

`ans = num/2 + 5*(1 + num++);`

编译器会自己选择先运算`num/2`还是`5*(1 + num++)`

所以不要写这样的代码！

## 1Expresiosion1

111







