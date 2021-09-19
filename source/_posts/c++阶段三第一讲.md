---
title: c++阶段三第一讲
date: 2021-08-31 16:18:28
tags: [教材,阶段三]
categories: c++
description: c++阶段三第三讲--引用与结构体
top_img: https://i.loli.net/2021/09/01/3TLgNjv8qmcfU1S.png
cover: https://i.loli.net/2021/09/01/3TLgNjv8qmcfU1S.png
---



# 第一讲

## 引用

通过指针能够直接对变量的内存空间进行操作，如果我不用指针，想让两个变量共用同一个内存空间可以吗？  答案是可以，那就是使用引用。以此引出对引用的使用。  

引用：

**引用变量是其他对象的别名，对其的任何操作和对原来的对象具有相同作用，有点像为原来的对象取的别名。且一个引用被初始化后，就无法再去引用另一个对象。**

创建公式：

`数据类型& 引用名`

> 程序中的引用在程序运行结束前必须被初始化，否则会报错。

创建一个函数，他接收两个引用，用于交换两个变量的值。

```c++
#include <iostream>
using namespace std;
void swap(int & a,int & b)
{
int tmp;
tmp=a;
a=b;
b=tmp;
}
int main()
{
int x,y;
cout << "请输入x" << endl;
cin >> x;
cout << "请输入y" << endl;
cin >> y;
cout<<"ͨ使用引用交换y和x的值"<<endl;
swap(x,y);
cout << "x=" << x <<endl;
cout << "y=" << y <<endl;
}
```

## 结构体

结构体：

**结构体是由多个不同类型的数据组合而成的数据集合。**

创建公式：

```c++
struct 结构体名{
   成员数据类型1 成员名1;
   …
   成员数据类型n 成员名n;
}；
```

如：

```c++
struct Person
{
int index;
char name[30];
short age;
};
```

创建好了之后就可以使用了！

使用结构体的方法：

**就如同创建一个变量一样，只不过需要将原来的`int`,`double`这些数据类型换为结构体的名字。**

如：`Person p;`

接下来就可以通过这个`p`去访问到结构体中的成员`index`,`name`,`age`。

如：`p.index`

并且还可以给它赋值：`p.index = 1`

代码案例：

```c++
struct Person
{
int index;
string name;
short age;
};
int main(){
    Person p;
    p.index = 1;
    p.name = "张三";
    p.age = 15;
}
```

创建一个学生结构体，这个结构体里有`学号`，`姓名`，`年龄`，`性别`。

```c++
struct Student
{
	int number;
	string name;
	short age;
    bool sex;
};
```

在主函数里添加三个学生的信息，并显示出来。

```c++
#include <iostream>
using namespace std;

struct Student
{
	int number;
	string name;
	short age;
	bool sex;
};
int main() {
	Student s1;
	Student s2;
	Student s3;
	s1.number = 01;
	s2.number = 02;
	s3.number = 03;
	s1.name = "001";
	s2.name = "002";
	s3.name = "003";
	s1.age = 14;
	s2.age = 15;
	s3.age = 16;
	s1.sex = true;
	s2.sex = false;
	s3.sex = true;
	cout << s1.number << " " << s1.name << " " << s1.age << " " << s1.sex << endl;
	cout << s2.number << " " << s2.name << " " << s2.age << " " << s2.sex << endl;
	cout << s3.number << " " << s3.name << " " << s3.age << " " << s3.sex<<endl;
}
```

创建结构体还有一种方式：

在创建结构体的同时，将对应变量也一起创建。

```c++
struct Person
{
	int index;
	string name;
	short age;
}s1;
// 也可以创建多个变量
struct Person
{
	int index;
	string name;
	short age;
}s1,s2;
```

也可以同时给其成员赋值：

```c++
struct Person
{
	int index;
	string name;
	short age;
}s1 = {1,"01",10};
```

结构体还可以嵌套?

结构体的嵌套：**在定义结构体时可以声明其他已经创建好的结构体变量，也可以在创建一个结构体时创建子结构体。**

```c++
#include <iostream>
using namespace std;
int main()
{
	struct PersonInfo
	{
		int index;
		char name[30];
		short age;
		struct WorkPlace
		{
			char Address[150];
			char PostCode[30];
			char GateCode[50];
			char Street[100];
			char Area[50];
		} WP;
	};
	PersonInfo pInfo;
	strcpy(pInfo.WP.Address, "House");
	strcpy(pInfo.WP.PostCode, "10000");
	strcpy(pInfo.WP.GateCode, "302");
	strcpy(pInfo.WP.Street, "Lan Tian");
	strcpy(pInfo.WP.Area, "china");
	cout << pInfo.WP.Address << endl;
	cout << pInfo.WP.PostCode << endl;
	cout << pInfo.WP.GateCode << endl;
	cout << pInfo.WP.Street << endl;
	cout << pInfo.WP.Area << endl;
}
```

## 练习

设计一个小汽车的结构体，在这个结构体中还有一个表示发动机的结构体。

```c++
#include <iostream>
using namespace std;
int main(int argc, char* argv[])
{
	struct Car {
		struct _Engine {
			int height;
			int width;
		} engine;
		char color[30];
	} a_car;
	a_car.engine.width = 40;
	a_car.engine.height = 60;
	strcpy(a_car.color, "黑色");
	return 0;
}
```

