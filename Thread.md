---
title: Java 并发编程系列(1)
tags: Java
date: 2017-06-09 08:28:00
categories: Java
---

 （*文中的方法名参考了Objective-C的语法，方法前面的‘-’表示该方法是非静态方法，‘+’表示是静态方法*）
 
## 与Thread有关的方法
### -start()
功能：开启线程
### -run()
功能：线程启动后会执行run()方法内部的代码

---

*注意：如果直接调用run()方法。它只会在当前线程中串行执行run()中的代码*。

---

<!--more-->

### -join()
功能：等待调用join的线程执行完成后，当前线程再执行以后的代码。
说明：join的本质是调用线程中的一个对象（lock）在当前线程对象示例上wait(),直到调用线程执行完毕后，调用notifyAll()方法通知所有等待线程继续执行。
```
  //join的源码
  public final void join() throws InterruptedException {
        synchronized (lock) {
            while (isAlive()) {
                lock.wait();
            }
        }
    }
```

使用场景：老师要计算某次考试全班平均成绩，安排了三个学生分组统计分数，计算分数的工作必须在三个学生都计算完成后才能进行。这时候就可以用join方法。

---

*Java的**CountDownLatch**和**CycliBarrier**能实现类似的效果。*

---


### +sleep()
功能：顾名思义，让线程睡上一段时间
说明: sleep是一个静态方法，有两种使用方法sleep(millis)和sleep(long millis,int nanos) ,millis:毫秒表示的时间，nanos：毫微妙表示的时间,线程会睡(millis+nanos/1000000)毫秒的时间。

---

*线程sleep的时候不会释放线程占有的资源*

---

### -wait()
功能：让线程进入等待状态(WAITING,TIMED_WAITING)
说明: wait有三种方法，wait()和wait(long millis)，wait(long millis,int nanos),第一种让线程进入无限时间等待的状态(WAITING)，直到其他线程调用notify();后两种让线程进入有限时间的等待,等待时间耗尽或者其它线程调用notify()都会使线程继续执行。

---

 *线程共有New,RUNNABLE,BLOCKED,WAITING,TIMED_WAITING,TERMMINATED六种状态*
*线程wait的时候释会放线程占有的资源，这也是sleep与wait方法一个主要区别*

---

### -notify()
功能：唤醒等待线程
说明: 如果有多个线程同时等待，notify方法会从等待线程中随机挑选一个唤醒，如果想同时唤醒所有等待线程可以使用notifyAll()方法。

---

 **wait()**，**notify()**,**notifyAll()** *都是Object对象的方法*

---

### -interrupt()
功能: 先当前线程送一个中断请求（原文：Posts an interrupt request to this Thread）
说明：interrupt并不会真正中断线程，你可以在run方法内通过Thread.currentThread.isInterrupt()判断线程是否被中断，自己决定是否结束线程。
还有一个静态方法Thread.interrupted()也能判断当前线程的中断状态，但是此方法会清除中断标志，而isInterrupt()不会。

---

*线程在wait(),sleep(),join()期间，如果收到interrupt请求，这些方法会抛出InterruptedException异常。*

---

### +yield() 
功能：让当前线程让出CPU
说明：让出CPU，并不是该线程就不执行了。线程让出CPU后，仍然会参与CPU的争夺，但是不一定能够再次分配到。

### -stop() （已废弃）
功能：终止线程
说明：stop 方法已经被废弃了，不建议使用。原因是此方法过于暴力，强行终止线程，释放线程持有的锁，可能造成一些数据不一致的问题。

---

stop方法不建议使用的话，那么如果终止一个线程呢，可以在线程中设置一个Flag，用于标记线程是否需要被终止，在run()方法中检查Flag，如果Flag标记为终止，就return。

---

### -destory() （已废弃）
说明：此方法已经被废弃，如果调用的话会抛出UnsupportedOperationException

### -suspend() （已废弃）
功能： 线程挂起
说明：此方法已经被废弃，如果调用的话会抛出UnsupportedOperationException

### -resume() （已废弃）
功能： 线程继续执行
说明：此方法已经被废弃，如果调用的话会抛出UnsupportedOperationException
