---
icon: '4'
description: >-
  第4章
  复合类型:C++让程序员能够使用基本的内置类型来创建更复杂的类型。最高级的形式是类（9～13章）。本章主要包括数组(存储多个同类型的值)、结构(存储多个不同类型的值)、指针(标识内存位置)。您还将学习如何创建和存储文本字符串及如何使用C风格字符数组和C++
  string类来处理文本输入输出。最后，还将学习C++处理内存分配的方法，包括用于显式地管理内存的new和delete运算符。
---

# 复合类型

4.1 数组

<details>

<summary>Demo</summary>

```cpp
// arrayone.cpp -- small arrays of integers
#include <iostream>
int main()
{
    using namespace std;
    int yams[3];    // creates array with three elements
    yams[0] = 7;    // assign value to first element
    yams[1] = 8;
    yams[2] = 6;

    int yamcosts[3] = {20, 30, 5}; // create, initialize array
    // int yamcosts[3]; // not allowed
    // yamcosts = {20, 30, 5}; // not allowed

    // NOTE: If your C++ compiler or translator can't initialize
    // this array, use static int yamcosts[3] instead of
    // int yamcosts[3]

    cout << "Total yams = ";
    cout << yams[0] + yams[1] + yams[2] << endl;
    cout << "The package with " << yams[1] << " yams costs ";
    cout << yamcosts[1] << " cents per yam.\n";
    int total = yams[0] * yamcosts[0] + yams[1] * yamcosts[1];
    total = total + yams[2] * yamcosts[2];
    cout << "The total yam expense is " << total << " cents.\n";

    cout << "\nSize of yams array = " << sizeof yams;
    cout << " bytes.\n";
    cout << "Size of one element = " << sizeof yams[0];
    cout << " bytes.\n";

    // cin.get();
    return 0; 
}

```

```
(base) kimshan@MacBook-Pro output % ./"arrayone"
Total yams = 21
The package with 8 yams costs 30 cents per yam.
The total yam expense is 410 cents.

Size of yams array = 12 bytes.
Size of one element = 4 bytes.
```

</details>

<details>

<summary>初始化</summary>

```cpp
// 赋值
int a[3] = {1,2,3};
// [1,2,3]
int b[3] = {1,2};
// [1,2,0]
int c[3] = {0};
// [0,0,0]

// 可以省略= （C++11）
int d[3] {1,2,3};
// [1,2,3]
int e[3] {0};
// [0,0,0]
```

</details>

***

### 4.2 字符串

<details>

<summary>Demo</summary>

```cpp
// strings.cpp -- storing strings in an array
#include <iostream>
#include <cstring>  // for the strlen() function
int main()
{
    using namespace std;
    const int Size = 15;
    char name1[Size];               // empty array
    char name2[Size] = "C++owboy";  // initialized array
    // NOTE: some implementations may require the static keyword
    // to initialize the array name2

    cout << "Howdy! I'm " << name2;
    cout << "! What's your name?\n";
    cin >> name1;
    cout << "Well, " << name1 << ", your name has ";
    cout << strlen(name1) << " letters and is stored\n";
    cout << "in an array of " << sizeof(name1) << " bytes.\n";
    cout << "Your initial is " << name1[0] << ".\n";
    name2[3] = '\0';                // set to null character
    cout << "Here are the first 3 characters of my name: ";
    cout << name2 << endl;
    // cin.get();
    // cin.get();
    return 0;
}

```

```
Howdy! I'm C++owboy! What's your name?
Charles
Well, Charles, your name has 7 letters and is stored
in an array of 15 bytes.
Your initial is C.
Here are the first 3 characters of my name: C++
```

</details>



***

### 4.3 string类简介





***

### 4.4 结构简介





***

### 4.5 共用体



***

### 4.6 枚举



***

### 4.7 指针和自由存储空间



***

### 4.8 指针、数组和指针算数



***

### 4.9 类型组合



***

### 4.10 数组的替代品





