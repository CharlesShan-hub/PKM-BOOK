---
icon: '3'
description: https://rustwiki.org/zh-CN/book/ch03-00-common-programming-concepts.html
---

# 通用编程概念

## [**3.1.** 变量和可变性](https://rustwiki.org/zh-CN/book/ch03-01-variables-and-mutability.html)

### 可变性

{% hint style="info" %}
rust 特点：“变量不可变”。如何记住呢，可以这样理解，生成一个变量用的是`let`，本来也没说可以变。可以想象一个稳定的真理世界，里边都是不变的永恒的东西，这样就觉得很安全吧。如果要定义一个东西确实可以变，那就再加上 mut。
{% endhint %}

不可变变量

```rust
let x = 5;
```

可变变量

```rust
let mut x = 5;
```

常量：常量只能设置为常量表达式，而不能是函数调用的结果或是只能在运行时计算得到的值。

```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

### 遮蔽

{% hint style="info" %}
rust 特点：“变量重复声明”。如何记住呢（我的理解）：

* 对于 c，一个作用域中我们不能两次声明变量 x。我们的内存空间就很稳定，但是程序写的不方便，没用的东西没办法及时丢掉。
* 对于 python，可以重复的创建同样变量名的 x，每次后边就会取代前边。这样程序很好写，但是由于 python 是解释型语言，性能就会很差。（可以发现变量每变一次地址都不一样）。而且 Python 由于他的“逐行解释”，不能支持遮蔽了。

```python
s = "Hello"
print(id(s)) # 4534146672
s = s+" World"
print(id(s)) # 4534146544

x = 1
print(id(x)) # 4531576152
x = x+1
print(id(x)) # 4531576184

y = 1
print(id(y)) # 4531576152
y += 1
print(id(y)) # 4531576184
```

* 对于 rust，我们可以重复声明变量x，让程序好写。然后通过编译环节来提高性能，这样就能精准的控制每个变量的作用域了。

```rust
fn main() {
    let a = "String";
    println!("{a}"); // String
    let a = a.len();
    println!("{a}"); // 6
}
```
{% endhint %}

遮蔽就是内部的作用域的变量传不出去，但可以访问外部的作用域的变量。很多语言都可以做到：

{% code title="C（可以遮蔽）" %}
```c
#include <stdio.h>

int main()
{
    int i = 1;
    {
        int j = i;
        int i = j + 1;
        printf("%d\n", i); // 2
    }
    printf("%d\n", i); // 1
    return 0;
}
```
{% endcode %}

{% code title="Python（不能遮蔽）" %}
```python
x = 1
def f():
    x = x+1 # UnboundLocalError: cannot access local variable 'x' where it is not associated with a value
    print(x+1)
f()
print(x)
```
{% endcode %}

{% code title="Rust（可以遮蔽）" %}
```rust
fn main() {
    let a = "String";
    {
        let a = a.len();
        println!("{a}"); // 6let a = a.len();
    }
    println!("{a}"); // String
}
```
{% endcode %}

总得来讲，Rust 既可以像 C 一样遮蔽，又可以像 Python 一样好用。

***

## [**3.2.** 数据类型](https://rustwiki.org/zh-CN/book/ch03-02-data-types.html)

### 标量类型

### 复合类型







***

## [**3.3.** 函数](https://rustwiki.org/zh-CN/book/ch03-03-how-functions-work.html)



***

## [**3.4.** 注释](https://rustwiki.org/zh-CN/book/ch03-04-comments.html)



***

## [**3.5.** 控制流](https://rustwiki.org/zh-CN/book/ch03-05-control-flow.html)





