---
icon: gopuram
description: 一些很基础的东西，以及一些背景介绍
---

# Background

## Overview

* C 标准变化历程
* 不同操作系统的编译与调试工具
* Hello Word Demo

## C Standard

1. 1987 年的 **K\&R**，民间的的约定俗成。
2. **ISO C89 (ANSI C)** - 1989年发布，这是C语言的第一个官方标准。
3. **ISO C90** - 1990年发布，是对ISO C89标准的微小修订。
4. **ISO C99** - 1999年发布，引入了许多新特性，如变长数组、布尔类型、复合字面量、长长整型、新的整数类型、自定义字符串处理函数、对齐约束、更好的浮点数处理、原子操作等。
5. **ISO C11** - 2011年发布，引入了更现代的特性，如静态断言、自动类型推导、右值引用、原子类型、threads和原子操作库、泛型编程支持、基于范围的for循环、改进的字符串处理等。

## Work Pipline

<table><thead><tr><th width="140">操作系统</th><th width="231">编译与链接</th><th>调试工具</th><th>开发环境</th></tr></thead><tbody><tr><td>Windows</td><td>MinGW，MSYS2，Cygwin</td><td>GDB</td><td>Visual Studio</td></tr><tr><td>Linux</td><td>GCC，Clang，Id，Make</td><td>GDB</td><td>Emacs，Vim</td></tr><tr><td>macOS</td><td>clang</td><td>LLDB</td><td>Xcode</td></tr></tbody></table>

## Hello World

```c
// first.c
#include <stdio.h>
int main(void)                /* a simple program             */
{
    int num;                  /* define a variable called num */
    num = 1;                  /* assign a value to num        */
    
    printf("I am a simple "); /* use the printf() function    */
    printf("computer.\n");
    printf("My favorite number is %d because it is first.\n",num);
    
    return 0;
}

```







