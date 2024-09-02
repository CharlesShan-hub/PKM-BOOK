---
icon: envelope-open-text
description: 字符串
---

# String

## 字符串基础

<details>

<summary>字符串常量（字符串字面量）</summary>

* `char array[] = "Hello, World!";`

<!---->

* array是字符串变量
* 右边的"Hello, World!"是字符串常量

</details>

<details>

<summary>字符串：是以'\0'为结尾的 char 数组。未被初始化的富裕内存也被初始化为\0</summary>

```c
#include <stdio.h>
int main()
{
    char array1[8] = "Hello";
    char array2[8] = "Hello\0\0\0";
    for (int i = 0; i < 8; i++) // 11111111
        printf("%d", array1[i] == array2[i]);
    return 0;
}
```

</details>

<details>

<summary>字符串数组不能递增，而指向字符串的指针可以</summary>

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char array1[] = "Hello";
    char *array2 = "World";
    for (int i = 0; i < strlen(array1); i++)
        printf("%c", array1[i]); // Hello
    for (int i = 0; i < strlen(array2); i++)
        printf("%c", array2[i]); // World
    // for (int i = 0; i < strlen(array1); i++)
    //     printf("%c", *array1++); // Wrong!!
    for (int i = 0; i < strlen(array2); i++)
        printf("%c", *array2++); // World
    return 0;
}
```

</details>

<details>

<summary> 字符串数组：<code>const char *mytalents[LIM]</code></summary>

```c
//  arrchar.c -- array of pointers, array of strings
#include <stdio.h>
#define SLEN 40
#define LIM 5
int main(void)
{
    // const char(*mytalents)[LIM]
    const char *mytalents[LIM] = {
        "Adding numbers swiftly",
        "Multiplying accurately", "Stashing data",
        "Following instructions to the letter",
        "Understanding the C language"};
    char yourtalents[LIM][SLEN] = {
        "Walking in a straight line",
        "Sleeping", "Watching television",
        "Mailing letters", "Reading email"};
    int i;

    puts("Let's compare talents.");
    printf("%-36s  %-25s\n", "My Talents", "Your Talents");
    for (i = 0; i < LIM; i++)
        printf("%-36s  %-25s\n", mytalents[i], yourtalents[i]);
    printf("\nsizeof mytalents: %zd, sizeof yourtalents: %zd\n",
           sizeof(mytalents), sizeof(yourtalents));

    return 0;
}

```

</details>



## 字符串相关的库

{% hint style="info" %}
详见：[stdio.h.md](../library/stdio.h.md "mention")
{% endhint %}

* 输入
  * `printf()`
  * `gets()`：读取整行（包括空格），不检查字符串长度。不要用
  * `fgets()`：推荐用
  * `gets_s()`：C11 的新函数，编译器大概率不支持
* 输出
  * `scanf`
  * `puts`：会自动换行
  * `fputs`：不会自动换行

{% hint style="info" %}
&#x20;详见：[string.h.md](../library/string.h.md "mention")
{% endhint %}





