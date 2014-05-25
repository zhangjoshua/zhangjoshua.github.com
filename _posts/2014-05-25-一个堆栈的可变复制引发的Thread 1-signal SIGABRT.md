---
layout: post
title: 一个堆栈的可变复制引发的Thread 1:signal SIGABRT
category: Objective-C
tags:
- obj学习

---

午觉醒后，将拖延半个月的作业继续往下啃，在调试时发现了坑。最惨的是，已经忘记之前做到了哪里，只好将代码重头看来，妈蛋，这就是个天杀的坏习惯。

逻辑理顺了，发现没有任何坑的迹象，暂时理解为软件抽风吧，强行再次build，呵呵，奔溃重现：`Thread 1:signal SIGABRT`，经过多次尝试放弃了，还是去 stackoverflow 看看吧。


![image](http://pic.yupoo.com/zhangjoshua/DMxWmZAQ/medish.jpg)

解决思路：先找到问题代码

1、找教程发现了一个 add Exception Breakpoint 的方法

* 先打上断点：

![image](http://pic.yupoo.com/zhangjoshua/DMxWmTWo/medish.jpg)


* 再重新运行一次，就会在出错的地方停下来，并且错误的地方会标识出来


![image](http://pic.yupoo.com/zhangjoshua/DMxWmHyN/medish.jpg)

OK，问题已经找到。现在需要尝试消除错误。

`if(topOfStack)[stack removeLastObject];`

表面上看一点问题都没有，逻辑都正确，从下面监控可以看出，值没有传到 formattedString，但仍就没有思路。

![image](http://pic.yupoo.com/zhangjoshua/DMy1tQ8E/medish.jpg)

多次尝试发现，removeLastObject 是在原堆栈里进行，意味着，为了显示将堆栈中的数据删除了，而后期计算将得不到任何数据。

果断加上 `stack = [stack mutableCopy];`

警报解除，运行正常。

##### 总结
* Thread 1: signal SIGABRT类型的错误，实际上都是具体的某种内部的错误，然后最终传递到上层的thread的，而报此错误的。
* 学会了断点排查方法
* 错误有时候不在逻辑上，某个细小的引用也不能忽视

##### 参考

* [【已解决】Xcode中编译iOS程序，运行出错：Thread 1: signal SIGABRT](http://www.crifan.com/thread_1_signal_sigabrt_xcode_ios/)
* [I have an error in main.m “Thread 1: signal SIGABRT” How can I fix this?](http://stackoverflow.com/questions/9782621/i-have-an-error-in-main-m-thread-1-signal-sigabrt-how-can-i-fix-this)





