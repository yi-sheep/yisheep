---
title: Flutter-Container详解
date: 2021-09-17 17:27:16
tags: [笔记]
categories: flutter
description: Flutter-Container详解
top_img: https://gitee.com/gaoxianglong/picgo/raw/master/img/f3b8af27140c9ac90ab83012cec99bc746546e28.jpg
cover: https://gitee.com/gaoxianglong/picgo/raw/master/img/f3b8af27140c9ac90ab83012cec99bc746546e28.jpg
---

# Flutter-Container详解

# 概述

Container是一个拥有绘制、定位、调整大小的 widget，是开发中最常用、最基础的组件。虽然最基础但不可小觑，熟悉每一个属性可以帮助我们更好更快的实现想要的效果，避免走弯路，也能避免代码冗余。本文主要针对其属性进行讲解。

# 属性

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

### key

key用于控制控件如何取代树中的另一个控件，即若widget指定了相同的key，则这些widget可以复用。 如果widget的key值不为空，会判断key._currentElement值所指向的widget，和当前widget的类型key都相同，那么就从旧的父节点上移除，作为当前的节点的子widget之一， 否则将进行真实的创建新的Element。若开发中对组建的使用没有较高要求，一般不设置该属性。

### alignment

alignment可以理解为Container内容的锚点位置或重力方向，锚点在哪，内容就从哪里开始。alignment的类型为AlignmentGeometry类型，通常我们会使用其实现类Alignment来进行设置。AlignmentGeometry属于抽象类：

```java
@immutable
abstract class AlignmentGeometry {...}
复制代码
```

一般不直接使用AlignmentGeometry ，而是使用其实现类。Flutter中实现或继承了AlignmentGeometry的公共可直接调用的类有两个：Alignment，AlignmentDirectional。这两个实现类的使用方法和相似，可以直接调用其内部属性：

```dart
  static const Alignment topLeft = Alignment(-1.0, -1.0);
  static const Alignment topCenter = Alignment(0.0, -1.0);
  static const Alignment topRight = Alignment(1.0, -1.0);
  static const Alignment centerLeft = Alignment(-1.0, 0.0);
  static const Alignment center = Alignment(0.0, 0.0);
  static const Alignment centerRight = Alignment(1.0, 0.0);
  static const Alignment bottomLeft = Alignment(-1.0, 1.0);
  static const Alignment bottomCenter = Alignment(0.0, 1.0);
  static const Alignment bottomRight = Alignment(1.0, 1.0);
```

使用的时候直接用Alignment.topLeft调用即可，也可直接设置参数数值比如Alignment(-1.0, -1.0)即可。根据设置不同的alignment属性值，视图效果也是不一样的： ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/b3681934fb184cce9f9396f0bf41b653~tplv-k3u1fbpfcp-watermark.awebp) 若在其他组件中需要设置TextDirection，可以考虑使用AlignmentDirectional。AlignmentDirectional和Alignment差不多：

```dart
  static const AlignmentDirectional topStart = AlignmentDirectional(-1.0, -1.0);
  static const AlignmentDirectional topCenter = AlignmentDirectional(0.0, -1.0);
  static const AlignmentDirectional topEnd = AlignmentDirectional(1.0, -1.0);
  static const AlignmentDirectional centerStart = AlignmentDirectional(-1.0, 0.0);
  static const AlignmentDirectional center = AlignmentDirectional(0.0, 0.0);
  static const AlignmentDirectional centerEnd = AlignmentDirectional(1.0, 0.0);
  static const AlignmentDirectional bottomStart = AlignmentDirectional(-1.0, 1.0);
  static const AlignmentDirectional bottomCenter = AlignmentDirectional(0.0, 1.0);
  static const AlignmentDirectional bottomEnd = AlignmentDirectional(1.0, 1.0);
```

使用方法和Alignment一样，不再叙述。

### padding、margin

padding为内边距，margin为外边距。 ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/52b995b0a8af4963b960e1e85529be46~tplv-k3u1fbpfcp-watermark.awebp)

针对于上图中Container2，Container1与Container2之间的边框距离称之为margin，Container2与内容之间距离为padding。通常margin和padding使用EdgeInsets，EdgeInsets使用方法如下：

