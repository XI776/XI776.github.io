---
title: array.md
date: 2024-07-21 13:06:04
categories: C++ 基础与标准库
description: 记录数组和指针的区别、sizeof 的常见误区与 std::array。
---
指针是在堆上的，局部变量是在栈上。

用new分配的内存，他将一直存在，直到删除delete。
例如，如果有一个函数返回数组，必须使用一个new关键字来分配它，除非你传入一个数组地址参数。。
如果你想返回一个数组，这个数组是在函数中创立的，这样会一直跳，所以如果有可能的话，应该在栈上创立数组来避免这种情况，（这样在内存中跳跃，性能肯定会有影响）

# 区别
```CPP
#include <iostream>
class Entity
{
public:
	int* example = new int[5];
	int count;
	Entity()
	{
		int a[5];
		 count = sizeof(example) / sizeof(int);
		for (int i = 0; i < 5; i++)
			example[i] = 5;
	}
};
int main()
{
	Entity e;
	std::cout <<e.count << std::endl;
}
```
答案是2而不是5
这是因为：
sizeof(example) 计算的是 example 指针的大小，而不是指针所指向的数组的大小。example 是一个指向 int 的指针，在一个典型的64位系统上，指针的大小是8个字节（在32位系统上是4个字节）。

指针的大小在给定的系统架构下是固定的，与指针所指向的数据类型无关。在典型的64位系统上，所有指针的大小都是8个字节；在32位系统上，所有指针的大小都是4个字节。这适用于任何类型的指针，包括指向 int、char、double 或其他类型的指针。
# C++11中
数组可以这样写：
包含#include <array>
std::array<int ,5>another;
count = another.size();