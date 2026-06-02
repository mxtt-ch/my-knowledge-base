# C++ Primer Plus 第六版学习笔记 - 第14章：C++中的代码重用

## 目录

- [1. 包含对象成员的类](#1-包含对象成员的类)
- [2. 私有继承](#2-私有继承)
- [3. 保护继承](#3-保护继承)
- [4. 多重继承](#4-多重继承)
- [5. 类模板](#5-类模板)
- [6. 函数模板](#6-函数模板)
- [7. 模板的具体化](#7-模板的具体化)
- [8. 编译器如何处理模板](#8-编译器如何处理模板)
- [9. 本章小结](#9-本章小结)
- [10. 练习题](#10-练习题)

---

## 1. 包含对象成员的类

### 1.1 组合（has-a关系）

```cpp
#include <iostream>
#include <string>

class Engine {
private:
    int cylinders;
    double horsepower;
    
public:
    Engine(int cyl, double hp) : cylinders(cyl), horsepower(hp) {
        std::cout << "Engine created: " << cylinders << " cylinders, " 
                  << horsepower << " HP" << std::endl;
    }
    
    ~Engine() {
        std::cout << "Engine destroyed" << std::endl;
    }
    
    void start() const {
        std::cout << "Engine started with " << horsepower << " HP" << std::endl;
    }
    
    void stop() const {
        std::cout << "Engine stopped" << std::endl;
    }
    
    int getCylinders() const { return cylinders; }
    double getHorsepower() const { return horsepower; }
};

class Transmission {
private:
    std::string type;
    int gears;
    
public:
    Transmission(const std::string& t, int g) : type(t), gears(g) {
        std::cout << "Transmission created: " << type << ", " 
                  << gears << " gears" << std::endl;
    }
    
    ~Transmission() {
        std::cout << "Transmission destroyed" << std::endl;
    }
    
    void shiftUp() const {
        std::cout << "Shifting up in " << type << " transmission" << std::endl;
    }
    
    void shiftDown() const {
        std::cout << "Shifting down in " << type << " transmission" << std::endl;
    }
    
    const std::string& getType() const { return type; }
    int getGears() const { return gears; }
};

// Car包含Engine和Transmission（has-a关系）
class Car {
private:
    std::string model;
    std::string color;
    Engine engine;           // 对象成员
    Transmission transmission; // 对象成员
    
public:
    Car(const std::string& m, const std::string& c, 
        int cyl, double hp, const std::string& transType, int gears)
        : model(m), color(c), 
          engine(cyl, hp), 
          transmission(transType, gears) {
        std::cout << "Car created: " << model << std::endl;
    }
    
    ~Car() {
        std::cout << "Car destroyed: " << model << std::endl;
    }
    
    void drive() const {
        std::cout << "\nDriving " << color << " " << model << ":" << std::endl;
        engine.start();
        transmission.shiftUp();
        std::cout << "Car is moving..." << std::endl;
    }
    
    void park() const {
        std::cout << "\nParking " << model << ":" << std::endl;
        transmission.shiftDown();
        engine.stop();
    }
    
    void displaySpecs() const {
        std::cout << "\n=== Car Specifications ===" << std::endl;
        std::cout << "Model: " << model << std::endl;
        std::cout << "Color: " << color << std::endl;
        std::cout << "Engine: " << engine.getCylinders() << " cylinders, "
                  << engine.getHorsepower() << " HP" << std::endl;
        std::cout << "Transmission: " << transmission.getType() << ", "
                  << transmission.getGears() << " gears" << std::endl;
    }
};

int main() {
    Car myCar("Tesla Model S", "Red", 0, 1020, "Automatic", 1);
    
    myCar.displaySpecs();
    myCar.drive();
    myCar.park();
    
    return 0;
}
```

### 1.2 初始化列表的重要性

```cpp
#include <iostream>
#include <string>

class Student {
private:
    std::string name;
    int id;
    
public:
    Student(const std::string& n, int i) : name(n), id(i) {
        std::cout << "Student created: " << name << " (ID: " << id << ")" << std::endl;
    }
    
    ~Student() {
        std::cout << "Student destroyed: " << name << std::endl;
    }
    
    void study() const {
        std::cout << name << " is studying" << std::endl;
    }
    
    const std::string& getName() const { return name; }
    int getId() const { return id; }
};

class Course {
private:
    std::string courseName;
    Student instructor;  // 对象成员，必须在初始化列表中初始化
    
public:
    // 必须使用初始化列表初始化instructor
    Course(const std::string& cname, const std::string& iname, int iid)
        : courseName(cname), instructor(iname, iid) {
        std::cout << "Course created: " << courseName << std::endl;
    }
    
    ~Course() {
        std::cout << "Course destroyed: " << courseName << std::endl;
    }
    
    void teach() const {
        std::cout << instructor.getName() << " is teaching " << courseName << std::endl;
        instructor.study();
    }
};

int main() {
    Course cs101("Computer Science 101", "Dr. Smith", 1001);
    cs101.teach();
    
    return 0;
}
```

### 1.3 组合vs继承的选择

```cpp
#include <iostream>
#include <string>
#include <vector>

// 使用组合：Team包含多个Player
class Player {
private:
    std::string name;
    int number;
    std::string position;
    
public:
    Player(const std::string& n, int num, const std::string& pos)
        : name(n), number(num), position(pos) {}
    
    void play() const {
        std::cout << name << " (#" << number << ") playing as " 
                  << position << std::endl;
    }
    
    const std::string& getName() const { return name; }
    int getNumber() const { return number; }
    const std::string& getPosition() const { return position; }
};

class Team {
private:
    std::string teamName;
    std::vector<Player> players;  // 组合：Team包含Players
    
public:
    Team(const std::string& name) : teamName(name) {}
    
    void addPlayer(const Player& player) {
        players.push_back(player);
    }
    
    void playMatch() const {
        std::cout << "\n=== " << teamName << " is playing ===" << std::endl;
        for (const auto& player : players) {
            player.play();
        }
    }
    
    size_t getPlayerCount() const {
        return players.size();
    }
    
    const std::string& getTeamName() const { return teamName; }
};

// 使用继承：BasketballPlayer是Player的一种
class BasketballPlayer : public Player {
private:
    double pointsPerGame;
    double reboundsPerGame;
    
public:
    BasketballPlayer(const std::string& n, int num, const std::string& pos,
                     double ppg, double rpg)
        : Player(n, num, pos), pointsPerGame(ppg), reboundsPerGame(rpg) {}
    
    void displayStats() const {
        std::cout << getName() << " - PPG: " << pointsPerGame 
                  << ", RPG: " << reboundsPerGame << std::endl;
    }
};

int main() {
    // 组合示例
    Team lakers("Los Angeles Lakers");
    
    lakers.addPlayer(Player("LeBron James", 23, "Forward"));
    lakers.addPlayer(Player("Anthony Davis", 3, "Center"));
    lakers.addPlayer(Player("Russell Westbrook", 0, "Guard"));
    
    std::cout << "Team has " << lakers.getPlayerCount() << " players" << std::endl;
    lakers.playMatch();
    
    // 继承示例
    std::cout << "\n=== Player Stats ===" << std::endl;
    BasketballPlayer lebron("LeBron James", 23, "Forward", 27.5, 7.5);
    lebron.play();
    lebron.displayStats();
    
    return 0;
}
```

---

## 2. 私有继承

### 2.1 私有继承的基本概念

```cpp
#include <iostream>
#include <string>

class Stack {
private:
    static const int MAX_SIZE = 100;
    int items[MAX_SIZE];
    int top;
    
public:
    Stack() : top(0) {}
    
    bool isEmpty() const {
        return top == 0;
    }
    
    bool isFull() const {
        return top == MAX_SIZE;
    }
    
    void push(int item) {
        if (!isFull()) {
            items[top++] = item;
        }
    }
    
    int pop() {
        if (!isEmpty()) {
            return items[--top];
        }
        throw std::runtime_error("Stack is empty");
    }
    
    int size() const {
        return top;
    }
};

// 私有继承：StackOfIntegers是一种特殊的Stack，但不公开Stack的接口
class StackOfIntegers : private Stack {
private:
    std::string name;
    
public:
    StackOfIntegers(const std::string& n) : name(n) {}
    
    // 重新暴露需要的接口
    void add(int item) {
        push(item);
    }
    
    int remove() {
        return pop();
    }
    
    bool empty() const {
        return isEmpty();
    }
    
    int count() const {
        return size();
    }
    
    void displayName() const {
        std::cout << "Stack name: " << name << std::endl;
    }
    
    // Stack的其他方法被隐藏，外部无法访问
};

int main() {
    StackOfIntegers stack("My Integer Stack");
    stack.displayName();
    
    stack.add(10);
    stack.add(20);
    stack.add(30);
    
    std::cout << "Stack size: " << stack.count() << std::endl;
    
    while (!stack.empty()) {
        std::cout << "Popped: " << stack.remove() << std::endl;
    }
    
    // stack.push(100); // 错误：push是私有的
    // stack.pop();     // 错误：pop是私有的
    
    return 0;
}
```

### 2.2 私有继承的应用场景

```cpp
#include <iostream>
#include <string>
#include <map>

// 基类：提供日志功能
class Logger {
private:
    std::string logFile;
    
public:
    Logger(const std::string& file = "app.log") : logFile(file) {}
    
    void log(const std::string& message) const {
        std::cout << "[LOG] " << message << std::endl;
    }
    
    void error(const std::string& message) const {
        std::cout << "[ERROR] " << message << std::endl;
    }
    
    void warning(const std::string& message) const {
        std::cout << "[WARNING] " << message << std::endl;
    }
};

// 私有继承：Database使用Logger的功能，但不暴露Logger的接口
class Database : private Logger {
private:
    std::string connectionString;
    std::map<std::string, std::string> data;
    
public:
    Database(const std::string& connStr)
        : Logger("database.log"), connectionString(connStr) {
        log("Database initialized: " + connectionString);
    }
    
    void insert(const std::string& key, const std::string& value) {
        log("Inserting: " + key + " = " + value);
        data[key] = value;
    }
    
    std::string select(const std::string& key) {
        auto it = data.find(key);
        if (it != data.end()) {
            log("Selecting: " + key);
            return it->second;
        }
        error("Key not found: " + key);
        return "";
    }
    
    void remove(const std::string& key) {
        log("Removing: " + key);
        data.erase(key);
    }
    
    size_t count() const {
        return data.size();
    }
    
    // Logger的方法对外部不可见
    // log(), error(), warning() 都是私有的
};

int main() {
    Database db("localhost:5432/mydb");
    
    db.insert("user1", "Alice");
    db.insert("user2", "Bob");
    
    std::cout << "User1: " << db.select("user1") << std::endl;
    std::cout << "User2: " << db.select("user2") << std::endl;
    std::cout << "Total records: " << db.count() << std::endl;
    
    db.remove("user1");
    std::cout << "After removal: " << db.count() << " records" << std::endl;
    
    // db.log("test"); // 错误：log是私有的
    
    return 0;
}
```

---

## 3. 保护继承

### 3.1 保护继承的特性

```cpp
#include <iostream>
#include <string>

class Base {
private:
    int privateData;
    
protected:
    int protectedData;
    
public:
    int publicData;
    
    Base() : privateData(1), protectedData(2), publicData(3) {}
    
    void baseMethod() {
        std::cout << "Base method" << std::endl;
    }
    
protected:
    void protectedBaseMethod() {
        std::cout << "Protected base method" << std::endl;
    }
};

// 保护继承：Base的public和protected成员在Derived中变为protected
class Derived : protected Base {
public:
    void accessMembers() {
        // privateData;      // 错误：不能访问基类的private成员
        protectedData = 10;  // 正确：可以访问基类的protected成员
        publicData = 20;     // 正确：public成员变为protected，仍可访问
        
        baseMethod();           // 正确
        protectedBaseMethod();  // 正确
    }
    
    void exposeBaseMethod() {
        // 将基类方法重新暴露为public
        Base::baseMethod();
    }
};

class MoreDerived : public Derived {
public:
    void accessFromGrandchild() {
        // 可以访问Derived中从Base继承的protected成员
        protectedData = 30;
        publicData = 40;
        
        baseMethod();           // 正确
        protectedBaseMethod();  // 正确
    }
};

int main() {
    Derived derived;
    
    // derived.baseMethod();       // 错误：baseMethod是protected
    // derived.publicData = 100;   // 错误：publicData是protected
    
    derived.exposeBaseMethod();  // 正确：重新暴露为public
    
    MoreDerived moreDerived;
    moreDerived.accessFromGrandchild();
    moreDerived.exposeBaseMethod();
    
    return 0;
}
```

### 3.2 保护继承的实际应用

```cpp
#include <iostream>
#include <string>
#include <vector>

// 基础集合类
class Collection {
protected:
    std::vector<int> items;
    
public:
    Collection() {}
    
    void addItem(int item) {
        items.push_back(item);
    }
    
    size_t size() const {
        return items.size();
    }
    
protected:
    // 保护方法：只允许派生类访问
    void sortItems() {
        std::sort(items.begin(), items.end());
    }
    
    void removeDuplicates() {
        std::sort(items.begin(), items.end());
        items.erase(std::unique(items.begin(), items.end()), items.end());
    }
};

// 保护继承：SortedCollection是一种特殊的Collection
class SortedCollection : protected Collection {
public:
    void addAndSort(int item) {
        addItem(item);
        sortItems();  // 可以访问保护的sortItems
    }
    
    void display() const {
        std::cout << "Sorted collection: ";
        for (int item : items) {
            std::cout << item << " ";
        }
        std::cout << std::endl;
    }
    
    // 重新暴露部分接口
    using Collection::size;
};

// 公有继承自SortedCollection
class UniqueSortedCollection : public SortedCollection {
public:
    void addUnique(int item) {
        // 先添加，然后去重并排序
        addItem(item);
        removeDuplicates();  // 可以访问保护的removeDuplicates
        sortItems();
    }
    
    void show() const {
        display();  // 可以访问SortedCollection的display
    }
};

int main() {
    SortedCollection sorted;
    sorted.addAndSort(5);
    sorted.addAndSort(2);
    sorted.addAndSort(8);
    sorted.addAndSort(1);
    
    std::cout << "Size: " << sorted.size() << std::endl;
    sorted.display();
    
    UniqueSortedCollection unique;
    unique.addUnique(3);
    unique.addUnique(1);
    unique.addUnique(3);
    unique.addUnique(2);
    unique.addUnique(1);
    
    unique.show();
    
    return 0;
}
```

---

## 4. 多重继承

### 4.1 多重继承的基本语法

```cpp
#include <iostream>
#include <string>

class Flyable {
public:
    virtual ~Flyable() = default;
    
    virtual void fly() const {
        std::cout << "Flying..." << std::endl;
    }
    
    virtual int getMaxAltitude() const {
        return 10000;
    }
};

class Swimmable {
public:
    virtual ~Swimmable() = default;
    
    virtual void swim() const {
        std::cout << "Swimming..." << std::endl;
    }
    
    virtual int getMaxDepth() const {
        return 100;
    }
};

class Drivable {
public:
    virtual ~Drivable() = default;
    
    virtual void drive() const {
        std::cout << "Driving..." << std::endl;
    }
    
    virtual int getMaxSpeed() const {
        return 200;
    }
};

// 多重继承：Duck可以飞和游泳
class Duck : public Flyable, public Swimmable {
private:
    std::string name;
    
public:
    Duck(const std::string& n) : name(n) {}
    
    void fly() const override {
        std::cout << name << " is flying" << std::endl;
    }
    
    void swim() const override {
        std::cout << name << " is swimming" << std::endl;
    }
    
    void quack() const {
        std::cout << name << " says: Quack!" << std::endl;
    }
    
    const std::string& getName() const { return name; }
};

// 多重继承：AmphibiousVehicle可以驾驶和游泳
class AmphibiousVehicle : public Drivable, public Swimmable {
private:
    std::string model;
    
public:
    AmphibiousVehicle(const std::string& m) : model(m) {}
    
    void drive() const override {
        std::cout << model << " is driving on land" << std::endl;
    }
    
    void swim() const override {
        std::cout << model << " is swimming in water" << std::endl;
    }
    
    void transform() const {
        std::cout << model << " is transforming..." << std::endl;
    }
};

int main() {
    Duck donald("Donald");
    std::cout << "=== Duck ===" << std::endl;
    donald.fly();
    donald.swim();
    donald.quack();
    std::cout << "Max altitude: " << donald.getMaxAltitude() << " ft" << std::endl;
    std::cout << "Max depth: " << donald.getMaxDepth() << " m" << std::endl;
    
    std::cout << "\n=== Amphibious Vehicle ===" << std::endl;
    AmphibiousVehicle vehicle("Amphicar");
    vehicle.drive();
    vehicle.swim();
    vehicle.transform();
    std::cout << "Max speed: " << vehicle.getMaxSpeed() << " km/h" << std::endl;
    std::cout << "Max depth: " << vehicle.getMaxDepth() << " m" << std::endl;
    
    return 0;
}
```

### 4.2 菱形继承问题

```cpp
#include <iostream>
#include <string>

// 不使用虚继承会导致菱形问题
class Animal {
protected:
    std::string species;
    
public:
    Animal(const std::string& s) : species(s) {
        std::cout << "Animal constructor: " << species << std::endl;
    }
    
    virtual ~Animal() = default;
    
    virtual void breathe() const {
        std::cout << species << " is breathing" << std::endl;
    }
    
    const std::string& getSpecies() const { return species; }
};

// 虚继承解决菱形问题
class Bird : virtual public Animal {
public:
    Bird(const std::string& s) : Animal(s) {
        std::cout << "Bird constructor" << std::endl;
    }
    
    void fly() const {
        std::cout << species << " is flying" << std::endl;
    }
};

class Fish : virtual public Animal {
public:
    Fish(const std::string& s) : Animal(s) {
        std::cout << "Fish constructor" << std::endl;
    }
    
    void swim() const {
        std::cout << species << " is swimming" << std::endl;
    }
};

// FlyingFish继承自Bird和Fish
class FlyingFish : public Bird, public Fish {
public:
    FlyingFish(const std::string& s) : Animal(s), Bird(s), Fish(s) {
        std::cout << "FlyingFish constructor" << std::endl;
    }
    
    void display() const {
        std::cout << "Species: " << getSpecies() << std::endl;
        breathe();  // 只有一个Animal基类，不会歧义
        fly();
        swim();
    }
};

int main() {
    std::cout << "=== Creating FlyingFish ===" << std::endl;
    FlyingFish ff("Exocoetus");
    
    std::cout << "\n=== Display ===" << std::endl;
    ff.display();
    
    return 0;
}
```

### 4.3 多重继承的最佳实践

```cpp
#include <iostream>
#include <string>
#include <vector>

// 接口类（纯抽象类）
class Serializable {
public:
    virtual ~Serializable() = default;
    virtual std::string serialize() const = 0;
    virtual void deserialize(const std::string& data) = 0;
};

class Drawable {
public:
    virtual ~Drawable() = default;
    virtual void draw() const = 0;
    virtual void setPosition(double x, double y) = 0;
    virtual double getX() const = 0;
    virtual double getY() const = 0;
};

class Updatable {
public:
    virtual ~Updatable() = default;
    virtual void update(double deltaTime) = 0;
};

// 实现多个接口的类
class GameObject : public Serializable, public Drawable, public Updatable {
private:
    std::string name;
    double x, y;
    std::string texture;
    
public:
    GameObject(const std::string& n, double px, double py, const std::string& tex)
        : name(n), x(px), y(py), texture(tex) {}
    
    // Serializable接口
    std::string serialize() const override {
        return name + "|" + std::to_string(x) + "|" + 
               std::to_string(y) + "|" + texture;
    }
    
    void deserialize(const std::string& data) override {
        std::cout << "Deserializing: " << data << std::endl;
    }
    
    // Drawable接口
    void draw() const override {
        std::cout << "Drawing " << name << " at (" << x << ", " << y 
                  << ") with texture " << texture << std::endl;
    }
    
    void setPosition(double px, double py) override {
        x = px;
        y = py;
    }
    
    double getX() const override { return x; }
    double getY() const override { return y; }
    
    // Updatable接口
    void update(double deltaTime) override {
        std::cout << "Updating " << name << " (delta: " << deltaTime << ")" << std::endl;
    }
    
    const std::string& getName() const { return name; }
};

class GameEngine {
private:
    std::vector<GameObject*> gameObjects;
    
public:
    void addObject(GameObject* obj) {
        gameObjects.push_back(obj);
    }
    
    void updateAll(double deltaTime) {
        for (auto obj : gameObjects) {
            obj->update(deltaTime);
        }
    }
    
    void renderAll() const {
        for (const auto obj : gameObjects) {
            obj->draw();
        }
    }
    
    void saveAll() const {
        std::cout << "\n=== Saving Game State ===" << std::endl;
        for (const auto obj : gameObjects) {
            std::cout << obj->getName() << ": " << obj->serialize() << std::endl;
        }
    }
};

int main() {
    GameEngine engine;
    
    GameObject player("Player", 100, 200, "player.png");
    GameObject enemy("Enemy", 300, 200, "enemy.png");
    GameObject coin("Coin", 200, 150, "coin.png");
    
    engine.addObject(&player);
    engine.addObject(&enemy);
    engine.addObject(&coin);
    
    std::cout << "=== Game Loop ===" << std::endl;
    engine.updateAll(0.016);
    engine.renderAll();
    engine.saveAll();
    
    return 0;
}
```

---

## 5. 类模板

### 5.1 类模板的基本语法

```cpp
#include <iostream>
#include <string>
#include <stdexcept>

template<typename T>
class Stack {
private:
    static const int MAX_SIZE = 100;
    T items[MAX_SIZE];
    int top;
    
public:
    Stack() : top(0) {}
    
    bool isEmpty() const {
        return top == 0;
    }
    
    bool isFull() const {
        return top == MAX_SIZE;
    }
    
    void push(const T& item) {
        if (!isFull()) {
            items[top++] = item;
        } else {
            throw std::overflow_error("Stack overflow");
        }
    }
    
    T pop() {
        if (!isEmpty()) {
            return items[--top];
        } else {
            throw std::underflow_error("Stack underflow");
        }
    }
    
    T& peek() {
        if (!isEmpty()) {
            return items[top - 1];
        } else {
            throw std::underflow_error("Stack is empty");
        }
    }
    
    const T& peek() const {
        if (!isEmpty()) {
            return items[top - 1];
        } else {
            throw std::underflow_error("Stack is empty");
        }
    }
    
    int size() const {
        return top;
    }
    
    void clear() {
        top = 0;
    }
};

int main() {
    // 整数栈
    Stack<int> intStack;
    intStack.push(10);
    intStack.push(20);
    intStack.push(30);
    
    std::cout << "Integer stack:" << std::endl;
    while (!intStack.isEmpty()) {
        std::cout << intStack.pop() << " ";
    }
    std::cout << std::endl;
    
    // 字符串栈
    Stack<std::string> stringStack;
    stringStack.push("Hello");
    stringStack.push("World");
    stringStack.push("!");
    
    std::cout << "\nString stack:" << std::endl;
    while (!stringStack.isEmpty()) {
        std::cout << stringStack.pop() << " ";
    }
    std::cout << std::endl;
    
    // 双精度浮点数栈
    Stack<double> doubleStack;
    doubleStack.push(3.14);
    doubleStack.push(2.71);
    doubleStack.push(1.41);
    
    std::cout << "\nDouble stack:" << std::endl;
    std::cout << "Top: " << doubleStack.peek() << std::endl;
    std::cout << "Size: " << doubleStack.size() << std::endl;
    
    return 0;
}
```

### 5.2 多参数模板

```cpp
#include <iostream>
#include <string>
#include <array>

template<typename T, int Size>
class FixedArray {
private:
    std::array<T, Size> data;
    
public:
    FixedArray() : data{} {}
    
    T& operator[](int index) {
        if (index < 0 || index >= Size) {
            throw std::out_of_range("Index out of range");
        }
        return data[index];
    }
    
    const T& operator[](int index) const {
        if (index < 0 || index >= Size) {
            throw std::out_of_range("Index out of range");
        }
        return data[index];
    }
    
    int size() const {
        return Size;
    }
    
    void fill(const T& value) {
        data.fill(value);
    }
    
    void display() const {
        std::cout << "FixedArray[" << Size << "]: ";
        for (int i = 0; i < Size; ++i) {
            std::cout << data[i] << " ";
        }
        std::cout << std::endl;
    }
};

// 带默认参数的模板
template<typename T = int, int Size = 10>
class DefaultArray {
private:
    std::array<T, Size> data;
    
public:
    DefaultArray() : data{} {}
    
    T& operator[](int index) {
        return data[index];
    }
    
    const T& operator[](int index) const {
        return data[index];
    }
    
    int size() const {
        return Size;
    }
    
    void display() const {
        std::cout << "DefaultArray[" << Size << "]: ";
        for (int i = 0; i < Size; ++i) {
            std::cout << data[i] << " ";
        }
        std::cout << std::endl;
    }
};

int main() {
    FixedArray<int, 5> intArray;
    for (int i = 0; i < 5; ++i) {
        intArray[i] = i * 10;
    }
    intArray.display();
    
    FixedArray<double, 3> doubleArray;
    doubleArray[0] = 1.1;
    doubleArray[1] = 2.2;
    doubleArray[2] = 3.3;
    doubleArray.display();
    
    // 使用默认参数
    DefaultArray<> defaultInt;
    defaultInt[0] = 100;
    defaultInt.display();
    
    DefaultArray<double, 5> defaultDouble;
    defaultDouble.fill(3.14);
    defaultDouble.display();
    
    return 0;
}
```

### 5.3 模板特化

```cpp
#include <iostream>
#include <string>
#include <cstring>

// 通用模板
template<typename T>
class Compare {
public:
    static bool equals(const T& a, const T& b) {
        return a == b;
    }
    
    static bool lessThan(const T& a, const T& b) {
        return a < b;
    }
};

// 针对double的特化（处理浮点数精度问题）
template<>
class Compare<double> {
private:
    static constexpr double EPSILON = 1e-9;
    
public:
    static bool equals(double a, double b) {
        return std::abs(a - b) < EPSILON;
    }
    
    static bool lessThan(double a, double b) {
        return a < b - EPSILON;
    }
};

// 针对C字符串的特化
template<>
class Compare<const char*> {
public:
    static bool equals(const char* a, const char* b) {
        return std::strcmp(a, b) == 0;
    }
    
    static bool lessThan(const char* a, const char* b) {
        return std::strcmp(a, b) < 0;
    }
};

// 针对std::string的特化
template<>
class Compare<std::string> {
public:
    static bool equals(const std::string& a, const std::string& b) {
        return a == b;
    }
    
    static bool lessThan(const std::string& a, const std::string& b) {
        return a < b;
    }
};

int main() {
    std::cout << "Comparing integers:" << std::endl;
    std::cout << "5 == 5: " << Compare<int>::equals(5, 5) << std::endl;
    std::cout << "5 < 10: " << Compare<int>::lessThan(5, 10) << std::endl;
    
    std::cout << "\nComparing doubles:" << std::endl;
    std::cout << "0.1 + 0.2 == 0.3: " 
              << Compare<double>::equals(0.1 + 0.2, 0.3) << std::endl;
    
    std::cout << "\nComparing C strings:" << std::endl;
    std::cout << "\"hello\" == \"hello\": " 
              << Compare<const char*>::equals("hello", "hello") << std::endl;
    std::cout << "\"apple\" < \"banana\": " 
              << Compare<const char*>::lessThan("apple", "banana") << std::endl;
    
    std::cout << "\nComparing std::string:" << std::endl;
    std::string s1 = "world";
    std::string s2 = "world";
    std::cout << "s1 == s2: " << Compare<std::string>::equals(s1, s2) << std::endl;
    
    return 0;
}
```

---

## 6. 函数模板

### 6.1 函数模板的基本语法

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

// 函数模板：交换两个值
template<typename T>
void swapValues(T& a, T& b) {
    T temp = a;
    a = b;
    b = temp;
}

// 函数模板：查找数组中的最大值
template<typename T>
T findMax(const T arr[], int size) {
    if (size <= 0) {
        throw std::invalid_argument("Array size must be positive");
    }
    
    T maxVal = arr[0];
    for (int i = 1; i < size; ++i) {
        if (arr[i] > maxVal) {
            maxVal = arr[i];
        }
    }
    return maxVal;
}

// 函数模板：打印数组
template<typename T>
void printArray(const T arr[], int size) {
    std::cout << "[";
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i];
        if (i < size - 1) {
            std::cout << ", ";
        }
    }
    std::cout << "]" << std::endl;
}

// 函数模板：对数组进行排序
template<typename T>
void sortArray(T arr[], int size) {
    for (int i = 0; i < size - 1; ++i) {
        for (int j = 0; j < size - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                swapValues(arr[j], arr[j + 1]);
            }
        }
    }
}

int main() {
    // 整数操作
    int intArr[] = {5, 2, 8, 1, 9};
    int size = 5;
    
    std::cout << "Original: ";
    printArray(intArr, size);
    
    sortArray(intArr, size);
    std::cout << "Sorted: ";
    printArray(intArr, size);
    
    std::cout << "Max: " << findMax(intArr, size) << std::endl;
    
    // 双精度浮点数操作
    double doubleArr[] = {3.14, 2.71, 1.41, 1.73};
    size = 4;
    
    std::cout << "\nOriginal: ";
    printArray(doubleArr, size);
    
    sortArray(doubleArr, size);
    std::cout << "Sorted: ";
    printArray(doubleArr, size);
    
    // 字符串操作
    std::string strArr[] = {"banana", "apple", "cherry", "date"};
    size = 4;
    
    std::cout << "\nOriginal: ";
    printArray(strArr, size);
    
    sortArray(strArr, size);
    std::cout << "Sorted: ";
    printArray(strArr, size);
    
    // 交换示例
    int a = 10, b = 20;
    std::cout << "\nBefore swap: a = " << a << ", b = " << b << std::endl;
    swapValues(a, b);
    std::cout << "After swap: a = " << a << ", b = " << b << std::endl;
    
    return 0;
}
```

### 6.2 函数模板的重载

```cpp
#include <iostream>
#include <string>
#include <vector>

// 模板版本：适用于任何支持<<运算符的类型
template<typename T>
void display(const T& value) {
    std::cout << "Template version: " << value << std::endl;
}

// 特化版本：针对C字符串
void display(const char* str) {
    std::cout << "C-string version: " << str << std::endl;
}

// 重载版本：针对vector
template<typename T>
void display(const std::vector<T>& vec) {
    std::cout << "Vector version: [";
    for (size_t i = 0; i < vec.size(); ++i) {
        std::cout << vec[i];
        if (i < vec.size() - 1) {
            std::cout << ", ";
        }
    }
    std::cout << "]" << std::endl;
}

// 重载版本：针对两个参数
template<typename T>
void display(const T& a, const T& b) {
    std::cout << "Two values: " << a << ", " << b << std::endl;
}

// 不同模板参数的重载
template<typename T, typename U>
void display(const T& a, const U& b) {
    std::cout << "Mixed types: " << a << ", " << b << std::endl;
}

int main() {
    display(42);                    // 调用模板版本
    display(3.14);                  // 调用模板版本
    display("Hello");               // 调用C-string版本
    display(std::string("World"));  // 调用模板版本
    
    std::vector<int> vec = {1, 2, 3, 4, 5};
    display(vec);                   // 调用vector版本
    
    display(10, 20);                // 调用两个参数版本
    display(10, 3.14);              // 调用混合类型版本
    
    return 0;
}
```

---

## 7. 模板的具体化

### 7.1 显式具体化

```cpp
#include <iostream>
#include <string>
#include <cstring>

// 通用模板
template<typename T>
void showMessage(const T& value) {
    std::cout << "Generic message: " << value << std::endl;
}

// 显式具体化：针对int
template<>
void showMessage<int>(const int& value) {
    std::cout << "Integer message: " << value << std::endl;
}

// 显式具体化：针对double
template<>
void showMessage<double>(const double& value) {
    std::cout << "Double message: " << value << std::endl;
}

// 显式具体化：针对std::string
template<>
void showMessage<std::string>(const std::string& value) {
    std::cout << "String message: " << value << std::endl;
}

// 显式具体化：针对指针
template<typename T>
void showMessage<T*>(T* const& ptr) {
    if (ptr) {
        std::cout << "Pointer message: " << *ptr << std::endl;
    } else {
        std::cout << "Null pointer" << std::endl;
    }
}

int main() {
    showMessage(42);              // 调用int具体化
    showMessage(3.14);            // 调用double具体化
    showMessage(std::string("Hello"));  // 调用string具体化
    showMessage('A');             // 调用通用模板
    
    int x = 100;
    showMessage(&x);              // 调用指针具体化
    
    return 0;
}
```

### 7.2 部分具体化

```cpp
#include <iostream>
#include <string>

// 通用模板
template<typename T, typename U>
class Pair {
private:
    T first;
    U second;
    
public:
    Pair(const T& f, const U& s) : first(f), second(s) {}
    
    void display() const {
        std::cout << "Pair<" << typeid(T).name() << ", " 
                  << typeid(U).name() << ">: (" 
                  << first << ", " << second << ")" << std::endl;
    }
    
    const T& getFirst() const { return first; }
    const U& getSecond() const { return second; }
};

// 部分具体化：当两个类型相同时
template<typename T>
class Pair<T, T> {
private:
    T first;
    T second;
    
public:
    Pair(const T& f, const T& s) : first(f), second(s) {}
    
    void display() const {
        std::cout << "Pair<" << typeid(T).name() << ", " 
                  << typeid(T).name() << ">: (" 
                  << first << ", " << second << ")" << std::endl;
    }
    
    bool areEqual() const {
        return first == second;
    }
    
    const T& getFirst() const { return first; }
    const T& getSecond() const { return second; }
};

// 部分具体化：当第二个类型是指针时
template<typename T>
class Pair<T, T*> {
private:
    T first;
    T* second;
    
public:
    Pair(const T& f, T* s) : first(f), second(s) {}
    
    void display() const {
        std::cout << "Pair<" << typeid(T).name() << ", " 
                  << typeid(T).name() << "*>: (" 
                  << first << ", ";
        if (second) {
            std::cout << *second;
        } else {
            std::cout << "null";
        }
        std::cout << ")" << std::endl;
    }
    
    const T& getFirst() const { return first; }
    T* getSecond() const { return second; }
};

int main() {
    // 通用版本
    Pair<int, double> p1(10, 3.14);
    p1.display();
    
    // 部分具体化：相同类型
    Pair<int, int> p2(5, 5);
    p2.display();
    std::cout << "Are equal: " << p2.areEqual() << std::endl;
    
    // 部分具体化：指针
    int x = 100;
    Pair<int, int*> p3(10, &x);
    p3.display();
    
    return 0;
}
```

---

## 8. 编译器如何处理模板

### 8.1 模板实例化过程

```cpp
#include <iostream>
#include <string>

// 模板定义
template<typename T>
class Box {
private:
    T content;
    
public:
    Box(const T& c) : content(c) {
        std::cout << "Box<" << typeid(T).name() << "> constructed" << std::endl;
    }
    
    ~Box() {
        std::cout << "Box<" << typeid(T).name() << "> destroyed" << std::endl;
    }
    
    const T& getContent() const {
        return content;
    }
    
    void setContent(const T& c) {
        content = c;
    }
    
    void display() const {
        std::cout << "Box contains: " << content << std::endl;
    }
};

// 显式实例化声明（告诉编译器生成特定类型的代码）
template class Box<int>;
template class Box<double>;
template class Box<std::string>;

int main() {
    std::cout << "Creating boxes..." << std::endl;
    
    Box<int> intBox(42);
    Box<double> doubleBox(3.14);
    Box<std::string> stringBox("Hello");
    
    std::cout << "\nDisplaying contents:" << std::endl;
    intBox.display();
    doubleBox.display();
    stringBox.display();
    
    std::cout << "\nDestroying boxes..." << std::endl;
    
    return 0;
}
```

### 8.2 模板编译模型

```cpp
// 头文件：MyTemplate.h
#ifndef MY_TEMPLATE_H
#define MY_TEMPLATE_H

#include <iostream>

// 方法1：将所有实现放在头文件中（推荐）
template<typename T>
class Calculator {
private:
    T value;
    
public:
    Calculator(T v) : value(v) {}
    
    T add(T other) const {
        return value + other;
    }
    
    T multiply(T other) const {
        return value * other;
    }
    
    void display() const {
        std::cout << "Value: " << value << std::endl;
    }
};

#endif

// 主程序
#include "MyTemplate.h"

int main() {
    Calculator<int> intCalc(10);
    intCalc.display();
    std::cout << "10 + 5 = " << intCalc.add(5) << std::endl;
    std::cout << "10 * 3 = " << intCalc.multiply(3) << std::endl;
    
    Calculator<double> doubleCalc(2.5);
    doubleCalc.display();
    std::cout << "2.5 + 1.5 = " << doubleCalc.add(1.5) << std::endl;
    std::cout << "2.5 * 4 = " << doubleCalc.multiply(4) << std::endl;
    
    return 0;
}
```

---

## 9. 本章小结

### 9.1 核心概念回顾

1. **包含对象成员的类**
   - has-a关系（组合）
   - 初始化列表的重要性
   - 组合vs继承的选择

2. **私有继承**
   - 私有继承的特性
   - 实现细节的隐藏
   - 应用场景

3. **保护继承**
   - 保护继承的特性
   - 成员访问权限的变化
   - 多层继承中的应用

4. **多重继承**
   - 多重继承的基本语法
   - 菱形继承问题
   - 虚继承的使用
   - 接口类设计

5. **类模板**
   - 类模板的基本语法
   - 多参数模板
   - 模板特化
   - 默认参数

6. **函数模板**
   - 函数模板的基本语法
   - 函数模板的重载
   - 模板参数推导

7. **模板的具体化**
   - 显式具体化
   - 部分具体化
   - 编译器处理机制

### 9.2 最佳实践

- **组合优先于继承**：优先考虑has-a关系
- **私有继承用于实现**：当需要实现而非接口时使用
- **虚继承解决菱形问题**：避免重复基类子对象
- **模板代码放在头文件**：确保编译器能看到完整定义
- **使用constexpr优化**：编译期计算提高性能
- **SFINAE原则**：利用替换失败不是错误

### 9.3 常见陷阱

| 陷阱 | 原因 | 解决方案 |
|------|------|----------|
| 忘记初始化列表 | 对象成员未正确初始化 | 始终使用初始化列表 |
| 菱形继承歧义 | 多个基类路径 | 使用虚继承 |
| 模板链接错误 | 实现不在头文件 | 将实现放在头文件中 |
| 模板膨胀 | 过多实例化 | 使用显式实例化控制 |
| 访问权限混淆 | 不理解继承类型 | 明确继承语义 |

---

## 10. 练习题

### 基础练习

1. **学生课程系统**
   ```cpp
   // 使用组合实现学生和课程的关系
   // Student包含多个Course对象
   ```

2. **泛型栈实现**
   ```cpp
   // 实现一个支持任意类型的Stack模板类
   // 包含push、pop、peek等操作
   ```

3. **比较器模板**
   ```cpp
   // 实现一个通用的Comparator模板
   // 支持等于、小于、大于等比较操作
   ```

### 中级练习

4. **智能指针模板**
   ```cpp
   // 实现一个简单的unique_ptr模板
   // 支持移动语义和资源管理
   ```

5. **观察者模式模板**
   ```cpp
   // 使用模板实现通用的观察者模式
   // 支持任意类型的事件数据
   ```

6. **缓存系统**
   ```cpp
   // 实现一个LRU缓存模板类
   // 支持任意键值类型
   ```

### 高级练习

7. **元组实现**
   ```cpp
   // 使用可变参数模板实现Tuple类
   // 支持任意数量和类型的元素
   ```

8. **函数式编程工具**
   ```cpp
   // 实现map、filter、reduce等函数式编程工具
   // 使用模板和lambda表达式
   ```

9. **类型 Traits**
   ```cpp
   // 实现自定义的类型traits
   // 检测类型是否具有某些特性
   ```

10. **综合应用**
    ```cpp
    // 设计一个通用的容器库
    // 包括Vector、List、Map等
    // 使用模板和迭代器
    ```

---

**学习建议：**
- 深入理解组合和继承的区别
- 掌握模板的基本语法和特化
- 通过实际项目巩固所学知识
- 阅读STL源码学习优秀的模板设计

通过本章的学习，您应该能够熟练运用C++的代码重用技术，设计出灵活、可复用的类和模板。

### 11. 高级主题深入

#### 11.1 可变参数模板

```cpp
#include <iostream>
#include <string>
#include <tuple>

// 递归终止条件
template<typename T>
void print(const T& value) {
    std::cout << value << std::endl;
}

// 递归模板函数
template<typename T, typename... Args>
void print(const T& first, const Args&... rest) {
    std::cout << first << ", ";
    print(rest...);
}

// 计算参数数量
template<typename... Args>
size_t countArgs(const Args&... args) {
    return sizeof...(args);
}

// 求和
template<typename T>
T sum(const T& value) {
    return value;
}

template<typename T, typename... Args>
T sum(const T& first, const Args&... rest) {
    return first + sum(rest...);
}

// 元组实现
template<typename... Types>
class Tuple;

// 基本情况：空元组
template<>
class Tuple<> {};

// 递归情况：至少有一个元素
template<typename Head, typename... Tail>
class Tuple<Head, Tail...> : public Tuple<Tail...> {
private:
    Head head;
    
public:
    Tuple() : head(), Tuple<Tail...>() {}
    
    Tuple(const Head& h, const Tail&... t)
        : head(h), Tuple<Tail...>(t...) {}
    
    Head getHead() const { return head; }
    const Tuple<Tail...>& getTail() const { return *this; }
};

int main() {
    std::cout << "=== Variadic Templates ===" << std::endl;
    
    print(1, 2.5, "Hello", 'A');
    
    std::cout << "\nArgument count: " << countArgs(1, 2, 3, 4, 5) << std::endl;
    
    std::cout << "Sum: " << sum(1, 2, 3, 4, 5) << std::endl;
    std::cout << "Sum (double): " << sum(1.1, 2.2, 3.3) << std::endl;
    
    // 使用元组
    Tuple<int, double, std::string> tuple(42, 3.14, "Hello");
    std::cout << "\nTuple head: " << tuple.getHead() << std::endl;
    
    return 0;
}
```

#### 11.2 SFINAE和enable_if

```cpp
#include <iostream>
#include <type_traits>
#include <string>

// 使用enable_if实现条件编译
template<typename T>
typename std::enable_if<std::is_integral<T>::value, std::string>::type
describeType(T value) {
    return "Integer: " + std::to_string(value);
}

template<typename T>
typename std::enable_if<std::is_floating_point<T>::value, std::string>::type
describeType(T value) {
    return "Floating point: " + std::to_string(value);
}

template<typename T>
typename std::enable_if<std::is_same<T, std::string>::value, std::string>::type
describeType(const T& value) {
    return "String: " + value;
}

// C++17的if constexpr
template<typename T>
void processValue(T value) {
    if constexpr (std::is_integral_v<T>) {
        std::cout << "Processing integer: " << value << std::endl;
    } else if constexpr (std::is_floating_point_v<T>) {
        std::cout << "Processing float: " << value << std::endl;
    } else if constexpr (std::is_same_v<T, std::string>) {
        std::cout << "Processing string: " << value << std::endl;
    } else {
        std::cout << "Processing unknown type" << std::endl;
    }
}

// 检测类型是否有size()方法
template<typename T, typename = void>
struct HasSizeMethod : std::false_type {};

template<typename T>
struct HasSizeMethod<T, std::void_t<decltype(std::declval<T>().size())>>
    : std::true_type {};

template<typename T>
void printSize(const T& container) {
    if constexpr (HasSizeMethod<T>::value) {
        std::cout << "Size: " << container.size() << std::endl;
    } else {
        std::cout << "No size() method" << std::endl;
    }
}

int main() {
    std::cout << describeType(42) << std::endl;
    std::cout << describeType(3.14) << std::endl;
    std::cout << describeType(std::string("Hello")) << std::endl;
    
    std::cout << "\n=== If Constexpr ===" << std::endl;
    processValue(10);
    processValue(2.5);
    processValue(std::string("World"));
    
    std::cout << "\n=== Type Traits ===" << std::endl;
    std::vector<int> vec = {1, 2, 3};
    printSize(vec);
    
    int arr[] = {1, 2, 3};
    printSize(arr);
    
    return 0;
}
```

#### 11.3 CRTP（奇异递归模板模式）

```cpp
#include <iostream>
#include <string>

// CRTP基类
template<typename Derived>
class ShapeCRTP {
public:
    void draw() const {
        static_cast<const Derived*>(this)->drawImpl();
    }
    
    double area() const {
        return static_cast<const Derived*>(this)->areaImpl();
    }
    
    void display() const {
        std::cout << "Shape type: " << static_cast<const Derived*>(this)->getType() << std::endl;
        std::cout << "Area: " << area() << std::endl;
        draw();
        std::cout << std::endl;
    }
};

class CircleCRTP : public ShapeCRTP<CircleCRTP> {
private:
    double radius;
    
public:
    CircleCRTP(double r) : radius(r) {}
    
    void drawImpl() const {
        std::cout << "Drawing circle with radius " << radius << std::endl;
    }
    
    double areaImpl() const {
        return 3.14159 * radius * radius;
    }
    
    std::string getType() const {
        return "Circle";
    }
};

class RectangleCRTP : public ShapeCRTP<RectangleCRTP> {
private:
    double width, height;
    
public:
    RectangleCRTP(double w, double h) : width(w), height(h) {}
    
    void drawImpl() const {
        std::cout << "Drawing rectangle " << width << "x" << height << std::endl;
    }
    
    double areaImpl() const {
        return width * height;
    }
    
    std::string getType() const {
        return "Rectangle";
    }
};

// 使用CRTP实现静态多态
template<typename Shape>
void renderShape(const ShapeCRTP<Shape>& shape) {
    shape.display();
}

int main() {
    CircleCRTP circle(5.0);
    RectangleCRTP rect(10.0, 5.0);
    
    std::cout << "=== CRTP Example ===" << std::endl;
    renderShape(circle);
    renderShape(rect);
    
    return 0;
}
```

### 12. 实际项目案例

#### 12.1 通用容器库

```cpp
#include <iostream>
#include <vector>
#include <memory>
#include <stdexcept>
#include <algorithm>

// 迭代器基类
template<typename T>
class Iterator {
public:
    virtual ~Iterator() = default;
    virtual T& operator*() = 0;
    virtual Iterator& operator++() = 0;
    virtual bool operator!=(const Iterator& other) const = 0;
};

// 向量容器
template<typename T>
class Vector {
private:
    std::vector<T> data;
    
public:
    class VectorIterator : public Iterator<T> {
    private:
        typename std::vector<T>::iterator it;
        
    public:
        VectorIterator(typename std::vector<T>::iterator i) : it(i) {}
        
        T& operator*() override { return *it; }
        
        VectorIterator& operator++() override {
            ++it;
            return *this;
        }
        
        bool operator!=(const Iterator<T>& other) const override {
            const VectorIterator* vi = dynamic_cast<const VectorIterator*>(&other);
            return vi && it != vi->it;
        }
    };
    
    void push_back(const T& value) {
        data.push_back(value);
    }
    
    T& operator[](size_t index) {
        if (index >= data.size()) {
            throw std::out_of_range("Index out of range");
        }
        return data[index];
    }
    
    const T& operator[](size_t index) const {
        if (index >= data.size()) {
            throw std::out_of_range("Index out of range");
        }
        return data[index];
    }
    
    size_t size() const {
        return data.size();
    }
    
    bool empty() const {
        return data.empty();
    }
    
    VectorIterator begin() {
        return VectorIterator(data.begin());
    }
    
    VectorIterator end() {
        return VectorIterator(data.end());
    }
    
    void display() const {
        std::cout << "Vector[" << data.size() << "]: ";
        for (const auto& item : data) {
            std::cout << item << " ";
        }
        std::cout << std::endl;
    }
};

// 链表节点
template<typename T>
struct ListNode {
    T data;
    std::unique_ptr<ListNode> next;
    
    ListNode(const T& value) : data(value), next(nullptr) {}
};

// 链表容器
template<typename T>
class LinkedList {
private:
    std::unique_ptr<ListNode<T>> head;
    size_t listSize;
    
public:
    class ListIterator : public Iterator<T> {
    private:
        ListNode<T>* node;
        
    public:
        ListIterator(ListNode<T>* n) : node(n) {}
        
        T& operator*() override { return node->data; }
        
        ListIterator& operator++() override {
            if (node) {
                node = node->next.get();
            }
            return *this;
        }
        
        bool operator!=(const Iterator<T>& other) const override {
            const ListIterator* li = dynamic_cast<const ListIterator*>(&other);
            return li && node != li->node;
        }
    };
    
    LinkedList() : head(nullptr), listSize(0) {}
    
    void push_front(const T& value) {
        auto newNode = std::make_unique<ListNode<T>>(value);
        newNode->next = std::move(head);
        head = std::move(newNode);
        ++listSize;
    }
    
    size_t size() const {
        return listSize;
    }
    
    bool empty() const {
        return listSize == 0;
    }
    
    ListIterator begin() {
        return ListIterator(head.get());
    }
    
    ListIterator end() {
        return ListIterator(nullptr);
    }
    
    void display() const {
        std::cout << "LinkedList[" << listSize << "]: ";
        ListNode<T>* current = head.get();
        while (current) {
            std::cout << current->data << " ";
            current = current->next.get();
        }
        std::cout << std::endl;
    }
};

int main() {
    std::cout << "=== Vector ===" << std::endl;
    Vector<int> vec;
    vec.push_back(10);
    vec.push_back(20);
    vec.push_back(30);
    vec.display();
    
    std::cout << "Element at index 1: " << vec[1] << std::endl;
    
    std::cout << "\n=== LinkedList ===" << std::endl;
    LinkedList<int> list;
    list.push_front(30);
    list.push_front(20);
    list.push_front(10);
    list.display();
    
    std::cout << "List size: " << list.size() << std::endl;
    
    return 0;
}
```

#### 12.2 策略模式实现

```cpp
#include <iostream>
#include <string>
#include <memory>
#include <functional>

// 排序策略接口
template<typename T>
class SortStrategy {
public:
    virtual ~SortStrategy() = default;
    virtual void sort(T arr[], int size) const = 0;
    virtual std::string getName() const = 0;
};

// 冒泡排序
template<typename T>
class BubbleSort : public SortStrategy<T> {
public:
    void sort(T arr[], int size) const override {
        for (int i = 0; i < size - 1; ++i) {
            for (int j = 0; j < size - i - 1; ++j) {
                if (arr[j] > arr[j + 1]) {
                    std::swap(arr[j], arr[j + 1]);
                }
            }
        }
    }
    
    std::string getName() const override {
        return "Bubble Sort";
    }
};

// 快速排序
template<typename T>
class QuickSort : public SortStrategy<T> {
private:
    int partition(T arr[], int low, int high) const {
        T pivot = arr[high];
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
    
    void quickSortHelper(T arr[], int low, int high) const {
        if (low < high) {
            int pi = partition(arr, low, high);
            quickSortHelper(arr, low, pi - 1);
            quickSortHelper(arr, pi + 1, high);
        }
    }
    
public:
    void sort(T arr[], int size) const override {
        quickSortHelper(arr, 0, size - 1);
    }
    
    std::string getName() const override {
        return "Quick Sort";
    }
};

// 上下文类
template<typename T>
class Sorter {
private:
    std::unique_ptr<SortStrategy<T>> strategy;
    
public:
    void setStrategy(std::unique_ptr<SortStrategy<T>> strat) {
        strategy = std::move(strat);
    }
    
    void sortArray(T arr[], int size) const {
        if (strategy) {
            std::cout << "Using " << strategy->getName() << std::endl;
            strategy->sort(arr, size);
        }
    }
};

template<typename T>
void printArray(const T arr[], int size) {
    std::cout << "[";
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i];
        if (i < size - 1) std::cout << ", ";
    }
    std::cout << "]" << std::endl;
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int size = 7;
    
    Sorter<int> sorter;
    
    std::cout << "Original: ";
    printArray(arr, size);
    
    // 使用冒泡排序
    sorter.setStrategy(std::make_unique<BubbleSort<int>>());
    int arr1[] = {64, 34, 25, 12, 22, 11, 90};
    sorter.sortArray(arr1, size);
    std::cout << "Sorted: ";
    printArray(arr1, size);
    
    std::cout << "\n";
    
    // 使用快速排序
    sorter.setStrategy(std::make_unique<QuickSort<int>>());
    int arr2[] = {64, 34, 25, 12, 22, 11, 90};
    sorter.sortArray(arr2, size);
    std::cout << "Sorted: ";
    printArray(arr2, size);
    
    return 0;
}
```

### 13. 性能优化技巧

#### 13.1 模板元编程

```cpp
#include <iostream>

// 编译期计算阶乘
template<int N>
struct Factorial {
    static constexpr int value = N * Factorial<N - 1>::value;
};

template<>
struct Factorial<0> {
    static constexpr int value = 1;
};

// 编译期计算斐波那契数列
template<int N>
struct Fibonacci {
    static constexpr int value = Fibonacci<N - 1>::value + Fibonacci<N - 2>::value;
};

template<>
struct Fibonacci<0> {
    static constexpr int value = 0;
};

template<>
struct Fibonacci<1> {
    static constexpr int value = 1;
};

// 编译期判断素数
template<int N, int D = N - 1>
struct IsPrime {
    static constexpr bool value = (N % D != 0) && IsPrime<N, D - 1>::value;
};

template<int N>
struct IsPrime<N, 1> {
    static constexpr bool value = true;
};

template<>
struct IsPrime<1, 1> {
    static constexpr bool value = false;
};

int main() {
    std::cout << "=== Compile-time Calculations ===" << std::endl;
    
    std::cout << "Factorial of 5: " << Factorial<5>::value << std::endl;
    std::cout << "Factorial of 10: " << Factorial<10>::value << std::endl;
    
    std::cout << "\nFibonacci sequence:" << std::endl;
    std::cout << "Fib(0) = " << Fibonacci<0>::value << std::endl;
    std::cout << "Fib(1) = " << Fibonacci<1>::value << std::endl;
    std::cout << "Fib(10) = " << Fibonacci<10>::value << std::endl;
    
    std::cout << "\nPrime check:" << std::endl;
    std::cout << "Is 7 prime? " << IsPrime<7>::value << std::endl;
    std::cout << "Is 10 prime? " << IsPrime<10>::value << std::endl;
    std::cout << "Is 13 prime? " << IsPrime<13>::value << std::endl;
    
    return 0;
}
```

#### 13.2 移动语义优化

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <chrono>

template<typename T>
class EfficientVector {
private:
    T* data;
    size_t size;
    size_t capacity;
    
    void reallocate(size_t newCapacity) {
        T* newData = new T[newCapacity];
        for (size_t i = 0; i < size; ++i) {
            newData[i] = std::move(data[i]);  // 使用移动语义
        }
        delete[] data;
        data = newData;
        capacity = newCapacity;
    }
    
public:
    EfficientVector() : data(nullptr), size(0), capacity(0) {}
    
    ~EfficientVector() {
        delete[] data;
    }
    
    // 拷贝构造函数
    EfficientVector(const EfficientVector& other)
        : data(new T[other.capacity]), size(other.size), capacity(other.capacity) {
        for (size_t i = 0; i < size; ++i) {
            data[i] = other.data[i];
        }
    }
    
    // 移动构造函数
    EfficientVector(EfficientVector&& other) noexcept
        : data(other.data), size(other.size), capacity(other.capacity) {
        other.data = nullptr;
        other.size = 0;
        other.capacity = 0;
    }
    
    // 拷贝赋值
    EfficientVector& operator=(const EfficientVector& other) {
        if (this != &other) {
            delete[] data;
            capacity = other.capacity;
            size = other.size;
            data = new T[capacity];
            for (size_t i = 0; i < size; ++i) {
                data[i] = other.data[i];
            }
        }
        return *this;
    }
    
    // 移动赋值
    EfficientVector& operator=(EfficientVector&& other) noexcept {
        if (this != &other) {
            delete[] data;
            data = other.data;
            size = other.size;
            capacity = other.capacity;
            other.data = nullptr;
            other.size = 0;
            other.capacity = 0;
        }
        return *this;
    }
    
    void push_back(T value) {
        if (size >= capacity) {
            reallocate(capacity == 0 ? 1 : capacity * 2);
        }
        data[size++] = std::move(value);  // 使用移动语义
    }
    
    T& operator[](size_t index) {
        return data[index];
    }
    
    const T& operator[](size_t index) const {
        return data[index];
    }
    
    size_t getSize() const { return size; }
    size_t getCapacity() const { return capacity; }
};

void benchmarkMoveSemantics() {
    const int ITERATIONS = 100000;
    
    // 测试普通vector
    auto start = std::chrono::high_resolution_clock::now();
    std::vector<std::string> vec1;
    for (int i = 0; i < ITERATIONS; ++i) {
        vec1.push_back(std::string("Test string ") + std::to_string(i));
    }
    auto end = std::chrono::high_resolution_clock::now();
    auto time1 = std::chrono::duration_cast<std::chrono::milliseconds>(end - start);
    
    // 测试高效vector
    start = std::chrono::high_resolution_clock::now();
    EfficientVector<std::string> vec2;
    for (int i = 0; i < ITERATIONS; ++i) {
        vec2.push_back(std::string("Test string ") + std::to_string(i));
    }
    end = std::chrono::high_resolution_clock::now();
    auto time2 = std::chrono::duration_cast<std::chrono::milliseconds>(end - start);
    
    std::cout << "Move semantics benchmark:" << std::endl;
    std::cout << "std::vector time: " << time1.count() << " ms" << std::endl;
    std::cout << "EfficientVector time: " << time2.count() << " ms" << std::endl;
}

int main() {
    benchmarkMoveSemantics();
    return 0;
}
```

### 14. 调试技巧

#### 14.1 模板调试宏

```cpp
#include <iostream>
#include <string>
#include <typeinfo>

// 调试宏
#define DEBUG_PRINT(x) std::cout << #x << " = " << x << std::endl
#define DEBUG_TYPE(x) std::cout << #x << " type: " << typeid(x).name() << std::endl

// 模板调试工具
template<typename T>
class DebugWrapper {
private:
    T value;
    std::string name;
    
public:
    DebugWrapper(const T& v, const std::string& n) : value(v), name(n) {
        std::cout << "[DEBUG] Created " << name << " with value: " << value << std::endl;
    }
    
    ~DebugWrapper() {
        std::cout << "[DEBUG] Destroyed " << name << std::endl;
    }
    
    T& get() {
        std::cout << "[DEBUG] Accessing " << name << std::endl;
        return value;
    }
    
    const T& get() const {
        std::cout << "[DEBUG] Reading " << name << std::endl;
        return value;
    }
    
    void set(const T& newValue) {
        std::cout << "[DEBUG] Setting " << name << " from " << value << " to " << newValue << std::endl;
        value = newValue;
    }
};

// 追踪函数调用
template<typename Func, typename... Args>
auto traceCall(const std::string& funcName, Func&& func, Args&&... args) {
    std::cout << "[TRACE] Entering " << funcName << std::endl;
    auto result = func(std::forward<Args>(args)...);
    std::cout << "[TRACE] Exiting " << funcName << std::endl;
    return result;
}

int add(int a, int b) {
    return a + b;
}

int main() {
    std::cout << "=== Debug Macros ===" << std::endl;
    
    int x = 42;
    double y = 3.14;
    std::string z = "Hello";
    
    DEBUG_PRINT(x);
    DEBUG_PRINT(y);
    DEBUG_PRINT(z);
    
    DEBUG_TYPE(x);
    DEBUG_TYPE(y);
    DEBUG_TYPE(z);
    
    std::cout << "\n=== Debug Wrapper ===" << std::endl;
    DebugWrapper<int> wrappedInt(100, "myInt");
    wrappedInt.set(200);
    std::cout << "Value: " << wrappedInt.get() << std::endl;
    
    std::cout << "\n=== Function Tracing ===" << std::endl;
    int result = traceCall("add", add, 5, 3);
    std::cout << "Result: " << result << std::endl;
    
    return 0;
}
```

---

**最终总结：**

第14章全面深入地讲解了C++代码重用的所有关键知识点。通过本章的学习，您已经掌握了：

**核心概念：**
- 组合（has-a关系）vs继承（is-a关系）
- 私有继承和保护继承的使用场景
- 多重继承和虚继承
- 类模板和函数模板

**高级特性：**
- 可变参数模板
- SFINAE和enable_if
- CRTP（奇异递归模板模式）
- 模板特化和部分特化

**工程实践：**
- 通用容器库设计
- 策略模式实现
- 智能指针和资源管理
- 迭代器模式

**性能优化：**
- 模板元编程
- 移动语义优化
- 编译期计算
- 缓存友好设计

**问题解决：**
- 菱形继承的处理
- 模板链接问题
- 类型推导和转换
- 调试技巧

这些技能将使您能够：
- 设计灵活可复用的代码架构
- 正确使用模板提高代码通用性
- 避免常见的代码重用陷阱
- 编写高性能的泛型代码

代码重用是C++的核心优势之一，掌握这些技术将大大提高您的开发效率和代码质量！

### 15. 补充内容：现代C++模板特性

#### 15.1 Concepts（C++20）

```cpp
#include <iostream>
#include <string>
#include <concepts>

// 定义concept
template<typename T>
concept Addable = requires(T a, T b) {
    { a + b } -> std::convertible_to<T>;
};

template<typename T>
concept Printable = requires(T t) {
    { std::cout << t } -> std::same_as<std::ostream&>;
};

template<typename T>
concept Numeric = std::integral<T> || std::floating_point<T>;

// 使用concept约束模板参数
template<Addable T>
T add(const T& a, const T& b) {
    return a + b;
}

template<Numeric T>
T multiply(const T& a, const T& b) {
    return a * b;
}

template<Printable T>
void printValue(const T& value) {
    std::cout << "Value: " << value << std::endl;
}

// 多个concept的组合
template<typename T>
requires Addable<T> && Printable<T>
void processAndPrint(const T& a, const T& b) {
    T result = add(a, b);
    printValue(result);
}

int main() {
    std::cout << "=== Concepts Example ===" << std::endl;
    
    std::cout << "add(5, 3) = " << add(5, 3) << std::endl;
    std::cout << "add(2.5, 1.5) = " << add(2.5, 1.5) << std::endl;
    
    std::cout << "multiply(4, 5) = " << multiply(4, 5) << std::endl;
    std::cout << "multiply(2.0, 3.5) = " << multiply(2.0, 3.5) << std::endl;
    
    printValue(42);
    printValue(std::string("Hello"));
    
    processAndPrint(10, 20);
    
    return 0;
}
```

#### 15.2 Fold Expressions（C++17）

```cpp
#include <iostream>
#include <string>
#include <vector>

// 折叠表达式：求和
template<typename... Args>
auto sum(Args... args) {
    return (... + args);
}

// 折叠表达式：乘积
template<typename... Args>
auto product(Args... args) {
    return (... * args);
}

// 折叠表达式：打印所有参数
template<typename... Args>
void printAll(Args... args) {
    (std::cout << ... << args) << std::endl;
}

// 折叠表达式：检查所有条件是否为真
template<typename... Args>
bool allTrue(Args... args) {
    return (... && args);
}

// 折叠表达式：检查是否有任何条件为真
template<typename... Args>
bool anyTrue(Args... args) {
    return (... || args);
}

int main() {
    std::cout << "=== Fold Expressions ===" << std::endl;
    
    std::cout << "Sum: " << sum(1, 2, 3, 4, 5) << std::endl;
    std::cout << "Product: " << product(1, 2, 3, 4, 5) << std::endl;
    
    std::cout << "Print: ";
    printAll("Hello", " ", "World", "!");
    
    std::cout << "All true: " << allTrue(true, true, true) << std::endl;
    std::cout << "Any true: " << anyTrue(false, false, true) << std::endl;
    
    return 0;
}
```

---

**最终结语：**

恭喜您完成了第14章的学习！本章涵盖了C++代码重用的所有核心知识点，包括：

- **组合与继承**：has-a关系vs is-a关系
- **私有和保护继承**：实现细节的隐藏
- **多重继承**：虚继承解决菱形问题
- **类模板和函数模板**：泛型编程基础
- **模板特化**：针对特定类型的优化
- **可变参数模板**：处理任意数量的参数
- **现代C++特性**：Concepts、Fold Expressions等

通过系统的学习和大量的代码示例，您已经掌握了编写高质量、可复用C++代码的关键技能。记住，理论与实践相结合才能真正掌握这些知识。

建议您在实际项目中应用这些技术，不断积累经验。C++是一门需要长期学习和实践的编程语言，但它的强大功能和灵活性将使您能够解决各种复杂的编程问题。

祝您在C++编程的道路上越走越远，成为一名优秀的C++开发者！

### 16. 常见问题和解决方案

#### 16.1 模板编译错误调试

```cpp
#include <iostream>
#include <string>
#include <type_traits>

// 常见的模板错误示例

// 错误1：忘记包含必要的头文件
// #include <algorithm> // 需要这个头文件才能使用std::sort

template<typename T>
void sortArray(T arr[], int size) {
    // std::sort(arr, arr + size); // 如果没有包含<algorithm>会报错
    for (int i = 0; i < size - 1; ++i) {
        for (int j = 0; j < size - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                std::swap(arr[j], arr[j + 1]);
            }
        }
    }
}

// 错误2：类型不匹配
template<typename T>
T add(const T& a, const T& b) {
    return a + b;
}

// 错误3：缺少必要的运算符
template<typename T>
bool compare(const T& a, const T& b) {
    return a < b; // 如果T没有定义<运算符会报错
}

// 解决方案：使用SFINAE或concepts进行约束
template<typename T>
auto safeAdd(const T& a, const T& b) -> decltype(a + b) {
    return a + b;
}

int main() {
    int arr[] = {5, 2, 8, 1, 9};
    sortArray(arr, 5);
    
    std::cout << "Sorted: ";
    for (int i = 0; i < 5; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
    
    std::cout << "add(5, 3) = " << add(5, 3) << std::endl;
    std::cout << "safeAdd(2.5, 1.5) = " << safeAdd(2.5, 1.5) << std::endl;
    
    return 0;
}
```

#### 16.2 内存管理最佳实践

```cpp
#include <iostream>
#include <memory>
#include <vector>
#include <string>

// 使用智能指针管理动态内存
template<typename T>
class SafeContainer {
private:
    std::vector<std::unique_ptr<T>> items;
    
public:
    void addItem(std::unique_ptr<T> item) {
        items.push_back(std::move(item));
    }
    
    T* getItem(size_t index) {
        if (index < items.size()) {
            return items[index].get();
        }
        return nullptr;
    }
    
    size_t size() const {
        return items.size();
    }
    
    void clear() {
        items.clear();
    }
};

class Resource {
private:
    std::string name;
    
public:
    Resource(const std::string& n) : name(n) {
        std::cout << "Resource created: " << name << std::endl;
    }
    
    ~Resource() {
        std::cout << "Resource destroyed: " << name << std::endl;
    }
    
    void use() const {
        std::cout << "Using resource: " << name << std::endl;
    }
    
    const std::string& getName() const { return name; }
};

int main() {
    SafeContainer<Resource> container;
    
    container.addItem(std::make_unique<Resource>("Resource1"));
    container.addItem(std::make_unique<Resource>("Resource2"));
    container.addItem(std::make_unique<Resource>("Resource3"));
    
    std::cout << "Container size: " << container.size() << std::endl;
    
    for (size_t i = 0; i < container.size(); ++i) {
        Resource* res = container.getItem(i);
        if (res) {
            res->use();
        }
    }
    
    // 不需要手动delete，智能指针会自动管理
    container.clear();
    
    return 0;
}
```

---

**附录：常用模板技巧速查表**

| 技巧 | 用途 | 示例 |
|------|------|------|
| 模板特化 | 针对特定类型优化 | `template<> class MyClass<int>` |
| 部分特化 | 针对类型类别优化 | `template<typename T> class MyClass<T*>` |
| SFINAE | 条件编译 | `enable_if<condition, T>::type` |
| Variadic Templates | 可变参数 | `template<typename... Args>` |
| Fold Expressions | 参数折叠 | `(... + args)` |
| Concepts | 类型约束 | `template<Addable T>` |
| CRTP | 静态多态 | `class Derived : public Base<Derived>` |
| Type Traits | 类型查询 | `is_integral<T>::value` |

**推荐学习路径：**

1. **基础阶段**：掌握类模板和函数模板的基本语法
2. **进阶阶段**：学习模板特化和部分特化
3. **高级阶段**：深入理解SFINAE和可变参数模板
4. **专家阶段**：掌握Concepts和模板元编程

**实践建议：**

- 从简单的模板开始，逐步增加复杂度
- 阅读STL源码，学习优秀的模板设计
- 在实际项目中应用模板技术
- 参与开源项目，学习他人的模板用法

祝您学习愉快，成为C++模板大师！