| 方法                                                         | 使用                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| EdgeInsets.fromLTRB(this.left, this.top, this.right, this.bottom) | 左上右下依次填写                                             |
| EdgeInsets.all(double value)                                 | 所有边距一样                                                 |
| EdgeInsets.only({this.left = 0.0,this.top = 0.0,this.right = 0.0,this.bottom = 0.0, }) | 左上右下可选择设置                                           |
| EdgeInsets zero                                              | 左上右下都为0                                                |
| EdgeInsets.fromWindowPadding(ui.WindowPadding padding, double devicePixelRatio) | 左上右下距离窗口的边距，和设备像素比，而不是距离父组件的边距 |

EdgeInsets继承于EdgeInsetsGeometry，和之类似的还有EdgeInsetsDirectional，同样继承自EdgeInsetsGeometry，暴露出的方法有：

```dart
class EdgeInsetsDirectional extends EdgeInsetsGeometry {
  const EdgeInsetsDirectional.fromSTEB(this.start, this.top, this.end, this.bottom);
  const EdgeInsetsDirectional.only({
    this.start = 0.0,
    this.top = 0.0,
    this.end = 0.0,
    this.bottom = 0.0,
  });
  static const EdgeInsetsDirectional zero = EdgeInsetsDirectional.only();
  ...
}
```

EdgeInsetsDirectional使用方法和EdgeInsets类似，多用于TextDirection。

### color

color为Container颜色，设置颜色通常可以调用Colors.white，Colors.red等Flutter定义好的颜色，如没有适合的颜色，可以使用Color(0xFFFFFFFF)，自定义颜色，0x代表16进制，前面两个FF代表透明度（Android中可以不写，但Flutter中不可省略），后面6个F代表颜色数值。以Color(0xFFFFFFFF)为例，以下表格对Color的使用进行说明

| 方法                                   | 含义                      |
| -------------------------------------- | ------------------------- |
| Color(0xFFFFFFFF).value                | 获取颜色数值(0-255)       |
| Color(0xFFFFFFFF).red                  | 获取颜色中红色            |
| Color(0xFFFFFFFF).blue                 | 获取颜色中蓝色            |
| Color(0xFFFFFFFF).opacity              | 获取颜色不透明度(0.0-1.0) |
| Color(0xFFFFFFFF).alpha                | 获取颜色透明度            |
| Color(0xFFFFFFFF).green                | 获取颜色中绿色            |
| Color(0xFFFFFFFF).withOpacity(opacity) | 设置颜色不透明度          |
| Color(0xFFFFFFFF).computeLuminance()   | 计算颜色亮度(0-1)         |
| Color(0xFFFFFFFF).withAlpha(a)         | 设置颜色透明度 (0-255)    |
| Color(0xFFFFFFFF).withBlue(b)          | 设置颜色中蓝色值(0-255)   |
| Color(0xFFFFFFFF).withGreen(g)         | 设置颜色中绿值            |
| Color(0xFFFFFFFF).withRed(r)           | 设置颜色中红色值          |

关于Color大多有这几个常用的方法，若Container设置了decoration，Container的color就不要设置了，两者冲突会报错，以decoration中的color为准。

### decoration，foregroundDecoration

decoration为背景装饰，foregroundDecoration为前景装饰。简单理解就是设置样式，不仅仅是设置颜色，还包括形状、图片、渐变、阴影、模糊等。 decoration指定类型为Decoration，同样Decoration为抽象类，没有具体的实现，需要使用其实现类或子类，其实现类主要有BoxDecoration、FlutterLogoDecoration、UnderlineTabIndicator、ShapeDecoration。Container中通常使用BoxDecoration，BoxDecoration有如下几个参数：

```dart
  const BoxDecoration({
    this.color,
    this.image,
    this.border,
    this.borderRadius,
    this.boxShadow,
    this.gradient,
    this.backgroundBlendMode,
    this.shape = BoxShape.rectangle,
  })
```

##### color

颜色直接在BoxDecoration中设置即可，以下分别是红色和蓝色的效果图 ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/41646f7a778f4c76aadf7c0eacff70fb~tplv-k3u1fbpfcp-watermark.awebp)

##### image

image就是设置装饰图片，图片分为资源图片、本地图片和网络图片，这里只能使用DecorationImage

```dart
 const DecorationImage({
    required this.image,
    this.onError,
    this.colorFilter,
    this.fit,
    this.alignment = Alignment.center,
    this.centerSlice,
    this.repeat = ImageRepeat.noRepeat,
    this.matchTextDirection = false,
    this.scale = 1.0
  })
```

