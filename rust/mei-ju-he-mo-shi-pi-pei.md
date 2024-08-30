---
icon: '6'
description: https://rustwiki.org/zh-CN/book/ch06-00-enums.html
---

# 枚举和模式匹配

## [**6.1.** 定义枚举](https://rustwiki.org/zh-CN/book/ch06-01-defining-an-enum.html)

### 枚举基础

枚举和结构类似，都有自己的变量和方法，不过枚举更倾向于列举出所有的可能性。

<details>

<summary>枚举可以作为数据类型</summary>

自己定义枚举 IP = {v4, v6}

```rust
fn main() {
    // 定义枚举
    #[derive(PartialEq)] // to use "=="
    enum IpAddrKind {
        V4,
        V6,
    }

    // 访问枚举
    let four = IpAddrKind::V4;
    let six = IpAddrKind::V6;

    // 作为函数参数类型
    fn route(ip_type: IpAddrKind) {
        if ip_type == IpAddrKind::V4 {
            println!("Type of route is V4");
        } else {
            println!("Type of route is V6");
        }
    }
    route(four); // Type of route is V4
    route(six); // Type of route is V6
}

```

</details>

<details>

<summary>枚举可以包含数据，关联方法（有点像结构体了）</summary>

```rust
fn main() {
    // 枚举可以包含数据
    #[derive(PartialEq)]
    enum IpAddr {
        V4(u8, u8, u8, u8),
        V6(String),
    }

    impl IpAddr {
        fn test(&self) {
            println!("我也不知道干点啥\n");
        }
    }

    let home = IpAddr::V4(127, 0, 0, 1);
    let loopback = IpAddr::V6(String::from("::1"));
    home.test();
}
```

</details>

<details>

<summary> 更好的方案，enum 里边套结构体</summary>

这个是rust 标准库里边对 IP 类型枚举的实现方案

```rust
#![allow(unused)]
fn main() {
    struct Ipv4Addr {
        // --snip--
    }

    struct Ipv6Addr {
        // --snip--
    }

    enum IpAddr {
        V4(Ipv4Addr),
        V6(Ipv6Addr),
    }
}

```

</details>

### Option 枚举和其相对于空值的优势

空值容易引发错误的原因是，人们按照非空的方式去调用空。

rust如何解决的：空与非空也是一种枚举，他就是 Option！

```rust
// rust 中对 Option 的定义
enum Option<T> {
    Some(T),
    None,
}
```

如果我们写了下面的函数，并尝试运行

```rust
let x: i8 = 5;
let y: Option<i8> = Some(5);

let sum = x + y;
```

这不会通过！因为 rust 不会把i8和 Option\<i8>加在一起。我们需要手动把Option\<i8>转换成i8，这样就可以保证，所有可以编译通过的代码不会把空加进去了。

***

## [**6.2.** match 控制流运算符](https://rustwiki.org/zh-CN/book/ch06-02-match.html)







***

## [**6.3.** if let 简单控制流](https://rustwiki.org/zh-CN/book/ch06-03-if-let.html)



