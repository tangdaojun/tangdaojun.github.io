---
layout: git-wiki-post
title:  Android性能优化系列（一）屏幕和UI性能
date:   2019-11-03 20:15:02 +0800
categories: android
permalink: /:categories/:year/:month/:day/high-performance-android-ui-2.html
---
# Android性能优化系列(一) - 屏幕和UI性能
推动消费者BG所有Android应用的UI能够快速渲染并流畅运行，为用户带来更好的用户体验。



#### 课程目标

1、掌握分析屏幕和UI性能的工具

2、掌握优化屏幕和UI性能的方法



#### 课程目录

1、UI性能基准

2、Android团队对UI和渲染性能的改进

3、Hierary View

4、过度绘制

5、分析卡顿

6、丢帧



####课程内容

##### UI性能基准

######人类心理感知

有研究显示，

0～100ms的延迟会让用户感知到瞬时的卡顿；

100～300ms的延迟会让用户感知迟缓；

300～1000ms的延迟会让用户感觉“手机卡死了”；

1000ms以上的延迟会让用户想去干别的事情。

另外有研究表明：

50%以上的用户已经开始放弃使用那些加载时间在3～4s的网页了，对于App也是如此。



###### 卡顿

大部分Android设备一秒刷新屏幕60次，也就是16ms刷新一次（1s/60fps=16ms/f），所以保证每帧的渲染时间少于16ms是非常重要的。如果有一帧跳过了，用户就能感知到动画跳跃，这样体验感觉就会比较差了。



##### Android团队对UI和渲染性能的改进

| Android版本号 | 代号               | 屏幕绘制                                  |
| ------------- | ------------------ | ----------------------------------------- |
| <=2.3         | Gingerbread        | CPU                                       |
| 3.0、3.1、3.2 | Honeycomb          | 默认CPU，可以指定使用GPU                  |
| \>= 4.0       | Ice Cream Sandwich | GPU硬件加速默认开启                       |
| 4.1           | Jelly Bean         | 黄油计划：改善VSYNC时许，增加额外的帧缓冲 |

<= Android 2.3 (Gingerbread) 的版本完全是通过软件来实现屏幕的绘制；

Android 3.0 (Honeycomb) ~ Android 3.2  (Honeycomb) 加入了GPU的支持，但是默认是关闭的，开发者可以选择打开；

Android 4.0 (IceCreamSandwich) 之后GPU硬件加速默认是开启的；

Android 4.1 (JellyBean) & Android 4.2 (JellyBean) “黄油计划”：改善VSYNC的时序（更好地调度帧的创建）、增加额外的帧缓冲；



Android团队在做这些改进的同事，也提供了一系列的工具来测量屏幕绘制、VSYNC缓冲和卡顿的情况，并对开发者开放这些工具。



##### Hierary View

1、减少视图深度/层级，减少视图个数

2、<include>，<merge>

3、延迟加载视图：ViewStub

Windows

​	Load View Hierarchy(Load the view hierarchy into the tree view)

Tree View

​	Profile Node(Obtain layout times for tree rooted at selected node)

Tree Overview

Layout View



![image-20190704092505812](/Users/tang/Library/Application Support/typora-user-images/image-20190704092505812.png)

未优化的翻译机3.0的首页

![image-20190704094243917](/Users/tang/Library/Application Support/typora-user-images/image-20190704094243917.png)

视图层级深度：19

1、减少不必要的View

2、减小视图深度/层级

3、如果XML文件里最外层的视图只是用来承载子视图的，那么它只是增加了App视图结构的深度。这种情况下，你可以移除这个视图，用<merge>标签来替代。



翻译记录页面

视图个数：63

视图层级深度：12

![image-20190704101547227](/Users/tang/Library/Application Support/typora-user-images/image-20190704101547227.png)

![image-20190704101632847](/Users/tang/Library/Application Support/typora-user-images/image-20190704101632847.png)



##### Layout Inspector

非常简单







##### 过度绘制

| 颜色 | 过度绘制次数 |
| ---- | ------------ |
| 白色 | 0            |
| 蓝色 | 1            |
| 绿色 | 2            |
| 粉色 | 3            |
| 红色 | 4            |

减少过度绘制的小技巧

1、

2、

3、

Overdraw Avoidance



#####分析卡顿



#####丢帧

systrace

android.os.Trace

Trace.beginTrace(String sectionName);

Trace.endTrace();

在代码中必须成对出现，一般将endTrace放到finally语句块中，另外，必须在同一个线程。

| 快捷键 | 作用                                          |
| ------ | --------------------------------------------- |
| W / S  | 放大 / 缩小 （和shift组合使用缩放速度会变快） |
| A / D  | 左移 / 右移（和shift组合使用移动速度会变快）  |
| F      | 放大选中节点                                  |
| 0      | 还原缩放比例                                  |
| G      | 展示16ms网格                                  |
| V      | 高亮VSYNC事件                                 |
| M      | 标记当前选中节点                              |



#### 参考

**Why 60fps?**

1、https://ww22211w.youtube.com/watch?v=CaMTIgxCSqU&index=25&list=PLWz5rJ2EKKc9CBxr3BVjPTPoDPLdPIFCE

**Hierarchy View:**

1、https://developer.android.com/studio/profile/hierarchy-viewer

2、https://developer.android.com/training/improving-layouts

**GPU overdraw**

1、https://developer.android.com/topic/performance/rendering/overdraw

**Profile GPU Rendering**

1、https://developer.android.com/studio/profile/inspect-gpu-rendering

2、https://developer.android.com/topic/performance/rendering/profile-gpu

3、https://developer.android.com/training/testing/performance

**systrace:**

1、https://developer.android.com/studio/profile/systrace.html

2、https://source.android.com/devices/tech/debug/systrace

**TraceView**

1、https://developer.android.com/studio/profile/traceview

**CPU profiler**

1、https://developer.android.com/studio/profile/cpu-profiler

1、[https://developer.android.com/topic/performance/vitals/render](https://developer.android.com/topic/performance/vitals/render)

2、[https://developer.android.com/topic/performance/vitals/frozen](https://developer.android.com/topic/performance/vitals/frozen)

3、https://developer.android.com/training/testing/performance



https://developer.android.com/guide/topics/graphics/hardware-accel

**Others**

1、《高性能Android应用开发》[美] Doug Sillars

2、https://developer.android.com/topic/performance/rendering/optimizing-view-hierarchies

3、https://android-developers.googleblog.com/2017/08/understanding-performance-benefits-of.html

4、https://developer.android.com/training/constraint-layout





------

**汤道军**



科大讯飞股份有限公司

消费者事业群 – 消费品研发四部（智能翻译）

手机：18355106425

邮箱：[djtang@iflytek.com](mailto:djtang@iflytek.com)

地址：安徽省合肥市望江西路666号讯飞大厦

------