- image

DecorationImage中指定了image的类型必须是ImageProvider，也就是这里使用的是AssetImage()、NetworkImage()、FileImage()，而不是Image.asset()、Image.net()、Image.file()等。 ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/f0cae560c70544c79980a29d78241b36~tplv-k3u1fbpfcp-watermark.awebp) 左图为AssetImage，右图为NetworkImage，FileImage()访问的是手机中的图片，和前两者一样，只要拿到路径都不是问题。

- onError

onError指的是图片错误监听，万一图片格式不对，大小不对，网络出错，加载出错，开发者需要知道错在哪里了，然后做错误处理。

- colorFilter

colorFilter就是相当于给图片加上一层滤镜，以上图中左边图片为例，ColorFilter使用方式有四种：

| 方法                                               | 含义                                                         |
| -------------------------------------------------- | ------------------------------------------------------------ |
| ColorFilter.mode(Color color, BlendMode blendMode) | 添加指定混合模式指定颜色的滤镜，BlendMode 大概有三十种，用户自由选择 |
| ColorFilter.matrix(List matrix)                    | 矩阵混合                                                     |
| ColorFilter.linearToSrgbGamma()                    | 将sRGB伽马曲线应用于RGB通道                                  |
| ColorFilter.srgbToLinearGamma()                    | 将sRGB伽马曲线逆应用于RGB通道                                |

效果： ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/10e86695928a4d4e9a0e9213bd660adf~tplv-k3u1fbpfcp-watermark.awebp) 通过上图可以发现，同一图片使用不同的滤镜，效果大不相同。如果需要开发图片滤镜功能，这一块会有大用处。

- fit

fit指的是图片适配模式，使用BoxFit即可，BoxFit也提供了几种模式供选择。

| 模式      | 含义                 |
| --------- | -------------------- |
| fill      | 根据图片比例填充     |
| contain   | 容器范围内尽可能最大 |
| cover     | 覆盖整个容器         |
| fitWidth  | 宽度适应             |
| fitHeight | 高度适应             |
| none      | 无                   |
| scaleDown | 等比例缩放           |

各种模式依次效果如下： ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/295cfc1025164faa939144c9abf10b53~tplv-k3u1fbpfcp-watermark.awebp) 上图中图片较小，容器固定，有些图片看不出区别，而实际使用过程中不同模式之间差别较大，以实际为准。

- alignment

alignment 同文章开头的alignment一样，不再叙述。

- centerSlice

centerSlice和fit效果有些相似，当两者同时使用的时候，可能没有效果，可能无法看到图片，使用时需要谨慎一些。 centerSlice类型为Rect，centerSlice用于nine-patch image，即可拉伸图片，后续这一块需要仔细研究一下。

| 方法                                                         |
| ------------------------------------------------------------ |
| Rect.fromLTRB(this.left, this.top, this.right, this.bottom)  |
| Rect.fromLTWH(double left, double top, double width, double height) |
| Rect.fromCircle({ required Offset center, required double radius }) |
| Rect.fromCenter({ required Offset center, required double width, required double height }) |
| Rect.fromPoints(Offset a, Offset b)                          |

- repeat

repeat 是空白区域图片重复模式。

| 方法                 | 含义         |
| -------------------- | ------------ |
| ImageRepeat.repeat   | 全部填充图片 |
| ImageRepeat.repeatX  | 水平重复     |
| ImageRepeat.repeatY  | 竖直重复     |
| ImageRepeat.noRepeat | 不重复       |

对于的效果依次如下： ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/57986d6cf4274deea6b69ee70df1f4e7~tplv-k3u1fbpfcp-watermark.awebp) 由于图片本身已经占用了容器的水平位置上的全部空间，所以repeatX和noRepeat效果一样，repeat和repeatY效果一样。若图片水平和竖直方向都有剩余空间，则repeat等于repeatX和repeatY叠加。

- matchTextDirection

matchTextDirection默认为false，表示背景图片和文字方向没有关系。当为true的时候，表示图片和文字方向一致。

- scale

scale表示图片缩放，默认为1.0，表示按原图大小显示。小于1.0，则按比例缩小图片；大于1.0，则表示按比例放大图片。

##### border

border是边框的意思，设置该属性，就可以设置Contaier边框样式。border指定类型为BoxBorder，BoxBorder，InputBorder，OutlinedBorder虽都继承自ShapeBorder ，但这里BoxBorder也是抽象类，所以需要使用其子类Border或BorderDirectional，这里通常使用Border。Border有四种构造方法：

