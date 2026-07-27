# 🚀 Learning C++

<p align="center">
  <img src="https://img.shields.io/badge/C++-20-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white" alt="C++20"/>
  <img src="https://img.shields.io/github/actions/workflow/status/Stelquis/Learning-Cpp/.github/workflows/build.yml?branch=main&style=for-the-badge&label=CI&logo=github" alt="CI Status"/>
  <img src="https://img.shields.io/badge/34%2F34-tests%20passed-2ea44f?style=for-the-badge&logo=checkmarx&logoColor=white" alt="34/34 Tests Passed"/>
  <img src="https://img.shields.io/github/license/Stelquis/Learning-Cpp?style=for-the-badge&color=blue" alt="License"/>
</p>

> 🧠 **从零到通神，34 个练习一步步吃透 C++20。**
>
> 📖 配套学习指南：[C++ Road to Mastery](./docs/Cpp-Road-to-Mastery.md)

---

## ✨ 这是什么？

一个**手把手带你学 C++20** 的练习项目。34 个练习从 `Hello World` 一路走到智能指针、模板、Ranges，覆盖 C++ 最核心的知识体系。

> 🌱 本项目基于 [InfiniTensor/learning-cxx](https://github.com/InfiniTensor/learning-cxx) 源仓库进行更新迭代，已升级至 **C++20** 标准并完成全部练习测试。详情见[版本差异](#-与源仓库的差异)。

```
00 🟢 Hello World              → 17 🟡 继承
01 🟢 变量与运算符              → 18 🟡 虚函数
02 🟢 函数                     → 19 🟡 虚析构
03 🟢 传参                     → 20 🟠 函数模板
04 🟢 static 关键字            → 21 🟠 运行时类型
05 🟢 constexpr                → 22 🟠 类模板
06 🟡 数组                     → 23 🟠 模板参数
07 🟡 循环                     → 24 🔵 std::array
08 🟡 指针                     → 25 🔵 std::vector
09 🟡 枚举 & 联合体             → 26 🔵 std::vector\<bool\>
10 🟡 结构体                   → 27 🔵 strides 步长
11 🟡 成员方法                  → 28 🔵 std::string
12 🟡 const 方法               → 29 🔵 std::map
13 🟡 类 & 构造函数             → 30 🔵 std::unique_ptr
14 🟡 析构 & RAII              → 31 🔵 std::shared_ptr
15 🟡 深拷贝                   → 32 🔵 std::transform
16 🟡 移动语义                  → 33 🔵 std::accumulate
```

> 🟢 基础 · 🟡 核心 · 🟠 进阶 · 🔵 标准库

---

## 🛠️ 快速开始

### 1️⃣ 安装 xmake

```shell
# macOS / Linux
curl -fsSL https://xmake.io/sh | bash

# Windows（PowerShell）
Invoke-Expression (Invoke-WebRequest 'https://xmake.io/ps' -UseBasicParsing).Content
```

> 📎 xmake 是跨平台的 C/C++ 构建系统，安装方便，配置简洁。  
> ⚠️ 还需要安装编译器：GCC / Clang / MSVC（Visual Studio）。

### 2️⃣ 克隆并编译

```shell
git clone https://github.com/Stelquis/Learning-Cpp.git
cd Learning-Cpp
xmake          # 编译学习系统
```

### 3️⃣ 开始练习 🎯

```shell
# 运行第 0 题：Hello World
xmake run learn 0

# 运行第 5 题：constexpr
xmake run learn 5

# 查看全部练习的通过情况
xmake run summary
```

---

## 📂 项目结构

```
Learning-Cpp/
├── 📄 xmake.lua                 ← 根构建配置
├── 📄 .clang-format             ← 代码格式化规则
├── 📄 .github/workflows/build.yml ← CI 自动化
│
├── 📁 exercises/                ← 🎯 34 个练习（核心！）
│   ├── 00_hello_world/main.cpp
│   ├── 01_variable_add/main.cpp
│   ├── ...
│   ├── 33_std_accumulate/main.cpp
│   ├── 📄 exercise.h            ← ASSERT 宏定义
│   └── 📄 xmake.lua             ← 练习构建配置
│
├── 📁 learn/                    ← 🧪 测试系统
│   ├── learn.cpp                ← 运行单个练习
│   ├── summary.cpp              ← 汇总所有练习
│   ├── test.cpp
│   └── test.h
│
└── 📁 docs/                     ← 📚 文档
    ├── Cpp-Road-to-Mastery.md   ← C++20 通神之路
    └── git-unsafe-repository.md ← Git 安全目录问题记录
```

---

## 🎓 学习路径

```
第一关 🧱 基石
├── 输出、变量、函数
├── 传参、static、constexpr
└── 写代码的基本功

第二关 🧠 内存与指针
├── 数组、指针、循环
├── 枚举、联合体、结构体
└── 手动内存管理

第三关 🏗️ 面向对象
├── 方法、构造、析构
├── 复制、移动
└── 继承、虚函数、多态

第四关 🔩 模板
├── 函数模板、类模板
├── 非类型模板参数
└── Concepts（C++20）

第五关 📦 标准库
├── array、vector、string
├── map、unique_ptr、shared_ptr
└── transform、accumulate

第六关 🚀 C++20 前沿
├── Ranges、format、<=>
├── Modules、Coroutines
└── 更多新特性 👉 docs/Cpp-Road-to-Mastery.md
```

---

## 🧪 验证全部练习

```shell
xmake run summary
```

期望输出：**`34/34`** ✅

---

## 📚 推荐学习资源

| 资源 | 说明 |
|:---|:---|
| 📖 [C++ 参考手册（中文）](https://zh.cppreference.com/w/cpp) | 查语法、查 STL 的最佳去处 |
| 📖 [Microsoft：欢迎回到 C++](https://learn.microsoft.com/zh-cn/cpp/cpp/welcome-back-to-cpp-modern-cpp?view=msvc-170) | 微软官方现代 C++ 教程 |
| 📖 [C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines) | C++ 之父参与编写的编码规范 |
| 📖 [C++ Road to Mastery](./docs/Cpp-Road-to-Mastery.md) | 本项目配套学习指南 |
| 📖 [360 安全规则集合](https://github.com/Qihoo360/safe-rules) | 企业级 C++ 安全编码规范 |

---

## 🤝 参与贡献

- 🐛 发现 Bug？提 [Issue](https://github.com/Stelquis/Learning-Cpp/issues)
- 💡 有改进建议？开 [Pull Request](https://github.com/Stelquis/Learning-Cpp/pulls)
- ⭐ 觉得有用？点个 Star 让更多人看到
- 🏗️ 原始项目：[InfiniTensor/learning-cxx](https://github.com/InfiniTensor/learning-cxx)

---

## 📋 与源仓库的差异

本项目基于 [InfiniTensor/learning-cxx](https://github.com/InfiniTensor/learning-cxx) 进行了以下更新：

| 项目 | 源仓库 | 本仓库 |
|:---|:---|:---|
| C++ 标准 | C++17 | **C++20** 🚀 |
| 练习完成度 | 部分完成 | **34/34 全部完成** ✅ |
| CI | 基础配置 | 修复 CI 名称，忽略文档变更 |
| 文档 | 仅有 README | 新增《C++ Road to Mastery》学习指南 📖 |
| 练习目录 | `01_variable&add` | `01_variable_add`（去掉特殊符号） |
| Git 安全目录 | 未处理 | 已配置兼容方案

---

> 🎯 **34 个练习，34 级台阶。一步一步，走完就是通神之路。**
