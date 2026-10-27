---
title: String
date: 2024-07-21 14:15:57
categories: C++ 基础与标准库
description: 从字符串拼接的示例认识 std::string 与运算符重载。
---
和c语言的字符串差不多，不过更丰富。
```CPP
#include <iostream>
int main()
{
	const char* name = "Xavier";
	 std::string name1=std::string("XAVIER")+"Hello!";
	 //name1 += "Hello!";
	 //name1.insert(name1.end()-3, 'm');
	 std::cout << name1 << std::endl;
	 std::cin.get();
}
```
std::string 类重载了 + 运算符，可以连接两个 std::string 对象，或一个 std::string 对象和一个 C 风格字符串（即 const char*）。
"Hello!" 是一个 C 风格字符串，类型是 const char*。
std::string("XAVIER") 是一个 std::string 对象。
当你使用 + 运算符时，编译器调用 std::string 的运算符重载函数，将这两个字符串连接起来，生成一个新的 std::string 对象，其内容是 "XAVIERHello!"。

# 关键点
运算符重载：std::string 类重载了 + 运算符，使其能够处理 std::string 对象和 C 风格字符串的连接。
临时对象：表达式 std::string("XAVIER") + "Hello!" 创建了一个临时的 std::string 对象，最终被赋值给 name1。

```CPP
#include <iostream>
#include <string>

class MyString {
public:
    std::string str;

    MyString(const char* s) : str(s) {}

    MyString operator+(const MyString& other) const {
        return MyString((str + other.str).c_str());
    }
};

int main() {
    MyString s1("Hello, ");
    MyString s2("World!");
    MyString s3 = s1 + s2;
    std::cout << s3.str << std::endl; // 输出: Hello, World!
    return 0;
}
```
什么时候选择运算符重载
适合使用运算符重载的情况：

当你希望自定义类的行为类似于内置类型，并且常见的运算符（如 +, -, *, /, [], () 等）能使代码更简洁。
当重载的运算符能显著提高代码的可读性和可维护性。
避免运算符重载的情况：

当运算符重载增加了不必要的复杂性，或使代码变得不直观时。
当运算符重载可能引起歧义或误导时，特别是当运算符的行为与其通常意义不符时。
运算符重载的优缺点

# 优点：

代码简洁，易读，易于维护。
提高代码的一致性和可复用性。
使得自定义类的使用更接近内置类型。

# 缺点：

可能增加代码的复杂性和理解难度，特别是对于新手。
可能导致滥用，特别是在不适当的情况下使用运算符重载。
需要额外的设计和实现工作。
总结
运算符重载是一种强大的特性，适当地使用可以显著提高代码的可读性和直观性。然而，它也需要谨慎使用，以避免增加代码的复杂性或引起误导。决定是否使用运算符重载，应权衡其带来的好处和可能的复杂性。






