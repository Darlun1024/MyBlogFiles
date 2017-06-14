﻿---
title: EventBus android.os.PersistableBundle错误
date: 2017-06-14 16:30:07
tags: Android
---

今日例行检查Bugly上报的异常数据，发现App抛出了这么一个错误
```
  java.lang.NoClassDefFoundError: android/os/PersistableBundle
    at java.lang.Class.getDeclaredMethods(Native Method)
    at java.lang.Class.getPublicMethodsRecursive(Class.java:901)
    at java.lang.Class.getMethods(Class.java:884)
    at org.greenrobot.eventbus.SubscriberMethodFinder.findUsingReflectionInSingleClass(SubscriberMethodFinder.java:157)
    at org.greenrobot.eventbus.SubscriberMethodFinder.findUsingInfo(SubscriberMethodFinder.java:88)
    at org.greenrobot.eventbus.SubscriberMethodFinder.findSubscriberMethods(SubscriberMethodFinder.java:64)
    at org.greenrobot.eventbus.EventBus.register(EventBus.java:136)
    at test.wsj.com.eventbustest.MainActivity.onCreate(MainActivity.java:19)
at android.app.Activity.performCreate(Activity.java:5501)
    at android.app.Instrumentation.callActivityOnCreate(Instrumentation.java:1088)
    at android.app.ActivityThread.performLaunchActivity(ActivityThread.java:2302)
    at android.app.ActivityThread.handleLaunchActivity(ActivityThread.java:2390)
    at android.app.ActivityThread.access$800(ActivityThread.java:151)
    ........
```
在开发过程中，真机测试从未发现过此类问题。Google之，发现这个问题已经有人遇到了，解决方案也很简单，干掉Activity中的以下方法

```
 @Override
public void onSaveInstanceState(Bundle outState, PersistableBundle outPersistentState) {
        super.onSaveInstanceState(outState, outPersistentState);
    }
```

解决方案找到了，但是本着惩前毖后，治病救人的宗旨,为以后遇到类似问题提供一个解决思路，我分析了一下这个错误产生的原因。
    EventBus的工作机制各位大神已经分析的很清楚了(不懂的请移步：http://blog.csdn.net/lmj623565791/article/details/40920453)，这里不再介绍。EventBus涉及的技术大概有单例、观察者模式、Java的反射、注解等。从LogCat打印出的方法调用栈信息，我们可以发现导致这个`NoClassDefFoundError`错误的发生在调用反射方法的位置。EventBus在注册时，会通过反射方法找到带有注解 `@Subscribe` 的公开方法，在此过程中会遍历到
`public void onSaveInstanceState(Bundle outState, PersistableBundle outPersistentState)`
    方法。PersistableBundle这个类是在Android 5.0才引入的，因此在Android版本低于5.0的手机上，Android运行库内找不着这个类，才爆出这个错误。从Bugly反馈信息来看，上传这个错误的设备系统正是Android 4.4版本的。
    同样的道理，如果在程序中使用Android6.0才有的新class，如代码中增加以下方法
```
public void readNetworkStats(NetworkStats stats){}
```
在Android6.0以下版本系统的手机也会爆出`NoClassDefFoundError`错误。因此，在开发App时，如果为兼容性考虑，新的功能和特性应该慎用。再次，App运行过程中发现这种错误，也切莫慌乱，答案其实就在问题之中。
    
    