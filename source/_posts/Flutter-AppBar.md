---
title: Flutter-AppBar详解
date: 2021-09-18 10:22:13
tags: [笔记]
categories: flutter
description: Flutter-AppBar详解
top_img: https://gitee.com/gaoxianglong/picgo/raw/master/img/f3b8af27140c9ac90ab83012cec99bc746546e28.jpg
cover: https://gitee.com/gaoxianglong/picgo/raw/master/img/f3b8af27140c9ac90ab83012cec99bc746546e28.jpg
---

# Flutter-AppBar详解

## AppBar介绍

AppBar是基于Material Design设计风格的应用栏，一般使用在Scaffold内部，作为顶部导航栏。

#### 为什么需要AppBar

1、因为导航栏里面一般由左侧功能键（返回键、菜单键）、标题、右侧功能键组成，而AppBar里面内置封装了这些组件，使用起来非常方便。

2、可以做一些特殊的导航栏，比如可滚动的导航栏。

3、根据环境 `MediaQuery` 的填充插入内容，以避免系统 `UI` 入侵。

## 示例代码

本文中很多效果都没有截图，可下载源代码运行项目 [源代码地址](https://github.com/JunAILiang/flutter_code)，或者通过视频教程查看 [视频教程地址](https://www.bilibili.com/video/BV1BM4y1L71Z?p=4)

## AppBar属性和说明

> 总共28个属性

| 字段                      | 属性                 | 描述                                                         |
| ------------------------- | -------------------- | ------------------------------------------------------------ |
| key                       | Key                  | 当组件在组件树中移动时使用Key可以保持组件之前状态            |
| leading                   | Widget               | 通常情况下返回一个返回键（IconButton)                        |
| leadingWidth              | double               | 左侧leading的宽度，默认56                                    |
| automaticallyImplyLeading | bool                 | 和leading配合使用，如果为true并且leading为空的情况下，会自动配置返回键 |
| title                     | Widget               | 导航栏的标题                                                 |
| centerTitle               | bool                 | 标题是否居中，不同操作系统默认显示位置不一样                 |
| actions                   | List                 | 一个Widget列表                                               |
| bottom                    | PreferredSizeWidget  | 出现在导航栏底部的控件                                       |
| elevation                 | double               | 控制导航栏下方阴影的大小                                     |
| shadowColor               | Color                | 控制导航栏下方阴影的颜色                                     |
| shape                     | ShapeBorder          | 导航栏的形状以及阴影                                         |
| backgroundColor           | Color                | 导航栏的背景颜色                                             |
| foregroundColor           | Color                | 导航栏中文本和图标的颜色                                     |
| backwardsCompatibility    | bool                 | 与foregroundColor配合使用                                    |
| iconTheme                 | IconThemeData        | 导航栏图标的颜色、透明度、大小的配置                         |
| actionsIconTheme          | IconThemeData        | 导航栏右侧图标的颜色、透明度、大小的配置                     |
| textTheme                 | TextTheme            | 导航栏文本的排版样式                                         |
| primary                   | bool                 | 导航栏是否显示在屏幕顶部                                     |
| excludeHeaderSemantics    | bool                 | 标题是否应该用 [Semantics] 包裹，默认false                   |
| titleSpacing              | double               | title内容的间距                                              |
| toolbarOpacity            | double               | 导航栏的透明度                                               |
| bottomOpacity             | double               | 导航栏底部的透明度                                           |
| toolbarHeight             | double               | 导航栏的高度，默认kToolbarHeight                             |
| toolbarTextStyle          | TextStyle            | 导航栏图标的颜色                                             |
| titleTextStyle            | TextStyle            | 导航栏标题的默认颜色                                         |
| flexibleSpace             | Widget               | 堆叠在工具栏和选项卡栏的后面                                 |
| systemOverlayStyle        | SystemUiOverlayStyle | 叠加层的样式                                                 |
| brightness                | Brightness           | 导航栏的亮度，改属性已废弃，用systemOverlayStyle代替         |

## AppBar详细使用

### 1、key

`key` 是用来作为`Widget` 、`Element` 和 `SemanticsNode` 的标识，当组件在组件树中移动时使用Key可以保持组件之前状态。

#### 使用方法

```dart
GlobalKey _appBarKey = GlobalKey(); 
@override Widget build(BuildContext context) { 
    return Scaffold(
        appBar: AppBar(    
            key: _appBarKey,  
        ), 
    );
} 
```

### 2、leading

appBar` 左侧显示的一个 `Widget`，一般显示返回键 `Icon` 或 `IconButton

#### 使用方法

```dart
@override Widget build(BuildContext context) { 
    return Scaffold(
        appBar: AppBar(  
            leading: IconButton(      
                onPressed: (){     
                    Navigator.pop(context);  
                },       
                icon: Icon(
                    Icons.arrow_back_sharp,
                    color: Colors.white,
                )    
            ),  
        ), 
    ); 
} 
```

### 3、leadingWidth

左侧leading的宽度，默认56

#### 使用方法

