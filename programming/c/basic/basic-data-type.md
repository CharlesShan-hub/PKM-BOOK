---
icon: donut
description: 基础数据类型
---

# Basic Data Type

## Overview

<img src="../../../.gitbook/assets/file.excalidraw (4).svg" alt="" class="gitbook-drawing">
<img src="../assets/file.excalidraw (4).svg" alt="" class="gitbook-drawing">

![aaaa](../assets/file.excalidraw%20(4).svg)
![img][../assets/test.excalidraw.svg]

***

## Intenger

### int, long, short, unsigned

int 可以与 short 等关键字搭配，构造更具体的 int：

* `int`代表整数
* `short`代表短
* `long`或者`long long`代表长
* `unsigned`代表无符号

不同的 int 在不同电脑中占用字节数不同，这也就代表了不同电脑的某种 int 可以表示的范围不同。

<details>

<summary>查看自己电脑不同类型整数所占字节数</summary>

```c
#include <stdio.h>
int main()
{
    // 定义各种数据类型变量
    int a;
    unsigned int h;
    short int b;
    short c;
    unsigned short int i;
    long int d;
    long e;
    unsigned long int j;
    long long int f;
    long long g;
    unsigned long long int k;

    // 输出每个变量的位数
    printf("int a: %d bytes\n", sizeof(a));
    printf("unsigned int h: %d bytes\n", sizeof(h));
    printf("short int b: %d bytes\n", sizeof(b));
    printf("short c: %d bytes\n", sizeof(c));
    printf("unsigned short int i: %d bytes\n", sizeof(i));
    printf("long int d: %d bytes\n", sizeof(d));
    printf("long e: %d bytes\n", sizeof(e));
    printf("unsigned long int j: %d bytes\n", sizeof(j));
    printf("long long int f: %d bytes\n", sizeof(f));
    printf("long long g: %d bytes\n", sizeof(g));
    printf("unsigned long long int k: %d bytes\n", sizeof(k));
    return 0;
}

// int a: 4 bytes
// unsigned int h: 4 bytes
// short int b: 2 bytes
// short c: 2 bytes
// unsigned short int i: 2 bytes
// long int d: 8 bytes
// long e: 8 bytes
// unsigned long int j: 8 bytes
// long long int f: 8 bytes
// long long g: 8 bytes
// unsigned long long int k: 8 bytes

```

</details>

一个具体写在程序中的数字叫做字面量，它可以加入**前缀**来表示不同的进制：

* 十进制（Decimal）：不加前缀，默认就是十进制。
* 二进制（Binary）：0b，0B。
* 八进制（Octal）：0。（数字 0️⃣，不是字母 O）
* 十六进制（Hexadecimal）：0x，0X。

<details>

<summary>Demo</summary>

```c
#include <stdio.h>
int main()
{
    // 定义各种数据类型变量
    int binary_number = 0b1010011010;
    int octal_number = 01232;
    int decimal_number = 666;
    int hexadecimal_number = 0x29a;

    // 查看他们是否想等
    printf("%d", (int)(binary_number == octal_number));        // 1
    printf("%d", (int)(octal_number == decimal_number));       // 1
    printf("%d", (int)(decimal_number == hexadecimal_number)); // 1
    return 0;
}

```

</details>

也可以为字面量加入**后缀**，来代表它是不同的整数类型：

* `u`：无符号数。
* `L`：Long。
* `LL`，`UL`，`ULL`，自由组合

最后，在 printf 函数中，要用不同的占位符来表示这些类型，下面是总结表：

<table><thead><tr><th>type</th><th width="86">printf</th><th>hexadecimal</th><th>octal</th><th>decimal</th></tr></thead><tbody><tr><td>char</td><td>%c</td><td>\0x41</td><td>\0101</td><td>N.A.</td></tr><tr><td>int</td><td>%d</td><td>0x41</td><td>0101</td><td>65</td></tr><tr><td>unsigned int</td><td>%u</td><td>0x41u</td><td>0101u</td><td>65u</td></tr><tr><td>long</td><td>%ld</td><td>0x41L</td><td>0101L</td><td>65L</td></tr><tr><td>unsigned long</td><td>%lu</td><td>0x41UL</td><td>0101UL</td><td>65UL</td></tr><tr><td>long long</td><td>%lld</td><td>0x41LL</td><td>0101LL</td><td>65LL</td></tr><tr><td>unsigned long long</td><td>%llu</td><td>0x41ULL</td><td>0101ULL</td><td>65ULL</td></tr></tbody></table>