| 方法                                                         | 含义                       |
| ------------------------------------------------------------ | -------------------------- |
| Border({BorderSide top: BorderSide.none, BorderSide right: BorderSide.none, BorderSide bottom: BorderSide.none, BorderSide left: BorderSide.none}) | 可分别设置上下左右边框     |
| Border.all({Color color: const Color(0xFF000000), double width: 1.0, BorderStyle style: BorderStyle.solid}) | 设置所有边框               |
| Border.fromBorderSide(BorderSide side)                       | 内边框                     |
| Border.symmetric({BorderSide vertical: BorderSide.none, BorderSide horizontal: BorderSide.none}) | 水平方向边框，竖直方向边框 |

通过上表可以发现，不管使用哪一种方法都要使用BorderSide，BorderSide指的是具体边框的样式，而Border指的是在哪个方向可以有边框。BorderSide比较简单：

```dart
  const BorderSide({
    this.color = const Color(0xFF000000),
    this.width = 1.0,
    this.style = BorderStyle.solid,
  })
```

color代表边框颜色，width代表边框宽度，style表示边框样式（默认实线-BorderStyle.solid）。具体效果如下图： ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/338d7a9a549b4309aabae85278a35d11~tplv-k3u1fbpfcp-watermark.awebp)

##### borderRadius

边角弧度，类型为BorderRadiusGeometry ，通常使用其实现类BorderRadius或BorderRadiusDirectional，其中BorderRadius最常用，以下是BorderRadius的一些用法：

| 方法                                                         | 含义                 |
| ------------------------------------------------------------ | -------------------- |
| BorderRadius.all(Radius radius)                              | 所有角的弧度         |
| BorderRadius.circular(double radius)                         | 所有角的弧度         |
| BorderRadius.horizontal({Radius left: Radius.zero, Radius right: Radius.zero}) | 所有角的水平方向弧度 |
| BorderRadius.only({Radius topLeft: Radius.zero, Radius topRight: Radius.zero, Radius bottomLeft: Radius.zero, Radius bottomRight: Radius.zero}) | 分别设置四角的弧度   |
| BorderRadius.vertical({Radius top: Radius.zero, Radius bottom: Radius.zero}) | 所有角的垂直方向弧度 |

和border一样，BorderRadius中除了 BorderRadius.circular外都是指定哪个角设置弧度，具体实现由Radius实现。Radius中Radius.circular(double radius)指的是圆角的弧度一样，Radius.elliptical(double x,double y)表示水平和垂直方向的弧度自由定义。 ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/26e68484fc054378810f2fa21be29734~tplv-k3u1fbpfcp-watermark.awebp) 总而言之，borderRadius针对于不同的角，不同方向，不同弧度都可以随意设置，比较灵活。

##### boxShadow

boxShadow设置Container阴影或投影，List boxShadow说明使用时是以数组的形式，对于稍显复杂的场景一层阴影无法达到要求，所有需要很多层阴影相互叠加来满足要求。BoxShadow使用相对简单

```dart
const BoxShadow(
{Color color: const Color(0xFF000000),
Offset offset: Offset.zero,
double blurRadius: 0.0,
double spreadRadius: 0.0}
)
```

color是阴影的颜色，Offset是投影偏移量，blurRadius投影模糊程度，spreadRadius则是投影的扩散程度。 ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/7e12889e7ccd427186f86c0312bade62~tplv-k3u1fbpfcp-watermark.awebp)blurRadius取值不同，效果不同，取值越大，阴影的色彩越淡，但是扩散的范围越大。 ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/12d35552e60f4f0c87af5ce8144b1ee1~tplv-k3u1fbpfcp-watermark.awebp) spreadRadius取值不同，阴影范围有明显区别。当取值大于0时，阴影向外扩散；当取值小于0时，阴影向内部聚集，若此时需要显示阴影，需要设置Offset，光线角度不同，阴影的投射方向也不同，所以设置内投影的时候，一定要设置Offset，让投影偏移出来，否则投影被遮挡无法显示。

##### gradient

gradient为设置渐变，渐变类型分为LinearGradient、RadialGradient、SweepGradient，分别为线性渐变、辐射渐变、扫描渐变。

- LinearGradient（线性渐变）

