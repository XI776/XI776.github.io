---
title: 纯虚函数
date: 2024-07-20 13:56:08
categories: C++ 面向对象
description: 用 Printable 和 Entity 的例子理解纯虚函数、接口与抽象基类。
---
纯虚函数允许我们在基类中定义一个没有实现的函数，然后强制子类去实现该函数

回到之前的虚函数：
```CPP
#include <iostream>
#include <cstring>

class Entity
{
public:
	virtual std::string GetName() { return "Entity"; }
};

class Player : public Entity
{
private:
	std::string m_Name;
public:
	Player(const std::string&name)
		:m_Name(name){}
	std::string GetName() override { return m_Name;  }
};
void PrintName(Entity *entity)
{
	std::cout << entity->GetName()<< std::endl;
}
int main()
{
	Entity *e=new Entity();
	PrintName(e);
	Player* p = new Player("Xavier");
	PrintName(p);
	Entity* entity = p;
	PrintName(entity);
	
}
```
可以看到Entity类中的虚函数，即使补充些，仍然可以调用Player.GetName()，但是有时候这种没有意义，实际上我们可能想要强制子类，为特定的函数提供自己的定义。（创建一个类，只有为实现的方法组成，然后强制子类去实际实现他们，这非常常见）----->这被称为接口.
所以类中的接口只包含未实现的方法，作为模板。
因为不包含方法实现，所以不能实例化。
# 定义虚函数
        virtual std::string GetName() = 0;
        =0表示纯虚函数，没有实现，所以不能实例化
如果确保每个类都有一个特定的方法，那么可以将这个类（抽象基类）作为参数（类型）放入一个通用的函数中，就可以调用这个方法或者做其他事情。
```CPP
#include <iostream>
#include <cstring>

class Printable
{
public:
	virtual std::string GetClassName() = 0;
};
class Entity:public Printable
{
public:
	virtual std::string GetName() { return "1"; };
	std::string GetClassName() override { return "Entity"; }
};

class Player : public Entity
{
private:
	std::string m_Name;
public:
	Player(const std::string&name)
		:m_Name(name){}
	std::string GetName() override { return m_Name;  }
	std::string GetClassName() override { return "PLAYER"; }
};
void PrintName(Entity *entity)
{
	std::cout << entity->GetName()<< std::endl;
}
void Print(Printable* entity)
{
	std::cout << entity->GetClassName() << std::endl;
}
int main()
{
	Entity *e=new Entity();
	//PrintName(e);
	Player* p = new Player("Xavier");
	//PrintName(p);//
	Entity* entity = p;
	//PrintName(entity);
	Print(e);
	Print(p);
}
```
