# [Rust][The Book] Day1 - Hello World!
## 环境配置

```bash

$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh

```

无痛安装
测试安装成功

```bash

$ rustc --version

```

> **_NOTE:_** 需要有c++ 编译环境
## Hello World
和所有语言一样，第一课一定是hello world来体验Rust项目的流程。
### 创建工程目录
```bash
$ mkdir ~/projects
$ cd ~/projects
$ mkdir hello_world
$ cd hello_world
```

### 文件
rust源文件常用.rs结尾，并且文件名也遵循下划线分割命名习惯。例如，hello_world.rs。
创建一个名为main.rs的文件并写入代码。

```rust
fn main() {
    println!("Hello, world!");
}
```

可以看到rust程序的入口也是main。
编译源码

```bash
$ rustc main.rs
```

可以得到可执行文件main，执行后可以看到命令行输出
> Hello，world!

## 解析

1. Rust 的程序入口也是main函数。
2. println! 是一个rust 宏，和C类似，宏在编译前展开（后面章节有详细内容）。
3. 句尾分号。

## Cargo项目管理工具
Cargo 是rust的包管理和项目编译工具，使用Cargo来管理和编译rust工程可以提供依赖库的下载、编译和项目工程的构建工作。

### 使用Cargo创建工程

```bash
$ cargo new hello_cargo
$ cd hello_cargo
```

第一行命令创建了一个新路径 hello_cargo，同时会以这个路径创建git仓库。同时，Cargo创建了名为Cargo.toml的配置文件以及一个名为src的源文件路径，和src/main.rc文件。

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
edition = "2021"
[dependencies]
```

TOML  文件用于配置Cargo工程。[packgae] 字段定义了该包的信息，[dependencies]字段定义了依赖包的信息。
### 编译Cargo工程
```bash
$ cargo build #编译 --release 可以打release包
$ cargo run #编译 + 运行
$ cargo check #检查编译能通过，但不生成可执行文件 
```

