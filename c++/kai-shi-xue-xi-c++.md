---
description: >-
  第2章 开始学习C++:本章介绍创建简单C++程序的步骤。您可以学习到main(
  )函数扮演的角色以及C++程序使用的一些语句。您将使用预定义的cout和cin对象来实现程序输出和输入，学习如何创建和使用变量。最后，本章还将介绍函数——C++的编程模块。
icon: '2'
---

# 开始学习 C++

### 2.1 进入 C++

```cpp
/* displays a message
 */

#include <iostream>                           // a PREPROCESSOR directive

int main() {                                 // function header
    // start of function body
    using namespace std;                      // make definitions visible
    cout << "Hello world!" << endl;           // message

    cout << "Comme up and C++ me some time."
         << endl;
    cout << "You won't regret it! " << endl;

    // If the output window closes before you can read it,
    // add the following code:
    cout << "Press any key to continue." << endl;
    cin.get();
    return 0;                                 // terminate main()
}                                             // end of function body
```































