---
icon: sliders-up
description: 运算符，表达式和语句
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

## Expression and Argument

* 表达式（expression）
  * <mark style="color:red;">每个表达式都有一个值</mark>。
  * 表达式是常量、变量或二者的组合。
* 语句（argument）
  * 语句是一条完整的计算机指令，以分号结尾（大多数）。
  * 单独一个分号叫做空语句。
  * `int a = 1;`这个语句去掉分号并不是表达式。
* 副作用（side effect）
  * c 语言的角度，它的目的是对表达式进行求值。如果改变了某个内存的数据，这个就是副作用。
  * 比如：`a = 5;`，求“5”本身是目的，把 5 存在了 a 是副作用。
  * （这么看有一种万物归一的感觉，表达式求值与改变内存进行了统一）
* 序列点（sequence point）
  * 程序执行的点：一个分号就是一个序列点，一个完整表达式的结束也算是一个序列点。
* 完整表达式（full expression）
  * 某个表达式并不是一个更大表达式的一部分
  * 比如：`while(i++ < 10) printf("%d \n", i);`，其中`i++ < 10`就是一个完整表达式。
  * 比如：，`y = (4+x++) + (6+x++)`，其中`4+x++`就不是一个完整表达式。因为程序无法保证x 在`4+x++`之后不再变化。

## 类型转换

### 自动类型转换

总的原则是“小的”转化成“大的”。（这样有优点有缺点。rust 中就不允许这样转换）

<details>

<summary>Demo</summary>

```c
/* convert.c -- automatic type conversions */
#include <stdio.h>
int main(void)
{
    char ch;
    int i;
    float fl;
    
    fl = i = ch = 'C';                                  /* line 9  */
    printf("ch = %c, i = %d, fl = %2.2f\n", ch, i, fl); /* line 10 */
    ch = ch + 1;                                        /* line 11 */
    i = fl + 2 * ch;                                    /* line 12 */
    fl = 2.0 * ch + i;                                  /* line 13 */
    printf("ch = %c, i = %d, fl = %2.2f\n", ch, i, fl); /* line 14 */
    ch = 1107;                                          /* line 15 */
    printf("Now ch = %c\n", ch);                        /* line 16 */
    ch = 80.89;                                         /* line 17 */
    printf("Now ch = %c\n", ch);                        /* line 18 */
    
    return 0;
}

// ch = C, i = 67, fl = 67.00
// ch = D, i = 203, fl = 339.00
// Now ch = S
// Now ch = P
```

</details>

### 强制类型转换

大转小也可以，但会发生“截断”

<details>

<summary>Demo</summary>

```c
#include <stdio.h>

int main()
{
    // float 转换为 int
    float f = 123.456f;
    printf("原始 float 值: %f\n", f);
    printf("强制转换后的 int 值: %d\n", (int)f);

    // double 转换为 float
    double d = 123456789.123456789;
    printf("原始 double 值: %lf\n", d);
    printf("强制转换后的 float 值: %f\n", (float)d);

    // int 转换为 char
    int i = 256; // 256 超出了 char 的范围
    printf("原始 int 值: %d\n", i);
    printf("强制转换后的 char 值: %d\n", (char)i);

    return 0;
}
// 原始 float 值: 123.456001
// 强制转换后的 int 值: 123
// 原始 double 值: 123456789.123457
// 强制转换后的 float 值: 123456792.000000
// 原始 int 值: 256
// 强制转换后的 char 值: 0
```

</details>



