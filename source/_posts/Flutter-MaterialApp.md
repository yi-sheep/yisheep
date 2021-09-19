---
title: Flutter-MaterialApp详解
date: 2021-09-18 08:48:33
tags: [笔记]
categories: flutter
description: Flutter-MaterialApp详解
top_img: https://gitee.com/gaoxianglong/picgo/raw/master/img/f3b8af27140c9ac90ab83012cec99bc746546e28.jpg
cover: https://gitee.com/gaoxianglong/picgo/raw/master/img/f3b8af27140c9ac90ab83012cec99bc746546e28.jpg
---

# Flutter-MaterialApp详解

## Flutter整体结构图

![img](https://gitee.com/gaoxianglong/picgo/raw/master/img/20191129195736853.png)

#### Flutter Framework

- Foundation、Animation、Painting、Gestures被合成了一个Dart UI层，对应的是Flutter中 `dart:ui` 包，是Flutter引擎暴露的底层UI库，主要提供动画、手势、绘制能力。

- Rendering层是一个抽象布局层，依赖于Dart UI层，Rendering层会构建一个UI树、当UI树有变化时，会计算出有变化的部分，然后更新UI树，最终绘制在屏幕上

- Widgets层是Flutter提供的一套基础组件库

- Material、Cupertino是Flutter提供了两种视觉风格的组件库（Android、iOS)

  #### Flutter Engine

  这是一个纯C++实现的SDK，主要执行相关的渲染、线程管理、平台事件等操作。其中包括了Skia引擎、Dart运行时、文字排版引擎等。在调用`dart:ui`库是，其实最终会走到Engine层，实现真正的绘制逻辑.

  #### Flutter Embedder

  提供四个Task Runner，将引擎一直到平台中间层代码的渲染设置、原生插件、打包、线程管理、时间循环、交互操作等。

- UI Runner 负责绑定渲染相关操作

- GPU Runner 用户执行GPU指令

- iOS Runner 处理图片数据、为GPU做准备的

- Platform Runner 所有接口调用都使用该接口

  ## 示例代码

