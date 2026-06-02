# C++ Primer Plus 第六版学习笔记 - 第7章：函数

## 目录

- [1. 函数的基本概念](#1-函数的基本概念)
- [2. 函数定义和声明](#2-函数定义和声明)
- [3. 函数参数](#3-函数参数)
- [4. 返回值](#4-返回值)
- [5. 函数原型](#5-函数原型)
- [6. 值传递和引用传递](#6-值传递和引用传递)
- [7. 默认参数](#7-默认参数)
- [8. 函数重载](#8-函数重载)
- [9. 递归函数](#9-递归函数)
- [10. 内联函数](#10-内联函数)
- [11. 函数指针](#11-函数指针)
- [12. lambda表达式（C++11）](#12-lambda表达式c11)
- [13. 本章小结](#13-本章小结)
- [14. 练习题](#14-练习题)

---

## 1. 函数的基本概念

函数是程序中执行特定任务的代码块，可以重复调用。

### 1.1 为什么使用函数

**优点：**
- 代码复用：避免重复编写相同代码
- 模块化：将复杂问题分解为小问题
- 可维护性：修改一处即可影响所有调用
- 可读性：通过函数名表达意图
- 测试性：可以单独测试每个函数

### 1.2 函数的组成部分

```cpp
返回类型 函数名(参数列表) {
    // 函数体
    return 返回值;
}
```

**组成部分：**
- **返回类型**：函数返回值的类型（void表示无返回值）
- **函数名**：标识符，遵循命名规则
- **参数列表**：传递给函数的数据（可以为空）
- **函数体**：执行的代码
- **return语句**：返回值并退出函数

### 1.3 基本示例

```cpp
#include <iostream>

// 简单的函数定义
void sayHello() {
    std::cout << "Hello, World!" << std::endl;
}

int add(int a, int b) {
    return a + b;
}

int main() {
    // 调用函数
    sayHello();
    
    int result = add(5, 3);
    std::cout << "5 + 3 = " << result << std::endl;
    
    return 0;
}
```

---

## 2. 函数定义和声明

### 2.1 函数声明（原型）

函数声明告诉编译器函数的存在，但不提供实现。

```cpp
#include <iostream>

// 函数声明（原型）
int multiply(int x, int y);
void printMessage(const std::string& msg);

int main() {
    // 可以在声明之后调用
    printMessage("Starting program...");
    
    int result = multiply(4, 5);
    std::cout << "4 * 5 = " << result << std::endl;
    
    return 0;
}

// 函数定义
int multiply(int x, int y) {
    return x * y;
}

void printMessage(const std::string& msg) {
    std::cout << msg << std::endl;
}
```

### 2.2 函数定义

函数定义包含完整的实现。

```cpp
#include <iostream>

// 函数定义在main之前，不需要单独声明
double calculateArea(double radius) {
    const double PI = 3.14159;
    return PI * radius * radius;
}

double calculateCircumference(double radius) {
    const double PI = 3.14159;
    return 2 * PI * radius;
}

int main() {
    double radius = 5.0;
    
    std::cout << "Radius: " << radius << std::endl;
    std::cout << "Area: " << calculateArea(radius) << std::endl;
    std::cout << "Circumference: " << calculateCircumference(radius) << std::endl;
    
    return 0;
}
```

### 2.3 头文件中的函数声明

```cpp
// math_utils.h
#ifndef MATH_UTILS_H
#define MATH_UTILS_H

// 函数声明
int factorial(int n);
double power(double base, int exponent);
bool isPrime(int n);

#endif
```

```cpp
// math_utils.cpp
#include "math_utils.h"

int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}

double power(double base, int exponent) {
    double result = 1.0;
    for (int i = 0; i < exponent; ++i) {
        result *= base;
    }
    return result;
}

bool isPrime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i * i <= n; ++i) {
        if (n % i == 0) return false;
    }
    return true;
}
```

```cpp
// main.cpp
#include <iostream>
#include "math_utils.h"

int main() {
    std::cout << "5! = " << factorial(5) << std::endl;
    std::cout << "2^10 = " << power(2, 10) << std::endl;
    std::cout << "Is 17 prime? " << (isPrime(17) ? "Yes" : "No") << std::endl;
    
    return 0;
}
```

---

## 3. 函数参数

### 3.1 无参数函数

```cpp
#include <iostream>

void printLine() {
    std::cout << "--------------------" << std::endl;
}

void greetUser() {
    std::cout << "Welcome to the program!" << std::endl;
}

int main() {
    greetUser();
    printLine();
    return 0;
}
```

### 3.2 单参数函数

```cpp
#include <iostream>
#include <string>

void greet(const std::string& name) {
    std::cout << "Hello, " << name << "!" << std::endl;
}

void printSquare(int size) {
    for (int i = 0; i < size; ++i) {
        for (int j = 0; j < size; ++j) {
            std::cout << "* ";
        }
        std::cout << std::endl;
    }
}

int main() {
    greet("Alice");
    printLine();
    printSquare(5);
    return 0;
}
```

### 3.3 多参数函数

```cpp
#include <iostream>

void displayInfo(const std::string& name, int age, double height) {
    std::cout << "Name: " << name << std::endl;
    std::cout << "Age: " << age << std::endl;
    std::cout << "Height: " << height << " m" << std::endl;
}

double calculateDistance(double x1, double y1, double x2, double y2) {
    double dx = x2 - x1;
    double dy = y2 - y1;
    return std::sqrt(dx * dx + dy * dy);
}

int main() {
    displayInfo("Bob", 25, 1.75);
    
    double dist = calculateDistance(0, 0, 3, 4);
    std::cout << "Distance: " << dist << std::endl;
    
    return 0;
}
```

### 3.4 可变参数函数

```cpp
#include <iostream>
#include <initializer_list>

// 使用initializer_list接受可变数量的参数
int sum(std::initializer_list<int> nums) {
    int total = 0;
    for (int num : nums) {
        total += num;
    }
    return total;
}

double average(std::initializer_list<double> nums) {
    if (nums.size() == 0) return 0.0;
    
    double total = 0.0;
    for (double num : nums) {
        total += num;
    }
    return total / nums.size();
}

int main() {
    std::cout << "Sum: " << sum({1, 2, 3, 4, 5}) << std::endl;
    std::cout << "Average: " << average({10.0, 20.0, 30.0}) << std::endl;
    
    return 0;
}
```

---

## 4. 返回值

### 4.1 返回基本类型

```cpp
#include <iostream>

int getMaximum(int a, int b) {
    return (a > b) ? a : b;
}

double getPi() {
    return 3.14159265358979;
}

char getGrade(int score) {
    if (score >= 90) return 'A';
    if (score >= 80) return 'B';
    if (score >= 70) return 'C';
    if (score >= 60) return 'D';
    return 'F';
}

int main() {
    std::cout << "Max: " << getMaximum(10, 20) << std::endl;
    std::cout << "Pi: " << getPi() << std::endl;
    std::cout << "Grade: " << getGrade(85) << std::endl;
    
    return 0;
}
```

### 4.2 返回void（无返回值）

```cpp
#include <iostream>

void printStars(int count) {
    for (int i = 0; i < count; ++i) {
        std::cout << "*";
    }
    std::cout << std::endl;
}

void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

int main() {
    printStars(10);
    
    int x = 5, y = 10;
    std::cout << "Before: x = " << x << ", y = " << y << std::endl;
    swap(x, y);
    std::cout << "After: x = " << x << ", y = " << y << std::endl;
    
    return 0;
}
```

### 4.3 返回多个值

```cpp
#include <iostream>
#include <tuple>

// 方法1：使用结构体
struct MinMax {
    int min;
    int max;
};

MinMax findMinMax(const int arr[], int size) {
    MinMax result;
    result.min = arr[0];
    result.max = arr[0];
    
    for (int i = 1; i < size; ++i) {
        if (arr[i] < result.min) result.min = arr[i];
        if (arr[i] > result.max) result.max = arr[i];
    }
    
    return result;
}

// 方法2：使用std::pair
std::pair<int, int> findMinMaxPair(const int arr[], int size) {
    int minVal = arr[0];
    int maxVal = arr[0];
    
    for (int i = 1; i < size; ++i) {
        if (arr[i] < minVal) minVal = arr[i];
        if (arr[i] > maxVal) maxVal = arr[i];
    }
    
    return std::make_pair(minVal, maxVal);
}

// 方法3：使用std::tuple
std::tuple<int, int, double> calculateStats(const int arr[], int size) {
    int sum = 0;
    int minVal = arr[0];
    int maxVal = arr[0];
    
    for (int i = 0; i < size; ++i) {
        sum += arr[i];
        if (arr[i] < minVal) minVal = arr[i];
        if (arr[i] > maxVal) maxVal = arr[i];
    }
    
    double avg = static_cast<double>(sum) / size;
    return std::make_tuple(minVal, maxVal, avg);
}

int main() {
    int numbers[] = {5, 2, 8, 1, 9, 3, 7, 4, 6};
    int size = sizeof(numbers) / sizeof(numbers[0]);
    
    // 使用结构体
    MinMax mm = findMinMax(numbers, size);
    std::cout << "Min: " << mm.min << ", Max: " << mm.max << std::endl;
    
    // 使用pair
    auto mmPair = findMinMaxPair(numbers, size);
    std::cout << "Min: " << mmPair.first << ", Max: " << mmPair.second << std::endl;
    
    // 使用tuple
    auto stats = calculateStats(numbers, size);
    std::cout << "Min: " << std::get<0>(stats) 
              << ", Max: " << std::get<1>(stats)
              << ", Avg: " << std::get<2>(stats) << std::endl;
    
    return 0;
}
```

### 4.4 提前返回

```cpp
#include <iostream>
#include <string>

std::string validatePassword(const std::string& password) {
    // 检查长度
    if (password.length() < 8) {
        return "Password must be at least 8 characters long";
    }
    
    // 检查是否包含数字
    bool hasDigit = false;
    for (char ch : password) {
        if (isdigit(ch)) {
            hasDigit = true;
            break;
        }
    }
    
    if (!hasDigit) {
        return "Password must contain at least one digit";
    }
    
    // 检查是否包含大写字母
    bool hasUpper = false;
    for (char ch : password) {
        if (isupper(ch)) {
            hasUpper = true;
            break;
        }
    }
    
    if (!hasUpper) {
        return "Password must contain at least one uppercase letter";
    }
    
    // 所有检查通过
    return "Valid password";
}

int main() {
    std::cout << validatePassword("abc") << std::endl;
    std::cout << validatePassword("abcdefgh") << std::endl;
    std::cout << validatePassword("Abcdefgh") << std::endl;
    std::cout << validatePassword("Abcdefg1") << std::endl;
    
    return 0;
}
```

---

## 5. 函数原型

### 5.1 函数原型的作用

函数原型（function prototype）也称为函数声明，它告诉编译器：
- 函数的名称
- 参数的类型和数量
- 返回值的类型

```cpp
#include <iostream>

// 函数原型
double calculatePower(double base, int exponent);
void printResult(double base, int exponent, double result);

int main() {
    double base = 2.0;
    int exponent = 10;
    
    double result = calculatePower(base, exponent);
    printResult(base, exponent, result);
    
    return 0;
}

// 函数定义
double calculatePower(double base, int exponent) {
    double result = 1.0;
    for (int i = 0; i < exponent; ++i) {
        result *= base;
    }
    return result;
}

void printResult(double base, int exponent, double result) {
    std::cout << base << "^" << exponent << " = " << result << std::endl;
}
```

### 5.2 原型与定义的一致性

```cpp
#include <iostream>

// 正确的原型
int add(int a, int b);

// 错误的原型（参数名可以不同，但类型必须匹配）
// int add(double x, double y);  // 错误！

int main() {
    std::cout << add(5, 3) << std::endl;
    return 0;
}

int add(int a, int b) {
    return a + b;
}
```

---

## 6. 值传递和引用传递

### 6.1 值传递（Pass by Value）

值传递会创建参数的副本，函数内部的修改不会影响原始变量。

```cpp
#include <iostream>

void modifyByValue(int x) {
    x = 100;  // 只修改副本，不影响原变量
    std::cout << "Inside function: x = " << x << std::endl;
}

int main() {
    int num = 10;
    std::cout << "Before call: num = " << num << std::endl;
    
    modifyByValue(num);
    
    std::cout << "After call: num = " << num << std::endl;
    
    return 0;
}
```

### 6.2 引用传递（Pass by Reference）

引用传递直接操作原始变量，函数内部的修改会影响原始变量。

```cpp
#include <iostream>

void modifyByReference(int& x) {
    x = 100;  // 直接修改原变量
    std::cout << "Inside function: x = " << x << std::endl;
}

void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

int main() {
    int num = 10;
    std::cout << "Before call: num = " << num << std::endl;
    
    modifyByReference(num);
    
    std::cout << "After call: num = " << num << std::endl;
    
    int x = 5, y = 10;
    std::cout << "Before swap: x = " << x << ", y = " << y << std::endl;
    swap(x, y);
    std::cout << "After swap: x = " << x << ", y = " << y << std::endl;
    
    return 0;
}
```

### 6.3 常量引用（Pass by Const Reference）

常量引用避免了复制开销，同时保证不修改原始数据。

```cpp
#include <iostream>
#include <string>
#include <vector>

// 使用const引用避免复制大型对象
void printVector(const std::vector<int>& vec) {
    // vec.push_back(100);  // 错误！不能修改const引用
    for (const auto& elem : vec) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;
}

void printString(const std::string& str) {
    std::cout << "String: " << str << std::endl;
    std::cout << "Length: " << str.length() << std::endl;
}

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    printVector(numbers);
    
    std::string message = "Hello, World!";
    printString(message);
    
    return 0;
}
```

### 6.4 指针传递

```cpp
#include <iostream>

void modifyByPointer(int* ptr) {
    if (ptr != nullptr) {
        *ptr = 100;
    }
}

void fillArray(int* arr, int size, int value) {
    for (int i = 0; i < size; ++i) {
        arr[i] = value;
    }
}

int main() {
    int num = 10;
    std::cout << "Before: num = " << num << std::endl;
    
    modifyByPointer(&num);
    std::cout << "After: num = " << num << std::endl;
    
    int arr[5];
    fillArray(arr, 5, 42);
    
    std::cout << "Array: ";
    for (int i = 0; i < 5; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

### 6.5 传递方式比较

| 传递方式 | 优点 | 缺点 | 适用场景 |
|----------|------|------|----------|
| 值传递 | 安全，不修改原值 | 复制开销大 | 小型数据类型 |
| 引用传递 | 高效，可修改原值 | 可能意外修改 | 需要修改原值时 |
| const引用 | 高效，保护原值 | 语法稍复杂 | 大型对象，只读访问 |
| 指针传递 | 灵活，可为nullptr | 需要检查nullptr | 可选参数，动态内存 |

---

## 7. 默认参数

### 7.1 基本用法

```cpp
#include <iostream>
#include <string>

// 带有默认参数的函数
void greet(const std::string& name = "Guest", const std::string& greeting = "Hello") {
    std::cout << greeting << ", " << name << "!" << std::endl;
}

// 多个默认参数
void displayInfo(const std::string& name, int age = 0, const std::string& city = "Unknown") {
    std::cout << "Name: " << name << std::endl;
    std::cout << "Age: " << age << std::endl;
    std::cout << "City: " << city << std::endl;
}

int main() {
    greet();                          // 使用所有默认值
    greet("Alice");                   // 使用默认greeting
    greet("Bob", "Hi");               // 提供所有参数
    
    std::cout << std::endl;
    
    displayInfo("Charlie");           // 只提供name
    displayInfo("David", 25);         // 提供name和age
    displayInfo("Eve", 30, "NYC");    // 提供所有参数
    
    return 0;
}
```

### 7.2 默认参数规则

```cpp
#include <iostream>

// 正确：默认参数从右到左
void func1(int a, int b = 10, int c = 20);

// 错误：不能有非默认参数在默认参数之后
// void func2(int a = 10, int b);  // 编译错误！

// 正确：可以在声明或定义中指定默认参数，但不能重复
void func3(int a, int b = 5);

int main() {
    func1(1);        // a=1, b=10, c=20
    func1(1, 2);     // a=1, b=2, c=20
    func1(1, 2, 3);  // a=1, b=2, c=3
    
    func3(10);       // a=10, b=5
    func3(10, 15);   // a=10, b=15
    
    return 0;
}

void func1(int a, int b, int c) {
    std::cout << "a=" << a << ", b=" << b << ", c=" << c << std::endl;
}

void func3(int a, int b) {
    std::cout << "a=" << a << ", b=" << b << std::endl;
}
```

### 7.3 实际应用

```cpp
#include <iostream>
#include <string>

// 日志函数，带有默认级别
enum class LogLevel {
    DEBUG = 0,
    INFO = 1,
    WARNING = 2,
    ERROR = 3
};

void log(const std::string& message, LogLevel level = LogLevel::INFO) {
    std::string levelStr;
    switch (level) {
        case LogLevel::DEBUG:   levelStr = "DEBUG"; break;
        case LogLevel::INFO:    levelStr = "INFO"; break;
        case LogLevel::WARNING: levelStr = "WARNING"; break;
        case LogLevel::ERROR:   levelStr = "ERROR"; break;
    }
    
    std::cout << "[" << levelStr << "] " << message << std::endl;
}

// 数学函数，带有默认精度
double roundToDecimal(double value, int decimals = 2) {
    double multiplier = 1.0;
    for (int i = 0; i < decimals; ++i) {
        multiplier *= 10;
    }
    return std::round(value * multiplier) / multiplier;
}

int main() {
    log("Application started");
    log("Debug information", LogLevel::DEBUG);
    log("Something went wrong", LogLevel::ERROR);
    
    std::cout << std::endl;
    
    std::cout << roundToDecimal(3.14159) << std::endl;          // 3.14
    std::cout << roundToDecimal(3.14159, 3) << std::endl;       // 3.142
    std::cout << roundToDecimal(3.14159, 0) << std::endl;       // 3
    
    return 0;
}
```

---

## 8. 函数重载

### 8.1 基本概念

函数重载允许同一函数名有多个版本，只要参数列表不同。

```cpp
#include <iostream>

// 重载的add函数
int add(int a, int b) {
    std::cout << "int version" << std::endl;
    return a + b;
}

double add(double a, double b) {
    std::cout << "double version" << std::endl;
    return a + b;
}

std::string add(const std::string& a, const std::string& b) {
    std::cout << "string version" << std::endl;
    return a + b;
}

int main() {
    std::cout << add(5, 3) << std::endl;
    std::cout << add(2.5, 3.7) << std::endl;
    std::cout << add("Hello, ", "World!") << std::endl;
    
    return 0;
}
```

### 8.2 重载规则

```cpp
#include <iostream>

// 正确的重载：参数类型不同
void print(int x) {
    std::cout << "int: " << x << std::endl;
}

void print(double x) {
    std::cout << "double: " << x << std::endl;
}

void print(const std::string& x) {
    std::cout << "string: " << x << std::endl;
}

// 正确的重载：参数数量不同
void display(int x) {
    std::cout << "One int: " << x << std::endl;
}

void display(int x, int y) {
    std::cout << "Two ints: " << x << ", " << y << std::endl;
}

// 错误：仅返回类型不同不能作为重载依据
// int getValue();
// double getValue();  // 编译错误！

int main() {
    print(10);
    print(3.14);
    print("Hello");
    
    display(5);
    display(5, 10);
    
    return 0;
}
```

### 8.3 实际应用

```cpp
#include <iostream>
#include <vector>
#include <string>

// 重载的max函数
int max(int a, int b) {
    return (a > b) ? a : b;
}

double max(double a, double b) {
    return (a > b) ? a : b;
}

int max(const std::vector<int>& vec) {
    if (vec.empty()) throw std::invalid_argument("Empty vector");
    
    int maxVal = vec[0];
    for (size_t i = 1; i < vec.size(); ++i) {
        if (vec[i] > maxVal) {
            maxVal = vec[i];
        }
    }
    return maxVal;
}

// 重载的print函数
void print(int x) {
    std::cout << x << std::endl;
}

void print(double x) {
    std::cout << x << std::endl;
}

void print(const std::string& x) {
    std::cout << x << std::endl;
}

void print(const std::vector<int>& vec) {
    std::cout << "[";
    for (size_t i = 0; i < vec.size(); ++i) {
        std::cout << vec[i];
        if (i < vec.size() - 1) {
            std::cout << ", ";
        }
    }
    std::cout << "]" << std::endl;
}

int main() {
    std::cout << "Max of 5 and 10: " << max(5, 10) << std::endl;
    std::cout << "Max of 3.14 and 2.71: " << max(3.14, 2.71) << std::endl;
    
    std::vector<int> numbers = {5, 2, 8, 1, 9};
    std::cout << "Max in vector: " << max(numbers) << std::endl;
    
    std::cout << std::endl;
    
    print(42);
    print(3.14);
    print("Hello, World!");
    print(numbers);
    
    return 0;
}
```

### 8.4 重载解析

```cpp
#include <iostream>

void func(int x) {
    std::cout << "func(int)" << std::endl;
}

void func(double x) {
    std::cout << "func(double)" << std::endl;
}

void func(int x, int y) {
    std::cout << "func(int, int)" << std::endl;
}

int main() {
    func(10);        // 调用func(int)
    func(3.14);      // 调用func(double)
    func(10, 20);    // 调用func(int, int)
    func('A');       // char提升为int，调用func(int)
    
    return 0;
}
```

---

## 9. 递归函数

### 9.1 基本概念

递归函数是调用自身的函数，必须包含基准情况（终止条件）。

```cpp
#include <iostream>

// 计算阶乘
long long factorial(int n) {
    // 基准情况
    if (n <= 1) {
        return 1;
    }
    // 递归情况
    return n * factorial(n - 1);
}

int main() {
    for (int i = 0; i <= 10; ++i) {
        std::cout << i << "! = " << factorial(i) << std::endl;
    }
    
    return 0;
}
```

### 9.2 斐波那契数列

```cpp
#include <iostream>

// 递归版本（效率低）
long long fibonacciRecursive(int n) {
    if (n <= 0) return 0;
    if (n == 1) return 1;
    return fibonacciRecursive(n - 1) + fibonacciRecursive(n - 2);
}

// 迭代版本（效率高）
long long fibonacciIterative(int n) {
    if (n <= 0) return 0;
    if (n == 1) return 1;
    
    long long prev = 0, curr = 1;
    for (int i = 2; i <= n; ++i) {
        long long next = prev + curr;
        prev = curr;
        curr = next;
    }
    return curr;
}

int main() {
    std::cout << "Fibonacci sequence:" << std::endl;
    for (int i = 0; i <= 15; ++i) {
        std::cout << "F(" << i << ") = " << fibonacciIterative(i) << std::endl;
    }
    
    return 0;
}
```

### 9.3 递归的实际应用

#### 应用1：二分查找

```cpp
#include <iostream>
#include <vector>

int binarySearch(const std::vector<int>& arr, int target, int left, int right) {
    // 基准情况：未找到
    if (left > right) {
        return -1;
    }
    
    int mid = left + (right - left) / 2;
    
    if (arr[mid] == target) {
        return mid;
    } else if (arr[mid] > target) {
        return binarySearch(arr, target, left, mid - 1);
    } else {
        return binarySearch(arr, target, mid + 1, right);
    }
}

int main() {
    std::vector<int> sorted = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};
    
    int target = 7;
    int result = binarySearch(sorted, target, 0, sorted.size() - 1);
    
    if (result != -1) {
        std::cout << target << " found at index " << result << std::endl;
    } else {
        std::cout << target << " not found" << std::endl;
    }
    
    return 0;
}
```

#### 应用2：汉诺塔

```cpp
#include <iostream>

void hanoi(int n, char from, char to, char aux) {
    if (n == 1) {
        std::cout << "Move disk 1 from " << from << " to " << to << std::endl;
        return;
    }
    
    // 将n-1个盘子从from移动到aux
    hanoi(n - 1, from, aux, to);
    
    // 将第n个盘子从from移动到to
    std::cout << "Move disk " << n << " from " << from << " to " << to << std::endl;
    
    // 将n-1个盘子从aux移动到to
    hanoi(n - 1, aux, to, from);
}

int main() {
    int disks = 3;
    std::cout << "Solving Tower of Hanoi with " << disks << " disks:" << std::endl;
    hanoi(disks, 'A', 'C', 'B');
    
    return 0;
}
```

#### 应用3：快速排序

```cpp
#include <iostream>
#include <vector>

int partition(std::vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    
    for (int j = low; j < high; ++j) {
        if (arr[j] <= pivot) {
            ++i;
            std::swap(arr[i], arr[j]);
        }
    }
    
    std::swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(std::vector<int>& arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int main() {
    std::vector<int> arr = {10, 7, 8, 9, 1, 5};
    
    std::cout << "Original: ";
    for (int x : arr) std::cout << x << " ";
    std::cout << std::endl;
    
    quickSort(arr, 0, arr.size() - 1);
    
    std::cout << "Sorted:   ";
    for (int x : arr) std::cout << x << " ";
    std::cout << std::endl;
    
    return 0;
}
```

### 9.4 递归的注意事项

```cpp
#include <iostream>

// 尾递归优化示例
long long factorialTailRecursive(int n, long long accumulator = 1) {
    if (n <= 1) {
        return accumulator;
    }
    return factorialTailRecursive(n - 1, n * accumulator);
}

// 记忆化递归（避免重复计算）
#include <unordered_map>

std::unordered_map<int, long long> memo;

long long fibonacciMemo(int n) {
    if (n <= 0) return 0;
    if (n == 1) return 1;
    
    // 检查是否已经计算过
    if (memo.find(n) != memo.end()) {
        return memo[n];
    }
    
    // 计算并存储结果
    memo[n] = fibonacciMemo(n - 1) + fibonacciMemo(n - 2);
    return memo[n];
}

int main() {
    std::cout << "Factorial (tail recursive): " << factorialTailRecursive(10) << std::endl;
    std::cout << "Fibonacci (memoized): " << fibonacciMemo(50) << std::endl;
    
    return 0;
}
```

---

## 10. 内联函数

### 10.1 基本概念

内联函数建议编译器将函数调用替换为函数体，减少调用开销。

```cpp
#include <iostream>

// 内联函数
inline int square(int x) {
    return x * x;
}

inline int max(int a, int b) {
    return (a > b) ? a : b;
}

int main() {
    std::cout << "Square of 5: " << square(5) << std::endl;
    std::cout << "Max of 3 and 7: " << max(3, 7) << std::endl;
    
    return 0;
}
```

### 10.2 内联函数的适用场景

```cpp
#include <iostream>

// 适合内联：简单、频繁调用
inline double degreesToRadians(double degrees) {
    return degrees * 3.14159265358979 / 180.0;
}

inline bool isEven(int n) {
    return n % 2 == 0;
}

// 不适合内联：复杂、递归、包含循环
void complexFunction() {
    for (int i = 0; i < 1000; ++i) {
        std::cout << i << " ";
    }
    std::cout << std::endl;
}

int main() {
    std::cout << "90 degrees = " << degreesToRadians(90) << " radians" << std::endl;
    std::cout << "Is 10 even? " << (isEven(10) ? "Yes" : "No") << std::endl;
    
    complexFunction();
    
    return 0;
}
```

---

## 11. 函数指针

### 11.1 基本用法

```cpp
#include <iostream>

int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}

int multiply(int a, int b) {
    return a * b;
}

int main() {
    // 声明函数指针
    int (*funcPtr)(int, int);
    
    // 指向add函数
    funcPtr = add;
    std::cout << "5 + 3 = " << funcPtr(5, 3) << std::endl;
    
    // 指向subtract函数
    funcPtr = subtract;
    std::cout << "10 - 4 = " << funcPtr(10, 4) << std::endl;
    
    // 指向multiply函数
    funcPtr = multiply;
    std::cout << "6 * 7 = " << funcPtr(6, 7) << std::endl;
    
    return 0;
}
```

### 11.2 函数指针作为参数

```cpp
#include <iostream>
#include <vector>

// 函数指针类型
typedef bool (*CompareFunc)(int, int);

bool ascending(int a, int b) {
    return a < b;
}

bool descending(int a, int b) {
    return a > b;
}

void customSort(std::vector<int>& arr, CompareFunc compare) {
    for (size_t i = 0; i < arr.size() - 1; ++i) {
        for (size_t j = 0; j < arr.size() - i - 1; ++j) {
            if (!compare(arr[j], arr[j + 1])) {
                std::swap(arr[j], arr[j + 1]);
            }
        }
    }
}

void printArray(const std::vector<int>& arr) {
    for (int x : arr) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
}

int main() {
    std::vector<int> numbers = {5, 2, 8, 1, 9, 3};
    
    std::cout << "Original: ";
    printArray(numbers);
    
    customSort(numbers, ascending);
    std::cout << "Ascending: ";
    printArray(numbers);
    
    customSort(numbers, descending);
    std::cout << "Descending: ";
    printArray(numbers);
    
    return 0;
}
```

### 11.3 函数指针数组

```cpp
#include <iostream>

int add(int a, int b) { return a + b; }
int subtract(int a, int b) { return a - b; }
int multiply(int a, int b) { return a * b; }
int divide(int a, int b) { return b != 0 ? a / b : 0; }

int main() {
    // 函数指针数组
    int (*operations[])(int, int) = {add, subtract, multiply, divide};
    const char* opNames[] = {"Add", "Subtract", "Multiply", "Divide"};
    
    int a = 10, b = 5;
    
    for (int i = 0; i < 4; ++i) {
        std::cout << opNames[i] << ": " << operations[i](a, b) << std::endl;
    }
    
    return 0;
}
```

---

## 12. lambda表达式（C++11）

### 12.1 基本语法

```cpp
[capture](parameters) -> return_type {
    // 函数体
}
```

### 12.2 基本示例

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    // 简单的lambda
    auto add = [](int a, int b) {
        return a + b;
    };
    
    std::cout << "5 + 3 = " << add(5, 3) << std::endl;
    
    // 带捕获的lambda
    int multiplier = 10;
    auto multiply = [multiplier](int x) {
        return x * multiplier;
    };
    
    std::cout << "5 * 10 = " << multiply(5) << std::endl;
    
    // 在算法中使用lambda
    std::vector<int> numbers = {5, 2, 8, 1, 9, 3};
    
    std::sort(numbers.begin(), numbers.end(), [](int a, int b) {
        return a > b;  // 降序排序
    });
    
    std::cout << "Sorted (descending): ";
    for (int x : numbers) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

### 12.3 捕获列表

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    int x = 10;
    int y = 20;
    
    // 不捕获任何变量
    auto noCapture = []() {
        return 42;
    };
    
    // 按值捕获
    auto byValue = [x, y]() {
        return x + y;
    };
    
    // 按引用捕获
    auto byRef = [&x, &y]() {
        x = 100;
        y = 200;
        return x + y;
    };
    
    // 捕获所有局部变量（按值）
    auto captureAllByValue = [=]() {
        return x + y;
    };
    
    // 捕获所有局部变量（按引用）
    auto captureAllByRef = [&]() {
        x = 300;
        return x + y;
    };
    
    std::cout << "No capture: " << noCapture() << std::endl;
    std::cout << "By value: " << byValue() << std::endl;
    std::cout << "By ref: " << byRef() << std::endl;
    std::cout << "After byRef - x: " << x << ", y: " << y << std::endl;
    
    return 0;
}
```

### 12.4 实际应用

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <functional>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    
    // 使用lambda过滤偶数
    std::vector<int> evens;
    std::copy_if(numbers.begin(), numbers.end(), std::back_inserter(evens),
                 [](int x) { return x % 2 == 0; });
    
    std::cout << "Even numbers: ";
    for (int x : evens) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
    
    // 使用lambda转换
    std::vector<int> squares;
    std::transform(numbers.begin(), numbers.end(), std::back_inserter(squares),
                   [](int x) { return x * x; });
    
    std::cout << "Squares: ";
    for (int x : squares) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
    
    // 使用lambda累加
    int sum = std::accumulate(numbers.begin(), numbers.end(), 0,
                              [](int acc, int x) { return acc + x; });
    
    std::cout << "Sum: " << sum << std::endl;
    
    return 0;
}
```

---

## 13. 本章小结

### 13.1 核心概念回顾

1. **函数定义和声明**
   - 函数由返回类型、名称、参数列表和函数体组成
   - 函数原型告诉编译器函数的接口
   - 函数定义提供完整实现

2. **参数传递**
   - 值传递：创建副本，安全但有开销
   - 引用传递：直接操作原值，高效
   - const引用：高效且安全
   - 指针传递：灵活但需检查nullptr

3. **返回值**
   - 可以返回基本类型、对象、指针、引用
   - 使用结构体、pair、tuple返回多个值
   - void表示无返回值

4. **默认参数**
   - 提供合理的默认值
   - 从右到左指定
   - 提高函数灵活性

5. **函数重载**
   - 同名函数，不同参数列表
   - 编译器根据参数选择合适版本
   - 提高代码可读性

6. **递归函数**
   - 函数调用自身
   - 必须有基准情况
   - 注意栈溢出风险

7. **内联函数**
   - 建议编译器展开函数
   - 适合简单、频繁调用的函数
   - 减少调用开销

8. **函数指针**
   - 指向函数的指针
   - 可以作为参数传递
   - 实现回调机制

9. **lambda表达式**
   - 匿名函数
   - 简洁的语法
   - 强大的捕获机制

### 13.2 最佳实践

- **单一职责**：每个函数只做一件事
- **合理命名**：函数名应清晰表达功能
- **参数验证**：检查输入的有效性
- **避免全局变量**：使用参数传递数据
- **文档注释**：说明函数的用途、参数和返回值
- **保持简洁**：函数不宜过长

### 13.3 常见陷阱

| 陷阱 | 原因 | 解决方案 |
|------|------|----------|
| 忘记返回 | 非void函数缺少return | 确保所有路径都有返回 |
| 悬垂引用 | 返回局部变量的引用 | 返回值或使用静态变量 |
| 无限递归 | 缺少基准情况 | 确保递归能终止 |
| 参数混淆 | 重载函数签名相似 | 使用不同的函数名 |
| 默认参数顺序 | 默认参数不在右侧 | 从右到左指定默认值 |

---

## 14. 练习题

### 基础练习

1. **简单函数**
   ```cpp
   // 编写函数，计算两个整数的最大公约数（GCD）
   ```

2. **参数传递**
   ```cpp
   // 编写函数，交换两个整数的值
   // 分别使用指针和引用实现
   ```

3. **返回值**
   ```cpp
   // 编写函数，判断一个数是否为素数
   // 返回布尔值
   ```

### 中级练习

4. **默认参数**
   ```cpp
   // 编写函数，计算幂运算
   // 默认指数为2（计算平方）
   ```

5. **函数重载**
   ```cpp
   // 重载print函数，支持int、double、string类型
   ```

6. **递归函数**
   ```cpp
   // 使用递归计算x的n次幂
   ```

### 高级练习

7. **函数指针**
   ```cpp
   // 实现一个简单的计算器
   // 使用函数指针数组存储加减乘除操作
   ```

8. **lambda表达式**
   ```cpp
   // 使用lambda和STL算法对vector进行排序、过滤、转换
   ```

9. **综合应用**
   ```cpp
   // 实现一个学生成绩管理系统
   // 使用函数模块化设计
   // 支持添加、删除、查询、统计功能
   ```

10. **递归算法**
    ```cpp
    // 使用递归实现归并排序
    ```

---

**学习建议：**
- 多练习函数的设计和实现
- 理解不同参数传递方式的区别
- 掌握递归的思维和实现技巧
- 熟悉函数重载的规则
- 学会使用lambda表达式简化代码
- 通过实际项目巩固所学知识

通过本章的学习，您应该能够熟练运用函数组织代码，为编写模块化、可维护的程序打下坚实的基础。

### 15. 高级主题深入

#### 15.1 可变参数模板（C++11）

```cpp
#include <iostream>

// 基准情况
void print() {
    std::cout << std::endl;
}

// 递归情况
template<typename T, typename... Args>
void print(const T& first, const Args&... args) {
    std::cout << first << " ";
    print(args...);
}

int main() {
    print(1, 2.5, "Hello", 'A', true);
    print("Multiple", "arguments", "of", "different", "types");
    
    return 0;
}
```

#### 15.2 constexpr函数（C++11/14）

```cpp
#include <iostream>

// constexpr函数可以在编译时求值
constexpr int factorial(int n) {
    return (n <= 1) ? 1 : n * factorial(n - 1);
}

constexpr int power(int base, int exp) {
    return (exp == 0) ? 1 : base * power(base, exp - 1);
}

int main() {
    // 编译时常量
    constexpr int fact5 = factorial(5);
    constexpr int pow2_10 = power(2, 10);
    
    std::cout << "5! = " << fact5 << std::endl;
    std::cout << "2^10 = " << pow2_10 << std::endl;
    
    // 也可以在运行时使用
    int x = 6;
    std::cout << x << "! = " << factorial(x) << std::endl;
    
    return 0;
}
```

#### 15.3 noexcept说明符

```cpp
#include <iostream>
#include <stdexcept>

// 声明函数不会抛出异常
int add(int a, int b) noexcept {
    return a + b;
}

// 可能抛出异常的函数
int divide(int a, int b) {
    if (b == 0) {
        throw std::runtime_error("Division by zero");
    }
    return a / b;
}

void testNoexcept() {
    std::cout << "add is noexcept: " 
              << std::boolalpha 
              << noexcept(add(1, 2)) << std::endl;
    
    std::cout << "divide is noexcept: " 
              << noexcept(divide(1, 2)) << std::endl;
}

int main() {
    testNoexcept();
    
    try {
        std::cout << "10 / 2 = " << divide(10, 2) << std::endl;
        std::cout << "10 / 0 = " << divide(10, 0) << std::endl;
    } catch (const std::exception& e) {
        std::cerr << "Error: " << e.what() << std::endl;
    }
    
    return 0;
}
```

### 16. 实际项目案例

#### 16.1 函数式编程工具库

```cpp
#include <iostream>
#include <vector>
#include <functional>
#include <algorithm>
#include <numeric>

template<typename T>
class FunctionalUtils {
public:
    // Map: 对每个元素应用函数
    static std::vector<T> map(const std::vector<T>& input, 
                              std::function<T(const T&)> func) {
        std::vector<T> result;
        std::transform(input.begin(), input.end(), 
                      std::back_inserter(result), func);
        return result;
    }
    
    // Filter: 过滤满足条件的元素
    static std::vector<T> filter(const std::vector<T>& input,
                                 std::function<bool(const T&)> predicate) {
        std::vector<T> result;
        std::copy_if(input.begin(), input.end(),
                    std::back_inserter(result), predicate);
        return result;
    }
    
    // Reduce: 累积操作
    static T reduce(const std::vector<T>& input,
                   T initial,
                   std::function<T(const T&, const T&)> operation) {
        return std::accumulate(input.begin(), input.end(), 
                              initial, operation);
    }
    
    // ForEach: 对每个元素执行操作
    static void forEach(const std::vector<T>& input,
                       std::function<void(const T&)> action) {
        std::for_each(input.begin(), input.end(), action);
    }
};

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    
    // Map: 计算平方
    auto squares = FunctionalUtils<int>::map(numbers, [](int x) {
        return x * x;
    });
    
    std::cout << "Squares: ";
    for (int x : squares) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
    
    // Filter: 筛选偶数
    auto evens = FunctionalUtils<int>::filter(numbers, [](int x) {
        return x % 2 == 0;
    });
    
    std::cout << "Evens: ";
    for (int x : evens) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
    
    // Reduce: 计算总和
    int sum = FunctionalUtils<int>::reduce(numbers, 0, [](int a, int b) {
        return a + b;
    });
    
    std::cout << "Sum: " << sum << std::endl;
    
    // ForEach: 打印每个元素
    std::cout << "Elements: ";
    FunctionalUtils<int>::forEach(numbers, [](int x) {
        std::cout << x << " ";
    });
    std::cout << std::endl;
    
    return 0;
}
```

#### 16.2 回调系统

```cpp
#include <iostream>
#include <vector>
#include <functional>
#include <string>
#include <map>

class EventSystem {
private:
    std::map<std::string, std::vector<std::function<void(const std::string&)>>> handlers;
    
public:
    // 注册事件处理器
    void on(const std::string& eventName, 
            std::function<void(const std::string&)> handler) {
        handlers[eventName].push_back(handler);
    }
    
    // 触发事件
    void emit(const std::string& eventName, const std::string& data = "") {
        auto it = handlers.find(eventName);
        if (it != handlers.end()) {
            for (const auto& handler : it->second) {
                handler(data);
            }
        }
    }
    
    // 移除所有处理器
    void clear(const std::string& eventName) {
        handlers.erase(eventName);
    }
};

int main() {
    EventSystem events;
    
    // 注册事件处理器
    events.on("message", [](const std::string& data) {
        std::cout << "[Message] " << data << std::endl;
    });
    
    events.on("error", [](const std::string& data) {
        std::cerr << "[Error] " << data << std::endl;
    });
    
    events.on("log", [](const std::string& data) {
        std::cout << "[Log] " << data << std::endl;
    });
    
    // 触发事件
    events.emit("message", "Hello, World!");
    events.emit("log", "Application started");
    events.emit("error", "Something went wrong");
    
    return 0;
}
```

#### 16.3 策略模式实现

```cpp
#include <iostream>
#include <functional>
#include <vector>
#include <algorithm>

template<typename T>
class Sorter {
private:
    std::function<bool(const T&, const T&)> comparison;
    
public:
    Sorter(std::function<bool(const T&, const T&)> comp) 
        : comparison(comp) {}
    
    void sort(std::vector<T>& arr) {
        std::sort(arr.begin(), arr.end(), comparison);
    }
};

int main() {
    std::vector<int> numbers = {5, 2, 8, 1, 9, 3, 7, 4, 6};
    
    // 升序排序
    Sorter<int> ascendingSorter([](int a, int b) {
        return a < b;
    });
    
    std::vector<int> ascNumbers = numbers;
    ascendingSorter.sort(ascNumbers);
    
    std::cout << "Ascending: ";
    for (int x : ascNumbers) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
    
    // 降序排序
    Sorter<int> descendingSorter([](int a, int b) {
        return a > b;
    });
    
    std::vector<int> descNumbers = numbers;
    descendingSorter.sort(descNumbers);
    
    std::cout << "Descending: ";
    for (int x : descNumbers) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

### 17. 性能优化技巧

#### 17.1 函数调用开销分析

```cpp
#include <iostream>
#include <chrono>
#include <cmath>

// 普通函数
double calculateSquare(double x) {
    return x * x;
}

// 内联函数
inline double inlineSquare(double x) {
    return x * x;
}

// 宏定义
#define MACRO_SQUARE(x) ((x) * (x))

void measurePerformance() {
    const int ITERATIONS = 10000000;
    double value = 3.14159;
    volatile double result;
    
    // 测试普通函数
    auto start = std::chrono::high_resolution_clock::now();
    for (int i = 0; i < ITERATIONS; ++i) {
        result = calculateSquare(value);
    }
    auto end = std::chrono::high_resolution_clock::now();
    std::chrono::duration<double> normalTime = end - start;
    
    // 测试内联函数
    start = std::chrono::high_resolution_clock::now();
    for (int i = 0; i < ITERATIONS; ++i) {
        result = inlineSquare(value);
    }
    end = std::chrono::high_resolution_clock::now();
    std::chrono::duration<double> inlineTime = end - start;
    
    // 测试宏
    start = std::chrono::high_resolution_clock::now();
    for (int i = 0; i < ITERATIONS; ++i) {
        result = MACRO_SQUARE(value);
    }
    end = std::chrono::high_resolution_clock::now();
    std::chrono::duration<double> macroTime = end - start;
    
    std::cout << "Performance comparison (" << ITERATIONS << " iterations):" << std::endl;
    std::cout << "Normal function: " << normalTime.count() << " seconds" << std::endl;
    std::cout << "Inline function: " << inlineTime.count() << " seconds" << std::endl;
    std::cout << "Macro: " << macroTime.count() << " seconds" << std::endl;
}

int main() {
    measurePerformance();
    return 0;
}
```

#### 17.2 尾递归优化

```cpp
#include <iostream>

// 普通递归（可能导致栈溢出）
long long factorialNormal(int n) {
    if (n <= 1) return 1;
    return n * factorialNormal(n - 1);
}

// 尾递归（编译器可以优化）
long long factorialTail(int n, long long accumulator = 1) {
    if (n <= 1) return accumulator;
    return factorialTail(n - 1, n * accumulator);
}

// 迭代版本（最优）
long long factorialIterative(int n) {
    long long result = 1;
    for (int i = 2; i <= n; ++i) {
        result *= i;
    }
    return result;
}

int main() {
    std::cout << "Factorial of 20:" << std::endl;
    std::cout << "Normal: " << factorialNormal(20) << std::endl;
    std::cout << "Tail: " << factorialTail(20) << std::endl;
    std::cout << "Iterative: " << factorialIterative(20) << std::endl;
    
    return 0;
}
```

### 18. 调试技巧

#### 18.1 函数调用跟踪

```cpp
#include <iostream>
#include <string>

class FunctionTracer {
private:
    std::string functionName;
    static int indentLevel;
    
public:
    FunctionTracer(const std::string& name) 
        : functionName(name) {
        printIndent();
        std::cout << "Enter: " << functionName << std::endl;
        ++indentLevel;
    }
    
    ~FunctionTracer() {
        --indentLevel;
        printIndent();
        std::cout << "Exit: " << functionName << std::endl;
    }
    
private:
    void printIndent() {
        for (int i = 0; i < indentLevel; ++i) {
            std::cout << "  ";
        }
    }
};

int FunctionTracer::indentLevel = 0;

// 使用示例
void functionA() {
    FunctionTracer tracer("functionA");
    functionB();
}

void functionB() {
    FunctionTracer tracer("functionB");
    functionC();
}

void functionC() {
    FunctionTracer tracer("functionC");
}

int main() {
    functionA();
    return 0;
}
```

#### 18.2 参数验证宏

```cpp
#include <iostream>
#include <stdexcept>
#include <cassert>

// 参数验证宏
#define REQUIRE(condition, message) \
    if (!(condition)) { \
        throw std::invalid_argument(message); \
    }

#define ENSURE(condition, message) \
    if (!(condition)) { \
        throw std::logic_error(message); \
    }

int safeDivide(int a, int b) {
    REQUIRE(b != 0, "Divisor cannot be zero");
    return a / b;
}

int factorial(int n) {
    REQUIRE(n >= 0, "Factorial requires non-negative input");
    REQUIRE(n <= 20, "Input too large for factorial");
    
    if (n <= 1) {
        ENSURE(n >= 0, "Base case should be non-negative");
        return 1;
    }
    
    int result = n * factorial(n - 1);
    ENSURE(result > 0, "Result should be positive");
    return result;
}

int main() {
    try {
        std::cout << "10 / 2 = " << safeDivide(10, 2) << std::endl;
        std::cout << "10 / 0 = " << safeDivide(10, 0) << std::endl;
    } catch (const std::exception& e) {
        std::cerr << "Error: " << e.what() << std::endl;
    }
    
    try {
        std::cout << "5! = " << factorial(5) << std::endl;
        std::cout << "-1! = " << factorial(-1) << std::endl;
    } catch (const std::exception& e) {
        std::cerr << "Error: " << e.what() << std::endl;
    }
    
    return 0;
}
```

### 19. 设计模式中的函数应用

#### 19.1 命令模式

```cpp
#include <iostream>
#include <functional>
#include <vector>
#include <string>

class Command {
private:
    std::function<void()> execute;
    std::function<void()> undo;
    std::string description;
    
public:
    Command(std::function<void()> exec, 
            std::function<void()> und,
            const std::string& desc)
        : execute(exec), undo(und), description(desc) {}
    
    void executeCommand() {
        std::cout << "Executing: " << description << std::endl;
        execute();
    }
    
    void undoCommand() {
        std::cout << "Undoing: " << description << std::endl;
        undo();
    }
};

class CommandHistory {
private:
    std::vector<Command> history;
    size_t currentIndex;
    
public:
    CommandHistory() : currentIndex(0) {}
    
    void addCommand(const Command& cmd) {
        // 移除当前位置之后的命令
        history.erase(history.begin() + currentIndex, history.end());
        history.push_back(cmd);
        ++currentIndex;
    }
    
    void undo() {
        if (currentIndex > 0) {
            --currentIndex;
            history[currentIndex].undoCommand();
        } else {
            std::cout << "Nothing to undo" << std::endl;
        }
    }
    
    void redo() {
        if (currentIndex < history.size()) {
            history[currentIndex].executeCommand();
            ++currentIndex;
        } else {
            std::cout << "Nothing to redo" << std::endl;
        }
    }
};

int main() {
    CommandHistory history;
    
    int value = 0;
    
    // 添加命令
    history.addCommand(Command(
        [&value]() { value += 10; },
        [&value]() { value -= 10; },
        "Add 10"
    ));
    
    history.addCommand(Command(
        [&value]() { value *= 2; },
        [&value]() { value /= 2; },
        "Multiply by 2"
    ));
    
    history.addCommand(Command(
        [&value]() { value += 5; },
        [&value]() { value -= 5; },
        "Add 5"
    ));
    
    // 执行所有命令
    for (size_t i = 0; i < 3; ++i) {
        history.redo();
    }
    
    std::cout << "Current value: " << value << std::endl;
    
    // 撤销
    history.undo();
    history.undo();
    
    std::cout << "After undo: " << value << std::endl;
    
    return 0;
}
```

#### 19.2 观察者模式

```cpp
#include <iostream>
#include <vector>
#include <functional>
#include <string>

class Subject {
private:
    std::vector<std::function<void(const std::string&)>> observers;
    
public:
    void addObserver(std::function<void(const std::string&)> observer) {
        observers.push_back(observer);
    }
    
    void notify(const std::string& message) {
        for (const auto& observer : observers) {
            observer(message);
        }
    }
};

int main() {
    Subject subject;
    
    // 添加观察者
    subject.addObserver([](const std::string& msg) {
        std::cout << "[Logger] " << msg << std::endl;
    });
    
    subject.addObserver([](const std::string& msg) {
        std::cout << "[Email] Sending: " << msg << std::endl;
    });
    
    subject.addObserver([](const std::string& msg) {
        std::cout << "[SMS] Sending: " << msg << std::endl;
    });
    
    // 通知所有观察者
    std::cout << "Notifying observers..." << std::endl;
    subject.notify("System update completed");
    
    return 0;
}
```

### 20. 测试和验证

#### 20.1 单元测试框架

```cpp
#include <iostream>
#include <string>
#include <functional>
#include <vector>
#include <sstream>

struct TestResult {
    std::string testName;
    bool passed;
    std::string message;
};

class TestSuite {
private:
    std::vector<TestResult> results;
    
public:
    void runTest(const std::string& name, std::function<bool()> test) {
        TestResult result;
        result.testName = name;
        
        try {
            result.passed = test();
            result.message = result.passed ? "PASSED" : "FAILED";
        } catch (const std::exception& e) {
            result.passed = false;
            result.message = std::string("EXCEPTION: ") + e.what();
        }
        
        results.push_back(result);
        
        std::cout << "[" << (result.passed ? "PASS" : "FAIL") << "] "
                  << name << ": " << result.message << std::endl;
    }
    
    void assertEqual(int expected, int actual, const std::string& msg = "") {
        if (expected != actual) {
            std::ostringstream oss;
            oss << "Expected " << expected << ", got " << actual;
            if (!msg.empty()) oss << " (" << msg << ")";
            throw std::runtime_error(oss.str());
        }
    }
    
    void assertTrue(bool condition, const std::string& msg = "") {
        if (!condition) {
            throw std::runtime_error(msg.empty() ? "Assertion failed" : msg);
        }
    }
    
    void printSummary() const {
        int total = results.size();
        int passed = 0;
        
        for (const auto& result : results) {
            if (result.passed) {
                ++passed;
            }
        }
        
        std::cout << "\n=== Test Summary ===" << std::endl;
        std::cout << "Total: " << total << std::endl;
        std::cout << "Passed: " << passed << std::endl;
        std::cout << "Failed: " << (total - passed) << std::endl;
    }
};

// 被测试的函数
int add(int a, int b) {
    return a + b;
}

int multiply(int a, int b) {
    return a * b;
}

bool isEven(int n) {
    return n % 2 == 0;
}

int main() {
    TestSuite suite;
    
    // 测试add函数
    suite.runTest("add(2, 3) == 5", [&]() {
        suite.assertEqual(5, add(2, 3));
        return true;
    });
    
    suite.runTest("add(-1, 1) == 0", [&]() {
        suite.assertEqual(0, add(-1, 1));
        return true;
    });
    
    // 测试multiply函数
    suite.runTest("multiply(3, 4) == 12", [&]() {
        suite.assertEqual(12, multiply(3, 4));
        return true;
    });
    
    // 测试isEven函数
    suite.runTest("isEven(4) == true", [&]() {
        suite.assertTrue(isEven(4));
        return true;
    });
    
    suite.runTest("isEven(3) == false", [&]() {
        suite.assertTrue(!isEven(3));
        return true;
    });
    
    suite.printSummary();
    
    return 0;
}
```

### 21. 扩展阅读和学习资源

#### 21.1 推荐书籍

1. **《Effective C++》** - Scott Meyers
   - 55个改善C++程序的具体方法
   - 函数设计和使用的最佳实践

2. **《More Effective C++》** - Scott Meyers
   - 35个新的改善建议
   - 深入探讨函数和参数传递

3. **《Functional Programming in C++》** - Ivan Čukić
   - 函数式编程技术
   - lambda和高阶函数

4. **《C++ Templates: The Complete Guide》** - David Vandevoorde
   - 模板元编程
   - 可变参数模板

#### 21.2 在线资源

1. **cppreference.com**
   - 权威的C++参考文档
   - 函数、lambda、模板的详细文档

2. **Stack Overflow**
   - 问答社区
   - 解决具体函数相关问题

3. **GitHub**
   - 开源项目
   - 学习优秀的函数设计

4. **Reddit r/cpp**
   - C++社区讨论
   - 最新语言和库特性

#### 21.3 练习平台

1. **LeetCode**
   - 算法练习
   - 函数设计和实现

2. **HackerRank**
   - 编程挑战
   - 函数式编程专题

3. **Codewars**
   - 编程kata
   - 函数组合和变换

4. **Exercism**
   - 导师指导
   - 代码审查和重构

---

**结语：**

函数是C++编程的核心构建块，它们让代码模块化、可复用、易维护。通过本章的学习，您已经掌握了：

- 函数的定义、声明和调用
- 各种参数传递方式的区别和应用
- 返回值的处理和多值返回技巧
- 默认参数和函数重载的使用
- 递归思维和实现技巧
- 内联函数和性能优化
- 函数指针和回调机制
- lambda表达式和函数式编程

这些技能将使您能够编写更加结构化、高效的程序。记住，好的函数设计不仅仅是语法正确，更重要的是接口清晰、职责单一、易于测试。继续练习，不断反思和改进您的函数设计，您的编程技能将会不断提升。

祝您在C++学习的道路上越走越远，创造出更多精彩的程序！

### 22. 常见错误和最佳实践

#### 22.1 常见错误总结

```cpp
#include <iostream>
#include <string>

// 错误1：忘记返回值
int getValue() {
    // 缺少return语句 - 编译警告/错误
    // return 42;
}

// 错误2：返回局部变量的引用
int& getBadReference() {
    int local = 10;
    // return local;  // 错误！返回悬垂引用
    static int value = 10;  // 正确：使用static
    return value;
}

// 错误3：默认参数顺序错误
// void func(int a = 10, int b);  // 错误！
void func(int a, int b = 10);  // 正确

// 错误4：重载歧义
void print(int x) {
    std::cout << "int: " << x << std::endl;
}

void print(double x) {
    std::cout << "double: " << x << std::endl;
}

// print(5);  // 调用print(int)
// print(5.0);  // 调用print(double)
// print('A');  // char提升为int，调用print(int)

// 错误5：递归没有终止条件
// void infiniteRecursion() {
//     infiniteRecursion();  // 无限递归，栈溢出！
// }

int main() {
    func(5);
    func(5, 20);
    
    print(10);
    print(3.14);
    
    return 0;
}
```

#### 22.2 代码重构技巧

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// 重构前：长函数，多个职责
void processDataOld(std::vector<int>& data) {
    // 验证
    if (data.empty()) {
        std::cout << "Empty data" << std::endl;
        return;
    }
    
    // 排序
    for (size_t i = 0; i < data.size() - 1; ++i) {
        for (size_t j = 0; j < data.size() - i - 1; ++j) {
            if (data[j] > data[j + 1]) {
                std::swap(data[j], data[j + 1]);
            }
        }
    }
    
    // 计算统计信息
    int sum = 0;
    for (int x : data) {
        sum += x;
    }
    double avg = static_cast<double>(sum) / data.size();
    
    // 打印结果
    std::cout << "Sorted data: ";
    for (int x : data) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
    std::cout << "Average: " << avg << std::endl;
}

// 重构后：拆分为小函数
bool validateData(const std::vector<int>& data) {
    return !data.empty();
}

void sortData(std::vector<int>& data) {
    std::sort(data.begin(), data.end());
}

double calculateAverage(const std::vector<int>& data) {
    if (data.empty()) return 0.0;
    
    int sum = 0;
    for (int x : data) {
        sum += x;
    }
    return static_cast<double>(sum) / data.size();
}

void printData(const std::vector<int>& data) {
    std::cout << "Sorted data: ";
    for (int x : data) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
}

void processDataNew(std::vector<int>& data) {
    if (!validateData(data)) {
        std::cout << "Empty data" << std::endl;
        return;
    }
    
    sortData(data);
    double avg = calculateAverage(data);
    printData(data);
    std::cout << "Average: " << avg << std::endl;
}

int main() {
    std::vector<int> data = {5, 2, 8, 1, 9, 3};
    processDataNew(data);
    return 0;
}
```

### 23. 实际工程应用

#### 23.1 插件系统架构

```cpp
#include <iostream>
#include <vector>
#include <functional>
#include <string>
#include <map>

class Plugin {
private:
    std::string name;
    std::function<void()> initialize;
    std::function<void()> execute;
    std::function<void()> cleanup;
    
public:
    Plugin(const std::string& n,
           std::function<void()> init,
           std::function<void()> exec,
           std::function<void()> clean)
        : name(n), initialize(init), execute(exec), cleanup(clean) {}
    
    void init() {
        std::cout << "Initializing plugin: " << name << std::endl;
        initialize();
    }
    
    void run() {
        std::cout << "Running plugin: " << name << std::endl;
        execute();
    }
    
    void shutdown() {
        std::cout << "Shutting down plugin: " << name << std::endl;
        cleanup();
    }
    
    const std::string& getName() const {
        return name;
    }
};

class PluginManager {
private:
    std::map<std::string, Plugin> plugins;
    
public:
    void registerPlugin(const Plugin& plugin) {
        plugins[plugin.getName()] = plugin;
    }
    
    void initializeAll() {
        for (auto& pair : plugins) {
            pair.second.init();
        }
    }
    
    void executeAll() {
        for (auto& pair : plugins) {
            pair.second.run();
        }
    }
    
    void shutdownAll() {
        for (auto& pair : plugins) {
            pair.second.shutdown();
        }
    }
};

int main() {
    PluginManager manager;
    
    // 注册插件
    manager.registerPlugin(Plugin("Logger",
        []() { std::cout << "  Logger initialized" << std::endl; },
        []() { std::cout << "  Logging..." << std::endl; },
        []() { std::cout << "  Logger cleaned up" << std::endl; }
    ));
    
    manager.registerPlugin(Plugin("Database",
        []() { std::cout << "  Database connected" << std::endl; },
        []() { std::cout << "  Querying database..." << std::endl; },
        []() { std::cout << "  Database disconnected" << std::endl; }
    ));
    
    manager.registerPlugin(Plugin("Cache",
        []() { std::cout << "  Cache warmed up" << std::endl; },
        []() { std::cout << "  Serving from cache..." << std::endl; },
        []() { std::cout << "  Cache cleared" << std::endl; }
    ));
    
    // 生命周期管理
    std::cout << "=== Initialization ===" << std::endl;
    manager.initializeAll();
    
    std::cout << "\n=== Execution ===" << std::endl;
    manager.executeAll();
    
    std::cout << "\n=== Shutdown ===" << std::endl;
    manager.shutdownAll();
    
    return 0;
}
```

#### 23.2 任务调度器

```cpp
#include <iostream>
#include <vector>
#include <functional>
#include <string>
#include <chrono>
#include <thread>

class Task {
private:
    std::string name;
    std::function<void()> func;
    int priority;
    
public:
    Task(const std::string& n, std::function<void()> f, int p = 0)
        : name(n), func(f), priority(p) {}
    
    void execute() {
        std::cout << "[Priority " << priority << "] Executing: " << name << std::endl;
        func();
    }
    
    int getPriority() const {
        return priority;
    }
    
    const std::string& getName() const {
        return name;
    }
};

class TaskScheduler {
private:
    std::vector<Task> tasks;
    
public:
    void addTask(const Task& task) {
        tasks.push_back(task);
        // 按优先级排序（高优先级在前）
        std::sort(tasks.begin(), tasks.end(),
                  [](const Task& a, const Task& b) {
                      return a.getPriority() > b.getPriority();
                  });
    }
    
    void executeAll() {
        std::cout << "Executing tasks in priority order:" << std::endl;
        for (auto& task : tasks) {
            task.execute();
        }
    }
    
    void executeByName(const std::string& name) {
        for (auto& task : tasks) {
            if (task.getName() == name) {
                task.execute();
                return;
            }
        }
        std::cout << "Task not found: " << name << std::endl;
    }
};

int main() {
    TaskScheduler scheduler;
    
    scheduler.addTask(Task("Backup", []() {
        std::cout << "  Performing backup..." << std::endl;
    }, 3));
    
    scheduler.addTask(Task("Cleanup", []() {
        std::cout << "  Cleaning temporary files..." << std::endl;
    }, 1));
    
    scheduler.addTask(Task("Report", []() {
        std::cout << "  Generating report..." << std::endl;
    }, 2));
    
    scheduler.addTask(Task("Alert", []() {
        std::cout << "  Sending alert..." << std::endl;
    }, 5));
    
    scheduler.executeAll();
    
    return 0;
}
```

### 24. 算法中的函数应用

#### 24.1 高阶函数实现

```cpp
#include <iostream>
#include <vector>
#include <functional>
#include <algorithm>

// Map: 转换每个元素
template<typename T, typename U>
std::vector<U> map(const std::vector<T>& input,
                   std::function<U(const T&)> func) {
    std::vector<U> result;
    std::transform(input.begin(), input.end(),
                  std::back_inserter(result), func);
    return result;
}

// Filter: 过滤元素
template<typename T>
std::vector<T> filter(const std::vector<T>& input,
                      std::function<bool(const T&)> predicate) {
    std::vector<T> result;
    std::copy_if(input.begin(), input.end(),
                std::back_inserter(result), predicate);
    return result;
}

// Reduce: 累积操作
template<typename T>
T reduce(const std::vector<T>& input,
         T initial,
         std::function<T(const T&, const T&)> operation) {
    return std::accumulate(input.begin(), input.end(),
                          initial, operation);
}

// Compose: 函数组合
template<typename A, typename B, typename C>
std::function<C(A)> compose(std::function<B(A)> f,
                            std::function<C(B)> g) {
    return [f, g](A x) {
        return g(f(x));
    };
}

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    
    // Map: 计算平方
    auto squares = map<int, int>(numbers, [](int x) {
        return x * x;
    });
    
    std::cout << "Squares: ";
    for (int x : squares) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
    
    // Filter: 筛选偶数
    auto evens = filter(numbers, [](int x) {
        return x % 2 == 0;
    });
    
    std::cout << "Evens: ";
    for (int x : evens) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
    
    // Reduce: 计算总和
    int sum = reduce(numbers, 0, [](int a, int b) {
        return a + b;
    });
    
    std::cout << "Sum: " << sum << std::endl;
    
    // Compose: 函数组合
    auto addOne = [](int x) { return x + 1; };
    auto multiplyByTwo = [](int x) { return x * 2; };
    auto addThenMultiply = compose<int, int, int>(addOne, multiplyByTwo);
    
    std::cout << "(5 + 1) * 2 = " << addThenMultiply(5) << std::endl;
    
    return 0;
}
```

#### 24.2 记忆化技术

```cpp
#include <iostream>
#include <unordered_map>
#include <functional>

// 通用记忆化包装器
template<typename ReturnType, typename... Args>
std::function<ReturnType(Args...)> memoize(
    std::function<ReturnType(Args...)> func) {
    
    static std::unordered_map<size_t, ReturnType> cache;
    
    return [func, &cache](Args... args) {
        // 创建哈希键（简化版本）
        size_t hash = 0;
        ((hash ^= std::hash<Args>{}(args) + 0x9e3779b9 + (hash << 6) + (hash >> 2)), ...);
        
        auto it = cache.find(hash);
        if (it != cache.end()) {
            return it->second;
        }
        
        ReturnType result = func(args...);
        cache[hash] = result;
        return result;
    };
}

// 斐波那契数列（带记忆化）
long long fibonacci(int n) {
    if (n <= 0) return 0;
    if (n == 1) return 1;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    auto memoFib = memoize<long long, int>(fibonacci);
    
    std::cout << "Fibonacci sequence:" << std::endl;
    for (int i = 0; i <= 20; ++i) {
        std::cout << "F(" << i << ") = " << memoFib(i) << std::endl;
    }
    
    return 0;
}
```

### 25. 性能分析和优化

#### 25.1 函数性能分析工具

```cpp
#include <iostream>
#include <chrono>
#include <functional>
#include <string>
#include <vector>
#include <map>

class PerformanceProfiler {
private:
    struct FunctionStats {
        std::string name;
        int callCount;
        double totalTime;
        double minTime;
        double maxTime;
        
        FunctionStats(const std::string& n)
            : name(n), callCount(0), totalTime(0),
              minTime(1e9), maxTime(0) {}
    };
    
    std::map<std::string, FunctionStats> stats;
    
public:
    template<typename Func, typename... Args>
    auto profile(const std::string& functionName, Func&& func, Args&&... args) {
        auto start = std::chrono::high_resolution_clock::now();
        
        auto result = func(std::forward<Args>(args)...);
        
        auto end = std::chrono::high_resolution_clock::now();
        std::chrono::duration<double> elapsed = end - start;
        
        double time = elapsed.count();
        
        auto it = stats.find(functionName);
        if (it == stats.end()) {
            stats[functionName] = FunctionStats(functionName);
            it = stats.find(functionName);
        }
        
        it->second.callCount++;
        it->second.totalTime += time;
        it->second.minTime = std::min(it->second.minTime, time);
        it->second.maxTime = std::max(it->second.maxTime, time);
        
        return result;
    }
    
    void printReport() const {
        std::cout << "\n=== Performance Report ===" << std::endl;
        std::cout.width(30);
        std::cout << "Function";
        std::cout.width(10);
        std::cout << "Calls";
        std::cout.width(15);
        std::cout << "Total (s)";
        std::cout.width(15);
        std::cout << "Avg (s)";
        std::cout.width(15);
        std::cout << "Min (s)";
        std::cout.width(15);
        std::cout << "Max (s)";
        std::cout << std::endl;
        
        for (const auto& pair : stats) {
            const auto& s = pair.second;
            double avgTime = s.totalTime / s.callCount;
            
            std::cout.width(30);
            std::cout << s.name;
            std::cout.width(10);
            std::cout << s.callCount;
            std::cout.width(15);
            std::cout << s.totalTime;
            std::cout.width(15);
            std::cout << avgTime;
            std::cout.width(15);
            std::cout << s.minTime;
            std::cout.width(15);
            std::cout << s.maxTime;
            std::cout << std::endl;
        }
    }
};

// 测试函数
void slowFunction() {
    for (int i = 0; i < 1000000; ++i) {
        volatile int x = i * i;
    }
}

void fastFunction() {
    volatile int x = 42;
}

int main() {
    PerformanceProfiler profiler;
    
    // 性能分析
    for (int i = 0; i < 5; ++i) {
        profiler.profile("slowFunction", slowFunction);
        profiler.profile("fastFunction", fastFunction);
    }
    
    profiler.printReport();
    
    return 0;
}
```

### 26. 扩展阅读和学习资源

#### 26.1 推荐书籍

1. **《Clean Code》** - Robert C. Martin
   - 编写清晰可维护的代码
   - 函数设计和命名的最佳实践

2. **《Refactoring》** - Martin Fowler
   - 改善既有代码的设计
   - 函数提取和重组技巧

3. **《Functional Programming in C++》** - Ivan Čukić
   - 函数式编程技术
   - 高阶函数和lambda表达式

4. **《Effective Modern C++》** - Scott Meyers
   - C++11/14最佳实践
   - lambda和std::function的使用

#### 26.2 在线资源

1. **cppreference.com**
   - 权威的C++参考文档
   - 函数、lambda、模板的详细文档

2. **Stack Overflow**
   - 问答社区
   - 解决具体函数相关问题

3. **GitHub**
   - 开源项目
   - 学习优秀的函数设计模式

4. **Reddit r/cpp**
   - C++社区讨论
   - 最新语言和库特性

#### 26.3 练习平台

1. **LeetCode**
   - 算法练习
   - 函数设计和实现

2. **HackerRank**
   - 编程挑战
   - 函数式编程专题

3. **Codewars**
   - 编程kata
   - 函数组合和变换

4. **Exercism**
   - 导师指导
   - 代码审查和重构

---

**最后的建议：**

函数是C++编程中最基本也是最重要的概念之一。它们不仅是代码复用的工具，更是程序设计的基石。通过本章的学习和实践，您已经掌握了：

- 函数的定义、声明和调用机制
- 各种参数传递方式的选择和应用
- 返回值处理和多重返回值的技巧
- 默认参数和函数重载的灵活运用
- 递归思维和算法实现
- 内联函数和性能优化策略
- 函数指针和回调系统的设计
- lambda表达式和函数式编程范式

记住，优秀的程序员不仅会写函数，更会设计出接口清晰、职责单一、易于测试和复用的函数。持续练习，不断反思和改进您的函数设计，您的编程技能将会不断提升。

愿您在C++的世界中不断探索，创造出优雅、高效、可维护的精彩程序！
