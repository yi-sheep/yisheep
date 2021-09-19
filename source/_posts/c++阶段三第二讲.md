---
title: c++阶段三第二讲
date: 2021-09-10 10:18:09
tags: [教材,阶段三]
categories: c++
description: c++阶段三第二讲
top_img: https://i.loli.net/2021/09/01/3TLgNjv8qmcfU1S.png
cover: https://i.loli.net/2021/09/01/3TLgNjv8qmcfU1S.png
---

# 第二讲

## 结构体

结构体可以作为函数的参数

具体写法：

```c++
void fun(struct 结构体名 结构体变量名){
    ...
}
```

例子：

```c++
#include <iostream>
#include <cstring> 
using namespace std;
struct PersonInfo                            //定义结构体
{
	int index;
	string name;
	string dizhi;
	short age;
};
void ShowStuctMessage(struct PersonInfo MyInfo)    //自定义函数，输出结构体变量成员
{
	cout << MyInfo.index << endl;
	cout << MyInfo.name << endl;
	cout << MyInfo.dizhi << endl;
	cout << MyInfo.age << endl;

}
int main()
{

	PersonInfo pInfo;                        //声明结构体
	pInfo.index = 1;
	pInfo.name="小王";
	pInfo.dizhi = "乐山市";
	pInfo.age = 20;
	ShowStuctMessage(pInfo);                //调用自定义函数
	return 0;
}
```

## 结构体指针

指针的创建：

`int* a;`

结构体指针的创建公式：

`结构体名* 指针名`;

结构体指针访问结构体内的属性

`结构体指针名->结构体中的属性`

例子：

```c++
#include <iostream>
#include <stdarg.h>
#include <string>
using namespace std;
struct stu {
	int i;
};
int main() {
	stu* s;
	s->i;
}
```

结构体指针作为函数参数

具体写法：

```c++
void fun(struct 结构体名* 指针名){
    ...
}
```

例子：

```c++
#include <iostream>
#include <cstring> 
using namespace std;
struct PersonInfo
{
    int index;
    char name[30];
    short age;
};
void ShowStuctMessage(struct PersonInfo* pInfo)
{
    cout << pInfo->index << endl;
    cout << pInfo->name << endl;
    cout << pInfo->age << endl;

}
int main()
{

    PersonInfo pInfo;
    pInfo.index = 1;
    strcpy(pInfo.name, "张三");
    pInfo.age = 20;
    ShowStuctMessage(&pInfo);  //传递的是pInfo的地址 
    return 0;
}
```

## 结构体数组

结构体还可以和数组结合

创建公式：

`结构体名 数组名[数字] = {{*,*,...},{*,*,...},....};`

例子:

```c++
#include <iostream>
#include<cstring> 
using namespace std;
int main()
{
    struct PersonInfo
    {
        int index;
        char name[30];
        short age;
    } Person[5] = { {1,"张三",20}, //创建结构体的同时创建结构体数组
        {2,"李可可",21},
        {3,"宋桥",22},
        {4,"元员",22},
        {5,"王冰冰",22}
    };
    struct PersonInfo* pPersonInfo;
    pPersonInfo = Person;
    for (int i = 0; i < 5; i++, pPersonInfo++)
    {
        cout << pPersonInfo->index << endl;
        cout << pPersonInfo->name << endl;
        cout << pPersonInfo->age << endl;
    }
    return 0;
}
```

## 结构体所占空间大小

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
	} pInfo;
	pInfo.index = 0;
	strcpy(pInfo.name, "小龙");
	pInfo.age = 20;
	cout << "index:" << sizeof(pInfo.index) << "name:" << sizeof(pInfo.name) << "age:" << sizeof(pInfo.age) << endl;
	cout << sizeof(pInfo) << endl;
}
```

## 修改int数据类型

我们可以为一个数据类型取别名使用`typedef`关键字

公式：`typedef 旧类型名 新类型名;`

例子：

```c++
#include <iostream>
using namespace std;
int main() {
    int a = 9;
    typedef int flag;
    flag b = 9;
    cout << a << b;
}
```

## 共用体

共用体数据类型是指将不同的数据项组织为一个整体，和结构体类似，但是共用体在内存中占用首地址相同的一段存储单元。

创建共用体的公式：

```c++
union 共用体类型名{
	成员数据类型  共用体成员名1；
	成员数据类型  共用体成员名2；
	...
	成员数据类型  共用体成员名n；
};
```

> 共用体变量所占内存大小是由最长的成员的长度决定的。

共用体的初始化

案例：

```c++
#include<iostream>
using namespace std;
union myUnion
{
    int iData;
    char chData;
    float fData;
} uStruct;
int main()
{
    uStruct.chData='A';
    uStruct.fData=0.3;
    uStruct.iData=100;
    cout << uStruct.chData << endl;
    cout << uStruct.fData << endl;
    cout << uStruct.iData << endl;        //正确显示
    uStruct.iData=100;
    uStruct.fData=0.3;
    uStruct.chData='A';
    cout << uStruct.chData<< endl;    //正确显示
    cout << uStruct.fData<< endl;
    cout << uStruct.iData<< endl;
    uStruct.iData=100;
    uStruct.chData='A';
    uStruct.fData=0.3;
    cout << uStruct.chData << endl;
    cout << uStruct.fData << endl;        //正确显示
    cout << uStruct.iData << endl;
    return 0;
}
```

> 由于是共用的同一个内存单元，所以结果中只有最后赋值的成员能正确显示。

## 枚举

枚举：是一些标识符的集合，其变量的值只能取自括号内的这些标识符。

枚举创建公式：`enum 枚举类型名 {标识符列表};`

创建带整型值的枚举类型的公式：

```c++
enum 枚举类型名 {
标识符=0，
标识符=1，
标识符=2，
标识符=3，
...
};
```

创建枚举类型变量的公式： `枚举类型名 变量名；`

```c++
#include <iostream>
using namespace std;
int main()
{
    enum Weekday {Sunday,Monday,Tuesday,Wednesday,Thursday,Friday,Saturday};
    int a=2,b=1;
    Weekday day;
    day=(Weekday)a;
    cout << day << endl;
    day=(Weekday)(a-b);
    cout << day << endl;
    day=(Weekday)(Sunday+Wednesday);
    cout << day << endl;
    day=(Weekday)5;
    cout << day << endl;
}
```

枚举类型的值可以和整型类型一起运算、比较等。

```c++
#include <iostream>
using namespace std;
enum Weekday { Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday };
int main()
{
    Weekday day1, day2;
    day1 = Monday;
    day2 = Saturday;
    int n;
    n = day1;
    n = day2 + 1;
    if (n > day1)            //可以比较
        cout << "n>day1" << endl;
    if (day1 < day2)
        cout << "day1<day2" << endl;
}
```

