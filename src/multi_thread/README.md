# C++ 多线程备忘

因代码不宜公开，因此先在这里建立工程进行代码编写和笔记总结。

## 0 为什么使用多线程

* 任务分解

耗时的操作，任务分解，实时响应

* 数据分解

充分利用多核 CPU 处理数据

* 数据流分解

读写分离，解耦合设计


## 1 thread 对象的生命周期和线程的等待、分离

这部分见代码的注释部分，在这一部分中老师的代码有些错误，已经在更改。

 ## 2 线程创建的几种方式

 1，2 部分已经演示了一种线程创建的方式，即用全局函数指针的方式。这里演示的是 thread 初始化可以是多个参数，并且位于 栈 中的参数的拷贝构造行为。在参数生命的时候新建并初始化参数，在线程创建的时候拷贝构造参数，在进入线程回调函数的时候，参数再次拷贝复制。

## 3 参数传递的有些坑

传递的空间已经销毁，多线程共享一块空间，传递的指针变量的声明周期小于线程，代码中查看这个坑的代码示例。

传递引用也是如此，线程是模板定义的，在内部并不知道传递来的参数是引用，引用不复制参数，当引用空间被释放了，还是会出错。正确的做法是用 ref 修饰，明确告知传递的是引用。

## 4 使用成员函数作为线程入口

前面章节的做法都是将全局函数或者静态函数作为线程的参数，这部分使用的成员函数与普通全局函数的性质是一致的。

成员函数作为线程入口，可以有两种做法，一种是以其它类的成员数作为线程回调函数，一种是以当前类的成员函数作为入口函数（成员函数是否封装在当前类内，是否隐藏线程数据结构 ）。代码参考示例程序。


## 5 lambda 函数作为线程入口

全局 lambda ，其需要捕获的参数可以在 thread 构造函数中指定，见示例；lambda 作为类成员函数，可以访问成员变量，格式是  ```[this](type value){ func defun;}```,



