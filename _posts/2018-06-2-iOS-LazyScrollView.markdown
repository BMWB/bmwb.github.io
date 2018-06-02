---
layout:     post
title:      "LazyScrollView"
subtitle:   "LazyScrollView"
date:       2018-06-02
author:     "WTJ"
header-img: "img/post-bg-js-module.jpg"
catalog: true
tags:
    - iOS

---

##LazyScrollView是什么

LazyScrollView 继承自ScrollView，目标是解决异构（与TableView的同构对比）滚动视图的复用回收问题。它可以支持跨View层的复用，用易用方式来生成一个高性能的滚动视图



## LazyScrollView结构

TMLazyScrollView:LazyScrollView主视图

TMLazyReusePool:LazyScrollView的缓存池

TMLazyModelBucket:存储、移除、重载、可显示数据

TMLazyItemModel:模型存储CGRectj和muiID，readonly上、下位置

UIView+TMLazyScrollView：分类



## TMLazyReusePool

```
@interface TMLazyReusePool () {
    NSMutableDictionary<NSString *, NSMutableSet *> *_reuseDict;
}
```

key：用来存储reuseIdentifier。

键：用NSMutableSet来存储reuseIdentifier下的所有view。

```
- (UIView *)dequeueItemViewForReuseIdentifier:(NSString *)reuseIdentifier andMuiID:(NSString *)muiID
{
    if (reuseIdentifier == nil || reuseIdentifier.length == 0) {
        return nil;
    }
    UIView *result = nil;
    NSMutableSet *reuseSet = [_reuseDict tm_safeObjectForKey:reuseIdentifier];
    if (reuseSet && reuseSet.count > 0) {
        if (!muiID) {
            result = [reuseSet anyObject];
        } else {
            for (UIView *itemView in reuseSet) {
                if ([itemView.muiID isEqualToString:muiID]) {
                    result = itemView;
                    break;
                }
            }
            if (!result) {
                result = [reuseSet anyObject];
            }
        }
        [reuseSet removeObject:result];
    }
    return result;
}
```

通过这个方法你可以看出是从缓存池中`_reuseDict`取响应View通过。可以通过下面两种方式：

1、`reuseIdentifier`取出任意一个View来加载视图上，加载视图上再会把这个view从缓存池中删掉，保证下次不会取相同的view。

2、`muiID`用来取指定View，没有指定muiID就取任意View。



## TMLazyItemModel

```
@property (nonatomic, assign) CGRect absRect;
@property (nonatomic, readonly) CGFloat top;
@property (nonatomic, readonly) CGFloat bottom;
@property (nonatomic, copy) NSString *muiID;
```

View的位置数据要提前算好，然后赋值。



## TMLazyModelBucket

```
- (NSSet<TMLazyItemModel *> *)showingModelsFrom:(CGFloat)startY to:(CGFloat)endY
{
    NSMutableSet *result = [NSMutableSet set];
    NSInteger startIndex = (NSInteger)floor(startY / _bucketHeight);
    NSInteger endIndex = (NSInteger)floor((endY - 0.01) / _bucketHeight);
    for (NSInteger index = 0; index <= endIndex; index++) {
        if (_buckets.count > index && index >= startIndex && index <= endIndex) {
            NSSet *bucket = [_buckets objectAtIndex:index];
            [result unionSet:bucket];
        }
    }
    NSMutableSet *needToBeRemoved = [NSMutableSet set];
    for (TMLazyItemModel *itemModel in result) {
        if (itemModel.top >= endY || itemModel.bottom <= startY) {
            [needToBeRemoved addObject:itemModel];
        }
    }
    [result minusSet:needToBeRemoved];
    return [result copy];
}
```

这个是方法是用来计算view是否在ScrollView上显示，显示加载



## TMLazyScrollView

1. 加载视图的时候, 会遍历所有的 rect, 计算已经显示或者将要显示的 id
2. 在计算显示的 id 的时候, 同时也要计算消失的 id
3. 获取显示的 id 对应的 view, 并且把他们放到 view 上
4. scrollView 重用显示是通过 delegate 来完成的
5. 需要为每个 item 返回一个 TMMuiRectModel
6. 需要通过 id 自行配置对应的 view(在这里需要注意的是获取 view 需要调用 scrollView 的方法)



##感谢：

​	1、[LazyScrollView](https://github.com/alibaba/LazyScrollView)