---
layout:     post
title:      "CBStoreHouseRefreshControl"
subtitle:   "CBStoreHouseRefreshControl"
date:       2018-03-020
author:     "WTJ"
header-img: "img/post-bg-js-module.jpg"
catalog: true
tags:
    - iOS

---

## 简介

​	CBStoreHouseRefreshControl是一个可自定义形状的刷新控件,通过plist文件加载所需要的自定义点数组绘制任何形状,效果如下所示：

 	<div>
​     	 	<img class="shadow" src="/img/in-post/CBStoreHouseRefreshControl1.gif" width="380">
   	</div>

## 使用自定义形状

​	CBStoreHouseRefreshControl的形状包含一些`BarItem`动画，每个`BarItem`都运行自己的动画，需要提供`startPoint`并`endPoint`通过一个plist文件。

所有`BarItem`将共享一个坐标系，其原点位于左上角。例如，如果你想绘制一个正方形，plist将看起来像这样：

​	<div>
​     	 	<img class="shadow" src="/img/in-post/square.png" width="380">
​      	</div>

结果将如下所示：

​	<div>
​     	 	<img class="shadow" src="/img/in-post/square.gif" width="380">
​      	</div>

- 确保你把正确的键是`startPoints`和`endPoints`。
- 确保你使用正确的格式（`{x,y}`）作为坐标。
- 高亮/加载动画将按照您在plist中声明的相同顺序突出显示每个小节项目，用于`reverseLoadingAnimation`反转动画。

##自定义形状绘制

​	使用[PaintCode](http://www.paintcodeapp.com/)来生成`startPoint`和`endPoint`：然后把这些点通过UIBezierPath进行重回。

### 参考：

​	1、[CBStoreHouseRefreshControl]https://github.com/coolbeet/CBStoreHouseRefreshControl)