### char

char 代表字符，采用 ASCII 码，占用内存 8 bits。

* ✅：`char a = 'T';`
* ❌：`char b = "T";`

除了普通的数字与字母，特殊含义的字符是转义字符

| 转义序列 | 含义                                    |
| ---- | ------------------------------------- |
| \a   | 警报（ANSI C）                            |
| \b   | 退格                                    |
| \f   | 换页                                    |
|      | 换行                                    |
|      | 回车                                    |
|      | 水平制表符                                 |
| \v   | 垂直制表符                                 |
| \\\\ | 反斜杠（\）                                |
| '    | 单引号                                   |
| "    | 双引号                                   |
| ?    | 问号                                    |
| \0oo | 八进制值（oo必须是有效的八进制数，即每个o可表示0\~7中的一个数）   |
| \xhh | 十六进制值（hh必须是有效的十六进制数，即每个h可表示0\~f中的一个数） |

### \_Bool

* C99添加了布尔类型，占用 1bit。 我们可以直接就使用`_Bool`
* 也可以通过引入`stdbool.h`来使用`bool`

{% content-ref url="../library/stdbool.h.md" %}
[stdbool.h.md](../library/stdbool.h.md)
{% endcontent-ref %}

<details>

<summary>Demo</summary>

使用 \_Bool

```c
// boolean.c -- using a _Bool variable
#include <stdio.h>
int main(void)
{
    long num;
    long sum = 0L;
    _Bool input_is_good;
    
    printf("Please enter an integer to be summed ");
    printf("(q to quit): ");
    input_is_good = (scanf("%ld", &num) == 1);
    while (input_is_good)
    {
        sum = sum + num;
        printf("Please enter next integer (q to quit): ");
        input_is_good = (scanf("%ld", &num) == 1);
    }
    printf("Those integers sum to %ld.\n", sum);
    
    return 0;
}

```

通过引入stdbool.h来使用 bool

```c
// divisors.c -- nested ifs display divisors of a number
#include <stdio.h>
#include <stdbool.h>
int main(void)
{
    unsigned long num;          // number to be checked
    unsigned long div;          // potential divisors
    bool isPrime;               // prime flag
    
    printf("Please enter an integer for analysis; ");
    printf("Enter q to quit.\n");
    while (scanf("%lu", &num) == 1)
    {
        for (div = 2, isPrime = true; (div * div) <= num; div++)
        {
            if (num % div == 0)
            {
                if ((div * div) != num)
                    printf("%lu is divisible by %lu and %lu.\n",
                           num, div, num / div);
                else
                    printf("%lu is divisible by %lu.\n",
                           num, div);
                isPrime= false; // number is not prime
            }
        }
        if (isPrime)
            printf("%lu is prime.\n", num);
        printf("Please enter another integer for analysis; ");
        printf("Enter q to quit.\n");
    }
    printf("Bye.\n");
    
    return 0;
}

```

</details>

### stdint.h & inttypes.h

> stdint.h：用于各种 int 的声明
>
> inttypes.h：用于各种 int 的 printf

{% content-ref url="../library/stdint.h.md" %}
[stdint.h.md](../library/stdint.h.md)
{% endcontent-ref %}

{% content-ref url="../library/inttypes.h.md" %}
[inttypes.h.md](../library/inttypes.h.md)
{% endcontent-ref %}

***

## Decimal

### float, double, long double

占用字节数与表示范围

| 类型          | 范围                      | 大小       |
| ----------- | ----------------------- | -------- |
| float       | 大约 -3.4e38 到 3.4e38     | 通常 4 字节  |
| double      | 大约 -1.8e308 到 1.8e308   | 通常 8 字节  |
| long double | 大约 -1.2e4932 到 1.2e4932 | 通常 16 字节 |

浮点型常量

