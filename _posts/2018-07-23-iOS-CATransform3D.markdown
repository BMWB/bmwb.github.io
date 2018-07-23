---
layout:     post
title:      "CATransform3D"
subtitle:   "CATransform3D"
date:       2018-07-23
author:     "WTJ"
header-img: "img/post-bg-js-module.jpg"
catalog: true
tags:
    - iOS
---



CATransform3D 的数据结构定义了一个同质的三维变换（4x4 CGFloat值的矩阵），用于图层的旋转，缩放，偏移，歪斜和应用的透视。

    
    struct CATransform3D
    {
        CGFloat m11(x缩放), m12(y切变),m13（旋转）, m14（）;
        CGFloat m21(x切变), m22(y缩放),m23（）,    m24（）;
        CGFloat m31(x旋转), m32(),    m33（）,    m34（透视效果，要操作的这个对象要有旋转的角度，否则没有效果。正直/负值都有意义）;
        CGFloat m41(x平移), m42(y平移),m43(z平移), m44（）;
    };

- CATransform3DIdentity

  >是单位矩阵，该矩阵没有缩放，旋转，歪斜，透视。该矩阵应用到图层上，就是设置默认值。

- 平移3D仿射

   CATransform3D CATransform3DMakeTranslation (CGFloat tx, CGFloat ty, CGFloat tz)

  >tx：X轴偏移位置，往下为正数。
  >
  >ty：Y轴偏移位置，往右为正数。
  >
  >tz：Z轴偏移位置，往外为正数。

  CATransform3D CATransform3DTranslate (CATransform3D t, CGFloat tx, CGFloat ty, CGFloat tz);

  >t：就是上一个函数。其他的都一样。
  >
  >就可以理解为：函数的叠加，效果的叠加。

  ​

- 缩放3D仿射

  CATransform3D CATransform3DMakeScale (CGFloat sx, CGFloat sy, CGFloat sz);

  >sx：X轴缩放，代表一个缩放比例，一般都是 0 --- 1 之间的数字。
  >
  >sy：Y轴缩放。
  >
  >sz：整体比例变换时，也就是m11（sx）== m22（sy）时，若m33（sz）>1，图形整体缩小，若0<1，图形整体放大，若m33（sz）<0，发生关于原点的对称等比变换。

  CATransform3D CATransform3DScale (CATransform3D t, CGFloat sx, CGFloat sy, CGFloat sz)

  >t：就是上一个函数。其他的都一样。
  >
  >就可以理解为：函数的叠加，效果的叠加。

- 旋转3D仿射

  CATransform3D CATransform3DMakeRotation (CGFloat angle, CGFloat x, CGFloat y, CGFloat z);

  >angle：旋转的弧度，所以要把角度转换成弧度：角度 * M_PI / 180。
  >
  >x：向X轴方向旋转。值范围-1 --- 1之间
  >
  >y：向Y轴方向旋转。值范围-1 --- 1之间
  >
  >z：向Z轴方向旋转。值范围-1 --- 1之间

  CATransform3D CATransform3DRotate (CATransform3D t, CGFloat angle, CGFloat x, CGFloat y, CGFloat z);

  >t：就是上一个函数。其他的都一样。
  >
  >就可以理解为：函数的叠加，效果的叠加。

  ​

- 把一个 CATransform3D 对象转换成一个 CGAffineTransform 对象

  CGAffineTransform CATransform3DGetAffineTransform (CATransform3D t)

  ​

- 检查是否有做过仿射3D效果 

  bool CATransform3DIsIdentity (CATransform3D t)

  ​

- 检查2个3D仿射效果是否相同

  CATransform3DEqualToTransform(transform1,transform2)

  >bool CATransform3DEqualToTransform (CATransform3D a, CATransform3D b);

  ​

- 3D仿射效果反转（反效果，比如原来扩大，就变成缩小）

  CATransform3D CATransform3DInvert (CATransform3D t);

## 感谢：

1、[3D变换](https://zsisme.gitbooks.io/ios-/content/chapter5/3d-transform.html)

2、[CATransform3D 特效详解](https://blog.csdn.net/sinat_27706697/article/details/46493443)