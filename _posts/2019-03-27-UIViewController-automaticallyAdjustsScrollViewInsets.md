---
layout: post
title: 'UIViewController automaticallyAdjustsScrollViewInsets'
date: 2019-03-27
cover: ''
tags: 'UIViewController ScrollView Insets'
---

在使用了 addSubView, addChildController 的场景下，childController 里的 collectionView 顶部会出现 20 pt 的偏移，并且在设置了 automaticallyAdjustsScrollViewInsets 为 NO 的情况下,部分设备并不生效。该属性设置在 collectionView 的初始化过程中。

首先在开发者文档里查看这个属性的描述如下:

该属性的默认值为 YES，它使得容器视图控制器知道，它应该调整视图控制器的滚动视图的插入，考虑留出空间给状态栏，搜索栏，导航栏，工具栏或者选项卡栏。如果你的视图控制器自己管理它的滚动视图的插入，那么就把这个属性设置为 NO。

那么问题就显而易见了，在将 collectionView 设置为外部容器控制器的子视图之后，应该在容器视图控制器中，去设置这个自动调整 insets 的属性，而不是在子控制器中进行配置。
