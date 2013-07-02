---
layout: post
title: "使用dispatch_once创建单例"
date: 2013-07-02 14:04
comments: true
categories: iOS
---
今天在看[BWStatusBarOverlay](https://github.com/brunow/BWStatusBarOverlay)的源码时发现他在实例化BWStatusBarOverlay时使用了单例模式。  
代码如下：

```
+ (BWStatusBarOverlay *)shared {
    static dispatch_once_t pred = 0;
    __strong static id _sharedObject = nil;
    dispatch_once(&pred, ^{
        _sharedObject = [[self alloc] init];
    });
    return _sharedObject;
}
```

创建单例关键使用到的方法就是dispatch_once函数。

函数`void dispatch_once( dispatch_once_t *predicate, dispatch_block_t block);`  

其中第一个参数predicate，该参数是检查后面第二个参数所代表的代码块是否被调用的谓词，第二个参数则是在整个应用程序中只会被调用一次的代码块。dispach_once函数中的代码块只会被执行一次，而且还是线程安全的。

通过这个函数我们就可以轻松的创建单例模式了:)