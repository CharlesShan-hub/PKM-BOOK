---
icon: '5'
description: https://rustwiki.org/zh-CN/book/ch05-00-structs.html
---

# 结构体

## [**5.1.** 定义和举例说明结构体](https://rustwiki.org/zh-CN/book/ch05-01-defining-structs.html)

### 基础的定义与赋值

<details>

<summary>Code</summary>

```rust
// 定义结构体
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    // 生成结构体
    // 注意整个实例必须是可变的；Rust 并不允许只将某个字段标记为可变
    let mut user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };

    // 改变结构体中的值
    user1.email = String::from("anotheremail@example.com");
}
```

</details>

<details>

<summary>结构体应拥有数据的所有权</summary>

<pre class="language-rust"><code class="lang-rust">struct User {
    active: bool,
<strong>    username: &#x26;str, // wrong! use String!
</strong><strong>    email: &#x26;str, // wrong! use String!
</strong>    sign_in_count: u64,
}

fn main() {
    let user1 = User {
        email: "someone@example.com",
        username: "someusername123",
        active: true,
        sign_in_count: 1,
    };
}

</code></pre>

</details>

### 语法糖：变量与字段同名

<details>

<summary>Code</summary>

<pre class="language-rust"><code class="lang-rust">struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn build_user(email: String, username: String) -> User {
    User {
<strong>        email,    // email:email,
</strong><strong>        username, // username:username,
</strong>        active: true,
        sign_in_count: 1,
    }
}

fn main() {
    let user1 = build_user(
        String::from("someone@example.com"),
        String::from("someusername123"),
    );
}

</code></pre>

</details>

### 语法糖：从别的结构体为模板创建新结构体

<details>

<summary>Code</summary>

<pre class="language-rust"><code class="lang-rust">struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    let user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };

    // let user2 = User {
    //     active: user1.active,
    //     username: user1.username,
    //     email: String::from("another@example.com"),
    //     sign_in_count: user1.sign_in_count,
    // };

    let user2 = User {
        email: String::from("another@example.com"),
<strong>        ..user1
</strong>    };
}
</code></pre>

</details>

### 元组结构体

<details>

<summary>Code</summary>

```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```

</details>

### 没有任何字段的类单元结构体

<details>

<summary>Code</summary>

```rust
struct AlwaysEqual;

fn main() {
    let subject = AlwaysEqual;
}
```

</details>

***

## [**5.2.** 使用结构体的代码例子](https://rustwiki.org/zh-CN/book/ch05-02-example-structs.html)



***

## [**5.3.** 方法语法](https://rustwiki.org/zh-CN/book/ch05-03-method-syntax.html)



