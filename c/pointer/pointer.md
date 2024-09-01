---
icon: down-left-and-up-right-to-center
description: 指针
---

# Pointer

## 指针

1. 指针是什么：指针是一个值，为内存地址的变量。
2. 声明指针（`int *pi, *pi2;`）：类型 \* 变量名 \* 变量名
3. &：取地址（`ptr = &pooh;`），把 pooh 的地址给 ptr。
4. \*：解引用（`val = *ptr;`），把 ptr 所指向的数据赋值给 val。
5. 运算优先级：\*与++相同，顺序从右往左

<details>

<summary>优先级</summary>

**“顺序从右到左”我的理解是，都在指针左边比如`*++p2`就先++再\*，但如果是`*p1++`那就还是先\*再++**

```c
/* order.c -- precedence in pointer operations */
#include <stdio.h>
int data[2] = {100, 200};
int moredata[2] = {300, 400};
int main(void)
{
    int * p1, * p2, * p3;
    
    p1 = p2 = data;
    p3 = moredata;
    printf("  *p1 = %d,   *p2 = %d,     *p3 = %d\n",
           *p1     ,   *p2     ,     *p3);
    printf("*p1++ = %d, *++p2 = %d, (*p3)++ = %d\n",
           *p1++     , *++p2     , (*p3)++);
    printf("  *p1 = %d,   *p2 = %d,     *p3 = %d\n",
           *p1     ,   *p2     ,     *p3);
    
    return 0;
}

//   *p1 = 100,   *p2 = 100,     *p3 = 300
// *p1++ = 100, *++p2 = 200, (*p3)++ = 300
//   *p1 = 200,   *p2 = 200,     *p3 = 301
```

</details>

6. pintf 指针：%p
7. 指向下一个内容：++
8. 严重错误：解引用未初始化的指针，相当于在不知道什么地方改变了数据

<details>

<summary>解引用未初始化的指针</summary>



```c
#include <stdio.h>
#include <stdlib.h>
int main()
{
    // wrong
    int *a = 1;

    // wrong
    int *b;
    *b = 100;

    // right
    int *c = malloc(sizeof(int));
    *c = 200;
    return 0;
}
```

</details>

## 指针与数组

* p代表指针，eg `int *p;`
* array代表数组 eg `int array[32];`
* 已经把指针指向数组：`p = array[0];`

<details>

<summary> 指针指向数组；通过指针访问数组</summary>

<pre class="language-c"><code class="lang-c">#include &#x3C;stdio.h>

int main()
{
    int array[8] = {0, 1, 2, 3, 4, 5, 6, 7};
<strong>    int *p1 = array;
</strong><strong>    int *p2 = &#x26;array[0];
</strong>
    for (int i = 0; i &#x3C; 8; i++)
    {
<strong>        printf("%d ", *(p1 + i)); // 0 1 2 3 4 5 6 7
</strong><strong>        printf("%d ", *(p2 + i)); // 0 1 2 3 4 5 6 7
</strong>    }

    return 0;

</code></pre>

</details>



## 指针与函数

* 通过 int array\[] 和 int \*array，作为形参是一样的

<details>

<summary>int array[] 与 int *array</summary>



```c
#include <stdio.h>
#include <stdlib.h>

void merge(int *array1, int array2[], int res[], int len1, int len2)
{
    for (int i = 0; i < len1 + len2; i++)
        *(res + i) = *(array1 + i);
    for (int i = 0; i < +len2; i++)
        res[i + len1] = array2[i];
}

int main()
{
    const int LEN1 = 4;
    const int LEN2 = 2;
    int array1[LEN1] = {0, 1, 2, 3};
    int array2[LEN2] = {4, 5};
    int *array3 = malloc(sizeof(int) * (LEN1 + LEN2));
    merge(array1, array2, array3, LEN1, LEN2);

    for (int i = 0; i < LEN1 + LEN2; i++)
        printf("%d ", *(array3 + i));
    return 0;
}
```

</details>

* 悬空指针：指针指向一个地方，但是那个地方作用域已经结束

<details>

<summary> 悬空指针（修改一行上边的代码）</summary>

<pre class="language-c"><code class="lang-c">#include &#x3C;stdio.h>
#include &#x3C;stdlib.h>

int *merge(int *array1, int array2[], int len1, int len2)
{
    int res[len1 + len2];
    for (int i = 0; i &#x3C; len1 + len2; i++)
        *(res + i) = *(array1 + i);
    for (int i = 0; i &#x3C; +len2; i++)
        res[i + len1] = array2[i];
<strong>    return res; // wrong!但是编译器能通过
</strong>}

int main()
{
    const int LEN1 = 4;
    const int LEN2 = 2;
    int array1[LEN1] = {0, 1, 2, 3};
    int array2[LEN2] = {4, 5};
    int *array3 = malloc(sizeof(int) * (LEN1 + LEN2));
    array3 = merge(array1, array2, LEN1, LEN2);

    for (int i = 0; i &#x3C; LEN1 + LEN2; i++)
        printf("%d ", *(array3 + i));
    return 0;
}

</code></pre>

</details>



