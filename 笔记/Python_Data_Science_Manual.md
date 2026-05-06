

# Python 数据科学体系化学习指南

-   [1. Python 数据科学栈架构全景图](#1-python-数据科学栈架构全景图)
-   [2. Python 语言基础与核心机制](#2-python-语言基础与核心机制)
    -   [2.1. 白话概述：Python 是什么？](#21-白话概述python-是什么)
    -   [2.2. 变量与数据类型：动态语言的灵魂](#22-变量与数据类型动态语言的灵魂)
    -   [2.3. 流程控制：程序的逻辑脉络](#23-流程控制程序的逻辑脉络)
    -   [2.4. 函数：代码复用的基石](#24-函数代码复用的基石)
    -   [2.5. 数据结构：数据的容器](#25-数据结构数据的容器)
    -   [2.6. 面向对象编程 (OOP)：构建复杂系统的蓝图](#26-面向对象编程-oop构建复杂系统的蓝图)
    -   [2.7. 模块与包：代码的组织与管理](#27-模块与包代码的组织与管理)
    -   [2.8. 文件与异常处理：与外部世界的交互](#28-文件与异常处理与外部世界的交互)
-   [3. NumPy：高性能数值计算基石](#3-numpy高性能数值计算基石)
    -   [3.1. 白话概述：为什么我们需要 NumPy？](#31-白话概述为什么我们需要-numpy)
    -   [3.2. ndarray 对象：多维数组的核心](#32-ndarray-对象多维数组的核心)
    -   [3.3. 数组创建：从零到一生成数据](#33-数组创建从零到一生成数据)
    -   [3.4. 数组的索引与切片：精准定位数据](#34-数组的索引与切片精准定位数据)
    -   [3.5. 形状变换：重塑你的数据视角](#35-形状变换重塑你的数据视角)
    -   [3.6. 通用函数 (ufunc)：向量化的力量](#36-通用函数-ufunc向量化的力量)
    -   [3.7. 广播 (Broadcasting)：不同形状数组的运算艺术](#37-广播-broadcasting不同形状数组的运算艺术)
    -   [3.8. 线性代数与随机数模块](#38-线性代数与随机数模块)
-   [4. Pandas：数据分析的核心利器](#4-pandas数据分析的核心利器)
    -   [4.1. 白话概述：从 Excel 到 Pandas 的思维跃迁](#41-白话概述从-excel-到-pandas-的思维跃迁)
    -   [4.2. 核心数据结构：Series 与 DataFrame](#42-核心数据结构series-与-dataframe)
    -   [4.3. 数据导入与导出：连接各种数据源](#43-数据导入与导出连接各种数据源)
    -   [4.4. 数据查看与选择：精准提取数据子集](#44-数据查看与选择精准提取数据子集)
    -   [4.5. 数据清洗：为分析扫清障碍](#45-数据清洗为分析扫清障碍)
    -   [4.6. 数据变换：重塑数据结构](#46-数据变换重塑数据结构)
    -   [4.7. 分组与聚合：拆分-应用-合并的艺术](#47-分组与聚合拆分-应用-合并的艺术)
    -   [4.8. 连接与合并：组合多源数据](#48-连接与合并组合多源数据)
-   [5. Matplotlib：数据可视化利器](#5-matplotlib数据可视化利器)
    -   [5.1. 白话概述：用图形讲述数据故事](#51-白话概述用图形讲述数据故事)
    -   [5.2. Matplotlib 架构：两层 API 的设计哲学](#52-matplotlib-架构两层-api-的设计哲学)
    -   [5.3. Figure 与 Axes：画布与子图的层次](#53-figure-与-axes画布与子图的层次)
    -   [5.4. 常用图表绘制实战](#54-常用图表绘制实战)
    -   [5.5. 图表样式与自定义：打造专业级图表](#55-图表样式与自定义打造专业级图表)
    -   [5.6. 多子图与复杂布局](#56-多子图与复杂布局)
    -   [5.7. 与 Pandas 的无缝集成](#57-与-pandas-的无缝集成)
-   [6. 综合实战：将一切串联起来](#6-综合实战将一切串联起来)
    -   [6.1. 项目：电影数据分析报告](#61-项目电影数据分析报告)
-   [7. 扩展阅读与生态工具](#7-扩展阅读与生态工具)
    -   [7.1. 基础进阶：SciPy](#71-基础进阶scipy)
    -   [7.2. 机器学习：Scikit-learn](#72-机器学习scikit-learn)
    -   [7.3. 可视化进阶：Seaborn 与 Plotly](#73-可视化进阶seaborn-与-plotly)
-   [8. 总结：您的下一步学习路线图](#8-总结您的下一步学习路线图)

## 1. Python 数据科学栈架构全景图

在深入具体技术前，让我们先建立一个全局视图，理解 Python 数据科学生态的层次关系。

```mermaid
graph TD
    subgraph “应用层 (Application)”
        A[数据分析报告] --> B[机器学习模型]
        B --> C[商业智能仪表盘]
    end

    subgraph “高级接口层 (High-level APIs)”
        D[Seaborn, Plotly]
        E[Scikit-learn]
    end

    subgraph “核心数据处理层 (Core Data Processing)”
        F[<b>Pandas</b><br/>数据分析与处理]
        G[<b>Matplotlib</b><br/>数据可视化]
    end

    subgraph “基础计算层 (Foundational Computing)”
        H[<b>NumPy</b><br/>多维数组与数值计算]
    end

    subgraph “Python 解释器与系统层 (Interpreter & System)”
        I[Python 语言基础]
        J[C/Fortran 底层库]
    end

    D --> F
    D --> G
    E --> F
    F --> H
    G --> H
    H --> I
    H --> J
    A --> F
    B --> E
    C --> D
```

**架构解读：**

-   **底层**：NumPy 是整个科学计算栈的基石，它提供了高效的多维数组对象和底层数学函数。Pandas 和 Matplotlib 都构建在其之上。
-   **核心层**：Pandas 和 Matplotlib 是我们日常数据分析工作的核心。Pandas 负责数据的清洗、转换和分析，而 Matplotlib 负责将结果以图表形式呈现。
-   **高级接口层**：Seaborn 等库构建在 Matplotlib 之上，提供了更高级、更美观的统计图表绘制接口。Scikit-learn 则提供了大量经典的机器学习算法，其输入数据通常要求是 NumPy 数组或 Pandas 的 DataFrame。

> **专家提示**：在学习过程中，请时刻牢记这张架构图。当你在 Pandas 中操作数据时，要意识到其底层是 NumPy 的高效数组运算；当你在用 Matplotlib 绘图时，要明白传入的数据会被转换为 NumPy 数组来处理。这种“知其然，更知其所以然”的学习方式，会让你在遇到性能瓶颈或复杂问题时，能快速定位问题的根源。

## 2. Python 语言基础与核心机制

### 2.1. 白话概述：Python 是什么？

Python 是一种**解释型、动态类型的高级编程语言**，以其**简洁、易读的语法**而闻名。它强调代码的可读性，并允许你用比其他语言（如 C++/Java）少得多的代码来表达概念。

如果说 C++ 像一辆需要你手动换挡、关注引擎转速的赛车，那么 Python 就像一辆自动挡、带导航的轿车，让你能更专注于“去哪里”，而不是“怎么开车”。

### 2.2. 变量与数据类型：动态语言的灵魂

Python 是动态类型语言，你无需事先声明变量类型。解释器会在运行时自动推断。

```python
# 基本数据类型
name = "Alice"            # 字符串 (str)
age = 30                  # 整数 (int)
height = 1.75             # 浮点数 (float)
is_student = False        # 布尔值 (bool)

# 类型检查
print(type(name))         # <class 'str'>
print(type(age))          # <class 'int'>
```

> **专家提示**：动态类型带来便利的同时，也埋下了隐患。在大项目中，很容易因为类型不匹配导致运行时错误。因此，强烈建议在函数定义中使用 **Type Hints（类型注解）**，并结合 `mypy` 等工具进行静态检查。

```python
# 使用类型注解提高代码健壮性
def greet(name: str, age: int) -> str:
    return f"Hello, {name}. You are {age} years old."

# greet(30, "Alice")  # IDE会给出警告，mypy会报错
```

### 2.3. 流程控制：程序的逻辑脉络

程序的核心在于逻辑判断和循环。

```python
# if-elif-else 条件判断
score = 85
if score >= 90:
    grade = 'A'
elif score >= 80:
    grade = 'B'
elif score >= 70:
    grade = 'C'
else:
    grade = 'D'
print(f"Grade: {grade}")  # 输出: Grade: B

# for 循环 (通常用于遍历序列)
fruits = ['apple', 'banana', 'cherry']
for fruit in fruits:
    print(fruit)

# while 循环
count = 0
while count < 5:
    print(f"Count is {count}")
    count += 1
```

### 2.4. 函数：代码复用的基石

函数是组织代码的基本单元，它将一系列操作封装成一个可重复调用的逻辑块。

```python
def calculate_average(numbers: list) -> float:
    """计算并返回列表的平均值"""
    if not numbers:
        return 0.0
    return sum(numbers) / len(numbers)

scores = [90, 85, 78, 92]
avg = calculate_average(scores)
print(f"The average score is {avg:.2f}")
```

### 2.5. 数据结构：数据的容器

Python 内置了四种强大且灵活的数据结构，这是数据分析的基础。

| 数据结构 | 特性 | 可变性 | 有序性 | 示例 |
| :--- | :--- | :--- | :--- | :--- |
| **列表 (list)** | 元素有序，可重复，类型可不同 | 可变 | 有序 | `[1, 'a', 2.5]` |
| **元组 (tuple)** | 元素有序，可重复，类型可不同 | 不可变 | 有序 | `(1, 'a', 2.5)` |
| **字典 (dict)** | 键值对集合，键唯一不可变 | 可变 | 无序 (Python 3.7+ 有序) | `{'name': 'Alice', 'age': 30}` |
| **集合 (set)** | 元素唯一，不可重复 | 可变 | 无序 | `{1, 2, 3}` |

```python
# 列表推导式 (List Comprehension) - Python 的语法糖
numbers = [1, 2, 3, 4, 5]
squared_numbers = [n**2 for n in numbers]  # 结果: [1, 4, 9, 16, 25]
even_numbers = [n for n in numbers if n % 2 == 0]  # 结果: [2, 4]

# 字典
person = {'name': 'Bob', 'job': 'Engineer'}
person['city'] = 'New York'  # 添加键值对

# 集合
my_set = {1, 2, 2, 3}  # 自动去重，结果是 {1, 2, 3}
```

### 2.6. 面向对象编程 (OOP)：构建复杂系统的蓝图

面向对象编程（OOP）是一种将数据和操作数据的方法封装在一起的编程范式。类是创建对象的蓝图。

```python
class Dog:
    # 类属性
    species = "Canis familiaris"

    # 初始化方法 (构造函数)
    def __init__(self, name, age):
        # 实例属性
        self.name = name
        self.age = age

    # 实例方法
    def description(self):
        return f"{self.name} is {self.age} years old."

    def bark(self, sound):
        return f"{self.name} says {sound}."

# 创建对象 (实例化)
my_dog = Dog("Buddy", 5)
print(my_dog.description())  # 输出: Buddy is 5 years old.
print(my_dog.bark("Woof Woof")) # 输出: Buddy says Woof Woof.
```

> **专家提示**：在数据分析工作中，你更多的是**使用**别人写好的类（如 Pandas 的 `DataFrame`），而不是自己定义类。但理解 OOP 的基本概念，如类、对象、方法、属性，对于理解这些库的设计和API至关重要。例如，`df.head()` 就是在调用 `df` 这个 `DataFrame` 对象的 `head()` 方法。

### 2.7. 模块与包：代码的组织与管理

随着项目变大，你需要将代码拆分到不同的文件中。一个 `.py` 文件就是一个模块（module），一个包含 `__init__.py` 文件的文件夹就是一个包（package）。

```python
# 导入整个模块
import math
print(math.sqrt(16))  # 4.0

# 导入模块中的特定函数
from math import pi, sin
print(pi)  # 3.141592653589793

# 导入模块并起别名 (非常常用)
import numpy as np
import pandas as pd
```

### 2.8. 文件与异常处理：与外部世界的交互

程序需要与外界交互，最常见的就是读写文件。同时，程序也需要优雅地处理可能出现的错误（异常）。

```python
# 文件操作 (使用 with 语句自动管理资源)
try:
    with open('my_file.txt', 'w') as f:
        f.write("Hello, world!")
    with open('my_file.txt', 'r') as f:
        content = f.read()
        print(content)  # 输出: Hello, world!
except FileNotFoundError:
    print("Sorry, the file was not found.")
except Exception as e:
    print(f"An unexpected error occurred: {e}")
```

## 3. NumPy：高性能数值计算基石

### 3.1. 白话概述：为什么我们需要 NumPy？

Python 的列表很灵活，但效率低下。当你需要对包含数百万个数字的列表进行数学运算时，Python 原生列表的性能瓶颈会立刻显现。NumPy 的核心是 **`ndarray` (N-dimensional array)**，它是一个同质的、固定类型的多维数组。

-   **内存布局**：`ndarray` 在内存中是连续存储的，而 Python 列表存储的是指向对象的指针。这使得 `ndarray` 的内存占用更小，数据访问速度更快。
-   **向量化运算**：NumPy 允许你在整个数组上执行操作，而无需编写 `for` 循环。这些操作在底层由高度优化的 C 和 Fortran 代码执行。

下面的流程图直观地展示了 NumPy 在内存和性能上的优势：

```mermaid
graph LR
    subgraph “Python 列表 (List)”
        direction LR
        L[PyObject 1] --> P1[指向 int 1 的指针] --> D1[int 1 对象<br/>(存储值1, 引用计数等)]
        L2[PyObject 2] --> P2[指向 int 2 的指针] --> D2[int 2 对象<br/>(存储值2, 引用计数等)]
        L3[PyObject 3] --> P3[指向 int 3 的指针] --> D3[int 3 对象<br/>(存储值3, 引用计数等)]
    end

    subgraph “NumPy 数组 (ndarray)”
        direction LR
        A[ndarray 对象<br/>(头信息: dtype, shape, strides)] --> M[连续内存块<br/>int64 int64 int64<br/>1 2 3]
    end

    subgraph “操作效率对比”
        E1[Python: 循环遍历] --> R1[效率低]
        E2[NumPy: 向量化运算] --> R2[效率极高]
    end
```

### 3.2. ndarray 对象：多维数组的核心

`ndarray` 是 NumPy 的核心。它是一个同质多维容器，这意味着数组中的所有元素必须是相同的数据类型（如 `int64`, `float32`）。

```python
import numpy as np

# 关键属性
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(f"Shape (形状): {arr.shape}")      # (2, 3) - 2行3列
print(f"Dtype (数据类型): {arr.dtype}")   # int64
print(f"Size (元素个数): {arr.size}")    # 6
print(f"Ndim (维度): {arr.ndim}")        # 2
```

### 3.3. 数组创建：从零到一生成数据

创建数组的方式多种多样，以适应不同的场景。

```python
import numpy as np

# 从列表创建
a = np.array([1, 2, 3])

# 创建全零、全一数组
zeros = np.zeros((2, 3))      # 2x3 的全零数组
ones = np.ones((3, 2))        # 3x2 的全一数组

# 创建等差数列
range_arr = np.arange(0, 10, 2) # 从0到10，步长为2: [0 2 4 6 8]
lin_arr = np.linspace(0, 1, 5)  # 从0到1，等距取5个点: [0. 0.25 0.5 0.75 1.]

# 创建随机数组
rng = np.random.default_rng(seed=42)  # 推荐使用新的随机数生成器
rand_arr = rng.random((2, 3))         # 2x3 的 [0,1) 均匀分布随机数
randn_arr = rng.normal(0, 1, (3, 3))  # 均值为0，方差为1的正态分布随机数
```

### 3.4. 数组的索引与切片：精准定位数据

NumPy 提供了强大而灵活的索引方式，尤其是在多维数组上。

```python
arr = np.array([[1, 2, 3, 4],
                [5, 6, 7, 8],
                [9, 10, 11, 12]])

# 基础索引
print(arr[0, 1])    # 输出: 2 (第0行，第1列)

# 切片 (slice)
print(arr[:2, 1:3]) # 输出: [[2 3]
                    #      [6 7]]

# 花式索引 (Fancy Indexing) - 使用整数数组进行索引
indices = np.array([0, 2])
print(arr[indices]) # 输出第0行和第2行: [[ 1  2  3  4]
                    #                [ 9 10 11 12]]

# 布尔索引 (Boolean Indexing) - 条件筛选
bool_idx = arr > 5
print(arr[bool_idx]) # 输出所有大于5的元素: [ 6  7  8  9 10 11 12]
print(arr[arr % 2 == 0]) # 输出所有偶数: [ 2  4  6  8 10 12]
```

### 3.5. 形状变换：重塑你的数据视角

在不改变数据本身的情况下，你可以灵活地改变数组的形状，这对于数据处理至关重要。

```python
arr = np.arange(12)  # [ 0  1  2  3  4  5  6  7  8  9 10 11]

# reshape: 改变形状，必须保证元素总数不变
mat = arr.reshape(3, 4)
print(mat)
# [[ 0  1  2  3]
#  [ 4  5  6  7]
#  [ 8  9 10 11]]

# 转置 (Transpose): 交换行和列
print(mat.T)
# [[ 0  4  8]
#  [ 1  5  9]
#  [ 2  6 10]
#  [ 3  7 11]]

# flatten: 将多维数组展平为一维
print(mat.flatten()) # [ 0  1  2  3  4  5  6  7  8  9 10 11]
```

### 3.6. 通用函数 (ufunc)：向量化的力量

`ufunc` 是 NumPy 的核心特性之一。它使你能在数组上执行元素级的运算，而无需编写循环。

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

# 算术运算
print(a + b)      # 加法: [5 7 9]
print(a * b)      # 乘法: [4 10 18]
print(a ** 2)     # 幂: [1 4 9]

# 数学函数
print(np.sqrt(a)) # 开方: [1.         1.41421356 1.73205081]
print(np.sin(a))  # 三角函数: [0.84147098 0.90929743 0.14112001]

# 统计函数
print(a.sum())    # 求和: 6
print(a.mean())   # 平均值: 2.0
print(a.max())    # 最大值: 3
```

### 3.7. 广播 (Broadcasting)：不同形状数组的运算艺术

广播是 NumPy 中最强大的特性之一。它允许你对形状不完全相同的数组进行算术运算，NumPy 会自动将较小的数组“广播”到较大数组的形状上。它遵循一套严格的规则。

以下是一个广播过程的直观图解：

```mermaid
graph TD
    subgraph “数组 A (4x3)”
        A1[0 0 0]
        A2[1 1 1]
        A3[2 2 2]
        A4[3 3 3]
    end

    subgraph “数组 B (3,)”
        B1[0 1 2]
    end

    subgraph “广播后的数组 B (4x3)”
        B1_[0 1 2]
        B2_[0 1 2]
        B3_[0 1 2]
        B4_[0 1 2]
    end

    subgraph “结果 C = A + B (4x3)”
        C1[0 1 2]
        C2[1 2 3]
        C3[2 3 4]
        C4[3 4 5]
    end

    A1 --> C1
    A2 --> C2
    A3 --> C3
    A4 --> C4
    B1 -- “广播” --> B1_ & B2_ & B3_ & B4_
    B1_ --> C1
    B2_ --> C2
    B3_ --> C3
    B4_ --> C4
```

```python
import numpy as np

A = np.array([[0, 0, 0],
              [1, 1, 1],
              [2, 2, 2],
              [3, 3, 3]])

B = np.array([0, 1, 2])

# 广播发生: B 被虚拟地复制成4行
C = A + B
print(C)
# [[0 1 2]
#  [1 2 3]
#  [2 3 4]
#  [3 4 5]]
```

> **专家提示**：广播是 NumPy 的核心性能魔法。理解并善用广播，能让你写出简洁、高效的向量化代码，避免显式的 Python 循环，从而将计算推到 C 语言层面执行。不满足广播规则的形状会引发 `ValueError`。

### 3.8. 线性代数与随机数模块

NumPy 内置了线性代数和随机数生成功能，是科学计算的基础。

```python
import numpy as np

# 线性代数 (Linear Algebra)
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

# 矩阵乘法
print(A @ B)          # 推荐方式
print(np.dot(A, B))   # 传统方式
# [[19 22]
#  [43 50]]

# 矩阵求逆、特征值等
print(np.linalg.inv(A))  # 求逆矩阵
print(np.linalg.eig(A))  # 计算特征值和特征向量

# 随机数生成 (Random Sampling)
rng = np.random.default_rng(seed=42)  # 创建随机数生成器
# 从正态分布采样
print(rng.normal(loc=0, scale=1, size=5))  # 均值为0，标准差为1的5个样本
# 随机排列
arr = np.arange(10)
rng.shuffle(arr)
print(arr)
```

## 4. Pandas：数据分析的核心利器

### 4.1. 白话概述：从 Excel 到 Pandas 的思维跃迁

如果说 Excel 是手动挡的数据处理工具，那么 Pandas 就是一套自动化生产线。它专为处理**表格数据**和**时间序列数据**而设计，提供了高效、直观的数据结构和数据操作方法。Pandas 将数据表抽象为 `DataFrame` 对象，让你能以编程的方式，对数据进行筛选、清洗、转换、聚合和分析。

```mermaid
flowchart LR
    A[原始数据<br/>(CSV, Excel, SQL, etc.)] --> B{Pandas 导入<br/>pd.read_*}

    B --> C[DataFrame 对象]
    subgraph C [DataFrame 操作]
        C1[查看与选择] --> C2[清洗与处理] --> C3[变换与重塑] --> C4[分组与聚合] --> C5[合并与连接]
    end
    C --> D[分析结果]
    D --> E[Matplotlib/Seaborn<br/>可视化]
    D --> F[导出数据<br/>(CSV, Excel, etc.)]
```

### 4.2. 核心数据结构：Series 与 DataFrame

Pandas 提供了两种核心数据结构，所有操作都围绕它们展开。

| 结构 | 描述 | 类比 | 关键属性 |
| :--- | :--- | :--- | :--- |
| **Series** | 一维带标签的数组，可容纳任意数据类型。 | Excel 中的一列 | `index`, `values` |
| **DataFrame** | 二维带标签的、大小可变的表格结构，包含不同数据类型的列。 | Excel 中的一张工作表 | `index`, `columns`, `values`, `shape` |

```python
import pandas as pd

# 创建 Series
s = pd.Series([1, 3, 5, np.nan, 6], index=list('abcde'), name='my_series')
print(s)
# a    1.0
# b    3.0
# c    5.0
# d    NaN
# e    6.0
# Name: my_series, dtype: float64

# 创建 DataFrame (最常用方式：通过字典)
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Age': [25, 30, 35],
        'City': ['New York', 'Paris', 'London']}
df = pd.DataFrame(data)
print(df)
#       Name  Age      City
# 0    Alice   25  New York
# 1      Bob   30     Paris
# 2  Charlie   35    London
```

### 4.3. 数据导入与导出：连接各种数据源

Pandas 强大之处在于能轻松与各种数据源交互，这是数据分析的第一步。

```python
import pandas as pd

# 导入数据
df_csv = pd.read_csv('data.csv')                 # 从 CSV 文件
df_excel = pd.read_excel('data.xlsx', sheet_name='Sheet1') # 从 Excel 文件
df_json = pd.read_json('data.json')              # 从 JSON 文件
df_sql = pd.read_sql('SELECT * FROM my_table', connection) # 从 SQL 数据库

# 导出数据
df.to_csv('output.csv', index=False)             # 导出为 CSV，不保存行索引
df.to_excel('output.xlsx', sheet_name='Results') # 导出为 Excel
df.to_json('output.json', orient='records')      # 导出为 JSON
```

### 4.4. 数据查看与选择：精准提取数据子集

理解如何高效地选择和过滤数据是 Pandas 的核心技能。

```python
df = pd.DataFrame({'A': [1, 2, 3, 4],
                   'B': [5, 6, 7, 8],
                   'C': ['a', 'b', 'c', 'd']},
                   index=['row1', 'row2', 'row3', 'row4'])

# 查看头部/尾部数据
print(df.head(2))  # 前2行
print(df.tail(1))  # 后1行

# 选择列
print(df['A'])          # 选择单列，返回 Series
print(df[['A', 'C']])   # 选择多列，返回 DataFrame

# 选择行
print(df.loc['row2'])          # 通过索引标签选择 (返回 Series)
print(df.iloc[1])              # 通过整数位置选择 (返回 Series)
print(df.loc['row1':'row3'])   # 标签切片
print(df.iloc[0:2])            # 位置切片

# 条件选择 (布尔索引)
print(df[df['A'] > 2])         # 选择 A 列大于 2 的所有行
print(df[(df['A'] > 2) & (df['C'] == 'c')]) # 组合条件
```

### 4.5. 数据清洗：为分析扫清障碍

现实世界的数据通常是“脏”的，数据清洗是数据分析中最耗时但也最重要的步骤。

```python
# 创建一个包含缺失值和重复数据的 DataFrame
df_dirty = pd.DataFrame({'A': [1, 2, np.nan, 4, 2],
                         'B': [5, np.nan, np.nan, 8, 5]})

# 处理缺失值
print(df_dirty.isna().sum())          # 检查每列的缺失值数量
df_cleaned = df_dirty.dropna()        # 删除所有包含缺失值的行
df_filled = df_dirty.fillna(0)        # 用 0 填充所有缺失值
df_filled_mean = df_dirty.fillna(df_dirty.mean()) # 用每列的均值填充

# 处理重复值
print(df_dirty.duplicated().sum())    # 检查重复行数
df_no_dup = df_dirty.drop_duplicates() # 删除重复行，保留第一个

# 数据类型转换
df['A'] = df['A'].astype('int32')     # 将列转换为指定类型
```

### 4.6. 数据变换：重塑数据结构

Pandas 提供了类似 Excel 透视表的功能，用于重塑数据布局。

```python
# 创建一个示例数据框
df_long = pd.DataFrame({'Date': ['2024-01-01', '2024-01-01', '2024-01-02', '2024-01-02'],
                        'City': ['New York', 'Paris', 'New York', 'Paris'],
                        'Sales': [100, 150, 120, 180]})

# 使用 pivot 将长格式数据转换为宽格式
df_wide = df_long.pivot(index='Date', columns='City', values='Sales')
print(df_wide)
# City        New York  Paris
# Date
# 2024-01-01       100    150
# 2024-01-02       120    180

# 使用 melt 将宽格式数据转换回长格式
df_long_again = df_wide.reset_index().melt(id_vars='Date', value_name='Sales')
```

### 4.7. 分组与聚合：拆分-应用-合并的艺术

这是 Pandas 最强大的功能之一。它将数据按某个键分割成多个组，对每个组独立应用函数，然后将结果合并起来。

```mermaid
graph TD
    subgraph “原始 DataFrame”
        D[Date, City, Sales]
    end

    subgraph “拆分 (Split)”
        S1[组1: City=New York]
        S2[组2: City=Paris]
    end

    subgraph “应用 (Apply)”
        A1[计算平均销售额]
        A2[计算平均销售额]
    end

    subgraph “合并 (Combine)”
        C[结果 Series/DataFrame]
    end

    D --> S1
    D --> S2
    S1 --> A1 --> C
    S2 --> A2 --> C
```

```python
df = pd.DataFrame({'City': ['New York', 'Paris', 'New York', 'Paris', 'Paris'],
                   'Product': ['A', 'B', 'B', 'A', 'A'],
                   'Sales': [100, 150, 120, 180, 90]})

# 按城市分组，并计算平均销售额
print(df.groupby('City')['Sales'].mean())
# City
# New York    110.0
# Paris       140.0
# Name: Sales, dtype: float64

# 多列分组，多个聚合函数
result = df.groupby(['City', 'Product']).agg(
    total_sales=('Sales', 'sum'),
    avg_sales=('Sales', 'mean'),
    count=('Sales', 'count')
)
print(result)
```

### 4.8. 连接与合并：组合多源数据

在实际项目中，数据往往分散在多个表中。Pandas 提供了类似 SQL 的 `JOIN` 操作。

```python
df1 = pd.DataFrame({'key': ['A', 'B', 'C', 'D'],
                    'value': [1, 2, 3, 4]})
df2 = pd.DataFrame({'key': ['B', 'D', 'E', 'F'],
                    'value': [5, 6, 7, 8]})

# 内连接 (INNER JOIN): 只保留两个表中都有的键
print(pd.merge(df1, df2, on='key', how='inner'))
# 左连接 (LEFT JOIN): 保留左表所有键
print(pd.merge(df1, df2, on='key', how='left'))
# 右连接 (RIGHT JOIN): 保留右表所有键
print(pd.merge(df1, df2, on='key', how='right'))
# 外连接 (OUTER JOIN): 保留两个表所有键
print(pd.merge(df1, df2, on='key', how='outer'))

# 纵向拼接 (类似 SQL 的 UNION)
df3 = pd.DataFrame({'A': [1, 2], 'B': [3, 4]})
df4 = pd.DataFrame({'A': [5, 6], 'B': [7, 8]})
print(pd.concat([df3, df4], axis=0, ignore_index=True))  # 按行拼接
```

## 5. Matplotlib：数据可视化利器

### 5.1. 白话概述：用图形讲述数据故事

数据可视化是数据分析的“临门一脚”。Matplotlib 是 Python 中最基础、最强大的 2D 绘图库，它为你提供了创建**出版级质量图表**的所有工具。它就像一套画笔和画布，你可以精细地控制图表的每一个元素，从线条粗细、颜色到坐标轴标签和标题。

### 5.2. Matplotlib 架构：两层 API 的设计哲学

Matplotlib 有两种主要的 API 风格，理解它们能让你更好地控制你的图表。

| 层次 | API 风格 | 描述 | 特点 | 适用场景 |
| :--- | :--- | :--- | :--- | :--- |
| **脚本层 (pyplot)** | `plt.plot()` | 模仿 MATLAB 的绘图方式，状态机接口。 | 简单、快捷，适合交互式探索。 | 快速绘图、Jupyter Notebook 中使用 |
| **艺术家层 (Artist)** | `fig, ax = plt.subplots()` | 面向对象的 API，直接操作 Figure 和 Axes 对象。 | 更强大、灵活，适合创建复杂图表和精细控制。 | 复杂图表、需要精细定制的场景 |

> **专家提示**：**强烈推荐始终使用面向对象的（Artist）方式**。虽然 `pyplot` 看起来更简单，但当图表变得复杂时，它会导致代码难以理解和维护。面向对象的方式让你明确知道你在哪个“画布” (`Figure`) 和“子图” (`Axes`) 上操作。

### 5.3. Figure 与 Axes：画布与子图的层次

这是理解 Matplotlib 对象模型的关键。

```mermaid
graph TD
    F[<b>Figure</b><br/>最顶层的容器，代表整张画布] --> A1[<b>Axes</b> (Subplot)<br/>单个坐标系，所有绘图元素都包含在其中]
    F --> A2[<b>Axes</b> (Subplot)]
    F --> A3[...]

    A1 --> XA[x-axis (坐标轴)]
    A1 --> YA[y-axis (坐标轴)]
    A1 --> L[Line2D, Text, etc.<br/>(具体的图表元素)]
```

```python
import matplotlib.pyplot as plt
import numpy as np

# 面向对象方式 (推荐)
fig, ax = plt.subplots()  # 创建一个 Figure 和一个 Axes 对象

x = np.linspace(0, 2, 100)
ax.plot(x, x, label='linear')
ax.plot(x, x**2, label='quadratic')
ax.plot(x, x**3, label='cubic')

ax.set_xlabel('x label')
ax.set_ylabel('y label')
ax.set_title("Simple Plot")
ax.legend()

plt.show()
```

### 5.4. 常用图表绘制实战

Matplotlib 支持几乎所有你能想到的图表类型。

```python
import matplotlib.pyplot as plt
import numpy as np

# 准备数据
x = np.linspace(0, 2 * np.pi, 100)
y1 = np.sin(x)
y2 = np.cos(x)
categories = ['A', 'B', 'C']
values = [3, 7, 2]
data = np.random.randn(1000)

# 创建 2x2 的子图布局
fig, axes = plt.subplots(2, 2, figsize=(10, 8))

# 1. 折线图 (Line Plot)
axes[0, 0].plot(x, y1, label='sin(x)')
axes[0, 0].plot(x, y2, label='cos(x)')
axes[0, 0].set_title('Line Plot')
axes[0, 0].legend()

# 2. 散点图 (Scatter Plot)
axes[0, 1].scatter(x, y1, c=y2, cmap='viridis', alpha=0.7)
axes[0, 1].set_title('Scatter Plot')
axes[0, 1].colorbar = fig.colorbar(axes[0, 1].collections[0], ax=axes[0, 1])

# 3. 柱状图 (Bar Plot)
axes[1, 0].bar(categories, values, color=['red', 'green', 'blue'])
axes[1, 0].set_title('Bar Plot')

# 4. 直方图 (Histogram)
axes[1, 1].hist(data, bins=30, density=True, alpha=0.7, color='purple')
axes[1, 1].set_title('Histogram')

plt.tight_layout()  # 自动调整子图间距
plt.show()
```

### 5.5. 图表样式与自定义：打造专业级图表

Matplotlib 允许你完全自定义图表外观，包括颜色、线型、字体、图例等。

```python
import matplotlib.pyplot as plt
import numpy as np

# 使用内置样式
plt.style.use('seaborn-v0_8-darkgrid')  # 或者 'ggplot', 'fivethirtyeight' 等

x = np.linspace(0, 10, 100)
y = np.sin(x)

fig, ax = plt.subplots(figsize=(8, 5))
ax.plot(x, y, linewidth=2, linestyle='--', color='crimson', marker='o', markevery=10)

# 设置标题和轴标签
ax.set_title('Sine Wave', fontsize=16, fontweight='bold')
ax.set_xlabel('Time (s)', fontsize=12)
ax.set_ylabel('Amplitude', fontsize=12)

# 设置坐标轴范围
ax.set_xlim(0, 10)
ax.set_ylim(-1.5, 1.5)

# 添加网格
ax.grid(True, linestyle=':', alpha=0.7)

# 自定义图例
ax.legend(['sin(x)'], loc='upper right', frameon=True, fancybox=True, shadow=True)

plt.show()
```

### 5.6. 多子图与复杂布局

当需要在一个画布上展示多个相关图表时，`subplots` 是最佳选择。对于更复杂的布局，可以使用 `subplot_mosaic`。

```python
import matplotlib.pyplot as plt
import numpy as np

# 使用 subplot_mosaic 创建非对称布局
mosaic = [['A', 'A', 'B'],
          ['A', 'A', 'C'],
          ['D', 'E', 'E']]
fig, axd = plt.subplot_mosaic(mosaic, figsize=(10, 8))

x = np.linspace(0, 2*np.pi, 100)

axd['A'].plot(x, np.sin(x))
axd['A'].set_title('Sine (A)')

axd['B'].plot(x, np.cos(x), 'tab:orange')
axd['B'].set_title('Cosine (B)')

axd['C'].scatter(x, np.sin(x) + np.random.randn(100)*0.1, alpha=0.5)
axd['C'].set_title('Scatter (C)')

axd['D'].bar(['a', 'b', 'c'], [3, 7, 5])
axd['D'].set_title('Bar (D)')

axd['E'].hist(np.random.randn(1000), bins=30, density=True, alpha=0.7)
axd['E'].set_title('Histogram (E)')

plt.tight_layout()
plt.show()
```

### 5.7. 与 Pandas 的无缝集成

Pandas 的 `plot()` 方法是对 Matplotlib 的封装，让你可以直接从 `DataFrame` 或 `Series` 对象快速绘图。

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# 创建一个时间序列 DataFrame
dates = pd.date_range('20230101', periods=100)
df = pd.DataFrame(np.random.randn(100, 4), index=dates, columns=list('ABCD'))

# 使用 Pandas 快速绘制折线图
df.plot(figsize=(12, 6), title='Random Time Series')
plt.ylabel('Value')
plt.show()

# 绘制累积和
df.cumsum().plot(figsize=(12, 6), title='Cumulative Sum')
plt.show()

# 绘制柱状图
df.iloc[0].plot(kind='bar', title='First Row Values', rot=0)
plt.show()

# 绘制散点矩阵 (需要安装 pandas 的 plotting 模块)
# from pandas.plotting import scatter_matrix
# scatter_matrix(df, alpha=0.5, figsize=(10, 10), diagonal='kde')
# plt.show()
```

## 6. 综合实战：将一切串联起来

### 6.1. 项目：电影数据分析报告

现在，让我们将所学的一切应用到一个小型实战项目中。我们将分析一个电影数据集，并生成一份简要的报告。

**目标**：对电影数据进行探索性分析，回答以下问题：
1.  哪种类型的电影平均票房最高？
2.  电影预算与票房的关系是什么？
3.  不同年份的电影产量有何趋势？

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# 设置随机种子以保证结果可复现
np.random.seed(42)

# 1. 使用 NumPy 和 Pandas 生成模拟数据
n_movies = 1000
genres = np.random.choice(['Action', 'Comedy', 'Drama', 'Sci-Fi', 'Thriller'], n_movies)
years = np.random.randint(2000, 2024, n_movies)
budgets = np.random.uniform(1, 200, n_movies)  # 预算 (百万美元)
# 票房与预算正相关，但加入一些噪声。喜剧平均回报率更高，科幻波动大。
box_office = budgets * np.random.uniform(1.5, 4.0, n_movies)
box_office[genres == 'Comedy'] *= 1.3  # 喜剧电影回报率更高
box_office[genres == 'Sci-Fi'] *= np.random.uniform(0.5, 3.0, n_movies) # 科幻电影风险高，波动大
box_office = np.maximum(box_office, budgets * 0.1) # 确保票房至少是预算的10%

# 创建 DataFrame
df_movies = pd.DataFrame({
    'Title': [f'Movie_{i}' for i in range(n_movies)],
    'Genre': genres,
    'Year': years,
    'Budget_M': budgets,
    'BoxOffice_M': box_office
})

print("--- 数据概览 ---")
print(df_movies.head())
print("\n--- 数据信息 ---")
df_movies.info()
print("\n--- 描述性统计 ---")
print(df_movies.describe())

# 2. 数据清洗与分析 (Pandas)
# 问题1：哪种类型的电影平均票房最高？
avg_boxoffice_by_genre = df_movies.groupby('Genre')['BoxOffice_M'].mean().sort_values(ascending=False)
print("\n--- 各类型平均票房 (百万美元) ---")
print(avg_boxoffice_by_genre)

# 问题2：电影预算与票房的关系是什么？
correlation = df_movies['Budget_M'].corr(df_movies['BoxOffice_M'])
print(f"\n预算与票房的相关系数: {correlation:.3f}")

# 问题3：不同年份的电影产量有何趋势？
movies_per_year = df_movies['Year'].value_counts().sort_index()
print("\n--- 每年电影产量 ---")
print(movies_per_year.head())

# 3. 数据可视化 (Matplotlib)
plt.style.use('seaborn-v0_8-whitegrid')
fig = plt.figure(figsize=(16, 12))

# 图1：各类型平均票房 (柱状图)
ax1 = fig.add_subplot(2, 2, 1)
avg_boxoffice_by_genre.plot(kind='bar', ax=ax1, color='skyblue')
ax1.set_title('Average Box Office by Genre', fontsize=14)
ax1.set_xlabel('Genre')
ax1.set_ylabel('Average Box Office (Millions)')
ax1.tick_params(axis='x', rotation=45)

# 图2：预算 vs 票房 (散点图)
ax2 = fig.add_subplot(2, 2, 2)
scatter = ax2.scatter(df_movies['Budget_M'], df_movies['BoxOffice_M'], 
                      c=pd.factorize(df_movies['Genre'])[0], cmap='viridis', alpha=0.6)
ax2.set_title(f'Budget vs. Box Office (Correlation: {correlation:.2f})', fontsize=14)
ax2.set_xlabel('Budget (Millions)')
ax2.set_ylabel('Box Office (Millions)')
# 添加图例
legend1 = ax2.legend(*scatter.legend_elements(), title="Genres")
ax2.add_artist(legend1)

# 图3：电影产量年度趋势 (折线图)
ax3 = fig.add_subplot(2, 2, 3)
ax3.plot(movies_per_year.index, movies_per_year.values, marker='o', linestyle='-')
ax3.set_title('Number of Movies Released Per Year', fontsize=14)
ax3.set_xlabel('Year')
ax3.set_ylabel('Number of Movies')
ax3.grid(True)

# 图4：各类型电影数量分布 (饼图)
ax4 = fig.add_subplot(2, 2, 4)
genre_counts = df_movies['Genre'].value_counts()
ax4.pie(genre_counts.values, labels=genre_counts.index, autopct='%1.1f%%', startangle=90)
ax4.set_title('Distribution of Movie Genres', fontsize=14)

plt.tight_layout()
plt.show()
```

## 7. 扩展阅读与生态工具

掌握 Python、NumPy、Pandas 和 Matplotlib 后，你已经拥有了数据分析的核心能力。接下来，你可以根据兴趣向更专业的领域扩展：

### 7.1. 基础进阶：SciPy
SciPy 构建在 NumPy 之上，提供了更丰富的科学计算工具，包括最优化、线性代数、积分、插值、信号处理、图像处理等模块。

### 7.2. 机器学习：Scikit-learn
Scikit-learn 是 Python 中最流行的机器学习库，它提供了大量经典的机器学习算法，如分类、回归、聚类、降维等。它的 API 设计统一，并且与 NumPy 和 Pandas 无缝集成。

### 7.3. 可视化进阶：Seaborn 与 Plotly
-   **Seaborn**：构建在 Matplotlib 之上，提供了更高级的统计图表绘制接口，默认样式也更美观，能让你用几行代码绘制出复杂的统计图表。
-   **Plotly**：一个交互式图表库，可以创建可缩放、可平移、可悬停显示信息的图表，非常适合制作网页仪表盘。

## 8. 总结：您的下一步学习路线图

这份指南为你绘制了一张从 Python 基础到数据分析核心技能的蓝图。学习编程和数据分析是一个持续实践的过程。

1.  **动手实践**：不要只看不练。请务必亲手运行并修改本指南中的每一个代码示例。理解“为什么”比知道“是什么”更重要。
2.  **从小项目开始**：找一个你感兴趣的小数据集（例如，你所在城市的天气数据、你的个人财务记录、电影评分数据），尝试用 Pandas 进行清洗和分析，并用 Matplotlib 将你的发现可视化出来。这是巩固知识的最佳方式。
3.  **查阅官方文档**：本指南只能带你入门。NumPy、Pandas 和 Matplotlib 的官方文档是世界上最权威、最详尽的学习资源。当你遇到问题时，第一反应应该是去查官方文档。
4.  **加入社区**：遇到无法解决的问题，可以去 StackOverflow、GitHub Issues 或相关的技术社区提问。清晰地描述你的问题和你已经尝试过的方法，会更容易得到帮助。

你已经迈出了最重要的一步。祝你在数据科学的世界里探索愉快！