---
icon: '7'
description: >-
  https://rustwiki.org/zh-CN/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html
---

# 包、carte、模块

> * **包**（_Packages_）： Cargo 的一个功能，它允许你构建、测试和分享 crate。
> * **Crates** ：一个模块的树形结构，它形成了库或二进制项目。
> * **模块**（_Modules_）和 **use**： 允许你控制作用域和路径的私有性。
> * **路径**（_path_）：一个命名例如结构体、函数或模块等项的方式

## [**7.1.** 包和 crate](https://rustwiki.org/zh-CN/book/ch07-01-packages-and-crates.html)

1. `crate`是库
2. `crate root`是库的源文件，编译的起点
3. `binary crate`是库的二进制项
4. `packet` 是包，一个包里边有一个或多个库，一个包有一个 `Cargo.toml`
5. `cargo new`之后会生成一个包，rust 会默认创建一个叫做`src/main.rs`的crate root，这个是约定俗成。

***

## [**7.2.** 定义模块来控制作用域与私有性](https://rustwiki.org/zh-CN/book/ch07-02-defining-modules-to-control-scope-and-privacy.html)





***

## [**7.3.** 路径用于引用模块树中的项](https://rustwiki.org/zh-CN/book/ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html)





***

## [**7.4.** 使用 use 关键字将名称引入作用域](https://rustwiki.org/zh-CN/book/ch07-04-bringing-paths-into-scope-with-the-use-keyword.html)





***

## [**7.5.** 将模块分割进不同文件](https://rustwiki.org/zh-CN/book/ch07-05-separating-modules-into-different-files.html)





