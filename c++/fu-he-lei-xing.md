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

参考：[cstring.md](library/cstring.md "mention")

<details>

<summary>cin，遇到空白 （空格、制表符和换行符）代表输入结束</summary>

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

<details>

<summary>cin.getline，遇到换行符代表输入结束，换行符可以被自动删掉</summary>

{% code title="错误的输入案例" %}
```cpp
// instr1.cpp -- reading more than one string
#include <iostream>
int main()
{
    using namespace std;
    const int ArSize = 20;
    char name[ArSize];
    char dessert[ArSize];

    cout << "Enter your name:\n";
    cin >> name;
    cout << "Enter your favorite dessert:\n";
    cin >> dessert;
    cout << "I have some delicious " << dessert;
    cout << " for you, " << name << ".\n";
    // cin.get();
	// cin.get();
    return 0; 
}
```
{% endcode %}

```
(base) kimshan@MacBook-Pro output % ./"instr1"
Enter your name:
Jassica Windy
Enter your favorite dessert:
I have some delicious Windy for you, Jassica.
```

{% code title="正确的" %}
```cpp
// instr2.cpp -- reading more than one word with getline
#include <iostream>
int main()
{
    using namespace std;
    const int ArSize = 20;
    char name[ArSize];
    char dessert[ArSize];

    cout << "Enter your name:\n";
    cin.getline(name, ArSize);  // reads through newline
    cout << "Enter your favorite dessert:\n";
    cin.getline(dessert, ArSize);
    cout << "I have some delicious " << dessert;
    cout << " for you, " << name << ".\n";
    // cin.get();
    return 0; 
}

```
{% endcode %}

```
(base) kimshan@MacBook-Pro output % ./"instr2"
Enter your name:
Jassica Windy
Enter your favorite dessert:
Cookie
I have some delicious Cookie for you, Jassica Windy.
```

</details>

<details>

<summary>cin.get，遇到换行符代表输入结束，换行符可以不被删掉，要再 get 一下</summary>

```cpp
// instr3.cpp -- reading more than one word with get() & get()
#include <iostream>
int main()
{
    using namespace std;
    const int ArSize = 20;
    char name[ArSize];
    char dessert[ArSize];

    cout << "Enter your name:\n";
    cin.get(name, ArSize).get();    // read string, newline
    cout << "Enter your favorite dessert:\n";
    cin.get(dessert, ArSize).get();
    cout << "I have some delicious " << dessert;
    cout << " for you, " << name << ".\n";
    // cin.get();
    return 0; 
}

```

```
(base) kimshan@MacBook-Pro output % ./"instr3"
Enter your name:
Tony's Fu
Enter your favorite dessert:
Soup
I have some delicious Soup for you, Tony's Fu.
```

</details>

<details>

<summary>输入混合的字符串和数字（cin 会留一个回车在缓冲区）</summary>

<pre class="language-cpp"><code class="lang-cpp">// numstr.cpp -- following number input with line input
#include &#x3C;iostream>
int main()
{
    using namespace std;
    cout &#x3C;&#x3C; "What year was your house built?\n";
    int year;
<strong>    (cin >> year).get();
</strong><strong>    // cin.get();
</strong>    cout &#x3C;&#x3C; "What is its street address?\n";
    char address[80];
    cin.getline(address, 80);
    cout &#x3C;&#x3C; "Year built: " &#x3C;&#x3C; year &#x3C;&#x3C; endl;
    cout &#x3C;&#x3C; "Address: " &#x3C;&#x3C; address &#x3C;&#x3C; endl;
    cout &#x3C;&#x3C; "Done!\n";
    // cin.get();
    return 0;
}

</code></pre>

```
(base) kimshan@MacBook-Pro output % ./"numstr"
What year was your house built?
2022
What is its street address?
No1
Year built: 2022
Address: No1
Done!
```

</details>

***

### 4.3 string类简介

C++98 加入了 std::string。string 可以自动调整大小，char\[]不可以。

<details>

<summary>char[] vs string</summary>

