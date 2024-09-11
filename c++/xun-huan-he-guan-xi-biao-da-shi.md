---
icon: '5'
description: >-
  第5章 循环和关系表达式:程序经常需要执行重复性操作，为此 C++提供了3种循环结构:for循环、while循环和do
  while循环。这些循环必须知道何时终止，C++的关系运算符使程序员能够创建测试 来引导循环。本章还将介绍如何创建逐字符地读取和处理输入的循
  环。最后，您将学习如何创建二维数组以及如何使用嵌套循环来处 理它们。
---

# 循环和关系表达式

## 5.1 for循环

<details>

<summary>Basic Demo</summary>

没有大括号，默认后边的一行

```cpp
for (initialization; test-expression; update-expression)
    body;
```

有大括号

```cpp
for (initialization; test-expression; update-expression) {
    body;
}
```

&#x20;Demo

```cpp
// forloop.cpp -- introducing the for loop
#include <iostream>
int main()
{
    using namespace std;
    int i;  // create a counter
//   initialize; test ; update
    for (i = 0; i < 5; i++)
        cout << "C++ knows loops.\n";
    cout << "C++ knows when to stop.\n";
    // cin.get();
    return 0;
}

```

</details>

<details>

<summary>Update counter</summary>

* 可以++，--，注意理论上++i 比 i++速度快
* 可以倒序

```cpp
for (int i = word.size() - 1; i >= 0; i--)
        cout << word[i];
```

* 可以递增递减指针

```cpp
int main()
{
    using namespace std;
    
    double arr[5] = {2,4,6,8,10};
    double *p = arr;
    cout << *p++ << *p++ << *p++; // 2 4 6
    double * = arr;
    cout << *++q << *++q << *++q; // 4 6 8
    return 0;
}
```

```cpp
// 指针递增，然后取值
*++p;
// 取值然后指针递增
*p++;
// 指针指得地方++
++*p;
// 指针指得地方++
(*p)++;
```

</details>

<details>

<summary>more expression in one block</summary>

逗号运算符

<pre class="language-cpp"><code class="lang-cpp">// forstr2.cpp -- reversing an array
#include &#x3C;iostream>
#include &#x3C;string>
int main()
{
    using namespace std;
    cout &#x3C;&#x3C; "Enter a word: ";
    string word;
    cin >> word;

    // physically modify string object
    char temp;
    int i, j;
<strong>    for (j = 0, i = word.size() - 1; j &#x3C; i; --i, ++j)
</strong>    {                       // start block
        temp = word[i];
        word[i] = word[j];
        word[j] = temp;
    }                       // end block
    cout &#x3C;&#x3C; word &#x3C;&#x3C; "\nDone\n";
    // cin.get();
    // cin.get();
    return 0; 
}
</code></pre>

</details>

## 5.2 while 循环

<details>

<summary>Basic Demo</summary>

```cpp
while (test-condition)
    body
    
while (test-condition) {
    body
}
```

```cpp
// while.cpp -- introducing the while loop
#include <iostream>
const int ArSize = 20;
int main()
{
    using namespace std;
    char name[ArSize];

    cout << "Your first name, please: ";
    cin >> name;
    cout << "Here is your name, verticalized and ASCIIized:\n";
    int i = 0;                  // start at beginning of string
    while (name[i] != '\0')     // process to end of string
    {
        cout << name[i] << ": " << int(name[i]) << endl;
        i++;                    // don't forget this step
    }
    // cin.get();
    // cin.get();
    return 0; 
}

```

</details>

<details>

<summary>waiting Demo (with ctime)</summary>



<pre class="language-cpp"><code class="lang-cpp">// waiting.cpp -- using clock() in a time-delay loop
#include &#x3C;iostream>
#include &#x3C;ctime> // describes clock() function, clock_t type
int main()
{
    using namespace std;
    cout &#x3C;&#x3C; "Enter the delay time, in seconds: ";
    float secs;
    cin >> secs;
    clock_t delay = secs * <a data-footnote-ref href="#user-content-fn-1">CLOCKS_PER_SEC</a>;  // convert to clock ticks
    cout &#x3C;&#x3C; "starting\a\n";
    clock_t start = clock();
    while (clock() - start &#x3C; delay )        // wait until time elapses
        ;                                   // note the semicolon
    cout &#x3C;&#x3C; "done \a\n";
    // cin.get();
    // cin.get();
    return 0; 
}

</code></pre>

```
(base) kimshan@MacBook-Pro output % ./"waiting"
Enter the delay time, in seconds: 10
starting
done 
```

</details>

## 5.3 do while 循环



## 5.4 基于范围的 for 循环(C++11)



## 5.5 循环和文本输入



## 5.6 嵌套循环和二维数组

[^1]: in ctime
