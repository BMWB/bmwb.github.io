---
layout:     post
title:      "Auto Layout"
subtitle:   "Auto Layout"
date:       2018-06-04
author:     "WTJ"
header-img: "img/post-bg-js-module.jpg"
catalog: true
tags:
    - iOS

---

# AutoLayout原理

说完了 `Auto Layout` 的使用，再来看看它工作原理。

实际上，我们设置 `Auto Layout` 的约束，就构成一系列的条件,成为一个方程。然后解出 Frame 的坐标和大小。

例如，我们设置一个名为 A 的 UI :

```
A.center = super.center
A.width  = 40
A.height = 40

```

则:A.frame = (super.center.x-40/2,super.center.y-40/2,40,40)

再设置一个 B:

```
B.width  =  A.width
B.height =  A.height
B.top    =  A.bottom + 50
B.left   =  A.left

```

则:B.frame =  ( A.x , A.y + A.height + 50 , A.width , A.height )



##Cassowary

`Auto Layout` 内部有专门用来处理约束关系的算法，我一直以为是苹果自家研发的，查阅资料才发现是来自一个叫 `Cassowary` 的算法。

> Cassowary是个解析工具包，能够有效解析线性等式系统和线性不等式系统，用户的界面中总是会出现不等关系和相等关系，Cassowary开发了一种规则系统可以通过约束来描述视图间关系。约束就是规则，能够表示出一个视图相对于另一个视图的位置。
>
> - 戴铭 [<深入剖析Auto Layout，分析iOS各版本新增特性>](https://link.juejin.im?target=https%3A%2F%2Fming1016.github.io%2F2015%2F11%2F03%2Fdeeply-analyse-autolayout%2F)



##AutoLayout性能

在对 `Auto Layout` 进行一番了解之后,我们很容易得出 `Auto Layout` 因为多余的计算，性能差于 Frame 的结论。



##Auto Layout的生命周期

进入下面主题前可以先介绍下加入Auto Layout的生命周期。在得到自己的layout之前Layout Engine会将Views，约束，Priorities（优先级），instrinsicContentSize（主要是UILabel,UIImageView等）通过计算转换成最终的效果。在Layout Engine里会有约束变化到Deferred Layout Pass再到应用Run Loop再回到约束变化这样的循环机制。

##感谢：

​	1、[深入剖析Auto Layout，分析iOS各版本新增特性](https://ming1016.github.io/2015/11/03/deeply-analyse-autolayout/)

​	2、[iOS 上的 FlexBox 布局](https://juejin.im/post/5a33a6926fb9a045104a8d3c#heading-5)