```cpp
// Init
char array1[20]; // √
char array2[20] = "Hello"; // √
char array3[] = "Hello"; // √
char array4[20] = {"Hello"}; // √
char array5[] = {"Hello"}; // √

string str1 = "Hello"; √
string str2 = {"Hello"}; √

// Assign
array1 = array2;// x
str1 = str2; // √

// 拼接
str1 += str2; // √
```

```cpp
// strtype2.cpp - assigning, adding, and appending
#include <iostream>
#include <string>               // make string class available
int main()
{
    using namespace std;
    string s1 = "penguin";
    string s2, s3;

    cout << "You can assign one string object to another: s2 = s1\n";
    s2 = s1;
    cout << "s1: " << s1 << ", s2: " << s2 << endl;
    cout << "You can assign a C-style string to a string object.\n";
    cout << "s2 = \"buzzard\"\n";
    s2 = "buzzard";
    cout << "s2: " << s2 << endl;
    cout << "You can concatenate strings: s3 = s1 + s2\n";
    s3 = s1 + s2;
    cout << "s3: " << s3 << endl;
    cout << "You can append strings.\n";
    s1 += s2;
    cout <<"s1 += s2 yields s1 = " << s1 << endl;
    s2 += " for a day";
    cout <<"s2 += \" for a day\" yields s2 = " << s2 << endl;

    //cin.get();
    return 0; 
}
```

```
(base) kimshan@MacBook-Pro output % ./"strtype2"
You can assign one string object to another: s2 = s1
s1: penguin, s2: penguin
You can assign a C-style string to a string object.
s2 = "buzzard"
s2: buzzard
You can concatenate strings: s3 = s1 + s2
s3: penguinbuzzard
You can append strings.
s1 += s2 yields s1 = penguinbuzzard
s2 += " for a day" yields s2 = buzzard for a day
```

</details>

<details>

<summary>string的其他操作，比如.size（class  vs cstring）</summary>

```cpp
// strtype3.cpp -- more string class features
#include <iostream>
#include <string>               // make string class available
#include <cstring>              // C-style string library
int main()
{
    using namespace std;
    char charr1[20]; 
    char charr2[20] = "jaguar"; 
    string str1;  
    string str2 = "panther";

    // assignment for string objects and character arrays
    str1 = str2;                // copy str2 to str1
    strcpy(charr1, charr2);     // copy charr2 to charr1
 
    // appending for string objects and character arrays
    str1 += " paste";           // add paste to end of str1
    strcat(charr1, " juice");   // add juice to end of charr1

    // finding the length of a string object and a C-style string
    int len1 = str1.size();     // obtain length of str1
    int len2 = strlen(charr1);  // obtain length of charr1
 
    cout << "The string " << str1 << " contains "
         << len1 << " characters.\n";
    cout << "The string " << charr1 << " contains "
         << len2 << " characters.\n";
    // cin.get();

    return 0; 
}

```

```
(base) kimshan@MacBook-Pro output % ./"strtype3"
The string panther paste contains 13 characters.
The string jaguar juice contains 12 characters.
```

</details>

<details>

<summary>cin.getline(charr, 20); vs getline(cin, str);</summary>

```cpp
// strtype4.cpp -- line input
#include <iostream>
#include <string>               // make string class available
#include <cstring>              // C-style string library
int main()
{
    using namespace std;
    char charr[20]; 
    string str;

    cout << "Length of string in charr before input: " 
         << strlen(charr) << endl;
    cout << "Length of string in str before input: "
         << str.size() << endl;
    cout << "Enter a line of text:\n";
    cin.getline(charr, 20);     // indicate maximum length
    cout << "You entered: " << charr << endl;
    cout << "Enter another line of text:\n";
    getline(cin, str);          // cin now an argument; no length specifier
    cout << "You entered: " << str << endl;
    cout << "Length of string in charr after input: " 
         << strlen(charr) << endl;
    cout << "Length of string in str after input: "
         << str.size() << endl;
    // cin.get();

    return 0; 
}

```

```
(base) kimshan@MacBook-Pro output % ./"strtype4"
Length of string in charr before input: 0 
Length of string in str before input: 0
Enter a line of text:
qwertyuio
You entered: qwertyuio
Enter another line of text:
asdfghjkl
You entered: asdfghjkl
Length of string in charr after input: 9
Length of string in str after input: 9
```

</details>

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