![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/99cd24bd3d65407ba9e4a8df306a7d82~tplv-k3u1fbpfcp-watermark.awebp) begin线性渐变起点，end为线性渐变终点，可水平，可竖直，可对角，根据需要自由选择。stops里面数值数量要和colors里面的数量保持一致。tileMode为颜色填充模式：

| 模式              | 含义                                         |
| ----------------- | -------------------------------------------- |
| TileMode.clamp    | 夹钳模式，颜色与颜色之间有类似窄而明显的过渡 |
| TileMode.repeated | 重复                                         |
| TileMode.mirror   | 镜像                                         |
| TileMode.decal    | 贴花（探索中）                               |

具体效果如下： ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/a097c28eae154f22ac0d4932f7073e59~tplv-k3u1fbpfcp-watermark.awebp) 没有对TileMode.decal进行效果展示，是因为关于这个模式的解释比较模糊，也没有观察出到底有什么不同，需后续持续探索。 transform表示渐变色变换，一般有GradientRotation和SweepGradient供选择，主要用于SweepGradient和RadialGradient中。

- SweepGradient（扫描渐变）

```dart
SweepGradient({
    this.center = Alignment.center,
    this.startAngle = 0.0,
    this.endAngle = math.pi * 2,
    required List<Color> colors,
    List<double>? stops,
    this.tileMode = TileMode.clamp,
    GradientTransform? transform,
  })
```

默认中心的从Container中心开始，开始弧度为0.0，结束弧度为pi*2，也就是一周。运行效果如下： ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/dc27c7d62b9942feb5a605906f9536c4~tplv-k3u1fbpfcp-watermark.awebp) 如果设置好颜色，再搭配上旋转动画，像雷达扫描、大转盘这种效果是可以轻松实现的。

- RadialGradient（辐射渐变）

```dart
    RadialGradient({
    this.center = Alignment.center,
    this.radius = 0.5,
    required List<Color> colors,
    List<Color>? stops,
    this.tileMode = TileMode.clamp,
    this.focal,
    this.focalRadius = 0.0,
    GradientTransform? transform,
    })
```

效果如下： ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/0ec845126687477483a8891126a797c8~tplv-k3u1fbpfcp-watermark.awebp) 第一张图片是没有设置焦点。第二张图片是设置了焦点，焦点中心为Container中心，焦点半径为0.1。第三张图同样设置了焦点，但是焦点的中心为centerLeft，且焦点半径为1.0，焦点半径单位不是像素，focalRadius和focal设置的值不同，效果区别较大，有时和想象中的不太一样，所以使用的时候需仔细调试一下。

##### backgroundBlendMode

backgroundBlendMode为背景混合模式，和前面讲的图片滤镜差不多，大概有将近30种模式，有些差别较大，有些区别不是很明显，需要开发者多多尝试，这里随机选取了四种，效果如下： ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/39135332b8684ee7890caaea495d8085~tplv-k3u1fbpfcp-watermark.awebp)

##### shape

shape即为装饰的形状，默认为BoxShape.rectangle，用户也可以选择BoxShape.circle。BoxShape.circle是整个装饰为圆形，而RadialGradient是辐射状也为圆形，不容易区分到底是哪一个决定的，但LinearGradient区分比较开，如下图所示： ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/725a1faf253640febe05a55d3b6f0faa~tplv-k3u1fbpfcp-watermark.awebp) 所以shape和RadialGradient、SweepGradient有时可以实现相同的效果，可灵活使用。

### width，height

Container需要固定宽高，否则会报错。虽有时没有设置也能正常显示，是因为Container包含的组件的宽高固定了，只要子组件宽高固定，Container宽高也固定了，所以显示正常。

### constraints

constraints是Container的约束，主要指定的是宽高上面的约束：

```dart
BoxConstraints({
    this.minWidth = 0.0,
    this.maxWidth = double.infinity,
    this.minHeight = 0.0,
    this.maxHeight = double.infinity,
  })
```

constraints可以指定Container的最大宽高和最小宽高，否则有时超出某些范围页面显示异常。和BoxConstraints一样，同样继承自Constraint还有SliverConstraints，SliverConstraints在Sliver相关组件中使用，这里就不多讲了。

### transform

矩阵变化，类型为Matrix4，即四阶矩阵。常用的有以下几种用法：

