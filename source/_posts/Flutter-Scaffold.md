---
title: Flutter-Scaffold详解
date: 2021-09-18 09:25:34
tags: [笔记]
categories: flutter
description: Flutter-Scaffold详解
top_img: https://gitee.com/gaoxianglong/picgo/raw/master/img/f3b8af27140c9ac90ab83012cec99bc746546e28.jpg
cover: https://gitee.com/gaoxianglong/picgo/raw/master/img/f3b8af27140c9ac90ab83012cec99bc746546e28.jpg
---

## Scaffold介绍

`Scaffold` 我们通常俗称为脚手架，在前面的文章中我们说到，`Material` 组件（MDC）帮助开发者实现 [Material Design](https://material.io/design)，`Scaffold` 实现了基本的 [Material Design](https://material.io/design) 布局结构。在 `Material` 设计中定义的单个界面上的各种布局元素，在 Scaffold 中都支持。

#### Scaffold在什么情况下使用

在每一个页面中基本都需要用到`Scaffold` ，除非当你的页面不需要导航区，但仍希望您使用 `Scaffold` 来作为每个页面的顶级组件。

## 示例代码

本文中很多效果都没有截图，可通过视频教程查看 [视频教程地址](https://www.bilibili.com/video/BV1BM4y1L71Z?p=3)

## Scaffold属性和说明

> 总共23个属性

| 字段                           | 属性                         | 描述                                                   |
| ------------------------------ | ---------------------------- | ------------------------------------------------------ |
| appBar                         | PreferredSizeWidget          | 显示脚手架的顶部导航区                                 |
| body                           | Widget                       | 显示脚手架的主要内容                                   |
| floatingActionButton           | Widget                       | 悬浮按钮，位于右下角                                   |
| floatingActionButtonLocation   | FloatingActionButtonLocation | 决定悬浮按钮的位置                                     |
| floatingActionButtonAnimator   | FloatingActionButtonAnimator | 决定悬浮按钮的动画                                     |
| persistentFooterButtons        | List                         | 显示在脚手架底部的一组按钮                             |
| drawer                         | Widget                       | 左侧抽屉菜单组件                                       |
| onDrawerChanged                | DrawerCallback               | 左侧抽屉菜单改变事件回调                               |
| endDrawer                      | Widget                       | 右侧抽屉菜单组件                                       |
| onEndDrawerChanged             | DrawerCallback               | 右侧抽屉菜单改变事件回调                               |
| bottomNavigationBar            | Widget                       | 底部导航条                                             |
| bottomSheet                    | Widget                       | 持久在body下方，底部控件上方的控件                     |
| backgroundColor                | Color                        | 脚手架背景颜色                                         |
| resizeToAvoidBottomInset       | bool                         | 防止小组件重复                                         |
| primary                        | bool                         | 脚手架是否延伸到顶部                                   |
| drawerDragStartBehavior        | DragStartBehavior            | 检测手势行为方式，与drawer配合使用                     |
| extendBody                     | bool                         | 是否延伸到底部                                         |
| extendBodyBehindAppBar         | bool                         | 是否延伸到顶部，用于做半透明、毛玻璃效果的主要控制属性 |
| drawerScrimColor               | Color                        | 侧边栏弹出时非遮盖层主页面的颜色                       |
| drawerEdgeDragWidth            | double                       | 侧边栏弹出时非遮罩层的宽度                             |
| drawerEnableOpenDragGesture    | bool                         | 左侧抽屉是否支持手势滑动                               |
| endDrawerEnableOpenDragGesture | bool                         | 右侧抽屉是否支持手势滑动                               |
| restorationId                  | String                       | 状态还原标识符                                         |

## Scaffold属性详细使用

### 1、appBar

显示脚手架的顶部导航栏

#### 使用方法

```dart
Scaffold( 
    appBar: AppBar(   
        title: Text("Scaffold"),
    ),
); 
```

### 2、body

显示脚手架的主要内容

#### 使用方法

```dart
Scaffold(  
    appBar: AppBar(  
        title: Text("Scaffold"), 
    ), 
    body: Center(  
        child: Text("body"), 
    ), 
); 
```

### 3、floatingActionButton

悬浮按钮，默认位于右小角

#### 使用方法

```dart
Scaffold(  
    appBar: AppBar(  	
        title: Text("Scaffold"), 
    ),  
    body: Center(  
        child: Text("body"), 
    ),  
    floatingActionButton: FloatingActionButton(  
        onPressed: (){   
            print("add");  
        },  
        child: Icon(Icons.add) 
    ),
); 
```

### 4、floatingActionButtonLocation

决定悬浮按钮的位置

#### 使用方法

```dart
Scaffold( 
    appBar: AppBar(  	
        title: Text("Scaffold"), 
    ),  
    body: Center(  	
        child: Text("body"), 
    ),  
    floatingActionButton: FloatingActionButton(  
        onPressed: (){   
            print("add");  
        },  
        child: Icon(Icons.add) 
    ), 
    floatingActionButtonLocation: FloatingActionButtonLocation.miniCenterDocked,
); 
```

### 5、floatingActionButtonAnimator

决定悬浮按钮的动画

#### 使用方法

```dart
Scaffold( 
    appBar: AppBar(  
        title: Text("Scaffold"), 
    ),  
    body: Center(  
        child: Text("body"), 
    ), 
    floatingActionButton: FloatingActionButton( 
        onPressed: (){  
            print("add");   
        },  
        child: Icon(Icons.add) 
    ), 
    floatingActionButtonLocation:FloatingActionButtonLocation.miniCenterDocked,  
    floatingActionButtonAnimator: FloatingActionButtonAnimator.scaling, 
); 
```

### 6、persistentFooterButtons

显示在脚手架底部的一组按钮

#### 使用方法

```dart
Scaffold(  
    appBar: AppBar(  	
        title: Text("Scaffold"), 
    ),  
    body: Center(  
        child: Text("body"), 
    ), 
    persistentFooterButtons: [   
        TextButton(
            onPressed: (){}, 
            child: Text("Text1")),  
        TextButton(
            onPressed: (){}, 
            child: Text("Text2")), 
    ],
); 
```

### 7、drawer

左侧抽屉菜单组件，如果需要自定义可通过设置 `Scaffold` 的 `key` 来操作手动打开侧边栏，代码如下

#### 使用方法

```dart
GlobalKey<ScaffoldState> _scaffoldKey = GlobalKey(); 
Scaffold( 
    key: _scaffoldKey, 
    appBar: AppBar( 
        title: Text("Scaffold"), 
        leading: IconButton(
            onPressed: (){    
                _scaffoldKey.currentState.openDrawer(); 
            }, 
            icon: Icon(Icons.menu_open)), 
    ),
    body: Center(  
        child: Text("body"),
    ), 
    drawer: Drawer(   
        child: Center(child: Text("draw"),), 
    ) 
); 
```

### 8、onDrawerChanged

左侧抽屉菜单改变事件回调

#### 使用方法

```dart
GlobalKey<ScaffoldState> _scaffoldKey = GlobalKey(); 
Scaffold( 
    key: _scaffoldKey, 
    appBar: AppBar(  
        title: Text("Scaffold"),  
        leading: IconButton(
            onPressed: (){     
                _scaffoldKey.currentState.openDrawer();  
            }, 
            icon: Icon(Icons.menu_open)), 
    ),  
    body: Center(  
        child: Text("body"), 
    ), 
    drawer: Drawer(  
        child: Center(child: Text("draw"),), 
    ), 
    onDrawerChanged: (isOpen) {
        print(isOpen); 
    },
); 
```

### 9、endDrawer

右侧抽屉菜单组件,功能和 `drawer` 一样，唯一的区别是一个在左侧，一个在右侧。

#### 使用方法

```dart
GlobalKey<ScaffoldState> _scaffoldKey = GlobalKey();
Scaffold( 
    key: _scaffoldKey, 
    appBar: AppBar(  
        title: Text("Scaffold"),  
        leading: IconButton(
            onPressed: (){     
                _scaffoldKey.currentState.openDrawer();   
            }, 
            icon: Icon(Icons.menu_open)),
    ), 
    body: Center(  
        child: Text("body"), 
    ),
    endDrawer: Drawer(  
        child: Center(child: Text("draw"),), 
    ), 
); 
```

### 10、onEndDrawerChanged

右侧抽屉菜单改变事件回调，使用方式和 `onDrawerChanged` 一样。

#### 使用方法

```dart
GlobalKey<ScaffoldState> _scaffoldKey = GlobalKey(); 
Scaffold(  
    key: _scaffoldKey,  
    appBar: AppBar(  	
        title: Text("Scaffold"),   
        leading: IconButton(
            onPressed: (){ 
                _scaffoldKey.currentState.openDrawer(); 
            },
            icon: Icon(Icons.menu_open)), 
    ),  
    body: Center(  
        child: Text("body"), 
    ),
    endDrawer: Drawer(  
        child: Center(child: Text("draw"),),
    ),  
    onEndDrawerChanged: (isOpen) { 
        print(isOpen); 
    },
); 
```

### 11、bottomNavigationBar

 底部导航条，常用于切换底部 `item`

#### 使用方法

```dart
int _currentIndex = 0;  
List<Widget> _pages = [  
    Center(child: Text("tab1"),), 
    Center(child: Text("tab2"),), 
]; 
Scaffold( 
    appBar: AppBar(  
        title: Text("Scaffold"),
    ),
    body: _pages[_currentIndex], 
    bottomNavigationBar: BottomNavigationBar( 
        items: [  
            BottomNavigationBarItem(    
                label: "tab1",   
                icon: Icon(Icons.settings)  
            ),    
            BottomNavigationBarItem(    
                label: "tab2",  
                icon: Icon(Icons.settings)   
            )  
        ],  
        currentIndex: _currentIndex, 
        onTap: (currentIndex) { 
            setState(() {   
                _currentIndex = currentIndex;   
            });  
        }, 
    ), 
); 
```

### 12、bottomSheet

持久在body下方，底部控件上方的控件

#### 使用方法

```dart
Scaffold(  
    appBar: AppBar(   
        title: Text("Scaffold"), 
    ),  
    body: _pages[_currentIndex], 
    bottomSheet: Container(
        child: Row( 
            children: [    
                Expanded(child: TextField()),    
                ElevatedButton(
                    onPressed: (){}, 
                    child: Text("发送"))   
            ], 
        ),
    ) 
); 
```

### 13、backgroundColor

脚手架背景颜色

#### 使用方法

```dart
Scaffold( 
    appBar: AppBar(   
        title: Text("Scaffold"), 
    ), 
    body: _pages[_currentIndex], 
    backgroundColor: Colors.pink, 
); 
```

### 14、resizeToAvoidBottomInset

防止组件重复，当键盘弹起时会挡住组件，该值设置为 `ture` 可防止键盘遮挡

#### 使用方法

```dart
Scaffold( 
    appBar: AppBar(  
        title: Text("Scaffold"), 
    ), 
    body: _pages[_currentIndex], 
    resizeToAvoidBottomInset: true, 
); 
```

### 15、primary

脚手架是否延伸到顶部

#### 使用方法

```dart
Scaffold(  
    appBar: AppBar(  
        title: Text("Scaffold"), 
    ),  
    body: _pages[_currentIndex],
    primary: true, 
); 
```

### 16、drawerDragStartBehavior

拖动行为方式，与 `drawer `配合使用，用于打开和关闭抽屉的拖动行为将在检测到拖动手势时开始。 如果设置为 DragStartBehavior.down，它将在首次检测到 down 事件时开始。当拖动返回时会使用 `DragStartBehavior.down` 是有很明显的卡顿，建议使用 `DragStartBehavior.start`

#### 使用方法

```dart
GlobalKey<ScaffoldState> _scaffoldKey = GlobalKey(); 
Scaffold( 
    key: _scaffoldKey, 
    appBar: AppBar(  
        title: Text("Scaffold"), 
        leading: IconButton(
            onPressed: (){     
                _scaffoldKey.currentState.openDrawer();   
            }, 
            icon: Icon(Icons.menu_open)),  
    ),  
    body: Center(  
        child: Text("body"), 
    ), 
    drawer: Drawer(  
        child: Center(child: Text("draw"),), 
    ),  
    drawerDragStartBehavior: DragStartBehavior.start 
); 
```

### 17、extendBody

是否延伸到底部，主要用于做半透明效果。

#### 使用方法

```dart
Scaffold( 
    appBar: AppBar( 
        title: Text("Scaffold"),
    ), 
    body: _pages[_currentIndex],
    extendBody: true, 
); 
```

### 18、extendBodyBehindAppBar

是否延伸到顶部，用于做半透明、毛玻璃效果的主要控制属性

#### 使用方法

```dart
Scaffold( 
    appBar: AppBar(   
        title: Text("Scaffold"), 
    ), 
    body: _pages[_currentIndex], 
    extendBodyBehindAppBar: true, 
); 
```

### 19、drawerScrimColor

侧边栏弹出时非遮盖层主页面的颜色

#### 使用方法

```dart
GlobalKey<ScaffoldState> _scaffoldKey = GlobalKey(); 
Scaffold(  
    key: _scaffoldKey, 
    appBar: AppBar(  	
        title: Text("Scaffold"),   
        leading: IconButton(
            onPressed: (){  
                _scaffoldKey.currentState.openDrawer(); 
            }, 
            icon: Icon(Icons.menu_open)), 
    ), 
    body: Center(  
        child: Text("body"),  
    ), 
    drawer: Drawer(  
        child: Center(child: Text("draw"),), 
    ), 
    drawerScrimColor: Colors.green,
); 
```

### 20、drawerEdgeDragWidth

侧边栏弹出时非遮罩层的宽度，当滑动的距离小于该值时，遮罩层会弹出。默认值是20

#### 使用方法

```dart
GlobalKey<ScaffoldState> _scaffoldKey = GlobalKey(); 
Scaffold( 
    key: _scaffoldKey, 
    appBar: AppBar(  
        title: Text("Scaffold"),  
        leading: IconButton(
            onPressed: (){      
                _scaffoldKey.currentState.openDrawer();  
            },
            icon: Icon(Icons.menu_open)), 
    ), 
    body: Center(  
        child: Text("body"), 
    ),  
    drawer: Drawer( 
        child: Center(child: Text("draw"),), 
    ),  
    drawerScrimColor: Colors.green, 
    drawerEdgeDragWidth: 100,
); 
```

### 21、drawerEnableOpenDragGesture

左侧抽屉是否支持手势滑动，如果设置为 `false` ，将不能通过侧滑手势滑出，默认`true`

#### 使用方法

```dart
GlobalKey<ScaffoldState> _scaffoldKey = GlobalKey(); 
Scaffold( 
    key: _scaffoldKey, 
    appBar: AppBar(   
        title: Text("Scaffold"),  
        leading: IconButton(
            onPressed: (){     
                _scaffoldKey.currentState.openDrawer(); 
            }, 
            icon: Icon(Icons.menu_open)),
    ), 
    body: Center( 
        child: Text("body"), 
    ),  
    drawer: Drawer(  
        child: Center(child: Text("draw"),), 
    ),  
    drawerScrimColor: Colors.green,  
    drawerEnableOpenDragGesture: false, 
); 
```

### 22、endDrawerEnableOpenDragGesture

右侧抽屉是否支持手势滑动，如果设置为 `false` ，将不能通过侧滑手势滑出，默认 `true`

```dart
GlobalKey<ScaffoldState> _scaffoldKey = GlobalKey(); 
Scaffold( 
    key: _scaffoldKey, 
    appBar: AppBar(  
        title: Text("Scaffold"), 
        leading: IconButton(
            onPressed: (){   
                _scaffoldKey.currentState.openDrawer();   
            }, 
            icon: Icon(Icons.menu_open)),  
    ),  
    body: Center(  
        child: Text("body"),
    ),  
    drawer: Drawer(  
        child: Center(child: Text("draw"),), 
    ),  
    drawerScrimColor: Colors.green, 
    drawerEnableOpenDragGesture: false, 
    endDrawerEnableOpenDragGesture: false, 
); 
```

### 23、restorationId

状态还原标识符

### 使用方法

```dart
GlobalKey<ScaffoldState> _scaffoldKey = GlobalKey();
Scaffold(  
    key: _scaffoldKey,  
    appBar: AppBar(   
        title: Text("Scaffold"),  
        leading: IconButton(
            onPressed: (){  
                _scaffoldKey.currentState.openDrawer();   
            }, 
            icon: Icon(Icons.menu_open)), 
    ),  
    body: Center(  
        child: Text("body"), 
    ), 
    restorationId: "scaffold"
); 
```

## 总结

以上是针对Scaffold的所有使用方法，最常用的属性有`appBar`、`body`，其他属性都是在特定的情况才会使用。
