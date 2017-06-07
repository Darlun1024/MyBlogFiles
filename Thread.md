---
title: Java 并发编程系列(1)
tags: Java
---
## 首先看看Tread的相关方法
### start()
功能：开启线程
### run()
功能：线程启动后会执行run()方法内部的代码
*注意：如果直接调用run()方法。它只会在当前线程中串行执行run()中的代码*
### stop()
功能：终止线程
注意：stop 方法已经被废弃了，不建议使用。原因是此方法过于暴力，强行终止线程，释放线程持有的锁，可能造成一些数据不一致的问题。
```
//附带一个示例代码
```
stop方法不建议使用的话，那么如果终止一个线程呢，以后再说。
### join()
功能：等待调用join的线程执行完成后，当前线程在执行以后的代码。
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
wait()
notify()
interrupt()
isInterrupt()
sleep()
yield()
destory()
suspend()
resume()
