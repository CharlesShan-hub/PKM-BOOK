---
icon: arrows-rotate
description: 标准输入输出
---

# stdio.h

## Overview

<img src="../../.gitbook/assets/file.excalidraw (2) (1).svg" alt="stdio.h大致内容[1]" class="gitbook-drawing">

## Functions

### printf

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>printf format specifications quick reference[2]</p></figcaption></figure>

<details>

<summary>Demo</summary>

<pre class="language-c"><code class="lang-c">/* printout.c -- uses conversion specifiers */
#include &#x3C;stdio.h>
#define PI 3.141593
int main(void)
{
    int number = 7;
    float pies = 12.75;
    int cost = 7800;

<strong>    printf("The %d contestants ate %f berry pies.\n", number,
</strong><strong>           pies);
</strong><strong>    printf("The value of pi is %f.\n", PI);
</strong><strong>    printf("Farewell! thou art too dear for my possessing,\n");
</strong><strong>    printf("%c%d\n", '$', 2 * cost);
</strong>
    return 0;
}

// The 7 contestants ate 12.750000 berry pies.
// The value of pi is 3.141593.
// Farewell! thou art too dear for my possessing,
// $15600
</code></pre>

</details>

<details>

<summary> 转换说明[3]</summary>

* %a 浮点数、十六进制数和p记数法（C99/C11）
* %A 浮点数、十六进制数和p记数法（C99/C11）
* %c 单个字符
* %d 有符号十进制整数
* %e 浮点数，e记数法
* %E 浮点数，e记数法
* %f 浮点数，十进制记数法
* %_g 根据值的不同，自动选择_f或\*e。\*e格式用于指数小于-4或者大于或等于精度时
* %_G 根据值的不同，自动选择_f或\*E。\*E格式用于指数小于-4或者大于或等于精度时
* %_i 有符号十进制整数（与_a相同）
* %o 无符号八进制整数
* %p 指针
* %s 字符串
* %u 无符号十进制整数
* %x 无符号十六进制整数，使用十六进制数0f
* %X 无符号十六进制整数，使用十六进制数0F
* %% 打印一个百分号

</details>

<details>

<summary>转换说明修饰符</summary>

* 标记：五种标记（-, +, 空格, #, and 0）
  * **-**：等待打印项左对齐。即，从字段的左侧开始打印该项。示例：“%-20s”
  * \+：有符号值若为正，则在值前面显示加号；若为负，则在值前面显示减号。示例：“%+6.2f”
  * 空格：有符号值若为正，则在值前面显示前导空格（不显示任何符号）；若为负，则在值前面显示减号+标记覆盖一个空格。示例：“%6.2f”
  * \#：把结果转换为另一种形式。如果是%o格式，则以0开始；如果是xx或XX格式，则以0x或0X开始；对于所有的浮点格式，#保证了即使后面没有任何数字，也打印一个小数点字符。对于gg和GG格式，#防止结果后面的0被删除。示例：“%#0”、“%#8.0f”、“%+#10.3e”
  * 0：对于数值格式，用前导0代替空格填充字段宽度。对于整数格式，如果出现-标记或指定精度，则忽略该标记
* 数字：最小字段宽度。如果不能容纳字符串，会自动增长。Example: "%4d".
* .数字：精度。Example："%5.2f"，字段宽度为5字符，其中小数点后有两位数字
  * 对于%e、%E和%f转换，表示小数点右边数字的位数
  * 对于%g和%G转换，表示有效数字最大位数
  * 对于%s转换，表示待打印字符的最大数量
  * 对于整型转换，表示待打印数字的最小位数
  * 如有必要，使用前导0来达到这个位数
  * 只使用.表示其后跟随一个0，所以%.f和%.0f相同
* h
  * 和整型转换说明一起使用，表示short int或unsigned short int类型的值
  * 示例: "%hu"、"%hx"、"%6.4hd"&#x20;
* hh
  * 和整型转换说明一起使用，表示signed char或unsigned char类型的值&#x20;
  * 示例: "%hhu"、"%hhx"、"%6.4hhd"&#x20;
