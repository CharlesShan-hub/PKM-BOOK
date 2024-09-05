---
icon: flag-checkered
description: 预处理器指令
---

# Preprocessor Directives

## 预处理器指令

<details>

<summary>所有的预处理器指令（GPT）</summary>



C语言的预处理器（Preprocessor）是一段特殊的代码处理程序，它负责在编译器实际编译源代码之前对源代码进行处理。预处理器指令以井号 `#` 开头，并且它们不是C语言语句的一部分，而是被编译器识别并执行的指令。以下是一些常用的C语言预处理器指令：

1. **`#include`**：文件包含指令，用于将一个文件的内容包含到另一个文件中。
2. `#include_next`：与 `#include` 类似，但优先级较低，只在没有 `#include` 指令时才会被处理。
3. `#include_alias`：为 `#include` 指令提供一个别名。
4. `#include_guard`：使用 `#ifndef` 和 `#define` 宏来保护头文件，防止重复包含。
5. **`#define`**：宏定义指令，用于定义一个宏，它会在编译时被替换。
6. **`#undef`**：取消宏定义，用于删除之前用 `#define` 定义的宏。
7. **`#if`**：条件编译指令，如果指定的条件为真，则编译随后的代码。
8. **`#elif`**：条件编译指令，如果之前的 `#if` 条件为假，且该 `#elif` 条件为真，则编译随后的代码。
9. **`#else`**：条件编译指令，与 `#if` 或 `#elif` 结合使用，当 `#if` 或 `#elif` 的条件都不为真时编译随后的代码。
10. **`#endif`**：结束条件编译指令，用于标记 `#if`、`#elif` 或 `#else` 块的结束。
11. **`#ifdef`**：条件编译指令，如果指定的宏已经被定义，则编译随后的代码。
12. **`#ifndef`**：条件编译指令，如果指定的宏没有被定义，则编译随后的代码。
13. **`#if defined`**：条件编译指令，如果指定的宏被定义，则编译随后的代码。
14. **`#if !defined`**：条件编译指令，如果指定的宏没有被定义，则编译随后的代码。
15. **`#elif defined`**：条件编译指令，如果之前的 `#if` 或 `#elif` 条件为假，且该 `#elif defined` 条件为真，则编译随后的代码。
16. **`#elif !defined`**：条件编译指令，如果之前的 `#if` 或 `#elif` 条件为假，且该 `#elif !defined` 条件为真，则编译随后的代码。
17. `#ifdef` 和 `#ifndef` 的别名：
    1. `#if defined` 和 `#if !defined` 的别名分别为 `#ifdef` 和 `#ifndef`。
    2. `#elif defined` 和 `#elif !defined` 的别名分别为 `#elif` 和 `#else`。
18. `#pragma`：指令，用于指定编译器的行为，如内存模型、浮点环境等。
19. `#line`：指令，用于改变编译器的行号，通常用于调试和生成错误消息。
20. `#error`：指令，用于在编译时生成一个错误信息。
21. `#warning`：指令，用于在编译时生成一个警告信息。
22. `#message`：指令，用于在编译时生成一个消息，通常用于调试。
23. `#assert`：指令，用于在编译时检查一个表达式是否为真，如果为假，则生成一个错误信息。

</details>

## #define

<details>

<summary>#define</summary>

<pre class="language-c"><code class="lang-c">/* preproc.c -- simple preprocessor examples */
#include &#x3C;stdio.h>
<strong>#define TWO 2        /* you can use comments if you like   */
</strong><strong>#define OW "Consistency is the last refuge of the unimagina\
</strong><strong>tive. - Oscar Wilde" /* a backslash continues a definition */
</strong>/* to the next line                   */
<strong>#define FOUR  TWO*TWO
</strong><strong>#define PX printf("X is %d.\n", x)
</strong><strong>#define FMT  "X is %d.\n"
</strong>
int main(void)
{
    int x = TWO;
    
    PX;
    x = FOUR;
    printf(FMT, x);
    printf("%s\n", OW);
    printf("TWO: OW\n");
    
    return 0;
}

