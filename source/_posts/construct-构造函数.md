
---
title: Construct 构造函数
date: 2024-07-19 13:34:00
categories: C++ 面向对象
description: 从对象初始化出发，记录构造函数、析构函数与成员初始化列表。
---
构造函数基本上是一种特殊类型的方法，在每次实例化对象时运行

```cpp
#include <iostream>

class Entity {
private:
    float X, Y;
public:
    void print() {
        std::cout << X << " " << Y << std::endl;
    }
};

int main() {
    Entity e;
    e.print();
}
```


此时结果应为未经初始化的值，看似随机值，这是因为当我们实例化 Entity，并为它分配内存时实际上并没有初始化那个内存，我们得到了那个内存空间里原来的那些东西。

所以构造函数如下：

构造函数特点
没有返回类型，并且名称必须与类的名称相同。
在有些语言（例如 Java），数据基本类型会自动初始化为 0。
```cpp

#include <iostream>
class Entity {
private:
    float X, Y;
public:
    Entity() {
        X = 0.0f;
        Y = 0.0f;
    }
    Entity(float x, float y) {
        X = x;
        Y = y;
    }
    void print() {
        std::cout << X << " " << Y << std::endl;
    }
};

int main() {
    Entity e(1.2, 5.0);
    e.print();
}

```

注意
如果不实例化对象，构造函数将不会运行，所以只用一个类的静态方法时，它不会运行。
---
析构函数
构造函数是在创建一个新的实例对象时运行的，析构函数是在销毁对象时运行。构造函数通常是设置变量或者做任何你需要的初始化。
~Entity（）{
}
当析构函数调用时，Entity实例对象消失了。
# 成员初始化列表
很好用
```cpp
class MyClass {
private:
    int a;
    const int b;
    int& c;
public:
    // 构造函数使用成员初始化列表
    MyClass(int x, int y, int& z) : a(x), b(y), c(z) {}
};
```

