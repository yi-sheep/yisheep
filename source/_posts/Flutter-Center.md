---
title: Flutter-Center详解
date: 2021-09-17 17:49:32
tags: [笔记]
categories: flutter
description: Flutter-Center详解
top_img: https://gitee.com/gaoxianglong/picgo/raw/master/img/f3b8af27140c9ac90ab83012cec99bc746546e28.jpg
cover: https://gitee.com/gaoxianglong/picgo/raw/master/img/f3b8af27140c9ac90ab83012cec99bc746546e28.jpg
---

# Flutter-Center详解

# Center介绍

`Center`就是将子组件进行一个居中展示，它继承自`Align`，因为`Align`默认的对齐方式是居中的，所以它能实现居中效果，如果`Center`的尺寸没有受到限制，那么它将尽可能大。

## 示例代码

本文中很多效果都没有截图，可通过视频教程查看 [视频教程地址](https://www.bilibili.com/video/BV1BM4y1L71Z?p=15)

## 什么情况下使用Center？

当我们需要对子组件进行居中的时候使用`Center`。

## Center的属性和说明

| 字段         | 属性   | 描述     |
| ------------ | ------ | -------- |
| widthFactor  | double | 宽度系数 |
| heightFactor | double | 高度系数 |
| child        | Widget | 子组件   |

## Center使用

```dart
import 'package:flutter/material.dart'; 
class CenterExample extends StatefulWidget {  
    @override  _CenterExampleState createState() => _CenterExampleState(); 
} 
class _CenterExampleState extends State<CenterExample> {
    @override  Widget build(BuildContext context) { 
        return Scaffold(      
            appBar: AppBar(
                title: Text("AlignExample"),
            ),      
            body: Center(    
                child: Text("Jimi"), 
            ),  
        ); 
    }
} 
```

## 效果展示

[![img](https://gz-ljm-blog.oss-cn-guangzhou.aliyuncs.com/blog/center.png)](https://gz-ljm-blog.oss-cn-guangzhou.aliyuncs.com/blog/center.png)