* j
  * 和整型转换说明一起使用，表示intmax\_t或uintmax\_t类型的值。这些类型定义在stdint.h中&#x20;
  * 示例: "%ja"、"%8jx"&#x20;
* l
  * 和整型转换说明一起使用，表示long int或unsigned long int类型的值&#x20;
  * 示例: "%ld"、"%8lu"&#x20;
* ll
  * 和整型转换说明一起使用，表示long long int或unsigned long long int类型的值(C99)&#x20;
  * 示例: "%lld"、"%8llu"&#x20;
* L
  * 和浮点转换说明一起使用，表示long double类型的值&#x20;
  * 示例: "%Ld"、"%10.4Le"&#x20;
* t
  * 和整型转换说明一起使用，表示ptrdiff\_t类型的值。ptrdiff\_t是两个指针差值的类型(C99)&#x20;
  * 示例: "%td"、"%12ti"&#x20;
* z
  * 和整型转换说明一起使用，表示size\_t类型的值。size\_t是sizeof返回的类型(C99)&#x20;
  * 示例: "%zd"、"%12zd"

</details>

<details>

<summary>*：让程序指定 printf 宽度</summary>

<pre class="language-c"><code class="lang-c">/* varwid.c -- uses variable-width output field */
#include &#x3C;stdio.h>
int main(void)
{
    unsigned width, precision;
    int number = 256;
    double weight = 242.5;

    printf("Enter a field width:\n");
    scanf("%d", &#x26;width);
<strong>    printf("The number is :%*d:\n", width, number);
</strong>    printf("Now enter a width and a precision:\n");
    scanf("%d %d", &#x26;width, &#x26;precision);
<strong>    printf("Weight = %*.*f\n", width, precision, weight);
</strong>    printf("Done!\n");

    return 0;
}

// Enter a field width:
// 10
// The number is :       256:
// Now enter a width and a precision:
// 10 3
// Weight =    242.500
// Done!
</code></pre>

</details>

### scanf

{% hint style="info" %}
scanf() 最不常用，因为他容易卡住。最好用 getchar()或者fgets()吧。
{% endhint %}

scanf 与 printf 两点不一样：

1. 变量前要加&
2. double 的转换说明是 lf 而不是 f

<details>

<summary>Demo</summary>

<pre class="language-c"><code class="lang-c">// input.c -- when to use &#x26;
#include &#x3C;stdio.h>
int main(void)
{
    int age;      // variable
    float assets; // variable
    char pet[30]; // string

    printf("Enter your age, assets, and favorite pet.\n");
<strong>    scanf("%d %f", &#x26;age, &#x26;assets); // use the &#x26; here
</strong><strong>    scanf("%s", pet);              // no &#x26; for char array
</strong>    printf("%d $%.2f %s\n", age, assets, pet);

    return 0;
}

// 10 9.9
// a
// 10 $9.90 a
</code></pre>

</details>

<details>

<summary>*：让程序跳过某个输入（读取文件有常用）</summary>

```c
/* skiptwo.c -- skips over first two integers of input */
#include <stdio.h>
int main(void)
{
    int n;
    
    printf("Please enter three integers:\n");
    scanf("%*d %*d %d", &n);
    printf("The last integer was %d\n", n);
    
    return 0;
}

// Please enter three integers:
// 1 2 3
// The last integer was 3
```

</details>

### getchar 和 putchar

<details>

<summary>Demo</summary>

<pre class="language-c"><code class="lang-c">/* echo_eof.c -- repeats input to end of file */
#include &#x3C;stdio.h>
int main(void)
{
    int ch;
    
<strong>    while ((ch = getchar()) != EOF)
</strong><strong>        putchar(ch);
</strong>    
    return 0;
}

</code></pre>

</details>

## Reference

\[1] [https://www.runoob.com/cprogramming/c-function-fflush.html](https://www.runoob.com/cprogramming/c-function-fflush.html)

\[2] [https://www.pixelbeat.org/programming/gcc/format\_specs.html](https://www.pixelbeat.org/programming/gcc/format\_specs.html)

\[3] [https://www.gnu.org/software/libc/manual/html\_node/Table-of-Output-Conversions.html](https://www.gnu.org/software/libc/manual/html\_node/Table-of-Output-Conversions.html)