// X is 2.
// X is 4.
// Consistency is the last refuge of the unimaginative. - Oscar Wilde
// TWO: OW
</code></pre>

</details>

<details>

<summary>#define(注意)</summary>

注意长段的空格或者注释会编译成一个空格

```c
#define SIX 2*3
#define SIX 2 * 3 // 这两样是不一样的！
```

</details>

<details>

<summary>#define(函数)</summary>



```c
/* mac_arg.c -- macros with arguments */
#include <stdio.h>
#define SQUARE(X) X *X
#define PR(X) printf("The result is %d.\n", X)
int main(void)
{
    int x = 5;
    int z;

    printf("x = %d\n", x);
    z = SQUARE(x);
    printf("Evaluating SQUARE(x): ");
    PR(z);
    z = SQUARE(2);
    printf("Evaluating SQUARE(2): ");
    PR(z);
    printf("Evaluating SQUARE(x+2): ");
    PR(SQUARE(x + 2));
    printf("Evaluating 100/SQUARE(2): ");
    PR(100 / SQUARE(2));
    printf("x is %d.\n", x);
    printf("Evaluating SQUARE(++x): ");
    PR(SQUARE(++x));
    printf("After incrementing, x is %x.\n", x);

    return 0;
}
// (base) kimshan@MacBook-Pro output % ./"mac_arg"
// x = 5
// Evaluating SQUARE(x): The result is 25.
// Evaluating SQUARE(2): The result is 4.
// Evaluating SQUARE(x+2): The result is 17.
// Evaluating 100/SQUARE(2): The result is 100.
// x is 5.
// Evaluating SQUARE(++x): The result is 42.
// After incrementing, x is 7.
```

</details>

<details>

<summary>#define(井号)</summary>



```c
/* subst.c -- substitute in string */
#include <stdio.h>
#define PSQR(x) printf("The square of " #x " is %d.\n", ((x) * (x)))

int main(void)
{
    int y = 5;

    PSQR(y);
    PSQR(2 + 4);

    return 0;
}

// (base) kimshan@MacBook-Pro output % ./"subst"
// The square of y is 25.
// The square of 2 + 4 is 36.
```

</details>

<details>

<summary>#dehine(x2, x3, x4, ....)</summary>



```c
// glue.c -- use the ## operator
#include <stdio.h>
#define XNAME(n) x ## n
#define PRINT_XN(n) printf("x" #n " = %d\n", x ## n);

int main(void)
{
    int XNAME(1) = 14;  // becomes int x1 = 14;
    int XNAME(2) = 20;  // becomes int x2 = 20;
    int x3 = 30;
    PRINT_XN(1);        // becomes printf("x1 = %d\n", x1);
    PRINT_XN(2);        // becomes printf("x2 = %d\n", x2);
    PRINT_XN(3);        // becomes printf("x3 = %d\n", x3);
    return 0;
}

```

</details>

<details>

<summary>变参宏</summary>

```c
// variadic.c -- variadic macros
#include <stdio.h>
#include <math.h>
#define PR(X, ...) printf("Message " #X ": " __VA_ARGS__)

int main(void)
{
    double x = 48;
    double y;

    y = sqrt(x);
    PR(1, "x = %g\n", x);
    PR(2, "x = %.2f, y = %.4f\n", x, y);

    return 0;
}

// Message 1: x = 48
// Message 2: x = 48.00, y = 6.9282
```

</details>



## #include

<details>

<summary>Demo</summary>

```c
#include <stdio.h> // 标准库
#include "utils.h" // 本地
#include "/usr/biff/p.h" // 绝对路径
```

</details>



## C 预处理器的其他功能



## 通用选择表达式



## 内联函数



## C 库概述和一些特殊用途的方便函数





## 问题集锦

1. define 和 const 的区别：`#define`会在编译的时候替换，`const`不会。