本文中很多效果都没有截图，可通过视频教程查看 [视频教程地址](https://www.bilibili.com/video/BV1BM4y1L71Z?p=2)

## Material介绍

> Material 组件（MDC）帮助开发者实现 [Material Design](https://material.io/design)。MDC 由谷歌团队的工程师和 UX 设计师创造，为 Android、iOS、Web 和 Flutter 提供很多美观实用的 UI 组件。

## MaterialApp介绍

`MaterialApp` 包含了许多的 `Widget` ，这些 `Widget` 通常是实现 [Material Design](https://material.io/design) 的应用程序所必须要的，包含的 `Widget` 可以在 [Material Components widgets](https://flutter.dev/docs/development/ui/widgets/material) 中查看所有。 了解基本的概念，接下来我们详细看一下 `MaterialApp` 具体怎么使用。

#### Material属性和说明

> 总共33个属性

| **字段**                      | **属性**                        | **描述**                                   |
| :---------------------------- | ------------------------------- | ------------------------------------------ |
| navigatorKey                  | GlobalKey                       | 导航键                                     |
| scaffoldMessengerKey          | GlobalKey                       | 脚手架键                                   |
| home                          | Widget                          | 主页，应用打开时显示的页面                 |
| routes                        | Map<String, WidgetBuilder>      | 应用程序顶级路由表                         |
| initialRoute                  | String                          | 如果构建了导航器，则会显示第一个路由的名称 |
| onGenerateRoute               | RouteFactory                    | 路由管理拦截器                             |
| onGenerateInitialRoutes       | InitialRouteListFactory         | 生成初始化路由                             |
| onUnknownRoute                | RouteFactory                    | 当onGenerateRoute无法生成路由时调用        |
| navigatorObservers            | List                            | 创建导航器的观察者列表                     |
| builder                       | TransitionBuilder               | 在导航器上面插入小部件                     |
| title                         | String                          | 程序切换时显示的标题                       |
| onGenerateTitle               | GenerateAppTitle                | 程序切换时生成标题字符串                   |
| color                         | Color                           | 程序切换时应用图标背景颜色（仅安卓有效）   |
| theme                         | ThemeData                       | 主题颜色                                   |
| darkTheme                     | ThemeData                       | 暗黑模式主题颜色                           |
| highContrastTheme             | ThemeData                       | 系统请求“高对比度”使用的主题               |
| highContrastDarkTheme         | ThemeData                       | 系统请求“高对比度”暗黑模式下使用的主题颜色 |
| themeMode                     | ThemeMode                       | 使用哪种模式的主题（默认跟随系统）         |
| locale                        | Locale                          | 初始区域设置                               |
| localizationsDelegates        | Iterable<LocalizationsDelegate> | 本地化代理                                 |
| localeListResolutionCallback  | LocaleListResolutionCallback    | 失败或未提供设备的语言环境                 |
| localeResolutionCallback      | LocaleResolutionCallback        | 负责计算语言环境                           |
| supportedLocales              | Iterable                        | 本地化地区列表                             |
| debugShowMaterialGrid         | bool                            | 绘制基线网格叠加层（仅debug模式）          |
| showPerformanceOverlay        | bool                            | 显示性能叠加                               |
| checkerboardRasterCacheImages | bool                            | 打开栅格缓存图像的棋盘格。                 |
| checkerboardOffscreenLayers   | bool                            | 打开渲染到屏幕外位图的层的棋盘格。         |
| showSemanticsDebugger         | bool                            | 打开显示可访问性信息的叠加层               |
| debugShowCheckedModeBanner    | bool                            | 调试显示检查模式横幅                       |
| shortcuts                     | Map<LogicalKeySet, Intent>      | 应用程序意图的键盘快捷键的默认映射。       |
| actions                       | Map<Type, Action>               | 包含和定义用户操作的映射                   |
| restorationScopeId            | String                          | 应用程序状态恢复的标识符                   |
| scrollBehavior                | ScrollBehavior                  | 可滚动小部件的行为方式                     |

## 构造函数

##### 创建一个MaterialApp

> MaterialApp(…)

##### 创建一个使用 Router 而不是 Navigator 的 MaterialApp

> MaterialApp.router(…)

## 属性详解

### 1、navigatorKey

`navigatorKey` 相当于 `Navigator.of(context)` ，如果应用程序想实现无 `context` 跳转，那么可以通过设置该key, 通过 `navigatorKey.currentState.overlay.context` 获取全局context。

#### 使用方法

```dart
GlobalKey<NavigatorState> _navigatorKey = GlobalKey(); 
MaterialApp(  
    navigatorKey: _navigatorKey, 
); 
```

### 2、scaffoldMessengerKey

scaffoldMessengerKey` 主要是管理后代的 `Scaffolds`，可以实现无 `context` 调用 `snack bars

#### 使用方法

```dart
GlobalKey<ScaffoldMessengerState> _scaffoldKey = GlobalKey(); 
MaterialApp( 
    scaffoldMessengerKey: _scaffoldKey, 
);
_scaffoldKey.currentState.showSnackBar(
    SnackBar(content: Text("show SnackBar"))
); 
```

### 3、home

程序进入后的第一个界面，传入一个 `Widget`

##### 使用方法

```dart
... 
MaterialApp( 
    home: Scaffold(...),
); 
... 
```

### 4、routes

生成路由表，以键值对形式传入 `key` 为路由名字， `value` 为对应的`Widget`

##### 使用方法

```dart
MaterialApp( 
    routes: {   
        "/home": (_) => Home(), 
        "/my": (_) => My()  
            //.... 
    }, 
); 
```

### 5、initialRoute

初始路由，如果设置了该参数并且在 `routes` 找到了对应的key，将会展示对应的 `Widget` ，否则展示 `home`

##### 使用方法

```dart
MaterialApp( 
    routes: {    
        "/home": (_) => Home(),   
        "/my": (_) => My()  
    },   
    initialRoute: "/home", 
) 
```

### 6、onGenerateRoute

当跳转路由时，如果在 `routes` 找不到对应的 `key` ，会执行该回调，会调用会返回一个 `RouteSettings` ，该对象中有 `name` 路由名称、 `arguments` 路由参数。

##### 使用方法

```dart
MaterialApp(   
    routes: {    
        "/home": (_) => Home(),     
        "/my": (_) => My()   
    },  
    initialRoute: "/home",  
    onGenerateRoute: (setting) {    
        // 这里可以做进一步的逻辑处理    
        return MaterialPageRoute(builder: (_) => Home()); 
    }, 
) 
```

### 7、onGenerateInitialRoutes

如果提供了 `initialRoute` ，则用于生成初始路由的路由生成器回调，如果未设置此属性，则底层 [Navigator.onGenerateInitialRoutes](http://navigator.ongenerateinitialroutes/) 将默认为 [Navigator.defaultGenerateInitialRoutes](https://api.flutter.dev/flutter/widgets/Navigator/defaultGenerateInitialRoutes.html)。

##### 使用方法

```dart
MaterialApp(
    initialRoute: "/home",  
    onGenerateInitialRoutes: (initialRoute) {  
        return [   
            MaterialPageRoute(builder: (_) => Home()), 
            MaterialPageRoute(builder: (_) => My()),   
        ];
    }
) 
```

### 8、onUnknownRoute

效果和 `onGenerateRoute` 一样，只是先走 `onGenerateRoute` ，如果无法生成路由时则在调用 `onUnknownRoute` 。

##### 使用方法

```dart
MaterialApp(  
    routes: {    
        "/home": (_) => Home(),   
        "/my": (_) => My()    
    },   
    initialRoute: "/home",  
    onGenerateRoute: (setting) {
        return null; 
    },  
    onUnknownRoute: (setting) {   
        return MaterialPageRoute(builder: (_) => Home());  
    }, 
) 
```

### 9、navigatorObservers

路由监听器，主要是就是监听页面路由堆栈的变化，当页面进行 `push` `pop` `remove` `replace` 等操作时会进行监听。

##### 使用方法

```dart
MaterialApp( 
    navigatorObservers: [ 
        MyObserver() 
    ], 
) 
class MyObserver extends NavigatorObserver {  
    @override  void didPush(Route route, Route previousRoute) {  
        print(route); 
        print(previousRoute);   
        super.didPush(route, previousRoute); 
    }
} 
```

### 10、builder

当构建 `Widget` 前调用，主要用于字体大小、主题颜色等配置

##### 使用方法

```dart
MaterialApp(  
    routes: {    
        "/home": (_) => Home(),  
        "/my": (_) => My()  
    }, 
    initialRoute: "/home",   
    onGenerateRoute: (setting) {   
        return null; 
    },  
    onUnknownRoute: (setting) {    
        return MaterialPageRoute(builder: (_) => Home());  
    }, 	
    builder: (_, child) {  
        return Scaffold(
            appBar: AppBar(title: Text("build")), 
            body: child,
        );  
    },
) 
```

### 11、title

Android：任务管理器的程序快照之上 IOS: 程序切换管理器中

##### 使用方法

```dart
MaterialApp( 
    title: 'Flutter应用', 
); 
```

### 12、onGenerateTitle

如果非空，则调用此回调函数以生成应用程序的标题字符串，否则会使用 `title` 。每次重建页面是该方法就会回调执行。

##### 使用方法

```dart
MaterialApp( 
    title: 'Flutter应用', 
    onGenerateTitle: (_) {  
        return "我的天";   
    },
); 
```

### 13、color

设置该值的在程序切换时应用图标的背景颜色，当应用图标为透明时。

##### 使用方法

```dart
MaterialApp( 
    color: Colors.blue,
) 
```

### 14、theme

如果指定了 `darkTheme` ，那么用于提供用户界面的深色版本。如果提供了 `darkTheme` ， `themeMode` 将控制将使用哪个主题。默认值是 `ThemeData.light()` 应用程序的主题颜色

##### 使用方法

```dart
MaterialApp( 
    theme: ThemeData(    
        // 主要颜色 
        primaryColor: Colors.red 
    ),
) 
```

### 15、darkTheme

应用程序深色主题颜色

##### 使用方法

```dart
MaterialApp( 
    theme: ThemeData(   
        // 主要颜色    
        primaryColor: Colors.red 
    ),
) 
```

### 16、highContrastTheme

当系统请求“高对比度”时使用的 `ThemeData` ，当该值为空时会用 `theme` 应用该主题

##### 使用方法

```dart
MaterialApp( 
    highContrastTheme: ThemeData(  
        primaryColor: Colors.pink 
    ),
) 
```

### 17、highContrastDarkTheme

当系统再暗黑模式下请求“高对比度”时使用的 `ThemeData` ，当该值为空时会用 `darkTheme` 应用该主题。

##### 使用方法

```dart
MaterialApp( 
    highContrastDarkTheme: ThemeData(
        primaryColor: Colors.green
    ), 
) 
```

### 18、themeMode

白天模式和暗黑模式模式切换，默认值为 `ThemeMode.system`

##### 使用方法

```dart
MaterialApp( 
    themeMode: ThemeMode.dark
) 
```

### 19、locale

主要用于语言切换时，如果为 `null` 时使用系统区域

##### 使用方法

```dart
MaterialApp(  
    locale: Locale('zh', 'CN') // 中文简体 
) 
```

### 20、localizationsDelegates

本地化委托

##### 使用方法

```dart
MaterialApp( 
    locale: Locale('zh', 'CN') // 中文简体 
    localizationsDelegates: [  
        GlobalMaterialLocalizations.delegate,  
        GlobalWidgetsLocalizations.delegate, 
    ],
) 
```

### 21、supportedLocales

当前应用支持的 `Locale` 列表

##### 使用方法

```dart
MaterialApp(  
    locale: Locale('zh', 'CN'), // 中文简体  
    supportedLocales: [    
        Locale('en', 'US'), //美国英语    
        Locale("zh", 'CN'), //中文简体  
    ]
) 
```

### 22、localeListResolutionCallback

监听系统语言切换事件，一些安卓系统特性，可设置多语言列表，默认以第一个列表为默认语言

##### 使用方法

```dart
MaterialApp(  
    locale: Locale('zh', 'CN'), // 中文简体  
    supportedLocales: [   
        Locale('en', 'US'), //美国英语   
        Locale("zh", 'CN'), //中文简体 
    ],  
    localeListResolutionCallback: (List<Locale> locales, Iterable<Locale> supportedLocales) 
    {    
        // 系统切换语言时调用    
        return Locale("zh", 'CN'); 
    }, 
) 
```

### 23、localeResolutionCallback

监听系统语言切换事件

##### 使用方法

```dart
MaterialApp(
    locale: Locale('zh', 'CN'), // 中文简体  
    supportedLocales: [   
        Locale('en', 'US'), //美国英语  
        Locale("zh", 'CN'), //中文简体 
    ],  
    localeResolutionCallback: (Locale locale, Iterable<Locale> supportedLocales){   
        return Locale("zh", 'CN'); 
    },
) 
```

### 24、debugShowMaterialGrid

在 `debug` 模式下展示基线网格

##### 使用方法

```dart
MaterialApp( 
    debugShowMaterialGrid: true
) 
```

### 25、showPerformanceOverlay

显示性能叠加，开启此模式主要用于性能测试

##### 使用方法

```dart
MaterialApp( 
    showPerformanceOverlay: true 
) 
```

### 26、checkerboardRasterCacheImages

打开栅格缓存图像的棋盘格

##### 使用方法

```dart
MaterialApp(
    checkerboardRasterCacheImages: true
) 
```

### 27、checkerboardOffscreenLayers

打开渲染到屏幕外位图的层的棋盘格

##### 使用方法

```dart
MaterialApp( 
    checkerboardOffscreenLayers: true
) 
```

### 28、showSemanticsDebugger

打开显示可访问性信息的叠加层，展示组件之间的关系、占位大小

##### 使用方法

```dart
MaterialApp(
    showSemanticsDebugger: true 
) 
```

### 29、debugShowCheckedModeBanner

调试显示检查模式横幅

##### 使用方法

```dart
MaterialApp( 
    debugShowCheckedModeBanner: false
) 
```

### 30、shortcuts以及actions

`shortcuts` 和 `actions` 是将物理键盘事件绑定到用户界面中的操作。 比如，要在您的应用程序中定义键盘快捷键，这里不做过多的描述，后面我会专门拿一个专题来讲解。

### 31、restorationScopeId

定义一个应用程序状态恢复的标识符，提供标识符会将 [RootRestorationScope](https://api.flutter.dev/flutter/widgets/RootRestorationScope-class.html) 插入 `widget` 层次结构，从而为后代 `widget` 启用状态恢复。还可以通过标识符使 `WidgetsApp` 构建的导航器恢复其状态（即恢复活动路由的历史堆栈），由于这里涉及的内容较多，后面会专门拿一个专题来讲解。

### 32、scrollBehavior

统一滚动行为设置，设置后子组件将返回对应的滚动行为

##### 使用方法

```dart
MaterialApp( 
    scrollBehavior: ScrollBehaviorModified()
)  
class ScrollBehaviorModified extends ScrollBehavior { 
    const ScrollBehaviorModified();
    @override  ScrollPhysics getScrollPhysics(BuildContext context) {  
        switch (getPlatform(context)) {  
            case TargetPlatform.iOS:   
            case TargetPlatform.macOS:  
            case TargetPlatform.android:   
                return const BouncingScrollPhysics();  
            case TargetPlatform.fuchsia:   
            case TargetPlatform.linux: 
            case TargetPlatform.windows:     
                return const ClampingScrollPhysics();  
        }   
        return null; 
    } 
}
```

