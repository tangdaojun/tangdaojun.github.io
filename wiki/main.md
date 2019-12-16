---
title: "主页"
redirect_from: "/"
date: 2019-11-03 19:02:02 +0800
permalink: "main.html"
---

这是一个聚焦如何开发高性能Android应用程序的博客，我希望通过个人的分享给大家带来有价值的内容。

**一、UI性能调优**

- 常见问题：卡顿、丢帧
- 理论知识：16ms/f、Slow Rendering、Frozen Frames
- 实战教程：如何衡量UI性能指标
  - 1、GPU呈现模式
  - 2、adb shell dumpsys gfxinfo $package [framestats]
  - 3、FPS统计
- 实战教程：工具篇
  - 1、Hierarchy View（已废弃）
  - 2、Layout Inspector
  - 3、过度绘制
  - 4、systrace
  - 5、Perfetto
  - 6、Lint
  - 7、TraceView（已废弃）
  - 8、CPU Profiler
- 实战教程：代码篇
  - 1、\<include>
  - 2、\<merge>
  - 3、ConstraintLayout
  - 4、\<ViewStub>

**二、App启动时间优化**

**三、内存性能**

- 1、常见问题：常见内存问题
  - 1、内存溢出
  - 2、内存泄漏
  - 3、内存抖动、频繁GC
- 2、理论知识：Android内存它是如何工作的
  - 1、垃圾回收
  - 2、共享内存与私有内存
  - 3、脏内存与干净内存
- 3、实战教程：查看App内存使用情况
  - 1、adb shell dumpsys meminfo [pid]
  - 2、adb shell dumpsys meminfo -s package
- 4、实战教程：追踪内存泄漏的工具
  - 1、Android Studio Memory Profiler
  - 2、LeakCanary
  - 3、Logcat
  - 4、Lint
  - 5、StrictMode
- 5、经验总结：
  - 1、内存泄漏
    - 1、单例导致内存泄漏
    - 2、静态变量导致内存泄露
    - 3、Handler内存泄露
    - 4、未取消注册或回调导致内存泄露
    - 5、Timer和TimerTask导致内存泄露
    - 6、资源未关闭或释放导致内存泄露
    - 7、属性动画造成内存泄露
    - 8、WebView造成内存泄露
    - 9、bitmap
  - 2、内存溢出
    - 1、使用轻量的数据结构
      - SparseArray
      - ArrayMap
    - 2、尽量少使用Enum
    - 3、RecyclerView替代Listview

**四、CPU和CPU性能**

- 检测CPU占用率
- 使用Systrace分析CPU
- TraceView（遗留的监视器DDMS工具）
- CPU Profiler（Android Studio）
- 其他优化工具

**五、网络性能**

- WI-FI与蜂窝无线电
- 测试工具
- Android网络优化
- 全球移动网络覆盖范围

**六、硬件性能和电池寿命**

- Android的硬件特点
- 耗电原因
- 基本的电量消耗分析
- 高级电池监控
- JobScheduler