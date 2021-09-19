---
title: flutter笔记
date: 2021-09-17 10:25:27
tags: [笔记]
categories: flutter
description: flutter
top_img: https://gitee.com/gaoxianglong/picgo/raw/master/img/f3b8af27140c9ac90ab83012cec99bc746546e28.jpg
cover: https://gitee.com/gaoxianglong/picgo/raw/master/img/f3b8af27140c9ac90ab83012cec99bc746546e28.jpg
top: 10
---

# Flutter

**参考网站：**

[Flutter 中文文档 - Flutter 中文资源 | 安装和环境配置](https://flutter.cn/docs/get-started/install)

[Flutter中文网](https://flutterchina.club/)

[Flutter实战(电子书)](https://book.flutterchina.club/)

[Pub Dart第三方包](https://pub.flutter-io.cn/)

---

# Widget组件

Flutter中万物皆为`Widget`，就如同Android中的`Activity`，HarmonyOS中的`Ability`。

## StatelessWidget---无状态的组件

其他组件通过`extends`继承`StatelessWidget`来表示当前组件是无状态的。

`StatelessWidget`有一个待实现的函数`build`，当前这个`Widget`被创建的时候就会调用这个`build`函数，`build`要返回当前这个组件长样子，也就是返回的还是一个`Widget`。

例子：

```dart
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Widget();
  }
}
```

## StatefulWidget---有状态的组件

其他组件通过`extends`继承`StatefulWidget`来表示当前组件是有状态的。

继承了`StatefulWidget`的组件需要创建一个私有的状态类，用来管理组件的状态，状态类要继承`State<组件>`，这是泛型的写法。这个状态类要去实现`build`函数，`build`要返回当前这个组件长样子，也就是返回的还是一个`Widget`。

在这个组件的状态类中可以去调用`setState`，每一次调用`setState`都会重新绘制一次组件，也就是调用`build`函数。所以我们在`setState`中去修改一些和组件有关的数据时就能做到改变当前这个组件。

例子：

```dart
class MyWidget extends StatefulWidget {
  const MyWidget({Key? key}) : super(key: key);

  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  @override
  Widget build(BuildContext context) {
    return Widget();
  }
}
```

## MaterialApp---UI组件

让开发者的写的组件具有MD风格 [Material Design](https://material.io/design)

源码：

```dart
const MaterialApp({
    Key? key,
    this.navigatorKey,
    this.scaffoldMessengerKey,
    this.home,
    Map<String, WidgetBuilder> this.routes = const <String, WidgetBuilder>{},
    this.initialRoute,
    this.onGenerateRoute,
    this.onGenerateInitialRoutes,
    this.onUnknownRoute,
    List<NavigatorObserver> this.navigatorObservers = const <NavigatorObserver>[],
    this.builder,
    this.title = '',
    this.onGenerateTitle,
    this.color,
    this.theme,
    this.darkTheme,
    this.highContrastTheme,
    this.highContrastDarkTheme,
    this.themeMode = ThemeMode.system,
    this.locale,
    this.localizationsDelegates,
    this.localeListResolutionCallback,
    this.localeResolutionCallback,
    this.supportedLocales = const <Locale>[Locale('en', 'US')],
    this.debugShowMaterialGrid = false,
    this.showPerformanceOverlay = false,
    this.checkerboardRasterCacheImages = false,
    this.checkerboardOffscreenLayers = false,
    this.showSemanticsDebugger = false,
    this.debugShowCheckedModeBanner = true,
    this.shortcuts,
    this.actions,
    this.restorationScopeId,
    this.scrollBehavior,
  })
```

[Flutter-MaterialApp详解](https://gaoxianglong.gitee.io/yisheep/2021/09/18/Flutter-MaterialApp/)

# Scaffold---脚手架组件

`Scaffold`将我们的应用分为几个部分，方便我们去搭建整个应用。

源码：

```dart
const Scaffold({
    Key? key,
    this.appBar,
    this.body,
    this.floatingActionButton,
    this.floatingActionButtonLocation,
    this.floatingActionButtonAnimator,
    this.persistentFooterButtons,
    this.drawer,
    this.onDrawerChanged,
    this.endDrawer,
    this.onEndDrawerChanged,
    this.bottomNavigationBar,
    this.bottomSheet,
    this.backgroundColor,
    this.resizeToAvoidBottomInset,
    this.primary = true,
    this.drawerDragStartBehavior = DragStartBehavior.start,
    this.extendBody = false,
    this.extendBodyBehindAppBar = false,
    this.drawerScrimColor,
    this.drawerEdgeDragWidth,
    this.drawerEnableOpenDragGesture = true,
    this.endDrawerEnableOpenDragGesture = true,
    this.restorationId,
  })
```

[Flutter-Scaffold详解](https://gaoxianglong.gitee.io/yisheep/2021/09/18/Flutter-Scaffold/)

## AppBar---标题栏组件

一般在`Scaffold`中使用，能控制标题栏的属性。

```dart
AppBar({
    Key? key,
    this.leading,
    this.automaticallyImplyLeading = true,
    this.title,
    this.actions,
    this.flexibleSpace,
    this.bottom,
    this.elevation,
    this.shadowColor,
    this.shape,
    this.backgroundColor,
    this.foregroundColor,
    this.brightness,
    this.iconTheme,
    this.actionsIconTheme,
    this.textTheme,
    this.primary = true,
    this.centerTitle,
    this.excludeHeaderSemantics = false,
    this.titleSpacing,
    this.toolbarOpacity = 1.0,
    this.bottomOpacity = 1.0,
    this.toolbarHeight,
    this.leadingWidth,
    this.backwardsCompatibility,
    this.toolbarTextStyle,
    this.titleTextStyle,
    this.systemOverlayStyle,
  })
```

[Flutter-AppBar详解](https://gaoxianglong.gitee.io/yisheep/2021/09/18/Flutter-AppBar/)

## TabBar---导航栏组件



## Container---容器

像是一个盒子一样，能够使我们将组件放到里面去，可以更改其大小。

源码：

```dart
Container({
    Key? key,
    this.alignment,
    this.padding,
    this.color,
    this.decoration,
    this.foregroundDecoration,
    double? width,
    double? height,
    BoxConstraints? constraints,
    this.margin,
    this.transform,
    this.transformAlignment,
    this.child,
    this.clipBehavior = Clip.none,
  })
```

[Flutter-Container详解](https://gaoxianglong.gitee.io/yisheep/2021/09/17/Flutter-Container/)

## Center---居中布局

可以让`widget`位于该布局的中心。

源码：

```dart
const Center({ 
    Key? key, 
    double? widthFactor, 
    double? heightFactor, 
    Widget? child 
})
```

[Flutter-Center详解](https://gaoxianglong.gitee.io/yisheep/2021/09/17/Flutter-Center/)

