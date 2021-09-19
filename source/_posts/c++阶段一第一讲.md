---
title: c++阶段一第一讲
date: 2021-08-31 11:30:39
tags: [教材,阶段一]
categories: c++
description: c++阶段一第一讲--初始c++
top_img: https://i.loli.net/2021/09/01/3TLgNjv8qmcfU1S.png
cover: https://i.loli.net/2021/09/01/3TLgNjv8qmcfU1S.png
---

# 初始c++

## 课堂笔记

### 什么是编程？

编程就是人与计算机交流的过程！

### 计算机语言的发展过程

#### 机器语言

由0和1组成的低级语言，因为计算机只能识别有和无两种状态。

优点：执行速度块，因为计算机可以直接看得懂。

缺点：编写难度较大，出错率高且不易查找。

#### 汇编语言

由少量的人类语言组成，比如AX、BX等等。

优点：能被一部分人掌握，出错率这些都比机器语言好。

缺点：计算机不能直接看懂需要进行编译成机器码，所以执行速度没有机器语言快。

#### 高级语言

由大量的人类语言组成，比如if、else等等。

优点：能够被大部分人掌握，各方面都比前面的机器语言和汇编语言强。

缺点：计算机也不能直接看懂需要进行编译成机器码。

### 打开Visual Studio

![](https://i.loli.net/2021/08/31/EXfvesn97aoBV8U.png)

## 创建项目1

![](https://i.loli.net/2021/08/31/PX5RWoSzacQhEnv.png)

## 创建项目2

![](https://i.loli.net/2021/08/31/EQ2DFfX4op1lb7y.png)

## 创建项目3

![](https://i.loli.net/2021/08/31/dqPsmWXbuiKHwNr.png)

## 创建项目4

![](https://i.loli.net/2021/08/31/cxIE8FGh3zKT6Pt.png)

## 散掉注释行

![](https://i.loli.net/2021/08/31/lWiH9uPsfwDZ8Mp.png)

## 散掉空白行

![](https://i.loli.net/2021/08/31/kEGXKiPwg1U6QRL.png)

### c++：Hello,World!

```c++
// c++的第一个程序
#include <iostream>
int main(){
    std::cout<<"Hello,World!\n";
}
```

+ //

  注释，计算机不会运行，主要用作解释或标注某一行或多行代码的意思。

+ \#

  预处理符，在程序运行之前提前处理。

+ include

  调用某一个东西。

+ iostream

  输入、输出库文件。

+ main()

  主函数，程序的入口。

+ {}

  函数的范围。

  + 左 { 

    就表示这个函数从这里开始

  + 右 } 

    就表示这个函数从这里结束

+ std::

  命名空间，他里面包含了很多命令。

+ cout

  向控制台输出，存在与std这个命令空间里。

+ << 

  插入符，将右边的东西交给左边去执行。

+ ;

  结束符，表示我们这一句命令结束了。

+ \n

  换行符，相当于我们在某一个地方按了一下回车，必须写在""之中。

> 注意：除""里的字符意外其他的都需要是英文状态下的输入法输入才行!

## 课堂练习

+ 在控制台中打印自己的名字
+ 在控制台中将自己的名字竖着显示出来
+ 在控制台显示出一首古诗【格式按照语文课本】

```c++
#include<iostream
int main()
{
    // 打印自己的名字
    std::cout << "高老师";
    // 打印一首古诗
    std::cout << "  静夜思\n";
    std::cout << "床前明月光，\n";
    std::cout << "疑是地上霜。\n";
    std::cout << "举头望明月，\n";
    std::cout << "低头思故乡。\n";
}
```

