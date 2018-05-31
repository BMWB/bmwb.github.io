---
layout:     post
title:      "Hit-test View"
subtitle:   "Hit-test View"
date:       2018-05-30
author:     "WTJ"
header-img: "img/post-bg-js-module.jpg"
catalog: true
tags:
    - iOS

---

##HitTest是什么

文档说：*The lowest view in the view hierarchy that contains the touch point becomes the hit-test view*，我的理解是：当你点击了屏幕上的某个view，这个动作由硬件层传导到操作系统，然后又从底层封装成一个事件（Event）顺着view的层级往上传导，一直要找到含有这个点击点**且**层级最高（文档说是最低，我理解是视图树的根节点，或者最靠近你的手指的view）的view来响应事件，这个view就是**hit-test view**。

## HitTest调用顺序

```
touch->UIApplication->UIWindow->UIViewController.view->subViews->...->view
```

## HitTest和事件传递关系

事件传递的的顺序和`hitTest`中`pointInside`返回为`YES`的视图的执行顺序是相反的。事件传递是从最上层的视图开始传递的，直到`UIApplication`。

<div>

​    <img class="shadow" src="/img/in-post/img_hittest.png" width="380">

</div>

## HitTest主要解决什么问题

HitTest主要解决的也是子视图超出其视图范围还是能响应触摸事件,扩大响应热区。



### 感谢：

​	1、[iOS事件响应链中Hit-Test View的应用](https://www.jianshu.com/p/d8512dff2b3e)

​	2、[iOS-使用hitTest控制点击事件的响应对象](https://www.jianshu.com/p/ca3cd5306668)

