---
title: c++阶段一第三讲
date: 2021-09-15 09:13:44
tags: [教材,阶段一]
categories: c++
description: c++阶段一第三讲
top_img: https://i.loli.net/2021/09/01/3TLgNjv8qmcfU1S.png
cover: https://i.loli.net/2021/09/01/3TLgNjv8qmcfU1S.png
---

# 第三讲

## 常量

常量：是指其值一旦确定，就不会发生改变的量。

创建常量的公式：

+ `#define 常量名 常量值;`

  > 写在头文件的下边

  ```c++
  #include <iostream>
  #define a 1;
  int main()
  {
  	std::cout << a;
  }
  ```

+ `const 数据类型 常量名 = 常量值;`

  > 写在头文件的下边

  ```c++
  #include <iostream>
  const int a = 1;
  int main()
  {
  	std::cout << a;
  }
  ```

练习：尝试去修改常量的值

```c++
#include <iostream>
const int a = 10;
int main()
{
	a = 20;
	std::cout << a;
}
```

## 单目运算符

`++`：自增1

`--`：自减1

前置`++`：先自增，再参与其他运算。

后置`++`：先参与其他运算，再自增。

前置`--`：先自减，再参与其他运算。

后置`--`：先参与其他运算，再自减。

练习：

a的值是多少 

```c++
int a = 5;
std::cout<<a++;
```

```c++
int a = 5;
std::cout<<++a;
```

```c++
int a = 5;
std::cout<<a--;
```

```c++
int a = 5;
std::cout<<--a;
```

a和b的值是多少

```c++
int a = 5;
int b = a++;
std::cout<<a<<" "<<b;
```

```c++
int a = 5;
int b = ++a;
std::cout<<a<<" "<<b;
```

```c++
int a = 5;
int b = a--;
std::cout<<a<<" "<<b;
```

```c++
int a = 5;
int b = --a;
std::cout<<a<<" "<<b;
```

控制台会显示出什么样的结果

```c++
#include <iostream>
int main()
{
	int a = 5, b = 5;
	std::cout << a++ << " " << ++b << "\n";
	std::cout << --a << " " << b-- << "\n";
	std::cout << ++a << " " << b++ << "\n";
	std::cout << a-- << " " << --b << "\n";
}
```

## 类型转换

下面这段程序运行后有什么样的结果

```c++
#include <iostream>
int main()
{
	int a = 5.1;
	std::cout<<a;
}
```

![](https://gitee.com/gaoxianglong/picgo/raw/master/img/20210915112324.png)

自动数据类型转换的规则：

1. 横向红色的箭头表示的是无条件转换，float类型数据运算时，将其转换为double类型进行运算，运算结果再转换为float；short和char类型数据在做运算时，首先转换为int，再将运算结果转换为short、char类型。
2. 纵向的蓝色箭头，当不同数据类型之间进行运算时，位于箭头下方的数据类型会转换为箭头上方的数据类型。

## 强制类型转换

公式：

`(数据类型) 表达式`

如：

```c++
int s=(int)5.3;
std::cout<<s;
//或者
double t=5.3;
int s=(int)t;
std::cout<<s;
```

整数转小数时，直接加上 .0

小数转整数时，小数点后的数据全部舍弃（精度丢失）

整数转字符时，根据ASCII码表转换

字符转整数时，根据ASCll码表转换

练习：

分别找出a、z、A、Z这几个字符再ASCII码表里的整数是多少

