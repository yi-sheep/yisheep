---
title: androidDrawable
date: 2021-08-19 16:59:46
tags: [android,drawable]
categories: 教程
description: Android Drawable竟然还能这么写
---

# Android Drawable竟然还能这么写

通常我们在`res/drawable`下面自定义`shape`和`selector`来满足一些UI的设计，但是由于xml最终转换为`drawable`需要经过IO或反射创建，会有一些性能损耗，另外随着项目的增大和模块化等，很多通用的样式并不能快速复用，需要合理的项目资源管理规范才能实施。那么通过代码直接创建这些`drawable`，可以在一定程度上降低这些副作用。本篇介绍用`kotlin DSL`简洁的语法特性来实现常见的`drawable`。

## 代码对应效果预览

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt4N72WmYXdcsnLf4ZKR96G4ML6PBu1beWAPjx4co2ZYLbbFxmZXZ5QdqRYTCNMHE2df1gv2d76LpQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt4N72WmYXdcsnLf4ZKR96G4gheGkzKnqYsx0jvqgaBibQ8UNWmSJ86rX1zdg2ycY4QlnYKc2Bgv1eg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt4N72WmYXdcsnLf4ZKR96G4HPpwDiavwzaVxfCicHmsDuJf04PdqwAkcwjWGIguxZd6jXC29X4p1eKg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt4N72WmYXdcsnLf4ZKR96G4eb2Gld7tH8RboMF2wsTGZ55TM3Z6uVLyzRJItReKSkWoqlUAeNlYEg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_gif/v1LbPPWiaSt4N72WmYXdcsnLf4ZKR96G4QS9k9r6HTL74aUY7akWPWYHEpr94mHDIrOaz8ZD1jv00R6iaYOg22dQ/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

## 集成和使用

### 在项目级的build.gradle文件种添加仓库Jitpack

```
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```

### 添加依赖

```
dependencies {        
    implementation 'com.github.forJrking:DrawableDsl:0.0.3’
}
```



### 抛弃xml创建方式示例（其他参见demo)

```
// infix用法用于去掉括号更加简洁，详细后面说明
image src shapeDrawable {
    //指定shape样式
    shape(ShapeBuilder.Shape.RECTANGLE)
    //圆角，支持4个角单独设置
    corner(20f)
    //solid 颜色
    solid("#ABE2E3")
    //stroke 颜色，边框dp，虚线设置
    stroke(R.color.white, 2f, 5f, 8f)
}
//按钮点击样式
btn.background = selectorDrawable {
    //默认样式
    normal = shapeDrawable {
        corner(20f)
        gradient(90, R.color.F97794, R.color.C623AA2)
    }
    //点击效果
    pressed = shapeDrawable {
        corner(20f)
        solid("#84232323")
    }
}
```



## 实现思路

### xml如何转换成drawable

xml变成drawable，通过android.graphics.drawable.DrawableInflater这个类来IO解析标签创建，然后通过解析标签再设置属性：

```
//标签创建
private Drawable inflateFromTag(@NonNull String name) {
    switch (name) {
        case "selector":
            return new StateListDrawable();
        case "level-list":
            return new LevelListDrawable();
        case "layer-list":
            return new LayerDrawable();
        ....
        case "color":
            return new ColorDrawable();
        case "shape":
            return new GradientDrawable();
        case "vector":
            return new VectorDrawable();
        ...
    }
}
//反射创建
private Drawable inflateFromClass(@NonNull String className) {
    try {
        Constructor<? extends Drawable> constructor;
        synchronized (CONSTRUCTOR_MAP) {
            constructor = CONSTRUCTOR_MAP.get(className);
            if (constructor == null) {
                final Class<? extends Drawable> clazz = mClassLoader.loadClass(className).asSubclass(Drawable.class);
                constructor = clazz.getConstructor();
                CONSTRUCTOR_MAP.put(className, constructor);
            }
        }
        return constructor.newInstance();
    } catch (NoSuchMethodException e) {
    ...
}
```