```dart
@override Widget build(BuildContext context) {
    return Scaffold(  
        appBar: AppBar(    
            leading: IconButton(   
                onPressed: (){       
                    Navigator.pop(context);    
                },        
                icon: Icon(
                    Icons.arrow_back_sharp,
                    color: Colors.white,
                )   
            ),  
            leadingWidth: 60,  
        ), 
    ); 
} 
```

### 4、automaticallyImplyLeading

当`leading` 未配置时，在二级页面下会自动展示一个返回键，默认值为 `true`

#### 使用方法

```dart
@override Widget build(BuildContext context) { 
    return Scaffold(   
        appBar: AppBar(    
            automaticallyImplyLeading: false,   
        ),  
    ); 
} 
```

### 5、title

导航栏的标题，一般是显示当前页面的标题文字

#### 使用方法

```dart
@override Widget build(BuildContext context) { 
    return Scaffold(  
        appBar: AppBar( 
            title: Text("AppBarExample"), 
        ),  
    );
} 
```

### 6、centerTitle

标题是否居中，不同操作系统默认显示位置不一样，安卓默认显示在左侧，苹果默认显示在中间

#### 使用方法

```dart
@override Widget build(BuildContext context) {  
    return Scaffold(   
        appBar: AppBar(   
            title: Text("AppBarExample"),  
            centerTitle: true,  
        ),  
    );
} 
```

### 7、actions

一个 `Widget` 列表，代表 `Toolbar` 中所显示的菜单，对于常用的菜单，通常使用 `IconButton` 来表示；对于不常用的菜单通常使用 `PopupMenuButton` 来显示为三个点，点击后弹出二级菜单

```dart
@override Widget build(BuildContext context) {  
    return Scaffold(   
        appBar: AppBar(     
            actions: [      
                IconButton(      
                    onPressed: (){},    
                    tooltip: "扫一扫",   
                    icon: Icon(Icons.qr_code_scanner),  
                ),      
                IconButton(    
                    onPressed: (){},     
                    tooltip: "添加",      
                    icon: Icon(Icons.add),     
                )     
            ],  
        ), 
    ); 
} 
```

### 8、bottom

出现在应用栏底部的控件，一般是 `TabBar`

#### 使用方法

```dart
import 'package:flutter/material.dart'; 
class AppBarExample extends StatefulWidget {
    @override  _AppBarExampleState createState() => _AppBarExampleState(); 
} 
class _AppBarExampleState extends State<AppBarExample> with SingleTickerProviderStateMixin{
    TabController _tabController; 
    @override  void initState() { 
        // TODO: implement initState   
        super.initState();  
        _tabController = TabController(length: 2, vsync: this); 
    }  
    @override  Widget build(BuildContext context) {  
        return Scaffold(   
            appBar: AppBar(   
                bottom: TabBar(       
                    controller: _tabController,  
                    tabs: [     
                        Tab(
                            text: "火车", 
                            icon: Icon(Icons.bus_alert),
                        ),      
                        Tab(
                            text: "汽车", 
                            icon: Icon(Icons.bus_alert),
                        )      
                    ],     
                ),  
            ),    
        ); 
    } 
} 
```

### 9、elevation

控制应用栏下方阴影的大小，这个值不能是一个负值。

#### 使用方法

```dart
@override Widget build(BuildContext context) {
    return Scaffold(  
        appBar: AppBar(   
            elevation: 10,   
        ),
    ); 
} 
```

### 10、shadowColor

控制导航栏下方阴影的颜色

#### 使用方法

```dart
@override Widget build(BuildContext context) {  
    return Scaffold(    
        appBar: AppBar(     
            elevation: 10,   
            shadowColor: Colors.green, 
        ),
    );
} 
```

### 11、shape

导航栏的形状以及阴影

#### 使用方法

```dart
@override Widget build(BuildContext context) { 
    return Scaffold(   
        appBar: AppBar(    
            elevation: 10,     
            shadowColor: Colors.green,  
            shape: RoundedRectangleBorder(   
                side: BorderSide(     
                    color: Colors.red,     
                    width: 5     
                )    
            )  
        ), 
    ); 
} 
```

### 12、backgroundColor

导航栏的背景颜色

#### 使用方法

```dart
@override Widget build(BuildContext context) { 
    return Scaffold(
        appBar: AppBar(     
            backgroundColor: Colors.orange, 
        ), 
    ); 
} 
```

### 13、foregroundColor

导航栏中文本和图标的颜色

#### 使用方法

```dart
@override Widget build(BuildContext context) { 
    return Scaffold(  
        appBar: AppBar(  
            foregroundColor: Colors.black, 
        ), 
    ); 
} 
```

### 14、backwardsCompatibility

与foregroundColor配合使用

### 使用方法

```dart
@override Widget build(BuildContext context) {  
    return Scaffold(   
        appBar: AppBar(    
            foregroundColor: Colors.black,  
            backwardsCompatibility: true,   
        ), 
    ); 
} 
```

### 15、iconTheme

导航栏图标的颜色、透明度、大小的配置

### 使用方法