```c
 double a = .2; // 可以省略整数
 float b = 2. // 可以省略小数，但不能都省略
  
 float c = 6.6e3-34; // 科学计数法： 基数+e+指数,不能有空格
 double d = .8E-5; // 也可以用 E
```

不同格式的 printf

| 类型       | 占位符 |
| -------- | --- |
| 普通       | %f  |
| 科学计数法（e） | %e  |
| 科学计数法（E） | %E  |
| 自动选择     | %g  |

<details>

<summary>Demo1</summary>

```c
#include <stdio.h>

int main()
{
    double num = 12345.6789;

    // 使用 %f 打印浮点数
    printf("Decimal notation: %f\n", num);
    // Decimal notation: 12345.678900

    // 使用 %e 打印科学记数法
    printf("Scientific notation (lowercase e): %e\n", num);
    // Scientific notation (lowercase e): 1.234568e+04

    // 使用 %E 打印科学记数法
    printf("Scientific notation (uppercase E): %E\n", num);
    // Scientific notation (uppercase E): 1.234568E+04

    // 使用 %g 自动选择格式
    printf("General format: %g\n", num);
    // General format: 12345.7

    return 0;
}

```

</details>

<details>

<summary>Demo2</summary>

```c
/* showf_pt.c -- displays float value in two ways */
#include <stdio.h>
int main(void)
{
    float aboat = 32000.0;
    double abet = 2.14e9;
    long double dip = 5.32e-5;

    printf("%f can be written %e\n", aboat, aboat);
    // 32000.000000 can be written 3.200000e+04

    // next line requires C99 or later compliance
    printf("And it's %a in hexadecimal, powers of 2 notation\n", aboat);
    // And it's 0x1.f4p+14 in hexadecimal, powers of 2 notation
    printf("%f can be written %e\n", abet, abet);
    // 2140000000.000000 can be written 2.140000e+09
    printf("%Lf can be written %Le\n", dip, dip);
    // 0.000053 can be written 5.320000e-05

    return 0;
}

```

</details>

浮点数会产生舍入误差（因为 10 进制转换 成 2 进制有的数会转换成无限的小数）

<details>

<summary>Demo</summary>

```c
/* floaterr.c--demonstrates round-off error */
#include <stdio.h>
int main(void)
{
    float a, b;

    b = 2.0e20 + 1.0;
    a = b - 2.0e20;
    printf("%f \n", a); // 4008175468544.000000

    return 0;
}
```

</details>

### Complex, Imaginary

* C99
  * 复数：float \_Complex, double \_Complex, long double \_Complex
  * 虚数：float \_Imaginary, double \_Imaginary, long double \_Imaginary
* `complex.h`
  * 复数：float complex, double complex, long double complex
  * 虚数：I, float imaginary, double imaginary, long double imaginary

{% content-ref url="../library/complex.h.md" %}
[complex.h.md](../library/complex.h.md)
{% endcontent-ref %}

<details>

<summary>Demo</summary>

```c
#include <stdio.h>
#include <complex.h> // 包含对 _Complex 类型支持的函数和宏

int main()
{
    // 声明两个 _Complex 类型的变量
    double complex z1 = 3.0 + 2.0 * I; // 使用 I 宏表示虚数单位
    double complex z2 = 1.0 - 2.0 * I;

    // 打印原始复数
    printf("z1 = %f + %fi\n", creal(z1), cimag(z1));
    printf("z2 = %f + %fi\n", creal(z2), cimag(z2));

    // 复数加法
    _Complex double sum = z1 + z2;
    printf("Sum: %f + %fi\n", creal(sum), cimag(sum));

    // 复数减法
    _Complex double diff = z1 - z2;
    printf("Difference: %f + %fi\n", creal(diff), cimag(diff));

    // 复数乘法
    _Complex double product = z1 * z2;
    printf("Product: %f + %fi\n", creal(product), cimag(product));

    // 复数除法
    _Complex double quotient = z1 / z2;
    printf("Quotient: %f + %fi\n", creal(quotient), cimag(quotient));

    // 复数的模（绝对值）
    double magnitude = cabs(z1);
    printf("Magnitude of z1: %f\n", magnitude);

    return 0;
}
```

</details>