### 代码实现

由于创建shape等需要设置各种属性来构建，比较符合build设计模式，那我们首先封装build模式的shapeBuilder，这样做虽然代码比起直接使用apply{}要多，但是可以让纯java项目用起来很舒服，其他实现请查看源码：

```
class ShapeBuilder : DrawableBuilder {
    private var mRadius = 0f
    private var mWidth = 0f
    private var mHeight = 0f
    ...
    private var mShape = GradientDrawable.RECTANGLE
    private var mSolidColor = 0

    /**分别设置四个角的圆角*/
    fun corner(leftTop: Float,rightTop: Float,leftBottom: Float,rightBottom: Float): ShapeBuilder {
        ....if(dp)dp2px(leftTop) else leftTop
        return this
    }

    fun solid(@ColorRes colorId: Int): ShapeBuilder {
        mSolidColor = ContextCompat.getColor(context, colorId)
        return this
    }
    // 省略其他参数设置方法 详细代码查看源码
    override fun build(): Drawable {
        val gradientDrawable = GradientDrawable()
        gradientDrawable = GradientDrawable()
        gradientDrawable.setColor(mSolidColor)
        gradientDrawable.shape = mShape
        ....其他参数设置
        return gradientDrawable
    }    
}
```



### 把build模式转换为dsl

理论上所有的build模式都可以轻松转换为dsl写法：

```
inline fun shapeDrawable(builder: ShapeBuilder.() -> Unit): Drawable {
    return ShapeBuilder().also(builder).build()
}
//使用方法 
val drawable = shapeDrawable{
    ...
}
```



### 函数去括号

通过上面封装已经实现了dsl的写法，通常setBackground可以通过setter简化，但是我发现由于有些api设计还需要加括号，这样不太kotlin：

```
//容易阅读
iv1.background = shapeDrawable {
    shape(ShapeBuilder.Shape.RECTANGLE)
    solid("#ABE2E3")
}
//多了括号看起来不舒服
iv2.setImageDrawable(shapeDrawable {
    solid("#84232323")
})
```

怎么去掉括号呢？🈶2种方式infix函数(中缀表达)和property setter



#### infix函数特点和规范

- Kotlin允许在不使用括号和点号的情况下调用函数
- 必须只有一个参数
- 必须是成员函数或扩展函数
- 不支持可变参数和带默认值参数

```
/**为所有ImageView添加扩展infix函数 来去掉括号*/
infix fun ImageView.src(drawable: Drawable?) {
    this.setImageDrawable(drawable)
}
//使用如下
iv2 src shapeDrawable {
    shape(ShapeBuilder.Shape.OVAL)
    solid("#E3ABC2")
}
```

当然了代码是用来阅读的。个人认为如果我们大量使用infix函数，阅读困难会大大增加，所以建议函数命名必须可以直击函数功能，而且函数功能简单且单一。

#### property setter方式

主要使用kotlin可以简化setter为等号来去括号：

```
/**扩展变量*/var ImageView.src: Drawable    get() = drawable    set(value) {        this.setImageDrawable(value)    }//使用如下   iv2.src = shapeDrawable {    shape(ShapeBuilder.Shape.OVAL)    solid("#E3ABC2")}    
```



### 优缺点

#### 优点

- 代码直接创建比起xml方式可以提升性能
- dsl方式比起build模式和调用方法设置更加简洁符合kotlin风格
- 通过合适的代码管理可以复用这些代码，比xml管理方便



#### 缺点

- 没有as的预览功能，只有通过上机观测
- api还没有覆盖所有drawable属性（例如shape = ring等)



## 结语

上面把的DrawableDsl基础用法介绍完了，欢迎大家使用，欢迎提Issues，记得给个star哦。Github链接：

> https://github.com/forJrking/DrawableDsl