```dart
@override Widget build(BuildContext context) {
    return Scaffold(  
        appBar: AppBar(    
            leading: IconButton(     
                onPressed: (){  
                    Navigator.pop(context);    
                },       
                icon: Icon(Icons.arrow_back_sharp, color: Colors.white,)   
            ),    
            iconTheme: IconThemeData(     
                color: Colors.orange,   
                opacity: 1,    
                size: 50    
            ), 
        ), 
    );
} 
```

### 16、actionsIconTheme

导航栏右侧图标的颜色、透明度、大小的配置

### 使用方法

```dart
@override Widget build(BuildContext context) { 
    return Scaffold(  
        appBar: AppBar(   
            actions: [     
                IconButton(      
                    onPressed: (){},    
                    tooltip: "扫一扫",    
                    icon: Icon(Icons.qr_code_scanner),   
                ),      
                IconButton(   
                    onPressed: (){},      
                    tooltip: "添加",     
                    icon: Icon(Icons.add),    
                )    
            ],   
            actionsIconTheme: IconThemeData(  
                color: Colors.purple,  
            ),  
        ),  
    ); 
} 
```

### 17、textTheme

导航栏文本的排版样式，默认使用`ThemeData.primaryTextTheme`

### 18、primary

导航栏是否显示在屏幕顶部

#### 使用方法

```dart
@override Widget build(BuildContext context) { 
    return Scaffold( 
        appBar: AppBar(    
            backrogoundColor: Colors.black, 
            primary: true,  
        ), 
    ); 
} 
```

### 19、excludeHeaderSemantics

标题是否应该用 [Semantics] 包裹，默认false

#### 使用方法

```dart
@override Widget build(BuildContext context) {  
    return Scaffold(  
        appBar: AppBar(    
            backrogoundColor: Colors.black,   
            primary: true,  
            excludeHeaderSemantics: true,  
        ), 
    ); 
} 
```

### 20、titleSpacing

标题内容的间距，如果为0，将占用全部空间

#### 使用方法

```dart
@override Widget build(BuildContext context) { 
    return Scaffold(  
        appBar: AppBar(   
            title: Text("AppBarExample"), 
            centerTitle: true,    
            titleSpacing: 0,  
        ), 
    ); 
} 
```

### 21、toolbarOpacity

导航栏的透明度

#### 使用方法

```dart
@override Widget build(BuildContext context) {
    return Scaffold(  
        appBar: AppBar(     
            backrogoundColor: Colors.black,  
            toolbarOpacity: 0.5,   
        ), 
    );
} 
```

### 22、bottomOpacity

导航栏底部的透明度

#### 使用方法

```dart
import 'package:flutter/material.dart'; 
class AppBarExample extends StatefulWidget {  
    @override  _AppBarExampleState createState() => _AppBarExampleState(); 
}
class _AppBarExampleState extends State<AppBarExample> with SingleTickerProviderStateMixin{ 
    TabController _tabController;  
    @override  void initState() { 
        // TODO: implement initState   
        super.initState();   
        _tabController = TabController(length: 2, vsync: this); 
    } 
    @override  Widget build(BuildContext context) { 
        return Scaffold(    
            appBar: AppBar(      
                bottom: TabBar(     
                    controller: _tabController,       
                    tabs: [           
                        Tab(text: "火车", icon: Icon(Icons.bus_alert),),   
                        Tab(text: "汽车", icon: Icon(Icons.bus_alert),)     
                    ],     
                ), 		
                bottomOpacity: 0.5,   
            ),   
        ); 
    } 
} 
```

### 23、toolbarHeight

导航栏的高度，默认kToolbarHeight

#### 使用方法

```dart
@override Widget build(BuildContext context) { 
    return Scaffold( 
        appBar: AppBar(  
            backrogoundColor: Colors.black,  
            toolbarHeight: 200,
        ),
    ); 
} 
```

### 24、toolbarTextStyle

导航栏图标的颜色

#### 使用方法

```dart
@override Widget build(BuildContext context) { 
    return Scaffold(  
        appBar: AppBar(    
            leading: IconButton(   
                onPressed: (){  
                    Navigator.pop(context);  
                },        
                icon: Icon(Icons.arrow_back_sharp, color: Colors.white,)  
            ),    
            toolbarTextStyle: TextStyle(     
                color: Colors.black   
            ),  
        ),  
    );
} 
```

### 25、titleTextStyle

导航栏标题的默认颜色

#### 使用方法

```dart
@override Widget build(BuildContext context) { 
    return Scaffold(  
        appBar: AppBar(   
            title: Text("AppBarExample"),  
            centerTitle: true,    
            titleSpacing: 0,    
            titleTextStyle: TextStyle(  
                color: Colors.red    
            ),   
        ), 
    ); 
} 
```

### 26、flexibleSpace、systemOverlayStyle、brightness

`flexibleSpace` 以及 `systemOverlayStyle` 一般都是在配合 `SliverAppBar` 使用的，这里不做过多的描述。而 `brightness` 已经废弃，用 `systemOverlayStyle` 代替。

## 总结

以上是针对 `AppBar` 的所有使用方法，最常用的属有`leading`、`title`、`actions`、`centerTitle`、`bottom`、`backgroundColor`，其他属性都是在特定的情况才会使用。
