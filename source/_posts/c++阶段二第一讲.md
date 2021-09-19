---
title: c++阶段二第一讲
date: 2021-08-31 11:47:42
tags: [教材,阶段二]
categories: c++
description: c++阶段二第一讲--初始函数
top_img: https://i.loli.net/2021/09/01/3TLgNjv8qmcfU1S.png
cover: https://i.loli.net/2021/09/01/3TLgNjv8qmcfU1S.png
---

# 初始函数

## 思考

函数是什么？或者说你们觉得它有什么用？

数学上的函数：

两个一直在变化的量，一个量的改变会影响到另一个量的改变。

<img src="https://i.loli.net/2021/08/31/3HOrUMQptT7kwSm.png" style="zoom:200%;" />

我们使用过的函数：

+ printf()

  

+ scanf()

> 通过**按住`ctrl`+鼠标左键**可以查看这个函数是在哪儿定义的

## 函数

函数的主要作用：

**函数是指一段代码可以直接被另一段代码引用的代码。也叫做子程序。**一个较大的程序一般应分为若干个程序块，每一个模块用来实现一个特定的功能。所有的高级语言中都有子程序这个概念，用子程序实现模块的功能。在C++语言中，子程序的作用是由一个主函数和若干个函数构成。**由主函数调用其他函数，其他函数也可以互相调用。同一个函数可以被一个或多个函数调用任意多次。**

函数的必备要素：

```c++
// 完整的函数
void print(string a) {
	cout << a;
}
```

+ void

  这个位置是规定当前函数在运行之后需要有一个什么类型的结果，void表示没有结果，如果需要int类型的结果那就写int

+ print

  这个位置是函数的名字，和变量名类似

+ ()

  括号里写入这个函数在调用时需要的参数，称为形参

+ {}

  大括号里写入函数需要完成的逻辑代码

调用函数的方法：

调用函数有三种方式：

1. 没有返回值类型，也不需要参数

   `fun();`

2. 没有返回值类型，需要参数

   `fun(1);`

3. 有返回值，也需要参数

   `int a = fun(1);`

> 注：调用函数传入的参数称为这个函数的实参

### 自定义函数

```c++
// 打印一个字符串
void print(string a) {
	cout << a;
}
// 两个数相加
int add(int a,int b){
	return a + b;
}
```

这两个函数写在`mian`函数外面的上方

```c++
#include<iostream>
#include<windows.h>
using namespace std;
//打印一个字符串
void print(string a) {
	cout << a<<endl;
}
// 两个数相加
int add(int a,int b){
	return a + b;
}
int  main()
{
	print("123");
	cout << add(1, 2);
}
```

> 同学们动手敲敲这段代码，体会一些函数的作用。

## 练习

完成两个数相加，相减，相乘，相除。
