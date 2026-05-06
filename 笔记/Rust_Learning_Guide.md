
# Rust 语言体系化学习指南


-   [1. Rust 生态全景与核心哲学](#1-rust-生态全景与核心哲学)
    -   [1.1. 白话概述：Rust 是什么？为什么要学它？](#11-白话概述rust-是什么为什么要学它)
    -   [1.2. Rust 生态架构全景图](#12-rust-生态架构全景图)
    -   [1.3. 核心设计哲学：安全、性能、生产力的三角平衡](#13-核心设计哲学安全性能生产力的三角平衡)
-   [2. 环境搭建与工具链](#2-环境搭建与工具链)
    -   [2.1. 安装 Rust：rustup](#21-安装-rustrustup)
    -   [2.2. Cargo：Rust 的构建系统和包管理器](#22-cargorust-的构建系统和包管理器)
    -   [2.3. IDE 配置与开发效率工具](#23-ide-配置与开发效率工具)
-   [3. Rust 基础语法速通](#3-rust-基础语法速通)
    -   [3.1. 变量与可变性](#31-变量与可变性)
    -   [3.2. 数据类型](#32-数据类型)
    -   [3.3. 函数](#33-函数)
    -   [3.4. 控制流](#34-控制流)
    -   [3.5. 注释与文档](#35-注释与文档)
-   [4. 所有权：Rust 的核心基石](#4-所有权rust-的核心基石)
    -   [4.1. 所有权规则](#41-所有权规则)
    -   [4.2. 变量与数据交互：移动与克隆](#42-变量与数据交互移动与克隆)
    -   [4.3. 引用与借用](#43-引用与借用)
    -   [4.4. 切片类型](#44-切片类型)
-   [5. 结构体、枚举与模式匹配](#5-结构体枚举与模式匹配)
    -   [5.1. 结构体](#51-结构体)
    -   [5.2. 枚举与 Option](#52-枚举与-option)
    -   [5.3. 模式匹配](#53-模式匹配)
-   [6. 包、Crate 与模块系统](#6-包crate-与模块系统)
    -   [6.1. 包与 Crate](#61-包与-crate)
    -   [6.2. 模块](#62-模块)
    -   [6.3. 路径与 use 关键字](#63-路径与-use-关键字)
-   [7. 常用集合](#7-常用集合)
    -   [7.1. Vector](#71-vector)
    -   [7.2. 字符串](#72-字符串)
    -   [7.3. HashMap](#73-hashmap)
-   [8. 错误处理](#8-错误处理)
    -   [8.1. panic! 与不可恢复错误](#81-panic-与不可恢复错误)
    -   [8.2. Result 与可恢复错误](#82-result-与可恢复错误)
    -   [8.3. ? 运算符与错误传播](#83--运算符与错误传播)
-   [9. 泛型、Trait 与生命周期](#9-泛型trait-与生命周期)
    -   [9.1. 泛型数据类型](#91-泛型数据类型)
    -   [9.2. Trait：定义共享行为](#92-trait定义共享行为)
    -   [9.3. 生命周期](#93-生命周期)
-   [10. 测试与文档](#10-测试与文档)
    -   [10.1. 编写测试](#101-编写测试)
    -   [10.2. 文档注释与文档测试](#102-文档注释与文档测试)
-   [11. 函数式语言特性：迭代器与闭包](#11-函数式语言特性迭代器与闭包)
    -   [11.1. 闭包](#111-闭包)
    -   [11.2. 迭代器](#112-迭代器)
-   [12. 智能指针](#12-智能指针)
    -   [12.1. Box<T>：堆上分配](#121-boxt堆上分配)
    -   [12.2. Rc<T>：引用计数](#122-rct引用计数)
    -   [12.3. RefCell<T>：内部可变性](#123-refcellt内部可变性)
    -   [12.4. 循环引用与 Weak<T>](#124-循环引用与-weakt)
-   [13. 无畏并发](#13-无畏并发)
    -   [13.1. 线程基础](#131-线程基础)
    -   [13.2. 消息传递并发](#132-消息传递并发)
    -   [13.3. 共享状态并发](#133-共享状态并发)
    -   [13.4. Send 与 Sync Trait](#134-send-与-sync-trait)
-   [14. 面向对象编程特性](#14-面向对象编程特性)
    -   [14.1. Trait 对象](#141-trait-对象)
    -   [14.2. 面向对象设计模式的实现](#142-面向对象设计模式的实现)
-   [15. 模式与匹配进阶](#15-模式与匹配进阶)
    -   [15.1. 模式的所有使用场景](#151-模式的所有使用场景)
    -   [15.2. 可反驳性与不可反驳性](#152-可反驳性与不可反驳性)
-   [16. 高级特征](#16-高级特征)
    -   [16.1. Unsafe Rust](#161-unsafe-rust)
    -   [16.2. 高级 Trait](#162-高级-trait)
    -   [16.3. 高级类型](#163-高级类型)
    -   [16.4. 高级函数与闭包](#164-高级函数与闭包)
-   [17. 异步编程：async/await 与 Tokio](#17-异步编程asyncawait-与-tokio)
    -   [17.1. 异步编程模型](#171-异步编程模型)
    -   [17.2. Tokio 运行时](#172-tokio-运行时)
    -   [17.3. 实战：构建异步 Web 服务](#173-实战构建异步-web-服务)
-   [18. 宏与元编程](#18-宏与元编程)
    -   [18.1. 声明宏](#181-声明宏)
    -   [18.2. 过程宏](#182-过程宏)
-   [19. 项目实战：构建一个命令行工具](#19-项目实战构建一个命令行工具)
    -   [19.1. 项目概述：minigrep](#191-项目概述minigrep)
    -   [19.2. 分步实现](#192-分步实现)
-   [20. Rust 常用第三方库与生态](#20-rust-常用第三方库与生态)
    -   [20.1. Web 开发](#201-web-开发)
    -   [20.2. 数据库与 ORM](#202-数据库与-orm)
    -   [20.3. 序列化与反序列化](#203-序列化与反序列化)
    -   [20.4. 命令行工具](#204-命令行工具)
    -   [20.5. 并发与异步](#205-并发与异步)
    -   [20.6. 其他精选库](#206-其他精选库)
-   [21. 最佳实践与常见陷阱](#21-最佳实践与常见陷阱)
    -   [21.1. 所有权与借用常见错误](#211-所有权与借用常见错误)
    -   [21.2. 代码组织最佳实践](#212-代码组织最佳实践)
    -   [21.3. 错误处理最佳实践](#213-错误处理最佳实践)
    -   [21.4. 性能优化提示](#214-性能优化提示)
-   [22. 总结：您的下一步学习路线图](#22-总结您的下一步学习路线图)

## 1. Rust 生态全景与核心哲学

### 1.1. 白话概述：Rust 是什么？为什么要学它？

Rust 是一门**系统级编程语言**，它以一种前所未有的方式解决了困扰开发者数十年的难题：如何在保证**内存安全**和**线程安全**的同时，还能实现**不亚于 C/C++ 的性能**。

如果说 C++ 给了你赛车的全部控制权（包括随时可能翻车的风险），而 Java/Python 给了你一辆带防抱死系统和安全气囊的轿车（但牺牲了部分性能和底层控制力），那么 Rust 就像是**一辆既有赛车性能，又配备了世界顶尖安全系统的超级跑车**。

Rust 已经连续八年成为 Stack Overflow 开发者调查中“最受喜爱”的编程语言。它被用于：

-   **操作系统内核开发**（如 Redox OS）
-   **浏览器引擎**（Firefox 的 Servo 项目）
-   **区块链基础设施**（Polkadot、Solana）
-   **云原生基础设施**（Dropbox、AWS 的核心组件）
-   **命令行工具**（ripgrep、fd、bat）

### 1.2. Rust 生态架构全景图

在深入具体技术前，让我们先建立一个全局视图，理解 Rust 生态的层次关系。

```mermaid
graph TD
    subgraph “应用层 (Applications)”
        A1[Web 服务<br/>Axum, Actix-web]
        A2[CLI 工具<br/>clap, anyhow]
        A3[嵌入式/OS<br/>no_std, embassy]
        A4[游戏开发<br/>Bevy, wgpu]
    end

    subgraph “高级库层 (High-level Libraries)”
        B1[Tokio / async-std<br/>异步运行时]
        B2[Serde<br/>序列化框架]
        B3[Rayon<br/>数据并行]
        B4[SQLx / Diesel<br/>数据库]
    end

    subgraph “标准库 (std)”
        C[std::*<br/>集合、I/O、线程、网络、智能指针...]
    end

    subgraph “核心库 (core)”
        D[core::*<br/>基础类型、Trait、宏、内存操作<br/>（可用于裸机环境）]
    end

    subgraph “编译器与工具链”
        E1[rustc]
        E2[Cargo]
        E3[rustup]
        E4[rustfmt / Clippy]
    end

    A1 --> B1
    A2 --> B1
    A3 --> D
    A1 --> B3
    A2 --> B3
    B1 --> C
    B2 --> C
    B3 --> C
    B4 --> C
    C --> D
    E1 --> D
    E2 --> E1
```

**架构解读：**

-   **核心库（core）**：Rust 语言的最核心部分，不依赖任何操作系统，可以用于裸机（bare-metal）和嵌入式开发。定义了最基础的类型（如 `Option`、`Result`）、Trait 和宏。
-   **标准库（std）**：建立在 core 之上，提供了丰富的功能：集合类型（`Vec`、`HashMap`）、I/O 操作、线程管理、网络通信等。大多数 Rust 程序都依赖 std。
-   **高级库层**：这是 Rust 生态最活跃的部分。Tokio 是异步运行时的王者，Serde 是序列化的标准，Rayon 让数据并行变得简单。
-   **工具链**：`rustup` 管理 Rust 版本，`cargo` 管理项目和依赖，`rustfmt` 格式化代码，`Clippy` 提供静态检查建议。这套工具链的完善程度是 Rust 的一大优势。

### 1.3. 核心设计哲学：安全、性能、生产力的三角平衡

Rust 的核心创新在于通过**所有权系统**在编译期解决内存安全问题，无需垃圾回收即可避免悬垂指针、数据竞争等传统漏洞。

-   **所有权**：每个值都有一个唯一的所有者，所有者离开作用域时值被自动释放。
-   **借用**：通过引用临时借用数据，避免复制开销，同时通过“单一可变引用”规则防止数据竞争。
-   **生命周期**：显式标注引用的存活周期，编译器确保引用不会指向已释放的内存。

> **专家提示**：Rust 的学习曲线确实陡峭，前期需要适应所有权、借用与生命周期等编译期安全机制。但请相信我四十年的经验：这种“前期痛苦”是值得的。一旦你理解了 Rust 的规则，你会发现过去在 C/C++ 中花费大量时间调试的内存错误和并发 Bug，在 Rust 中几乎消失了。这就是“无畏并发”的真正含义。

## 2. 环境搭建与工具链

### 2.1. 安装 Rust：rustup

`rustup` 是 Rust 的官方工具链管理器，也是安装 Rust 的唯一推荐方式。

```bash
# Linux / macOS
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Windows
# 下载并运行 rustup-init.exe
```

安装完成后，重启终端或执行 `source $HOME/.cargo/env`，然后验证：

```bash
rustc --version
cargo --version
```

> **专家提示**：如果在中国大陆，配置 Cargo 镜像源可以显著提升下载速度。在 `$HOME/.cargo/config.toml` 中添加：

```toml
[source.crates-io]
replace-with = 'ustc'

[source.ustc]
registry = "https://mirrors.ustc.edu.cn/crates.io-index"
```

### 2.2. Cargo：Rust 的构建系统和包管理器

Cargo 是 Rust 的构建系统和包管理器，是 Rust 开发生态系统的核心工具。

```bash
# 创建新项目
cargo new hello_world
cd hello_world

# 项目结构
# hello_world/
# ├── Cargo.toml  # 项目配置文件（依赖、元数据）
# └── src/
#     └── main.rs  # 程序入口

# 常用命令
cargo build          # 编译（debug 模式）
cargo build --release # 编译（release 模式，优化）
cargo run            # 编译并运行
cargo check          # 快速检查代码是否能编译（比 build 快）
cargo test           # 运行测试
cargo doc --open     # 生成并打开文档
cargo clean          # 清理 target 目录
```

`Cargo.toml` 示例：

```toml
[package]
name = "hello_world"
version = "0.1.0"
edition = "2024"  # Rust 2024 Edition 已于 2025 年 2 月稳定

[dependencies]
serde = { version = "1.0", features = ["derive"] }
tokio = { version = "1.0", features = ["full"] }
```

### 2.3. IDE 配置与开发效率工具

推荐使用 **VS Code** 配合以下插件：

-   **rust-analyzer**：Rust 语言服务器，提供代码补全、跳转定义、实时错误提示等。
-   **CodeLLDB**：调试支持。
-   **Even Better TOML**：Cargo.toml 文件的语法高亮和补全。

其他必备工具：

```bash
# 安装代码格式化工具和静态检查工具
rustup component add rustfmt
rustup component add clippy

# 使用
cargo fmt       # 格式化代码
cargo clippy    # 静态检查，提供改进建议
```

## 3. Rust 基础语法速通

### 3.1. 变量与可变性

Rust 中的变量**默认不可变**。这是 Rust 推动函数式编程风格和安全性的一部分。

```rust
fn main() {
    let x = 5;          // 不可变变量
    // x = 6;           // 编译错误！不能对不可变变量赋值

    let mut y = 10;     // 可变变量（使用 mut 关键字）
    y = 20;             // 合法

    const MAX_POINTS: u32 = 100_000;  // 常量，必须标注类型，命名全大写

    // 遮蔽（Shadowing）
    let z = 5;
    let z = z + 1;      // 新的变量 z，遮蔽了旧的 z
    let z = "hello";    // 甚至可以改变类型
}
```

### 3.2. 数据类型

Rust 是**静态类型**语言，编译时必须知道所有变量的类型。

#### 标量类型

| 类型 | 描述 | 示例 |
| :--- | :--- | :--- |
| **整数** | `i8`/`u8`, `i16`/`u16`, `i32`/`u32`, `i64`/`u64`, `i128`/`u128`, `isize`/`usize` | `42`, `0xff`, `0b1010`, `1_000_000` |
| **浮点数** | `f32`, `f64`（默认） | `3.14`, `2.0` |
| **布尔值** | `bool` | `true`, `false` |
| **字符** | `char`（Unicode 标量值，4 字节） | `'a'`, `'中'`, `'😻'` |

#### 复合类型

```rust
fn main() {
    // 元组（Tuple）：固定长度，元素类型可不同
    let tup: (i32, f64, u8) = (500, 6.4, 1);
    let (x, y, z) = tup;                    // 解构
    println!("y = {}", y);
    println!("first = {}", tup.0);          // 索引访问

    // 数组（Array）：固定长度，元素类型必须相同
    let arr: [i32; 5] = [1, 2, 3, 4, 5];
    let zeros = [0; 100];                   // [0, 0, 0, ...]
    println!("first = {}", arr[0]);
}
```

### 3.3. 函数

```rust
// 函数定义
fn greet(name: &str) -> String {
    // 最后一个表达式作为返回值（不加分号）
    format!("Hello, {}!", name)
}

// 使用 return 关键字提前返回
fn max(a: i32, b: i32) -> i32 {
    if a > b {
        return a;
    }
    b  // 注意：没有分号，这是表达式，作为返回值
}

fn main() {
    let msg = greet("Rust");
    println!("{}", msg);
    println!("max(3, 7) = {}", max(3, 7));
}
```

### 3.4. 控制流

```rust
fn main() {
    let number = 6;

    // if 表达式
    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else {
        println!("number is not divisible by 4 or 3");
    }

    // if 是表达式，可以用于赋值
    let condition = true;
    let x = if condition { 5 } else { 6 };
    println!("x = {}", x);

    // loop 循环（无限循环，需要 break 退出）
    let mut counter = 0;
    let result = loop {
        counter += 1;
        if counter == 10 {
            break counter * 2;  // break 可以返回值
        }
    };
    println!("result = {}", result);

    // while 循环
    let mut n = 3;
    while n != 0 {
        println!("{}!", n);
        n -= 1;
    }
    println!("LIFTOFF!!!");

    // for 循环（最常用的遍历方式）
    let arr = [10, 20, 30, 40, 50];
    for element in arr.iter() {
        println!("value is: {}", element);
    }

    // Range
    for number in (1..4).rev() {
        println!("{}!", number);
    }
}
```

### 3.5. 注释与文档

```rust
// 单行注释

/*
 * 多行注释
 * 可以跨越多行
 */

/// 文档注释（支持 Markdown），用于函数、结构体等
/// 
/// # Examples
/// ```
/// let result = add(2, 3);
/// assert_eq!(result, 5);
/// ```
fn add(a: i32, b: i32) -> i32 {
    a + b
}

//! 模块级文档注释
//! 通常放在文件开头
```

## 4. 所有权：Rust 的核心基石

所有权是 Rust 最独特的特性，它让 Rust 无需垃圾回收器即可保证内存安全。

### 4.1. 所有权规则

Rust 的所有权模型可用三条规则概括：

1.  Rust 中的每个值都有一个**所有者**。
2.  值在任意时刻**有且仅有一个所有者**。
3.  当所有者离开作用域时，该值将被**自动释放**（调用 `drop` 函数）。

```rust
fn main() {
    {                      // s 在这里无效，它尚未声明
        let s = String::from("hello"); // s 从此处开始有效
        println!("{}", s);
    }                      // 此作用域结束，s 不再有效，内存自动释放
}
```

### 4.2. 变量与数据交互：移动与克隆

```rust
fn main() {
    // 栈上的数据：复制（Copy）
    let x = 5;
    let y = x;  // x 的值被复制给 y，x 仍然有效
    println!("x = {}, y = {}", x, y);  // 正常

    // 堆上的数据：移动（Move）
    let s1 = String::from("hello");
    let s2 = s1;  // s1 的所有权被移动到 s2，s1 不再有效
    // println!("{}", s1);  // 编译错误：s1 已被移动
    println!("{}", s2);     // 正常

    // 克隆（Clone）：深拷贝堆数据
    let s3 = String::from("world");
    let s4 = s3.clone();  // 堆数据被复制，s3 仍然有效
    println!("s3 = {}, s4 = {}", s3, s4);  // 正常
}
```

下面的流程图直观展示了所有权移动的过程：

```mermaid
graph TD
    subgraph “移动前”
        S1[s1: String] --> H1[堆内存: “hello”]
    end

    subgraph “移动后”
        S2[s2: String] --> H2[堆内存: “hello”]
        S1_Invalid[s1: 无效]
    end

    S1 --> S2
    H1 --> H2
    style S1_Invalid fill:#ffcccc
```

### 4.3. 引用与借用

引用允许你在不获取所有权的情况下使用值，这称为**借用**。

```rust
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);  // 借用 s1

    // s1 仍然有效，因为我们没有转移所有权
    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize {  // s 是对 String 的引用
    s.len()
}  // s 离开作用域，但由于它不拥有所有权，所以不会释放内存
```

**引用的规则**：
1.  在任意给定时间，**要么**只能有一个可变引用，**要么**只能有多个不可变引用。
2.  引用必须总是有效的。

```rust
fn main() {
    let mut s = String::from("hello");

    // 不可变引用（可以有多个）
    let r1 = &s;
    let r2 = &s;
    println!("{} and {}", r1, r2);

    // 可变引用（只能有一个，且不能与不可变引用同时存在）
    let r3 = &mut s;
    r3.push_str(", world");
    println!("{}", r3);
}
```

> **专家提示**：这条“可变引用唯一性”规则是 Rust 在编译期防止**数据竞争**的核心机制。数据竞争发生在：两个或多个指针同时访问同一数据，至少有一个用于写入，且没有同步机制。Rust 的借用检查器在编译时就能捕获这类问题，这是 C/C++ 中无数难以调试的 Bug 的根源。

### 4.4. 切片类型

切片允许你引用集合中一段连续的元素序列，而不需要获取所有权。

```rust
fn main() {
    let s = String::from("hello world");

    let hello = &s[0..5];   // 切片，类型是 &str
    let world = &s[6..11];

    println!("{} {}", hello, world);

    // 字符串字面量就是切片
    let literal = "hello";  // 类型是 &str
}

fn first_word(s: &String) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }

    &s[..]
}
```

## 5. 结构体、枚举与模式匹配

### 5.1. 结构体

```rust
// 定义结构体
struct User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}

fn main() {
    // 创建实例
    let mut user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };

    // 修改字段
    user1.email = String::from("anotheremail@example.com");

    // 结构体更新语法
    let user2 = User {
        email: String::from("another@example.com"),
        ..user1  // 其余字段从 user1 获取（注意：username 的所有权被移动了）
    };
}

// 元组结构体
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

// 单元结构体（没有任何字段）
struct AlwaysEqual;

// 方法定义
impl User {
    // 关联函数（通常用作构造函数）
    fn new(email: String, username: String) -> Self {
        Self {
            email,
            username,
            active: true,
            sign_in_count: 0,
        }
    }

    // 方法（第一个参数是 self）
    fn is_active(&self) -> bool {
        self.active
    }

    // 修改 self 的方法
    fn increment_sign_in(&mut self) {
        self.sign_in_count += 1;
    }
}
```

### 5.2. 枚举与 Option

```rust
// 定义枚举
enum IpAddrKind {
    V4,
    V6,
}

// 带数据的枚举
enum IpAddr {
    V4(u8, u8, u8, u8),
    V6(String),
}

// Option 枚举（定义在标准库中，无需导入）
// enum Option<T> {
//     Some(T),
//     None,
// }

fn main() {
    let home = IpAddr::V4(127, 0, 0, 1);
    let loopback = IpAddr::V6(String::from("::1"));

    // Option 的使用
    let some_number = Some(5);
    let some_string = Some("a string");
    let absent_number: Option<i32> = None;

    // Option 强制你处理 None 的情况
    let x: i8 = 5;
    let y: Option<i8> = Some(3);
    // let sum = x + y;  // 编译错误：不能将 Option<i8> 和 i8 相加
}
```

### 5.3. 模式匹配

```rust
#[derive(Debug)]
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

#[derive(Debug)]
enum UsState {
    Alabama,
    Alaska,
    // ...
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => {
            println!("Lucky penny!");
            1
        }
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter(state) => {
            println!("State quarter from {:?}!", state);
            25
        }
    }
}

fn main() {
    // 匹配 Option<T>
    let x: Option<i32> = Some(5);
    let y = match x {
        Some(n) => n,
        None => 0,
    };
    println!("y = {}", y);

    // if let 简洁控制流
    let config_max = Some(3u8);
    if let Some(max) = config_max {
        println!("The maximum is configured to be {}", max);
    }
}
```

## 6. 包、Crate 与模块系统

Rust 的模块系统帮助你组织代码，控制作用域和私有性。

```mermaid
graph TD
    subgraph “Crate 结构”
        C[Crate] --> M1[模块 mod]
        C --> M2[模块 mod]
        M1 --> SM1[子模块 mod]
        M1 --> SM2[子模块 mod]
        M2 --> SM3[子模块 mod]
    end

    subgraph “可见性”
        PUB[pub: 公开] --> |对外可见| C
        PRIV[无 pub: 私有] --> |仅模块内可见| C
    end
```

### 6.1. 包与 Crate

-   **包**：一个 Cargo 项目，可以包含多个二进制 crate 和至多一个库 crate。
-   **Crate**：Rust 的编译单元，分为二进制 crate（`src/main.rs`）和库 crate（`src/lib.rs`）。

### 6.2. 模块

```rust
// src/lib.rs
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
        fn seat_at_table() {}
    }

    mod serving {
        fn take_order() {}
        fn serve_order() {}
        fn take_payment() {}
    }
}

pub fn eat_at_restaurant() {
    // 绝对路径
    crate::front_of_house::hosting::add_to_waitlist();

    // 相对路径
    front_of_house::hosting::add_to_waitlist();
}
```

### 6.3. 路径与 use 关键字

```rust
// 使用 use 简化路径
use crate::front_of_house::hosting;
use std::collections::HashMap;

// 使用 as 重命名
use std::io::Result as IoResult;

// 使用 pub use 重导出
pub use crate::front_of_house::hosting;

// 嵌套路径
use std::{cmp::Ordering, io};
// 等价于：
// use std::cmp::Ordering;
// use std::io;

// 使用 * 导入所有公有项
use std::collections::*;

fn main() {
    hosting::add_to_waitlist();

    let mut map = HashMap::new();
    map.insert(1, 2);
}
```

## 7. 常用集合

### 7.1. Vector

```rust
fn main() {
    // 创建 Vector
    let v: Vec<i32> = Vec::new();
    let v2 = vec![1, 2, 3];  // 使用 vec! 宏

    // 更新 Vector
    let mut v3 = Vec::new();
    v3.push(5);
    v3.push(6);
    v3.push(7);

    // 读取元素
    let third: &i32 = &v3[2];
    println!("The third element is {}", third);

    match v3.get(2) {
        Some(third) => println!("The third element is {}", third),
        None => println!("There is no third element."),
    }

    // 遍历
    for i in &v3 {
        println!("{}", i);
    }

    // 遍历并修改
    for i in &mut v3 {
        *i += 50;  // 解引用
    }
}
```

### 7.2. 字符串

```rust
fn main() {
    // 创建字符串
    let mut s = String::new();
    let s2 = "initial contents".to_string();
    let s3 = String::from("initial contents");

    // 更新字符串
    s.push_str("bar");
    s.push('!');

    // 拼接
    let s4 = s2 + &s3;  // s2 的所有权被移动

    // 使用 format! 宏
    let s5 = format!("{}-{}-{}", s4, s3, "world");

    // 遍历字符串
    for c in "नमस्ते".chars() {
        println!("{}", c);
    }

    for b in "नमस्ते".bytes() {
        println!("{}", b);
    }
}
```

### 7.3. HashMap

```rust
use std::collections::HashMap;

fn main() {
    // 创建 HashMap
    let mut scores = HashMap::new();
    scores.insert(String::from("Blue"), 10);
    scores.insert(String::from("Yellow"), 50);

    // 使用 collect 创建
    let teams = vec![String::from("Blue"), String::from("Yellow")];
    let initial_scores = vec![10, 50];
    let scores: HashMap<_, _> = teams.into_iter().zip(initial_scores.into_iter()).collect();

    // 访问值
    let team_name = String::from("Blue");
    let score = scores.get(&team_name);
    match score {
        Some(s) => println!("Score: {}", s),
        None => println!("Team not found"),
    }

    // 遍历
    for (key, value) in &scores {
        println!("{}: {}", key, value);
    }

    // 更新
    // 覆盖
    scores.insert(String::from("Blue"), 25);

    // 只在键不存在时插入
    scores.entry(String::from("Yellow")).or_insert(50);
    scores.entry(String::from("Red")).or_insert(60);

    // 基于旧值更新
    let text = "hello world wonderful world";
    let mut map = HashMap::new();
    for word in text.split_whitespace() {
        let count = map.entry(word).or_insert(0);
        *count += 1;
    }
}
```

## 8. 错误处理

Rust 将错误分为两大类：**可恢复错误**和**不可恢复错误**。

### 8.1. panic! 与不可恢复错误

```rust
fn main() {
    // 手动触发 panic
    // panic!("crash and burn");

    // 数组越界访问会 panic
    let v = vec![1, 2, 3];
    // v[99];  // 这会导致 panic

    // 设置环境变量 RUST_BACKTRACE=1 可以获取回溯信息
}
```

### 8.2. Result 与可恢复错误

```rust
use std::fs::File;
use std::io::ErrorKind;

fn main() {
    let f = File::open("hello.txt");

    let f = match f {
        Ok(file) => file,
        Err(error) => match error.kind() {
            ErrorKind::NotFound => match File::create("hello.txt") {
                Ok(fc) => fc,
                Err(e) => panic!("Problem creating the file: {:?}", e),
            },
            other_error => {
                panic!("Problem opening the file: {:?}", other_error)
            }
        },
    };
}
```

### 8.3. ? 运算符与错误传播

```rust
use std::fs::File;
use std::io::{self, Read};

fn read_username_from_file() -> Result<String, io::Error> {
    let mut f = File::open("hello.txt")?;  // ? 在出错时提前返回 Err
    let mut s = String::new();
    f.read_to_string(&mut s)?;
    Ok(s)
}

// 更简洁的写法
fn read_username_from_file_short() -> Result<String, io::Error> {
    let mut s = String::new();
    File::open("hello.txt")?.read_to_string(&mut s)?;
    Ok(s)
}

// 使用标准库函数
fn read_username_from_file_std() -> Result<String, io::Error> {
    std::fs::read_to_string("hello.txt")
}

fn main() -> Result<(), Box<dyn std::error::Error>> {
    let username = read_username_from_file()?;
    println!("Username: {}", username);
    Ok(())
}
```

> **专家提示**：在库代码中，建议使用 `thiserror` 定义自定义错误类型；在应用程序中，`anyhow` 可以极大简化错误处理。这是 Rust 社区的成熟实践。

## 9. 泛型、Trait 与生命周期

### 9.1. 泛型数据类型

```rust
// 泛型函数
fn largest<T: PartialOrd>(list: &[T]) -> &T {
    let mut largest = &list[0];
    for item in list {
        if item > largest {
            largest = item;
        }
    }
    largest
}

// 泛型结构体
struct Point<T> {
    x: T,
    y: T,
}

// 泛型方法
impl<T> Point<T> {
    fn x(&self) -> &T {
        &self.x
    }
}

// 对特定类型实现方法
impl Point<f32> {
    fn distance_from_origin(&self) -> f32 {
        (self.x.powi(2) + self.y.powi(2)).sqrt()
    }
}

fn main() {
    let number_list = vec![34, 50, 25, 100, 65];
    let result = largest(&number_list);
    println!("The largest number is {}", result);

    let p = Point { x: 5, y: 10 };
    println!("p.x = {}", p.x());
}
```

### 9.2. Trait：定义共享行为

```rust
// 定义 Trait
pub trait Summary {
    fn summarize(&self) -> String;

    // 默认实现
    fn summarize_author(&self) -> String {
        String::from("(Author unknown)")
    }
}

pub struct NewsArticle {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}

impl Summary for Tweet {
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}

// Trait 作为参数
fn notify(item: &impl Summary) {
    println!("Breaking news! {}", item.summarize());
}

// Trait Bound 语法（等价写法）
fn notify_bound<T: Summary>(item: &T) {
    println!("Breaking news! {}", item.summarize());
}

// 多个 Trait Bound
fn notify_multiple(item: &(impl Summary + Display)) {}
fn notify_multiple_bound<T: Summary + Display>(item: &T) {}

// where 子句提高可读性
fn some_function<T, U>(t: &T, u: &U) -> i32
where
    T: Display + Clone,
    U: Clone + Debug,
{
    // ...
    0
}

// 返回实现了 Trait 的类型
fn returns_summarizable() -> impl Summary {
    Tweet {
        username: String::from("horse_ebooks"),
        content: String::from("of course, as you probably already know, people"),
        reply: false,
        retweet: false,
    }
}

fn main() {
    let tweet = Tweet {
        username: String::from("horse_ebooks"),
        content: String::from("of course, as you probably already know, people"),
        reply: false,
        retweet: false,
    };
    println!("1 new tweet: {}", tweet.summarize());
}
```

### 9.3. 生命周期

生命周期是 Rust 最独特的特性之一，它确保引用在使用期间始终有效。

```rust
// 生命周期标注语法
// &'a i32        // 带有显式生命周期的引用
// &'a mut i32    // 带有显式生命周期的可变引用

// 函数中的生命周期
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}

// 结构体中的生命周期
struct ImportantExcerpt<'a> {
    part: &'a str,
}

impl<'a> ImportantExcerpt<'a> {
    fn level(&self) -> i32 {
        3
    }

    fn announce_and_return_part(&self, announcement: &str) -> &str {
        println!("Attention please: {}", announcement);
        self.part
    }
}

fn main() {
    let string1 = String::from("long string is long");
    let string2 = String::from("xyz");

    let result = longest(string1.as_str(), string2.as_str());
    println!("The longest string is {}", result);

    let novel = String::from("Call me Ishmael. Some years ago...");
    let first_sentence = novel.split('.').next().expect("Could not find a '.'");
    let i = ImportantExcerpt {
        part: first_sentence,
    };
}
```

**生命周期省略规则**：
1.  每个是引用的参数都有它自己的生命周期参数。
2.  如果只有一个输入生命周期参数，那么它被赋予所有输出生命周期参数。
3.  如果方法有多个输入生命周期参数，但其中一个是 `&self` 或 `&mut self`，那么 `self` 的生命周期被赋予所有输出生命周期参数。

## 10. 测试与文档

### 10.1. 编写测试

```rust
// 使用 cargo test 运行测试

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn it_works() {
        let result = 2 + 2;
        assert_eq!(result, 4);
    }

    #[test]
    fn larger_can_hold_smaller() {
        let larger = Rectangle { width: 8, height: 7 };
        let smaller = Rectangle { width: 5, height: 1 };
        assert!(larger.can_hold(&smaller));
    }

    #[test]
    #[should_panic(expected = "Guess value must be less than or equal to 100")]
    fn greater_than_100() {
        Guess::new(200);
    }

    #[test]
    #[ignore]  // 默认跳过此测试
    fn expensive_test() {
        // 耗时测试
    }
}

pub struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    pub fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}

pub struct Guess {
    value: i32,
}

impl Guess {
    pub fn new(value: i32) -> Guess {
        if value < 1 || value > 100 {
            panic!("Guess value must be between 1 and 100, got {}.", value);
        }
        Guess { value }
    }
}
```

### 10.2. 文档注释与文档测试

```rust
/// 将两个数相加
///
/// # Examples
///
/// ```
/// let result = my_crate::add(2, 3);
/// assert_eq!(result, 5);
/// ```
///
/// # Panics
///
/// 此函数不会 panic。
///
/// # Errors
///
/// 此函数不会返回错误。
pub fn add(a: i32, b: i32) -> i32 {
    a + b
}

// 运行 cargo doc --open 生成并查看文档
// 运行 cargo test 也会运行文档测试
```

## 11. 函数式语言特性：迭代器与闭包

### 11.1. 闭包

```rust
use std::thread;
use std::time::Duration;

fn main() {
    // 定义闭包
    let expensive_closure = |num: u32| -> u32 {
        println!("calculating slowly...");
        thread::sleep(Duration::from_secs(2));
        num
    };

    // 闭包的类型推断
    let example_closure = |x| x;
    let s = example_closure(String::from("hello"));
    // let n = example_closure(5);  // 错误：闭包的类型已经确定为 String

    // 捕获环境
    let x = 4;
    let equal_to_x = |z| z == x;  // 闭包捕获了 x
    println!("can capture x: {}", equal_to_x(4));

    // 闭包的三种 Fn Trait
    // FnOnce: 获取所有权，只能调用一次
    // FnMut: 可变借用，可多次调用
    // Fn: 不可变借用，可多次调用
}

// 使用闭包优化代码
struct Cacher<T>
where
    T: Fn(u32) -> u32,
{
    calculation: T,
    value: Option<u32>,
}

impl<T> Cacher<T>
where
    T: Fn(u32) -> u32,
{
    fn new(calculation: T) -> Cacher<T> {
        Cacher {
            calculation,
            value: None,
        }
    }

    fn value(&mut self, arg: u32) -> u32 {
        match self.value {
            Some(v) => v,
            None => {
                let v = (self.calculation)(arg);
                self.value = Some(v);
                v
            }
        }
    }
}
```

### 11.2. 迭代器

```rust
fn main() {
    let v1 = vec![1, 2, 3];
    let v1_iter = v1.iter();

    // 使用迭代器
    for val in v1_iter {
        println!("Got: {}", val);
    }

    // 迭代器适配器（惰性求值）
    let v1: Vec<i32> = vec![1, 2, 3];
    let v2: Vec<_> = v1.iter().map(|x| x + 1).collect();
    assert_eq!(v2, vec![2, 3, 4]);

    // 消费适配器
    let total: i32 = v1.iter().sum();
    assert_eq!(total, 6);

    // 创建自定义迭代器
    struct Counter {
        count: u32,
    }

    impl Counter {
        fn new() -> Counter {
            Counter { count: 0 }
        }
    }

    impl Iterator for Counter {
        type Item = u32;

        fn next(&mut self) -> Option<Self::Item> {
            if self.count < 5 {
                self.count += 1;
                Some(self.count)
            } else {
                None
            }
        }
    }

    let mut counter = Counter::new();
    assert_eq!(counter.next(), Some(1));
    assert_eq!(counter.next(), Some(2));

    // 组合迭代器方法
    let sum: u32 = Counter::new()
        .zip(Counter::new().skip(1))
        .map(|(a, b)| a * b)
        .filter(|x| x % 3 == 0)
        .sum();
    assert_eq!(sum, 18);
}
```

## 12. 智能指针

智能指针是一类数据结构，它们表现类似于指针，但拥有额外的元数据和功能。

### 12.1. Box<T>：堆上分配

```rust
fn main() {
    // 在堆上分配一个 i32
    let b = Box::new(5);
    println!("b = {}", b);

    // 用于创建递归类型
    enum List {
        Cons(i32, Box<List>),
        Nil,
    }

    use List::{Cons, Nil};
    let list = Cons(1, Box::new(Cons(2, Box::new(Cons(3, Box::new(Nil))))));
}
```

### 12.2. Rc<T>：引用计数

```rust
use std::rc::Rc;

enum List {
    Cons(i32, Rc<List>),
    Nil,
}

use List::{Cons, Nil};

fn main() {
    let a = Rc::new(Cons(5, Rc::new(Cons(10, Rc::new(Nil)))));
    println!("count after creating a = {}", Rc::strong_count(&a));  // 1

    let b = Cons(3, Rc::clone(&a));
    println!("count after creating b = {}", Rc::strong_count(&a));  // 2

    {
        let c = Cons(4, Rc::clone(&a));
        println!("count after creating c = {}", Rc::strong_count(&a));  // 3
    }
    println!("count after c goes out of scope = {}", Rc::strong_count(&a));  // 2
}
```

### 12.3. RefCell<T>：内部可变性

```rust
// 内部可变性：允许在拥有不可变引用时修改数据

pub trait Messenger {
    fn send(&self, msg: &str);
}

pub struct LimitTracker<'a, T: Messenger> {
    messenger: &'a T,
    value: usize,
    max: usize,
}

impl<'a, T> LimitTracker<'a, T>
where
    T: Messenger,
{
    pub fn new(messenger: &'a T, max: usize) -> LimitTracker<'a, T> {
        LimitTracker {
            messenger,
            value: 0,
            max,
        }
    }

    pub fn set_value(&mut self, value: usize) {
        self.value = value;

        let percentage_of_max = self.value as f64 / self.max as f64;

        if percentage_of_max >= 1.0 {
            self.messenger.send("Error: You are over your quota!");
        } else if percentage_of_max >= 0.9 {
            self.messenger.send("Urgent warning: You've used up over 90% of your quota!");
        } else if percentage_of_max >= 0.75 {
            self.messenger.send("Warning: You've used up over 75% of your quota!");
        }
    }
}

#[cfg(test)]
mod tests {
    use super::*;
    use std::cell::RefCell;

    struct MockMessenger {
        sent_messages: RefCell<Vec<String>>,
    }

    impl MockMessenger {
        fn new() -> MockMessenger {
            MockMessenger {
                sent_messages: RefCell::new(vec![]),
            }
        }
    }

    impl Messenger for MockMessenger {
        fn send(&self, message: &str) {
            self.sent_messages.borrow_mut().push(String::from(message));
        }
    }

    #[test]
    fn it_sends_an_over_75_percent_warning_message() {
        let mock_messenger = MockMessenger::new();
        let mut limit_tracker = LimitTracker::new(&mock_messenger, 100);
        limit_tracker.set_value(80);

        assert_eq!(mock_messenger.sent_messages.borrow().len(), 1);
    }
}
```

### 12.4. 循环引用与 Weak<T>

```rust
use std::cell::RefCell;
use std::rc::{Rc, Weak};

#[derive(Debug)]
struct Node {
    value: i32,
    parent: RefCell<Weak<Node>>,
    children: RefCell<Vec<Rc<Node>>>,
}

fn main() {
    let leaf = Rc::new(Node {
        value: 3,
        parent: RefCell::new(Weak::new()),
        children: RefCell::new(vec![]),
    });

    println!("leaf parent = {:?}", leaf.parent.borrow().upgrade());
    println!("leaf strong = {}, weak = {}", Rc::strong_count(&leaf), Rc::weak_count(&leaf));

    {
        let branch = Rc::new(Node {
            value: 5,
            parent: RefCell::new(Weak::new()),
            children: RefCell::new(vec![Rc::clone(&leaf)]),
        });

        *leaf.parent.borrow_mut() = Rc::downgrade(&branch);

        println!("branch strong = {}, weak = {}", Rc::strong_count(&branch), Rc::weak_count(&branch));
        println!("leaf strong = {}, weak = {}", Rc::strong_count(&leaf), Rc::weak_count(&leaf));
    }

    println!("leaf parent = {:?}", leaf.parent.borrow().upgrade());
    println!("leaf strong = {}, weak = {}", Rc::strong_count(&leaf), Rc::weak_count(&leaf));
}
```

## 13. 无畏并发

### 13.1. 线程基础

```rust
use std::thread;
use std::time::Duration;

fn main() {
    // 创建新线程
    let handle = thread::spawn(|| {
        for i in 1..10 {
            println!("hi number {} from the spawned thread!", i);
            thread::sleep(Duration::from_millis(1));
        }
    });

    // 主线程继续执行
    for i in 1..5 {
        println!("hi number {} from the main thread!", i);
        thread::sleep(Duration::from_millis(1));
    }

    // 等待子线程完成
    handle.join().unwrap();

    // 使用 move 闭包转移所有权
    let v = vec![1, 2, 3];
    let handle = thread::spawn(move || {
        println!("Here's a vector: {:?}", v);
    });
    handle.join().unwrap();
}
```

### 13.2. 消息传递并发

```rust
use std::sync::mpsc;
use std::thread;
use std::time::Duration;

fn main() {
    // 创建通道
    let (tx, rx) = mpsc::channel();

    // 多个发送者
    let tx1 = tx.clone();
    thread::spawn(move || {
        let vals = vec![
            String::from("hi"),
            String::from("from"),
            String::from("the"),
            String::from("thread"),
        ];

        for val in vals {
            tx1.send(val).unwrap();
            thread::sleep(Duration::from_secs(1));
        }
    });

    thread::spawn(move || {
        let vals = vec![
            String::from("more"),
            String::from("messages"),
            String::from("for"),
            String::from("you"),
        ];

        for val in vals {
            tx.send(val).unwrap();
            thread::sleep(Duration::from_secs(1));
        }
    });

    // 接收消息
    for received in rx {
        println!("Got: {}", received);
    }
}
```

### 13.3. 共享状态并发

```rust
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    // Mutex：互斥锁
    let m = Mutex::new(5);
    {
        let mut num = m.lock().unwrap();
        *num = 6;
    }
    println!("m = {:?}", m);

    // Arc：原子引用计数（多线程安全的 Rc）
    let counter = Arc::new(Mutex::new(0));
    let mut handles = vec![];

    for _ in 0..10 {
        let counter = Arc::clone(&counter);
        let handle = thread::spawn(move || {
            let mut num = counter.lock().unwrap();
            *num += 1;
        });
        handles.push(handle);
    }

    for handle in handles {
        handle.join().unwrap();
    }

    println!("Result: {}", *counter.lock().unwrap());
}
```

### 13.4. Send 与 Sync Trait

-   **Send**：允许类型在线程间转移所有权。几乎所有 Rust 类型都是 `Send` 的，但 `Rc<T>` 不是。
-   **Sync**：允许多个线程同时访问。`Mutex<T>` 是 `Sync` 的，但 `RefCell<T>` 不是。

> **专家提示**：Rust 的并发模型基于所有权系统和借用检查器，能在编译期防止数据竞争。这是 Rust 相对于其他语言的最大优势之一。你不需要依赖复杂的锁机制或原子操作来避免数据竞争——编译器会替你检查。

## 14. 面向对象编程特性

### 14.1. Trait 对象

```rust
pub trait Draw {
    fn draw(&self);
}

pub struct Screen {
    pub components: Vec<Box<dyn Draw>>,
}

impl Screen {
    pub fn run(&self) {
        for component in self.components.iter() {
            component.draw();
        }
    }
}

pub struct Button {
    pub width: u32,
    pub height: u32,
    pub label: String,
}

impl Draw for Button {
    fn draw(&self) {
        // 实际绘制按钮的代码
    }
}

pub struct SelectBox {
    pub width: u32,
    pub height: u32,
    pub options: Vec<String>,
}

impl Draw for SelectBox {
    fn draw(&self) {
        // 实际绘制选择框的代码
    }
}

fn main() {
    let screen = Screen {
        components: vec![
            Box::new(SelectBox {
                width: 75,
                height: 10,
                options: vec![
                    String::from("Yes"),
                    String::from("Maybe"),
                    String::from("No"),
                ],
            }),
            Box::new(Button {
                width: 50,
                height: 10,
                label: String::from("OK"),
            }),
        ],
    };

    screen.run();
}
```

### 14.2. 面向对象设计模式的实现

```rust
// 状态模式
pub struct Post {
    state: Option<Box<dyn State>>,
    content: String,
}

impl Post {
    pub fn new() -> Post {
        Post {
            state: Some(Box::new(Draft {})),
            content: String::new(),
        }
    }

    pub fn add_text(&mut self, text: &str) {
        self.content.push_str(text);
    }

    pub fn content(&self) -> &str {
        self.state.as_ref().unwrap().content(self)
    }

    pub fn request_review(&mut self) {
        if let Some(s) = self.state.take() {
            self.state = Some(s.request_review())
        }
    }

    pub fn approve(&mut self) {
        if let Some(s) = self.state.take() {
            self.state = Some(s.approve())
        }
    }
}

trait State {
    fn request_review(self: Box<Self>) -> Box<dyn State>;
    fn approve(self: Box<Self>) -> Box<dyn State>;
    fn content<'a>(&self, post: &'a Post) -> &'a str {
        ""
    }
}

struct Draft {}

impl State for Draft {
    fn request_review(self: Box<Self>) -> Box<dyn State> {
        Box::new(PendingReview {})
    }

    fn approve(self: Box<Self>) -> Box<dyn State> {
        self
    }
}

struct PendingReview {}

impl State for PendingReview {
    fn request_review(self: Box<Self>) -> Box<dyn State> {
        self
    }

    fn approve(self: Box<Self>) -> Box<dyn State> {
        Box::new(Published {})
    }
}

struct Published {}

impl State for Published {
    fn request_review(self: Box<Self>) -> Box<dyn State> {
        self
    }

    fn approve(self: Box<Self>) -> Box<dyn State> {
        self
    }

    fn content<'a>(&self, post: &'a Post) -> &'a str {
        &post.content
    }
}
```

## 15. 模式与匹配进阶

### 15.1. 模式的所有使用场景

```rust
fn main() {
    // match 分支
    let x = Some(5);
    match x {
        Some(50) => println!("Got 50"),
        Some(y) => println!("Matched, y = {:?}", y),
        _ => println!("Default case, x = {:?}", x),
    }

    // if let
    let favorite_color: Option<&str> = None;
    let is_tuesday = false;
    let age: Result<u8, _> = "34".parse();

    if let Some(color) = favorite_color {
        println!("Using your favorite color, {}, as the background", color);
    } else if is_tuesday {
        println!("Tuesday is green day!");
    } else if let Ok(age) = age {
        if age > 30 {
            println!("Using purple as the background color");
        } else {
            println!("Using orange as the background color");
        }
    } else {
        println!("Using blue as the background color");
    }

    // while let
    let mut stack = Vec::new();
    stack.push(1);
    stack.push(2);
    stack.push(3);

    while let Some(top) = stack.pop() {
        println!("{}", top);
    }

    // for 循环
    let v = vec!['a', 'b', 'c'];
    for (index, value) in v.iter().enumerate() {
        println!("{} is at index {}", value, index);
    }

    // let 语句
    let (x, y, z) = (1, 2, 3);
    println!("x = {}, y = {}, z = {}", x, y, z);

    // 函数参数
    fn print_coordinates(&(x, y): &(i32, i32)) {
        println!("Current location: ({}, {})", x, y);
    }
    print_coordinates(&(3, 5));
}
```

### 15.2. 可反驳性与不可反驳性

-   **不可反驳模式**：能匹配任何可能值的模式（如 `let x = 5;` 中的 `x`）。
-   **可反驳模式**：可能无法匹配某些值的模式（如 `if let Some(x) = a_value`）。

## 16. 高级特征

### 16.1. Unsafe Rust

```rust
// 使用 unsafe 关键字进入不安全代码块
unsafe fn dangerous() {}

fn main() {
    // 1. 解引用裸指针
    let mut num = 5;
    let r1 = &num as *const i32;
    let r2 = &mut num as *mut i32;

    unsafe {
        println!("r1 is: {}", *r1);
        println!("r2 is: {}", *r2);
        dangerous();
    }

    // 2. 调用不安全函数或方法
    // 3. 访问或修改可变静态变量
    // 4. 实现不安全 trait
    // 5. 访问 union 的字段
}
```

### 16.2. 高级 Trait

```rust
// 关联类型
pub trait Iterator {
    type Item;
    fn next(&mut self) -> Option<Self::Item>;
}

// 默认泛型类型参数
trait Add<RHS=Self> {
    type Output;
    fn add(self, rhs: RHS) -> Self::Output;
}

// 完全限定语法
trait Pilot {
    fn fly(&self);
}

trait Wizard {
    fn fly(&self);
}

struct Human;

impl Pilot for Human {
    fn fly(&self) {
        println!("This is your captain speaking.");
    }
}

impl Wizard for Human {
    fn fly(&self) {
        println!("Up!");
    }
}

impl Human {
    fn fly(&self) {
        println!("*waving arms furiously*");
    }
}

fn main() {
    let person = Human;
    person.fly();  // 调用 Human 的方法
    Pilot::fly(&person);  // 调用 Pilot trait 的方法
    Wizard::fly(&person);  // 调用 Wizard trait 的方法
}

// 父 trait
trait OutlinePrint: fmt::Display {
    fn outline_print(&self) {
        let output = self.to_string();
        let len = output.len();
        println!("{}", "*".repeat(len + 4));
        println!("*{}*", " ".repeat(len + 2));
        println!("* {} *", output);
        println!("*{}*", " ".repeat(len + 2));
        println!("{}", "*".repeat(len + 4));
    }
}

// newtype 模式
struct Wrapper(Vec<String>);

impl fmt::Display for Wrapper {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "[{}]", self.0.join(", "))
    }
}
```

### 16.3. 高级类型

```rust
// 类型别名
type Kilometers = i32;
type Thunk = Box<dyn Fn() + Send + 'static>;

// 从不返回的 never 类型 !
fn bar() -> ! {
    panic!("This function never returns!");
}

// 动态大小类型（DST）
// str 是 DST，&str 是胖指针（包含地址和长度）
// dyn Trait 是 DST，Box<dyn Trait> 是胖指针

// 函数指针
fn add_one(x: i32) -> i32 {
    x + 1
}

fn do_twice(f: fn(i32) -> i32, arg: i32) -> i32 {
    f(arg) + f(arg)
}

fn main() {
    let answer = do_twice(add_one, 5);
    println!("The answer is: {}", answer);
}
```

### 16.4. 高级函数与闭包

```rust
// 返回闭包
fn returns_closure() -> Box<dyn Fn(i32) -> i32> {
    Box::new(|x| x + 1)
}

// 宏定义
macro_rules! vec {
    ( $( $x:expr ),* ) => {
        {
            let mut temp_vec = Vec::new();
            $(
                temp_vec.push($x);
            )*
            temp_vec
        }
    };
}
```

## 17. 异步编程：async/await 与 Tokio

Rust 的异步编程模型建立在零成本抽象和内存安全的基石之上。`async` 和 `await` 关键字让编写异步代码几乎和同步代码一样简单。

### 17.1. 异步编程模型

```rust
// async fn 返回一个 Future
async fn say_hello() -> String {
    "Hello from async!".to_string()
}

// Future 需要通过 .await 来驱动执行
// .await 会暂停当前任务，等待 Future 完成，然后恢复执行
```

### 17.2. Tokio 运行时

Tokio 是 Rust 生态中最广泛使用的异步运行时。

```rust
use tokio::time::{sleep, Duration};

#[tokio::main]  // 启动 Tokio 运行时
async fn main() {
    // 顺序执行
    let msg = say_hello().await;
    println!("{msg}");

    // 并发执行多个任务
    let task1 = tokio::spawn(async {
        sleep(Duration::from_secs(2)).await;
        "Task 1 done"
    });

    let task2 = tokio::spawn(async {
        sleep(Duration::from_secs(1)).await;
        "Task 2 done"
    });

    let (result1, result2) = tokio::join!(task1, task2);
    println!("{}, {}", result1.unwrap(), result2.unwrap());
}

async fn say_hello() -> String {
    "Hello from async!".to_string()
}
```

### 17.3. 实战：构建异步 Web 服务

使用 **Axum** 构建一个简单的 REST API：

```rust
use axum::{
    routing::get,
    Json, Router,
};
use serde::Serialize;
use tokio::net::TcpListener;

#[derive(Serialize)]
struct SystemStatus {
    uptime: u64,
    service: String,
}

async fn status_handler() -> Json<SystemStatus> {
    Json(SystemStatus {
        uptime: 3600,
        service: "payment-gateway".to_string(),
    })
}

#[tokio::main]
async fn main() {
    let app = Router::new()
        .route("/api/status", get(status_handler));

    let listener = TcpListener::bind("0.0.0.0:3000").await.unwrap();
    println!("Server running on port 3000");
    axum::serve(listener, app).await.unwrap();
}
```

> **专家提示**：异步编程在 Rust 中仍在快速发展。Rust 2024 Edition 已经稳定了异步闭包（async closures），并且 Rust 团队正在推动 async trait 的原生支持。这些改进将极大地简化异步 Rust 的开发体验。

## 18. 宏与元编程

宏是 Rust 中一种强大的元编程工具，允许你编写生成代码的代码。

### 18.1. 声明宏

```rust
// 使用 macro_rules! 定义声明宏
macro_rules! my_vec {
    // 匹配空 vector
    () => {
        Vec::new()
    };
    // 匹配一个或多个表达式
    ( $( $x:expr ),+ $(,)? ) => {
        {
            let mut temp_vec = Vec::new();
            $(
                temp_vec.push($x);
            )+
            temp_vec
        }
    };
}

// 更复杂的宏：模拟 vec! 宏
macro_rules! vec {
    ( $( $x:expr ),* ) => {
        {
            let mut temp_vec = Vec::new();
            $(
                temp_vec.push($x);
            )*
            temp_vec
        }
    };
}

fn main() {
    let v1: Vec<i32> = my_vec!();
    let v2 = my_vec![1, 2, 3];
    let v3 = my_vec![1, 2, 3,];
    println!("{:?}, {:?}, {:?}", v1, v2, v3);
}
```

### 18.2. 过程宏

过程宏更为强大，分为三类：

1.  **自定义派生宏**（如 `#[derive(Debug)]`）
2.  **属性宏**（如 `#[tokio::main]`）
3.  **函数宏**（如 `sqlx::query!`）

```rust
// 过程宏需要在单独的 crate 中定义，类型为 proc-macro
// 以下是一个简单的派生宏示例（需要在 proc-macro crate 中）

// use proc_macro::TokenStream;
// use quote::quote;
// use syn::{parse_macro_input, DeriveInput};
// 
// #[proc_macro_derive(HelloMacro)]
// pub fn hello_macro_derive(input: TokenStream) -> TokenStream {
//     let ast = parse_macro_input!(input as DeriveInput);
//     let name = &ast.ident;
//     let gen = quote! {
//         impl HelloMacro for #name {
//             fn hello_macro() {
//                 println!("Hello, Macro! My name is {}!", stringify!(#name));
//             }
//         }
//     };
//     gen.into()
// }
```

## 19. 项目实战：构建一个命令行工具

### 19.1. 项目概述：minigrep

我们将构建一个简化版的 `grep` 工具，它接受一个搜索字符串和一个文件路径，然后输出包含该字符串的所有行。

### 19.2. 分步实现

```rust
use std::env;
use std::fs;
use std::process;
use std::error::Error;

fn main() {
    let args: Vec<String> = env::args().collect();

    let config = Config::new(&args).unwrap_or_else(|err| {
        eprintln!("Problem parsing arguments: {}", err);
        process::exit(1);
    });

    println!("Searching for {}", config.query);
    println!("In file {}", config.filename);

    if let Err(e) = run(config) {
        eprintln!("Application error: {}", e);
        process::exit(1);
    }
}

struct Config {
    query: String,
    filename: String,
    case_sensitive: bool,
}

impl Config {
    fn new(args: &[String]) -> Result<Config, &'static str> {
        if args.len() < 3 {
            return Err("not enough arguments");
        }

        let query = args[1].clone();
        let filename = args[2].clone();

        // 检查环境变量控制是否区分大小写
        let case_sensitive = env::var("CASE_INSENSITIVE").is_err();

        Ok(Config {
            query,
            filename,
            case_sensitive,
        })
    }
}

fn run(config: Config) -> Result<(), Box<dyn Error>> {
    let contents = fs::read_to_string(config.filename)?;

    let results = if config.case_sensitive {
        search(&config.query, &contents)
    } else {
        search_case_insensitive(&config.query, &contents)
    };

    for line in results {
        println!("{}", line);
    }

    Ok(())
}

fn search<'a>(query: &str, contents: &'a str) -> Vec<&'a str> {
    contents
        .lines()
        .filter(|line| line.contains(query))
        .collect()
}

fn search_case_insensitive<'a>(query: &str, contents: &'a str) -> Vec<&'a str> {
    let query = query.to_lowercase();
    contents
        .lines()
        .filter(|line| line.to_lowercase().contains(&query))
        .collect()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn case_sensitive() {
        let query = "duct";
        let contents = "\
Rust:
safe, fast, productive.
Pick three.
Duct tape.";

        assert_eq!(vec!["safe, fast, productive."], search(query, contents));
    }

    #[test]
    fn case_insensitive() {
        let query = "rUsT";
        let contents = "\
Rust:
safe, fast, productive.
Pick three.
Trust me.";

        assert_eq!(
            vec!["Rust:", "Trust me."],
            search_case_insensitive(query, contents)
        );
    }
}
```

## 20. Rust 常用第三方库与生态

### 20.1. Web 开发

| 库 | 描述 | 特点 |
| :--- | :--- | :--- |
| **Axum** | 基于 Tokio/Hyper 的 Web 框架 | 类型安全、中间件生态完善 |
| **Actix-web** | 高性能 Actor 模型 Web 框架 | 久经考验，性能极高 |
| **Warp** | 基于 Filter 的轻量框架 | 组合性强 |
| **Hyper** | 底层 HTTP 实现 | Axum、Tonic 等框架的基石 |
| **Reqwest** | 高级 HTTP 客户端 | 简单易用，支持异步 |

### 20.2. 数据库与 ORM

| 库 | 描述 | 特点 |
| :--- | :--- | :--- |
| **SQLx** | 编译期 SQL 校验 | 异步支持，强类型查询 |
| **Diesel** | 类型安全 ORM | 传统 SQL 工程化，迁移工具完善 |
| **SeaORM** | 异步 ORM | 全功能，适合复杂业务 |

### 20.3. 序列化与反序列化

| 库 | 描述 | 特点 |
| :--- | :--- | :--- |
| **Serde** | 通用序列化框架 | Rust 序列化的标准 |
| **serde_json** | JSON 支持 | 配合 Serde 使用 |

### 20.4. 命令行工具

| 库 | 描述 | 特点 |
| :--- | :--- | :--- |
| **clap** | 命令行参数解析 | 功能全面，支持子命令和自动补全 |
| **anyhow** | 应用级错误处理 | 简化错误传播 |
| **thiserror** | 库级错误定义 | 定义清晰的错误类型 |
| **tracing** | 结构化日志与追踪 | 分布式追踪支持 |

### 20.5. 并发与异步

| 库 | 描述 | 特点 |
| :--- | :--- | :--- |
| **Tokio** | 异步运行时 | 生态最完善 |
| **Crossbeam** | 并发编程工具集 | 无锁数据结构、工作窃取队列 |
| **Rayon** | 数据并行 | 并行迭代器，自动负载均衡 |

### 20.6. 其他精选库

| 库 | 描述 |
| :--- | :--- |
| **regex** | 正则表达式 |
| **rand** | 随机数生成 |
| **chrono** | 日期时间处理 |
| **log** | 日志门面 |
| **env_logger** | 环境变量控制的日志实现 |

## 21. 最佳实践与常见陷阱

### 21.1. 所有权与借用常见错误

| 错误 | 描述 | 解决方案 |
| :--- | :--- | :--- |
| **cannot move out of borrowed content** | 试图从借用中移动值 | 使用 `clone()` 或重新设计 |
| **cannot borrow `x` as mutable more than once** | 同时存在多个可变引用 | 缩小作用域或使用内部可变性 |
| **value used here after move** | 使用已移动的值 | 使用引用或 `clone()` |

### 21.2. 代码组织最佳实践

1.  将相关的功能组织到同一个模块中。
2.  使用 `pub use` 重导出，提供简洁的公共 API。
3.  将大型 crate 拆分为多个子 crate，使用 Cargo workspace 管理。
4.  遵循 Rust API Guidelines（https://rust-lang.github.io/api-guidelines/）。

### 21.3. 错误处理最佳实践

1.  库代码：使用 `thiserror` 定义自定义错误类型。
2.  应用代码：使用 `anyhow` 简化错误传播。
3.  不要滥用 `unwrap()` 和 `expect()`，在生产代码中优先使用 `?` 和 `match`。
4.  为自定义错误类型实现 `std::error::Error` trait。

### 21.4. 性能优化提示

1.  使用 `cargo build --release` 编译生产代码。
2.  使用迭代器而非手动循环（零成本抽象）。
3.  避免不必要的 `clone()`。
4.  使用 `cargo flamegraph` 进行性能剖析。
5.  理解 `Vec` 的容量管理，使用 `with_capacity()` 预分配。

> **专家提示**：Rust 的学习曲线前期陡峭，但一旦你理解了所有权和借用规则，编译器就会成为你最可靠的伙伴，而不是敌人。编译器的错误信息通常非常详尽，仔细阅读它们能帮助你理解问题所在。

## 22. 总结：您的下一步学习路线图

这份指南为你绘制了一张从 Rust 基础到高级特性的完整蓝图。学习 Rust 是一个循序渐进的过程，建议按以下路线推进：

1.  **第 1-2 周：基础语法与所有权**
    -   安装 Rust 和 Cargo
    -   学习变量、数据类型、函数、控制流
    -   深入理解所有权、借用、生命周期

2.  **第 3-4 周：结构体、枚举与错误处理**
    -   掌握结构体、枚举、模式匹配
    -   理解 `Option` 和 `Result` 的使用
    -   学习模块系统和包管理

3.  **第 5-6 周：集合与泛型**
    -   熟练使用 `Vec`、`String`、`HashMap`
    -   理解泛型和 Trait
    -   学习迭代器和闭包

4.  **第 7-8 周：智能指针与并发**
    -   掌握 `Box`、`Rc`、`RefCell`
    -   学习线程、消息传递、共享状态
    -   理解 `Send` 和 `Sync`

5.  **第 9-10 周：异步编程与进阶特性**
    -   学习 `async`/`await` 和 Tokio
    -   构建异步 Web 服务
    -   了解宏和 Unsafe Rust

6.  **持续实践**
    -   阅读优秀的开源项目（如 ripgrep、tokio、bevy）
    -   参与 Rust 社区讨论
    -   将自己感兴趣的项目用 Rust 重写

**推荐学习资源：**

-   **《Rust 程序设计语言》**（The Book）：Rust 官方教程，必读
-   **《通过例子学 Rust》**（Rust by Example）：通过实例学习
-   **Rustlings**：交互式练习，巩固基础
-   **《Rust 语言圣经》**：中文社区精品教程，覆盖全面
-   **《Rust 秘典》**：Unsafe Rust 深入指南
-   **docs.rs**：查询任何 crate 的文档
