---
layout:     post
title:      "PaintCode工具"
subtitle:   "PaintCode工具"
date:       2018-03-20
author:     "WTJ"
header-img: "img/post-bg-js-module.jpg"
catalog: true
tags:
    - 工具

---

## 前言

[PaintCode](http://www.paintcodeapp.com/)是个非常棒又小而美的mac程序，主要用途是可以将你的矢量图轻松地转换成CoreGraphics代码，可以很轻松的把代码放在你的iOS app里。

对于移动端来讲，给用户良好的用户体验，动画效果是非常必不可少的，loading加载动画，过场动画，提示动画等等，都是我们增加用户体验的手段，但是如果我们通过编写代码去提供动画效果，那必然是一个恶果，所以大多数初创团队，在开发APP的时候，时间比较仓促，需要短时间内出效果，通常用图片来提供。

PaintCod此时的出现，能帮我们减轻计算的繁琐，节省用代码开发动画的时间, 降低了图片的使用率，app容量大大减小，而且做动效也容易了很多。是不是感觉太幸福了!!!

那接下来一起走进PaintCod吧！

## SVG

在运用PaintCode之前呢，我们需要先获取一张SVG格式的文件。

```SVG （可缩放矢量图形）
SVG可缩放矢量图形（Scalable Vector Graphics）是基于可扩展标记语言（XML），用于描述二维矢量图形的一种图形格式。SVG是W3C("World Wide Web ConSortium" 即 " 国际互联网标准组织")在2000年8月制定的一种新的二维矢量图形格式，也是规范中的网络矢量图形标准。SVG严格遵从XML语法，并用文本格式的描述性语言来描述图像内容，因此是一种和图像分辨率无关的矢量图形格式。
```

如果你想自己做自己的SVG文件，可以像[PaintCode让Logo飞出屏幕](https://www.jianshu.com/p/88da7eaf7c46)中讲的通过Sketch自己导出一张SVG格式的图片，当然你要自己购买Sketch软件，每年好像需要500大洋哦！土豪请随意吧！

如果你只想玩玩快速看一下成果你可以到[iconfount](http://www.iconfont.cn/home/index?spm=a313x.7781069.1998910419.2)自己搜索然后自己下载下来！

##PaintCode

当然你要先到这里[PaintCode](http://www.paintcodeapp.com)下载,不过你可能要先翻墙一下，然后可以免费试用5天玩玩。

PaintCode的用法很简单，直接将上面保存的SVG图片扔给他就好了，他会自动生成代码，包括swift和oc，直接将生成的代码复制即可。图片如下：

<div>

​    <img class="shadow" src="/img/in-post/paintCode.jpg" width="380">

</div>

看到没，直接生成代码哎，而且是直接可以用的哦，还可以直接导出文件，OC代码生成.h和.m两个文件。是不是感觉突然幸福了很多，是不是突然感觉自己的逼格升上来了！然后你就拿着这两个文件浪起来吧！

如果感觉不错的话，那你就开始掏钱购买吧！


### 感谢：

​	1、[PaintCode 教程：矢量图轻松转换成CoreGraphics代码](http://www.cocoachina.com/ios/20150601/11956.html)

​	2、[PaintCode让Logo飞出屏幕](https://www.jianshu.com/p/88da7eaf7c46)

