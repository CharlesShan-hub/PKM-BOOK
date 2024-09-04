---
icon: objects-column
description: 存储类别，链接，内存管理
---

# Storage

## 存储类别

### 作用域

1. 块作用域：其实就是花括号（在 C99 之前确实就是这样）
2. for 循环，while 循环，do while 循环，if 语句所用值得代码，及时没有花括号，也算作用域的一部分

```c
#include<stdio.h>
int main()
{
    for(int i=0; i<1;i++)
        printf("%d",i);
}
```

3. 只有在变长数组中，形参名才有用：`void use_a_VLA(int n, int m, ar[n][m]);`
4. 在 main 外边的变量，作用域是这个文件

### 链接

<pre class="language-c"><code class="lang-c">#include &#x3C;stdio.h>

<strong>int giants = 5;         // 文件作用域，外部链接
</strong><strong>static int dodgers = 3; // 文件作用域，内部链接
</strong>
int main()
{
    return 0;
}
</code></pre>

### 存储期

* 静态存储期：程序执行是一直存在——文件作用域
* 线程存储期：以\_\_Thread\_local声明一个独享，每个线程都获得改变量的私有备份
* 自动存储期：块作用域
* 动态分配存储期：malloc

| 存储类别   | 存储期 | 作用域 | 链接 | 声明方式                |
| ------ | --- | --- | -- | ------------------- |
| 自动     | 自动  | 块   | 无  | 块内                  |
| 寄存器    | 自动  | 块   | 无  | 块内, 使用关键字 register  |
| 静态外部链接 | 静态  | 文件  | 外部 | 所有函数外               |
| 静态内部链接 | 静态  | 文件  | 内部 | 所有函数外, 使用关键字 static |
| 静态无链接  | 静态  | 块   | 无  | 块内, 使用关键字 static    |

### 自动变量

可以显示的写：**auto**。（最好不要用 auto，因为和 C++不统一）。

我们可以实现 rust 中的“遮蔽”，C 里边叫“隐藏”

<details>

<summary>Demo</summary>

```
(base) kimshan@MacBook-Pro output % ./"hiding"
x in outer block: 30 at 0x7ff7bb130828
x in inner block: 77 at 0x7ff7bb130824
x in outer block: 30 at 0x7ff7bb130828
x in while loop: 101 at 0x7ff7bb130820
x in while loop: 101 at 0x7ff7bb130820
x in while loop: 101 at 0x7ff7bb130820
(这个最难理解，因为每次 while，里边的 x 都会重新声明，所以一直都是 101)
x in outer block: 34 at 0x7ff7bb130828
```

```c
// hiding.c -- variables in blocks
#include <stdio.h>
int main()
{
    int x = 30;      // original x
    
    printf("x in outer block: %d at %p\n", x, &x);
    {
        int x = 77;  // new x, hides first x
        printf("x in inner block: %d at %p\n", x, &x);
    }
    printf("x in outer block: %d at %p\n", x, &x);
    while (x++ < 33) // original x
    {
        int x = 100; // new x, hides first x 
        x++;
        printf("x in while loop: %d at %p\n", x, &x);
    }
    printf("x in outer block: %d at %p\n", x, &x);

    return 0;
}
```

</details>

### 寄存器变量

可以显示的写：**register**。（程序会尝试把内容存在寄存器，但不保证一定能存到，可能会被降级成普通）

`register int quick;`

### 块作用域的静态变量

可以显示的写：**static**。（证明了本文件可访问的全局变量）而且只被初始化一次。

<details>

<summary>Demo</summary>

```c
/* loc_stat.c -- using a local static variable */
#include <stdio.h>
void trystat(void);

int main(void)
{
    int count;

    for (count = 1; count <= 3; count++)
    {
        printf("Here comes iteration %d:\n", count);
        trystat();
    }

    return 0;
}

void trystat(void)
{
    int fade = 1;
    static int stay = 1;

    printf("fade = %d and stay = %d\n", fade++, stay++);
}

// (base) kimshan@MacBook-Pro output % ./"loc_stat"
// Here comes iteration 1:
// fade = 1 and stay = 1
// Here comes iteration 2:
// fade = 1 and stay = 2
// Here comes iteration 3:
// fade = 1 and stay = 3
```

</details>

### 外部链接的静态变量

使用外部的变量：extern。

* 如果用本文件内的全局变量，可以选择的写 extern
* 如果用别的文件的全局变量，必须要写 extern
* 不要用 extern 来创建新的变量，他是用来引用别的变量的

<details>

<summary>Demo</summary>

```c
int Erupt;            /* 外部定义的变量 */
double Up[100];       /* 外部定义的数组 */
extern char Coal;     /* 如果Coal被定义在另一个文件,则必须这样声明*/
void next(void);      
int main(void)
{
    extern int Erupt;  /* 可选的声明*/
    extern double Up[];/* 可选的声明*/
    ...
}
void next(void)
{
    ...
}
```

</details>

注意，初始化不可以用变量

```c
#include<stdio.h>
int x = 10; // 可以
int x2 = 2*x; // 不可以
int x3 = 2*10; // 可以
int main(){return 0;}
```

### 内部链接的静态变量

略

### 多文件

略

### 存储类别说明符



### 存储类别和函数



### 存储类别的选择



***

## 随机数函数和静态变量