| 方法            | 含义                                |
| --------------- | ----------------------------------- |
| Matrix4(...)    | 16个参数， 平移，旋转，缩放，扭曲等 |
| diagonal3Values | 缩放                                |
| rotationX       | 沿x旋转                             |
| rotationY       | 沿y旋转                             |
| rotationZ       | 沿z旋转                             |
| columns         | 设置新矩阵                          |
| compose         | 合并平移，旋转，缩放成新矩阵        |
| copy            | 复制矩阵                            |
| identity        | 单位矩阵                            |
| inverted        | 矩阵逆运算                          |
| outer           | 合并                                |
| skew            | 扭曲                                |
| skewX(          | x扭曲                               |
| skewY           | y扭曲                               |
| zero            | 零矩阵                              |
| fromList        | 数组转矩阵                          |

还有其他方法，这里就不一一列举。基本上所有的变换都是在Matrix4(...)基础上实现的，所以只要弄懂Matrix4(...) ，其他的也不是问题。高级变换是一定需要矩阵，复杂的动画也需要矩阵，基础的是四阶，复杂的有五阶、六阶等等，所以矩阵很重要。以下是几种简单的变换效果： ![在这里插入图片描述](https://gitee.com/gaoxianglong/picgo/raw/master/img/18b16f4dc62d4a01a6cd1cd47918ce36~tplv-k3u1fbpfcp-watermark.awebp) 实际中变换后的图片的大小、方位、角度都有不同，效果无法在上图中完全体现出来。

### transformAlignment

变换锚点或者是变换重力方向和上文中的alignment是一样的，这里就不再叙述。

### clipBehavior

clipBehavior就是组件内容边缘的切割方式，分为四种：

- none

不做处理。

- hardEdge

当内容溢出时，hardEdge切割容器边缘最快，但是精准度欠佳，可能会有一些锯齿存在。

- antiAlias

抗锯齿，速度要比hardEdge慢一些，但是边缘要平滑一些。

- antiAliasWithSaveLayer

图层抗锯齿，就是容器中每一个图层都做抗锯齿处理，而antiAlias是在容器的轮廓做抗锯齿，antiAliasWithSaveLayer效果肯定会更好更平滑，但是速度最慢，如果没有明确指明，建议使用antiAlias，这样效果和性能能够达到较好的平衡。

### Container

查看Container对于各种属性的处理如下：

```dart
 @override
  Widget build(BuildContext context) {
    Widget? current = child;

    if (child == null && (constraints == null || !constraints!.isTight)) {
      current = LimitedBox(
        maxWidth: 0.0,
        maxHeight: 0.0,
        child: ConstrainedBox(constraints: const BoxConstraints.expand()),
      );
    }

    if (alignment != null)
      current = Align(alignment: alignment!, child: current);

    final EdgeInsetsGeometry? effectivePadding = _paddingIncludingDecoration;
    if (effectivePadding != null)
      current = Padding(padding: effectivePadding, child: current);

    if (color != null)
      current = ColoredBox(color: color!, child: current);

    if (clipBehavior != Clip.none) {
      assert(decoration != null);
      current = ClipPath(
        clipper: _DecorationClipper(
          textDirection: Directionality.maybeOf(context),
          decoration: decoration!,
        ),
        clipBehavior: clipBehavior,
        child: current,
      );
    }

    if (decoration != null)
      current = DecoratedBox(decoration: decoration!, child: current);

    if (foregroundDecoration != null) {
      current = DecoratedBox(
        decoration: foregroundDecoration!,
        position: DecorationPosition.foreground,
        child: current,
      );
    }

    if (constraints != null)
      current = ConstrainedBox(constraints: constraints!, child: current);

    if (margin != null)
      current = Padding(padding: margin!, child: current);

    if (transform != null)
      current = Transform(transform: transform!, child: current, alignment: transformAlignment);

    return current!;
  }
```

Container并非是单元组件不可再次拆分，恰恰相反，Container中多数属性都有关联组件，所以当属性被设置的时候，也是调用了该属性关联的组件，然后在此基础上再依次进行嵌套，最后套成Container，所以Container是由其他组件组成的。 本文是对Container的属性进行单独解析，实际使用时，大多都是各种属性相互配合使用，实现的效果也要比文中呈现的效果要丰富得多。

# 注

- 文中有很多遗漏，错误，不准确的，欢迎补充批评指正。
- 熟悉基础，可以帮助开发者用简单、少量、高效的代码解决复杂问题。
