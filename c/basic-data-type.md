---
description: 基础数据类型
icon: donut
---

# Basic Data Type

## Overview

| 最初 K\&R 给出的关键字                            | C90标准添加的关键字 | C99标准添加的关键字 |
| ----------------------------------------- | ----------- | ----------- |
| int                                       | signed      | \_Bool      |
| <mark style="color:blue;">long</mark>     | void        | \_Complex   |
| <mark style="color:blue;">short</mark>    |             | \_Imaginary |
| <mark style="color:blue;">unsigned</mark> |             |             |
| char                                      |             |             |
| float                                     |             |             |
| double                                    |             |             |

## Intenger

### int, long, short, unsigned

int 可以与 short 等关键字搭配，构造更具体的 int：

* `int`代表整数
* `short`代表短
* `long`或者`long long`代表长
* `unsigned`代表无符号

不同的 int 在不同电脑中占用字节数不同，这也就代表了不同电脑的某种 int 可以表示的范围不同。

<details>

<summary> 查看自己电脑不同类型整数所占字节数</summary>

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

一个具体写在程序中的数字叫做字面量，它可以加入前缀来表示不同的进制：

* 十进制（Decimal）：不加前缀，默认就是十进制。
* 二进制（Binary）：0b，0B。
* 八进制（Octal）：0。（数字 0️⃣，不是字母 O）
* 十六进制（Hexadecimal）：0x，0X。

<details>

<summary> Demo</summary>

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

也可以为字面量加入后缀，来代表它是不同的整数类型：

* `u`：无符号数。
* `L`：Long。
* `LL`，`UL`，`ULL`，自由组合

最后，在 printf 函数中，要用不同的占位符来表示这些类型，下面是总结表：

| type               | printf | hexadecimal | octal   | decimal |
| ------------------ | ------ | ----------- | ------- | ------- |
| char               | %c     | \0x41       | \0101   | N.A.    |
| int                | %d     | 0x41        | 0101    | 65      |
| unsigned int       | %u     | 0x41u       | 0101u   | 65u     |
| long               | %ld    | 0x41L       | 0101L   | 65L     |
| unsigned long      | %lu    | 0x41UL      | 0101UL  | 65UL    |
| long long          | %lld   | 0x41LL      | 0101LL  | 65LL    |
| unsigned long long | %llu   | 0x41ULL     | 0101ULL | 65ULL   |

### \_Bool

C99添加了布尔类型，占用 1bit。 我们可以直接就使用`_Bool`，也可以通过引入`stdbool.h`来使用`bool`

<details>

<summary> Demo</summary>

&#x20;使用 \_Bool

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

## Decimal





