---
layout:     post
title:      "小马哥Java面试题课程总结"
subtitle:   "面试虐我千百遍，Java 并发真讨厌"
date:       2019-04-14
author:     "caojiele"
header-img: "img/in-post/2019.04/14/post-java-interview.jpg"
tags:
    - Java
    - 面试
    - 慕课网手记
---

> 本文来自于我的[慕课网手记](https://www.imooc.com/u/4024769)：[小马哥Java面试题课程总结](https://www.imooc.com/article/288342)，转载请保留链接 ;)

前段时间在慕课网直播上听[小马哥](https://www.imooc.com/t/5387391)面试劝退（"面试虐我千百遍，Java 并发真讨厌"），发现讲得东西比自己拿到offer还要高兴，于是自己在线下做了一点小笔记，供各位参考。

课程地址：[https://www.bilibili.com/video/av49124110](https://www.bilibili.com/video/av49124110)

源码文档地址：[https://github.com/mercyblitz/tech-weekly](https://github.com/mercyblitz/tech-weekly/tree/master/2019.04.12%20%E3%80%8C%E5%B0%8F%E9%A9%AC%E5%93%A5%E6%8A%80%E6%9C%AF%E5%91%A8%E6%8A%A5%E3%80%8D-%20%E7%AC%AC%E4%BA%8C%E5%8D%81%E4%B8%89%E6%9C%9F%E3%80%8A%E9%9D%A2%E8%AF%95%E8%99%90%E6%88%91%E5%8D%83%E7%99%BE%E9%81%8D%EF%BC%8CJava%20%E5%B9%B6%E5%8F%91%E7%9C%9F%E8%AE%A8%E5%8E%8C%EF%BC%88%E7%BB%AD%EF%BC%89%E3%80%8B)

## Java 多线程

### 1、线程创建

#### 基本版
有哪些方法创建线程？

仅仅只有**new thread**这种方法创建线程

```java
public class ThreadCreationQuestion {

    public static void main(String[] args) {
        // main 线程 -> 子线程
        Thread thread = new Thread(() -> {
        }, "子线程-1");

    }

    /**
     * 不鼓励自定义（扩展） Thread
     */
    private static class MyThread extends Thread {

        /**
         * 多态的方式，覆盖父类实现
         */
        @Override
        public void run(){
            super.run();
        }
    }

}
```

与运行线程方法区分：
**java.lang.Runnable()** 或 **java.lang.Thread类**

#### 进阶版
如何通过Java 创建进程？
```java
public class ProcessCreationQuestion {

    public static void main(String[] args) throws IOException {

        // 获取 Java Runtime
        Runtime runtime = Runtime.getRuntime();
        Process process = runtime.exec("cmd /k start http://www.baidu.com");
        process.exitValue();
    }
}
```

#### 劝退版
如何销毁一个线程？
```java
public class ThreadStateQuestion {


    public static void main(String[] args) {

        // main 线程 -> 子线程
        Thread thread = new Thread(() -> { // new Runnable(){ public void run(){...}};
            System.out.printf("线程[%s] 正在执行...\n", Thread.currentThread().getName());  // 2
        }, "子线程-1");

        // 启动线程
        thread.start();

        // 先于 Runnable 执行
        System.out.printf("线程[%s] 是否还活着: %s\n", thread.getName(), thread.isAlive()); // 1
        // 在 Java 中，执行线程 Java 是没有办法销毁它的，
        // 但是当 Thread.isAlive() 返回 false 时，实际底层的 Thread 已经被销毁了
    }
```

Java代码中是无法实现的，只能表现一个线程的状态。

而CPP是可以实现的。

### 2、线程执行

#### 基本版
如何通过 Java API 启动线程？

**thread.start();**

#### 进阶版
当有线程 T1、T2 以及 T3，如何实现T1 -> T2 -> T3的执行顺序？
```java
private static void threadJoinOneByOne() throws InterruptedException {
        Thread t1 = new Thread(ThreadExecutionQuestion::action, "t1");
        Thread t2 = new Thread(ThreadExecutionQuestion::action, "t2");
        Thread t3 = new Thread(ThreadExecutionQuestion::action, "t3");

        // start() 仅是通知线程启动
        t1.start();
        // join() 控制线程必须执行完成
        t1.join();

        t2.start();
        t2.join();

        t3.start();
        t3.join();
    }

    private static void action() {
        System.out.printf("线程[%s] 正在执行...\n", Thread.currentThread().getName());  // 2
    }
}
```
**CountDownLatch**也可以实现；

**调整优先级**并不能保证优先级高的线程先执行。

#### 劝退版
以上问题请至少提供另外一种实现？（1.5）

1、spin 方法

```java
    private static void threadLoop() {

        Thread t1 = new Thread(ThreadExecutionQuestion::action, "t1");
        Thread t2 = new Thread(ThreadExecutionQuestion::action, "t2");
        Thread t3 = new Thread(ThreadExecutionQuestion::action, "t3");

        t1.start();

        while (t1.isAlive()) {
            // 自旋 Spin
        }

        t2.start();

        while (t2.isAlive()) {

        }

        t3.start();

        while (t3.isAlive()) {

        }
    }
```

2、sleep 方法

```java
 private static void threadSleep() throws InterruptedException {

        Thread t1 = new Thread(ThreadExecutionQuestion::action, "t1");
        Thread t2 = new Thread(ThreadExecutionQuestion::action, "t2");
        Thread t3 = new Thread(ThreadExecutionQuestion::action, "t3");

        t1.start();

        while (t1.isAlive()) {
            // sleep
            Thread.sleep(0);
        }

        t2.start();

        while (t2.isAlive()) {
            Thread.sleep(0);
        }

        t3.start();

        while (t3.isAlive()) {
            Thread.sleep(0);
        }

    }
```

3、while 方法

```java
    private static void threadWait() throws InterruptedException {

        Thread t1 = new Thread(ThreadExecutionQuestion::action, "t1");
        Thread t2 = new Thread(ThreadExecutionQuestion::action, "t2");
        Thread t3 = new Thread(ThreadExecutionQuestion::action, "t3");

        threadStartAndWait(t1);
        threadStartAndWait(t2);
        threadStartAndWait(t3);
    }

    private static void threadStartAndWait(Thread thread) {

        if (Thread.State.NEW.equals(thread.getState())) {
            thread.start();
        }

        while (thread.isAlive()) {
            synchronized (thread) {
                try {
                    thread.wait(); // 到底是谁通知 Thread -> thread.notify();  JVM帮它唤起
                                  // LockSupport.park(); 
                                 // 死锁发生
                } catch (Exception e) {
                    throw new RuntimeException(e);
                }
            }
        }
    }
```
### 3、线程终止

#### 基本版
如何停止一个线程？

```java
public class HowToStopThreadQuestion {

    public static void main(String[] args) throws InterruptedException {

        Action action = new Action();

        // 方法一
        Thread t1 = new Thread(action, "t1");

        t1.start();

        // 改变 action stopped 状态
        action.setStopped(true);

        t1.join();

        // 方法二
        Thread t2 = new Thread(() -> {
            if (!Thread.currentThread().isInterrupted()) {
                action();
            }
        }, "t2");

        t2.start();
        // 中断操作(仅仅设置状态，而并非中止线程）
        t2.interrupt();
        t2.join();
    }


    private static class Action implements Runnable {

        // 线程安全问题，确保可见性（Happens-Before)
        private volatile boolean stopped = false;

        @Override
        public void run() {
            if (!stopped) {
                // 执行动作
                action();
            }
        }

        public void setStopped(boolean stopped) {

            this.stopped = stopped;
        }
    }

    private static void action() {
        System.out.printf("线程[%s] 正在执行...\n", Thread.currentThread().getName());  // 2
    }
}

```
想要停止一个线程是不可能的，真正的只能停止逻辑。

#### 进阶版
为什么 Java 要放弃 Thread 的 stop()方法？

**Because it is inherently unsafe. Stopping a thread causes it to unlock all the monitors that it has locked.**(The monitors are unlocked as the ThreadDeath exception propagates up the stack.) If any of the objects previously protected by these monitors were in an inconsistent state, other threads may now view these objects in an inconsistent state. Such objects are said to be damaged. When threads operate on damaged objects, arbitrary behavior can result. This behavior may be subtle and difficult to detect, or it may be pronounced. Unlike other unchecked exceptions, ThreadDeath kills threads silently; thus, the user has no warning that his program may be corrupted. The corruption can manifest itself at any time after the actual damage occurs, even hours or days in the future.

该方法具有固有的不安全性。用 Thread.stop 来终止线程将释放它已经锁定的所有监视器（作为沿堆栈向上传播的未检查 ThreadDeath 异常的一个自然后果）。如果以前受这些监视器保护的任何对象都处于一种不一致的状态，则损坏的对象将对其他线程可见，这有可能导致任意的行为。stop 的许多使用都应由只修改某些变量以指示目标线程应该停止运行的代码来取代。目标线程应定期检查该变量，并且如果该变量指示它要停止运行，则从其运行方法依次返回。如果目标线程等待很长时间（例如基于一个条件变量），则应使用 interrupt 方法来中断该等待。

[Why is Thread.stop deprecated?](https://docs.oracle.com/javase/7/docs/technotes/guides/concurrency/threadPrimitiveDeprecation.html)

**简单的说，防止死锁，以及状态不一致的情况出现。**

#### 劝退版
请说明 Thread interrupt()、isInterrupted() 以及 interrupted()的区别以及意义？

**Thread interrupt()：** 设置状态，调JVM的本地（native）`interrupt0`()方法。

```java
    public void interrupt() {
        if (this != Thread.currentThread())
            checkAccess();

        synchronized (blockerLock) {
            Interruptible b = blocker;
            if (b != null) {
                interrupt0();  // Just to set the interrupt flag
                              //--> private native void interrupt0();
                b.interrupt(this);
                return;
            }
        }
        interrupt0();
    }
```

**isInterrupted()：** 调的是静态方法`isInterrupted()`,当且仅当状态设置为中断时，返回`false`，并不清除状态。

```java
  public static boolean interrupted() {
        return currentThread().isInterrupted(true);
    }

    /**
     * Tests whether this thread has been interrupted.  The <i>interrupted
     * status</i> of the thread is unaffected by this method.
     *
     * <p>A thread interruption ignored because a thread was not alive
     * at the time of the interrupt will be reflected by this method
     * returning false.
     *
     * @return  <code>true</code> if this thread has been interrupted;
     *          <code>false</code> otherwise.
     * @see     #interrupted()
     * @revised 6.0
     */
     
    public boolean isInterrupted() {
        return isInterrupted(false);
    }
```

**interrupted()：** 私有本地方法，即判断中断状态，又清除状态。
```java
 private native boolean isInterrupted(boolean ClearInterrupted);
```

### 4、线程异常

#### 基本版
当线程遇到异常时，到底发生了什么？

线程会挂
```java
public class ThreadExceptionQuestion {

    public static void main(String[] args) throws InterruptedException {
        //...
        // main 线程 -> 子线程
        Thread t1 = new Thread(() -> {
            throw new RuntimeException("数据达到阈值");
        }, "t1");

        t1.start();
        // main 线程会中止吗？
        t1.join();

        // Java Thread 是一个包装，它由 GC 做垃圾回收
        // JVM Thread 可能是一个 OS Thread，JVM 管理，
        // 当线程执行完毕（正常或者异常）
        System.out.println(t1.isAlive());
    }
}
```

#### 进阶版
当线程遇到异常时，如何捕获？

```java
...
        Thread.setDefaultUncaughtExceptionHandler((thread, throwable) -> {
            System.out.printf("线程[%s] 遇到了异常，详细信息：%s\n",
                    thread.getName(),
                    throwable.getMessage());
        });
...
```

#### 劝退版
当线程遇到异常时，ThreadPoolExecutor 如何捕获异常？

```java
public class ThreadPoolExecutorExceptionQuestion {

    public static void main(String[] args) throws InterruptedException {

//        ExecutorService executorService = Executors.newFixedThreadPool(2);

        ThreadPoolExecutor executorService = new ThreadPoolExecutor(
                1,
                1,
                0,
                TimeUnit.MILLISECONDS,
                new LinkedBlockingQueue<>()
        ) {

            /**
             * 通过覆盖 {@link ThreadPoolExecutor#afterExecute(Runnable, Throwable)} 达到获取异常的信息
             * @param r
             * @param t
             */
            @Override
            protected void afterExecute(Runnable r, Throwable t) {
                System.out.printf("线程[%s] 遇到了异常，详细信息：%s\n",
                        Thread.currentThread().getName(),
                        t.getMessage());
            }

        };

        executorService.execute(() -> {
            throw new RuntimeException("数据达到阈值");
        });

        // 等待一秒钟，确保提交的任务完成
        executorService.awaitTermination(1, TimeUnit.SECONDS);

        // 关闭线程池
        executorService.shutdown();

    }
}
```

### 5、线程状态

#### 基本版
Java 线程有哪些状态，分别代表什么含义？

**NEW**: Thread state for a thread which has not yet started.

未启动的。不会出现在Dump中。

**RUNNABLE**: Thread state for a runnable thread. A thread in the runnable state is executing in the Java virtual machine, but it may be waiting for other resources from the operating system such as processor.

在虚拟机内执行的。运行中状态，可能里面还能看到locked字样，表明它获得了某把锁。

**BLOCKE**: Thread state for a thread blocked waiting for a monitor lock. A thread in the blocked state is waiting for a monitor lock to enter a synchronized block/method or reenter a synchronized block/method after calling {@link Object#wait() Object.wait}.

受阻塞并等待监视器锁。被某个锁(synchronizers)給block住了。

**WAITING**: Thread state for a waiting thread. A thread is in the waiting state due to calling one of the following methods:

```xml
<ul>
    <li>{@link Object#wait() Object.wait} with no timeout</li>
    <li>{@link #join() Thread.join} with no timeout</li>
    <li>{@link LockSupport#park() LockSupport.park}</li>
</ul>
```

A thread in the waiting state is waiting for another thread to perform a particular action.

For example, a thread that has called Object.wait() on an object is waiting for another thread to call Object.notify() or Object.notifyAll() on that object. A thread that has called Thread.join() is waiting for a specified thread to terminate.

无限期等待另一个线程执行特定操作。等待某个condition或monitor发生，一般停留在park(), wait(), sleep(),join() 等语句里。

**TIMED_WAITING**: Thread state for a waiting thread with a specified waiting time. A thread is in the timed waiting state due to calling one of the following methods with a specified positive waiting time:

```xml
<ul>
     <li>{@link #sleep Thread.sleep}</li>
     <li>{@link Object#wait(long) Object.wait} with timeout</li>
     <li>{@link #join(long) Thread.join} with timeout</li>
     <li>{@link LockSupport#parkNanos LockSupport.parkNanos}</li>
     <li>{@link LockSupport#parkUntil LockSupport.parkUntil}</li>
</ul>
```

有时限的等待另一个线程的特定操作。和WAITING的区别是wait() 等语句加上了时间限制 wait(timeout)。

**TERMINATED**: 已退出的; Thread state for a terminated thread. The thread has completed execution.

#### 进阶版
如何获取当前JVM 所有的现场状态？

方法一：命令

`jstack`: jstack用于打印出给定的java进程ID或core file或远程调试服务的Java堆栈信息。主要用来查看Java线程的调用堆栈的，可以用来分析线程问题（如死锁）。

`jsp`

`jsp [option/ -l] pid`

方法二：ThreadMXBean

```java
public class AllThreadStackQuestion {

    public static void main(String[] args) {
        ThreadMXBean threadMXBean = ManagementFactory.getThreadMXBean();
        long[] threadIds = threadMXBean.getAllThreadIds();

        for (long threadId : threadIds) {
            ThreadInfo threadInfo = threadMXBean.getThreadInfo(threadId);
            System.out.println(threadInfo.toString());
        }

    }
}
```

#### 劝退版
如何获取线程的资源消费情况？

```java
public class AllThreadInfoQuestion {

    public static void main(String[] args) {
        ThreadMXBean threadMXBean = (ThreadMXBean) ManagementFactory.getThreadMXBean();
        long[] threadIds = threadMXBean.getAllThreadIds();

        for (long threadId : threadIds) {
//            ThreadInfo threadInfo = threadMXBean.getThreadInfo(threadId);
//            System.out.println(threadInfo.toString());
            long bytes = threadMXBean.getThreadAllocatedBytes(threadId);
            long kBytes = bytes / 1024;
            System.out.printf("线程[ID:%d] 分配内存： %s KB\n", threadId, kBytes);
        }

    }
}
```

### 6、线程同步

#### 基本版
请说明 synchronized 关键字在修饰方法与代码块中的区别？

字节码的区别 (一个monitor,一个synchronized关键字)

```java
public class SynchronizedKeywordQuestion {

    public static void main(String[] args) {

    }

    private static void synchronizedBlock() {
        synchronized (SynchronizedKeywordQuestion.class) {
        }
    }

    private synchronized static void synchronizedMethod() {
    }
}
```

#### 进阶版
请说明 synchronized 关键字与 ReentrantLock 之间的区别？

- 两者都是可重入锁
- synchronized 依赖于 JVM 而 ReentrantLock 依赖于 API
- ReentrantLock 比 synchronized 增加了一些高级功能

相比synchronized，ReentrantLock增加了一些高级功能。主要来说主要有三点：①等待可中断；②可实现公平锁；③可实现选择性通知（锁可以绑定多个条件）
- 两者的性能已经相差无几

[谈谈 synchronized 和 ReentrantLock 的区别](https://snailclimb.top/JavaGuide/#/./essential-content-for-interview/PreparingForInterview/美团面试常见问题总结?id=_3-谈谈-synchronized-和-reentrantlock-的区别)

#### 劝退版
请解释偏向锁对 synchronized 与 ReentrantLock 的价值？

偏向锁只对 synchronized 有用，而 ReentrantLock 已经实现了偏向锁。

[Synchronization and Object Locking](https://wiki.openjdk.java.net/display/HotSpot/Synchronization)

### 7、线程通讯

#### 基本版
为什么 wait() 和 notify() 以及 notifyAll() 方法属于 Object ,并解释它们的作用？

Java所有对象都是来自 Object

**wait():**

**notify():**

**notifyAll():**

#### 进阶版
为什么 Object wait() notify() 以及 notifyAll() 方法必须 synchronized 之中执行？

**wait():** 获得锁的对象，释放锁，当前线程又被阻塞，等同于Java 5 LockSupport 中的park方法

**notify():** 已经获得锁，唤起一个被阻塞的线程，等同于Java 5 LockSupport 中的unpark()方法

**notifyAll():**

#### 劝退版
请通过 Java 代码模拟实现 wait() 和 notify() 以及 notifyAll() 的语义？

### 8、线程退出

#### 基本版
当主线程退出时，守护线程会执行完毕吗？

不一定执行完毕
```java
public class DaemonThreadQuestion {

    public static void main(String[] args) {
        // main 线程
        Thread t1 = new Thread(() -> {
            System.out.println("Hello,World");
//            Thread currentThread = Thread.currentThread();
//            System.out.printf("线程[name : %s, daemon:%s]: Hello,World\n",
//                    currentThread.getName(),
//                    currentThread.isDaemon()
//            );
        }, "daemon");
        // 编程守候线程
        t1.setDaemon(true);
        t1.start();

        // 守候线程的执行依赖于执行时间（非唯一评判）
    }
}
```

#### 进阶版
请说明 ShutdownHook 线程的使用场景，以及如何触发执行？

```java
public class ShutdownHookQuestion {

    public static void main(String[] args) {

        Runtime runtime = Runtime.getRuntime();

        runtime.addShutdownHook(new Thread(ShutdownHookQuestion::action, "Shutdown Hook Question"));

    }

    private static void action() {
        System.out.printf("线程[%s] 正在执行...\n", Thread.currentThread().getName());  // 2
    }
}
```

使用场景：Spring 中 AbstractApplicationContext 的 registerShutdownHook()


#### 劝退版
如何确保主线程退出前，所有线程执行完毕？

```java
public class CompleteAllThreadsQuestion {

    public static void main(String[] args) throws InterruptedException {

        // main 线程 -> 子线程
        Thread t1 = new Thread(CompleteAllThreadsQuestion::action, "t1");
        Thread t2 = new Thread(CompleteAllThreadsQuestion::action, "t2");
        Thread t3 = new Thread(CompleteAllThreadsQuestion::action, "t3");

        // 不确定 t1、t2、t3 是否调用 start()

        t1.start();
        t2.start();
        t3.start();

        // 创建了 N Thread

        Thread mainThread = Thread.currentThread();
        // 获取 main 线程组
        ThreadGroup threadGroup = mainThread.getThreadGroup();
        // 活跃的线程数
        int count = threadGroup.activeCount();
        Thread[] threads = new Thread[count];
        // 把所有的线程复制 threads 数组
        threadGroup.enumerate(threads, true);

        for (Thread thread : threads) {
            System.out.printf("当前活跃线程: %s\n", thread.getName());
        }
    }

    private static void action() {
        System.out.printf("线程[%s] 正在执行...\n", Thread.currentThread().getName());  // 2
    }

}
```

## Java 并发集合框架

### 1、线程安全集合

#### 基本版
请在 Java 集合框架以及 J.U.C 框架中各列举出 List、Set 以及 Map 的实现？

Java 集合框架: LinkedList、ArrayList、HashSet、TreeSet、HashMap

J.U.C 框架: CopyOnWriteArrayList、CopyOnWriteArraySet、ConcurrentSkipListSet、ConcurrentSkipListMap、ConcurrentHashMap

#### 进阶版
如何将普通 List、Set 以及 Map 转化为线程安全对象？
```java
public class ThreadSafeCollectionQuestion {

    public static void main(String[] args) {

        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);

        Set<Integer> set = Set.of(1, 2, 3, 4, 5);

        Map<Integer, String> map = Map.of(1, "A");

        // 以上实现都是不变对象，不过第一个除外

        // 通过 Collections#sychronized* 方法返回

        // Wrapper 设计模式（所有的方法都被 synchronized 同步或互斥）
        list = Collections.synchronizedList(list);

        set = Collections.synchronizedSet(set);

        map = Collections.synchronizedMap(map);

    }
}
```

#### 劝退版
如何在 Java 9+ 实现以上问题？
```java
public class ThreadSafeCollectionQuestion {

    public static void main(String[] args) {

        // Java 9 的实现
        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);

        // Java 9 + of 工厂方法，返回 Immutable 对象

        list = List.of(1, 2, 3, 4, 5);

        Set<Integer> set = Set.of(1, 2, 3, 4, 5);

        Map<Integer, String> map = Map.of(1, "A");

        // 以上实现都是不变对象，不过第一个除外

        // 通过 Collections#sychronized* 方法返回

        // Wrapper 设计模式（所有的方法都被 synchronized 同步或互斥）
        list = Collections.synchronizedList(list);

        set = Collections.synchronizedSet(set);

        map = Collections.synchronizedMap(map);

        //
        list = new CopyOnWriteArrayList<>(list);
        set = new CopyOnWriteArraySet<>(set);
        map = new ConcurrentHashMap<>(map);

    }
}
```

### 2、线程安全 LIST

#### 基本版
请说明 List、Vector 以及 CopyOnWriteArrayList 的相同点和不同点？

**相同点：**

Vector、CopyOnWriteArrayList 是 List 的实现。

**不同点：**

Vector 是同步的,任何时候不加锁。并且在设计中有个 interator ,返回的对象是 `fail-fast`；

CopyOnWriteArrayList 读的时候是不加锁；弱一致性，while true的时候不报错。

#### 进阶版
请说明 Collections#synchromizedList(List) 与 Vector 的相同点和不同点？

**相同点：** 

都是`synchromized` 的实现方式。

**不同点：** 

synchromized 返回的是list, 实现原理方式是 Wrapper 实现；

而 Vector 是 List 的实现。实现原理方式是非 Wrapper 实现。

#### 劝退版
Arrays#asList(Object...)方法是线程安全的吗？如果不是的话，如果实现替代方案？
```java
public class ArraysAsListMethodQuestion {

    public static void main(String[] args) {

        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);
        // 调整第三个元素为 9
        list.set(2, 9);
        // 3 -> 9
        // Arrays.asList 并非线程安全
        list.forEach(System.out::println);
        // Java < 5 , Collections#synchronizedList
        // Java 5+ , CopyOnWriteArrayList
        // Java 9+ , List.of(...) 只读
    }
}
```

### 3、线程安全 SET

#### 基本版
请至少举出三种线程安全的 Set 实现？

synchronizedSet、CopyOnWriteArraySet、ConcurrentSkipListSet

#### 进阶版
在 J.U.C 框架中，存在HashSet 的线程安全实现？如果不存在的话，要如何实现？

不存在；
```java
public class ConcurrentHashSetQuestion {


    public static void main(String[] args) {

    }

    private static class ConcurrentHashSet<E> implements Set<E> {

        private final Object OBJECT = new Object();

        private final ConcurrentHashMap<E, Object> map = new ConcurrentHashMap<>();

        private Set<E> keySet() {
            return map.keySet();
        }

        @Override
        public int size() {
            return keySet().size();
        }

        @Override
        public boolean isEmpty() {
            return keySet().isEmpty();
        }

        @Override
        public boolean contains(Object o) {
            return keySet().contains(o);
        }

        @Override
        public Iterator<E> iterator() {
            return keySet().iterator();
        }

        @Override
        public Object[] toArray() {
            return new Object[0];
        }

        @Override
        public <T> T[] toArray(T[] a) {
            return null;
        }

        @Override
        public boolean add(E e) {
            return map.put(e, OBJECT) == null;
        }

        @Override
        public boolean remove(Object o) {
            return map.remove(o) != null;
        }

        @Override
        public boolean containsAll(Collection<?> c) {
            return false;
        }

        @Override
        public boolean addAll(Collection<? extends E> c) {
            return false;
        }

        @Override
        public boolean retainAll(Collection<?> c) {
            return false;
        }

        @Override
        public boolean removeAll(Collection<?> c) {
            return false;
        }

        @Override
        public void clear() {

        }
    }
}
```

#### 劝退版
当 Set#iterator() 方法返回 Iterator 对象后，能否在其迭代中，给 Set 对象添加新的元素？

不一定；Set 在传统实现中，会有`fail-fast`问题；而在J.U.C中会出现弱一致性，对数据的一致性要求较低，是可以给 Set 对象添加新的元素。

### 4、线程安全 MAP

#### 基本版
请说明 Hashtable、HashMap 以及 ConcurrentHashMap 的区别？

**Hashtable：** key、value值都不能为空; 数组结构上，通过数组和链表实现。

**HashMap：** key、value值都能为空；数组结构上，当阈值到达8时，通过红黑树实现。

**ConcurrentHashMap：** key、value值都不能为空；数组结构上，当阈值到达8时，通过红黑树实现。

[HashMap和Hashtable的比较](https://zhuanlan.zhihu.com/p/37607299)

#### 进阶版
请说明 ConcurrentHashMap 在不同的JDK 中的实现？

JDK 1.6中，采用分离锁的方式，在读的时候，部分锁；写的时候，完全锁。而在JDK 1.7、1.8中，读的时候不需要锁的，写的时候需要锁的。并且JDK 1.8中在为了解决Hash冲突，采用红黑树解决。

[HashMap? ConcurrentHashMap? 相信看完这篇没人能难住你！](https://zhuanlan.zhihu.com/p/50675786)

#### 劝退版
请说明 ConcurrentHashMap 与 ConcurrentSkipListMap 各自的优势与不足？

在 java 6 和 8 中，ConcurrentHashMap 写的时候，是加锁的，所以内存占得比较小，而 ConcurrentSkipListMap 写的时候是不加锁的，内存占得相对比较大，通过空间换取时间上的成本，速度较快，但比前者要慢，ConcurrentHashMap 基本上是常量时间。ConcurrentSkipListMap 读和写都是log N实现，高性能相对稳定。

### 5、线程安全 QUEUE

#### 基本版
请说明 BlockingQueue 与 Queue 的区别？

BlockingQueue 继承了 Queue 的实现；put 方法中有个阻塞的操作（InterruptedException），当队列满的时候，put 会被阻塞；当队列空的时候，put方法可用。take 方法中，当数据存在时，才可以返回，否则为空。

#### 进阶版
请说明 LinkedBlockingQueue 与 ArrayBlockingQueue 的区别？

LinkedBlockingQueue 是链表结构；有两个构造器，一个是（Integer.MAX_VALUE)，无边界，另一个是(int capacity)，有边界；ArrayBlockingQueue 是数组结构；有边界。

#### 劝退版
请说明 LinkedTransferQueue 与 LinkedBlockingQueue 的区别？

LinkedTransferQueue 是java 7中提供的新接口，性能比后者更优化。

### 6、PRIORITYBLOCKINGQUEUE

#### 请评估以下程序的运行结果？

```java
public class priorityBlockingQueueQuiz{
    public static void main(String[] args) throw Exception {
        BlockingQueue<Integer> queue = new PriorityBlockingQueue<>(2);
        // 1. PriorityBlockingQueue put(Object) 方法不阻塞，不抛异常
        // 2. PriorityBlockingQueue offer(Object) 方法不限制，允许长度变长
        // 3. PriorityBlockingQueue 插入对象会做排序，默认参照元素 Comparable 实现，
        //    或者显示地传递 Comparator
        queue.put(9);
        queue.put(1);
        queue.put(8);
        System.out.println("queue.size() =" + queue.size());
        System.out.println("queue.take() =" + queue.take());
        System.out.println("queue =" + queue);
    }
}
```
运行结果：
```
queue.size() = 3
queue.take() = 1
queue = [8,9]
```
### 7、SYNCHRONOUSQUEUE

#### 请评估以下程序的运行结果？

```java
public class SynchronusQueueQuiz{
    
    public static void main(String[] args) throws Exception {
        BlockingQueue<Integer> queue = new SynchronousQueue<>();
        // 1. SynchronousQueue 是无空间，offer 永远返回 false
        // 2. SynchronousQueue take() 方法会被阻塞，必须被其他线程显示地调用 put(Object);
        System.out.pringln("queue.offer(1) = " + queue.offer(1));
        System.out.pringln("queue.offer(2) = " + queue.offer(2));
        System.out.pringln("queue.offer(3) = " + queue.offer(3));
        System.out.println("queue.take() = " + queue.take());
        System.out.println("queue.size = " + queue.size());
    }
}
```
运行结果：
```
queue.offer(1) = false
queue.offer(2) = false
queue.offer(3) = false
```
SynchronousQueue take() 方法会被阻塞

### 8、BLOCKINGQUEUE OFFER()

#### 请评估以下程序的运行结果？

```java
public class BlockingQueueQuiz{
    public static void main(String[] args) throws Exception {
        offer(new ArrayBlockingQueue<>(2));
        offer(new LinkedBlockingQueue<>(2));
        offer(new PriorityBlockingQueue<>(2));
        offer(new SynchronousQueue<>());
    }
}

private static void offer(BlockingQueue<Integer> queue) throws Exception {
    System.out.println("queue.getClass() = " +queue.getClass().getName());
    System.out.println("queue.offer(1) = " + queue.offer(1));
    System.out.println("queue.offer(2) = " + queue.offer(2));
    System.out.println("queue.offer(3) = " + queue.offer(3));
    System.out.println("queue.size() = " + queue.size());
    System.out.println("queue.take() = " + queue.take());
    }
}
```
运行结果：
```
queue.getClass() = java.util.concurrent.ArrayBlockingQueue
queue.offer(1) = true
queue.offer(2) = true
queue.offer(3) = false
queue.size() = 2
queue.take() = 1

queue.getClass() = java.util.concurrent.LinkedBlockingQueue
queue.offer(1) = true
queue.offer(2) = true
queue.offer(3) = false
queue.size() = 2
queue.take() = 1

queue.getClass() = java.util.concurrent.PriorityBlockingQueue
queue.offer(1) = true
queue.offer(2) = true
queue.offer(3) = false
queue.size() = 3
queue.take() = 1

queue.getClass() = java.util.concurrent.SynchronousQueue
queue.offer(1) = false
queue.offer(2) = false
queue.offer(3) = false
queue.size() = 0
```
queue.take() 方法会被阻塞

## Java 并发框架

### 1、锁 LOCK

#### 基本版
请说明 ReentranLock 与 ReentrantReadWriteLock 的区别？

jdk 1.5 以后，ReentranLock(重进入锁)与 ReentrantReadWriteLock 都是可重进入的锁，ReentranLock 都是互斥的，而 ReentrantReadWriteLock 是共享的，其中里面有两个类，一个是 ReadLock（共享，并行，强调数据一致性或者说可见性），另一个是 WriteLock(互斥，串行)。

#### 进阶版
请解释 ReentrantLock 为什么命名为重进入？

```java
public class ReentrantLockQuestion {

    /**
     * T1 , T2 , T3
     *
     * T1(lock) , T2(park), T3(park)
     * Waited Queue -> Head-> T2 next -> T3
     * T1(unlock) -> unpark all
     * Waited Queue -> Head-> T2 next -> T3
     * T2(free), T3(free)
     *
     * -> T2(lock) , T3(park)
     * Waited Queue -> Head-> T3
     * T2(unlock) -> unpark all
     * T3(free)
     */


    private static ReentrantLock lock = new ReentrantLock();

    public static void main(String[] args) {
        // thread[main] ->
        // lock     lock           lock
        // main -> action1() -> action2() -> action3()
        synchronizedAction(ReentrantLockQuestion::action1);
    }


    private static void action1() {
        synchronizedAction(ReentrantLockQuestion::action2);

    }

    private static void action2() {
        synchronizedAction(ReentrantLockQuestion::action3);
    }

    private static void action3() {
        System.out.println("Hello,World");
    }

    private static void synchronizedAction(Runnable runnable) {
        lock.lock();
        try {
            runnable.run();
        } finally {
            lock.unlock();
        }
    }
}
```
#### 劝退版
请说明 Lock#lock() 与 Lock#lockInterruptibly() 的区别？

```java
    /**
     * java.util.concurrent.locks.AbstractQueuedSynchronizer.acquireQueued
     * 如果当前线程已被其他线程调用了 interrupt() 方法时，这时会返回 true
     * acquireQueued 执行完时，interrupt 清空（false）
     * 再通过 selfInterrupt() 方法将状态恢复（interrupt=true）
     */
         public static void main(String[] args) {
         lockVsLockInterruptibly();
     }
     
        private static void lockVsLockInterruptibly() {

        try {
            lock.lockInterruptibly();
            action1();
        } catch (InterruptedException e) {
            // 显示地恢复中断状态
            Thread.currentThread().interrupt();
            // 当前线程并未消亡，线程池可能还在存活
        } finally {
            lock.unlock();
        }
    }
```

**lock()**  优先考虑获取锁，待获取锁成功后，才响应中断。

**lockInterruptibly() ** 优先考虑响应中断，而不是响应锁的普通获取或重入获取。

**ReentrantLock.lockInterruptibly** 允许在等待时由其它线程调用等待线程的 Thread.interrupt 方法来中断等待线程的等待而直接返回，这时不用获取锁，而会抛出一个 InterruptedException。

**ReentrantLock.lock** 方法不允许 Thread.interrupt 中断,即使检测到 Thread.isInterrupted ,一样会继续尝试获取锁，失败则继续休眠。只是在最后获取锁成功后再把当前线程置为 interrupted 状态,然后再中断线程。

### 2、条件变量 CONDITION

#### 基本版
请举例说明 Condition 使用场景？

1. CoutDownLatch (condition 变种)
2. CyclicBarrier (循环屏障)
3. 信号量/灯（Semaphore) java 9
4. 生产者和消费者
5. 阻塞队列

#### 进阶版
请使用 Condition 实现 “生产者-消费者问题”？

[使用Condition实现生产者消费者](https://blog.csdn.net/u014082714/article/details/83927697)

#### 劝退版
请解释 Condition await() 和 signal() 与 Object wait () 和 notify() 的相同与差异？

相同：阻塞和释放

差异：Java Thread 对象和实际 JVM 执行的 OS Thread 不是相同对象，JVM Thread 回调 Java Thread.run() 方法，同时 Thread 提供一些 native 方法来获取 JVM Thread 状态，当JVM thread 执行后，自动 notify()了。

```java
        while (thread.isAlive()) { // Thread 特殊的 Object
            // 当线程 Thread isAlive() == false 时，thread.wait() 操作会被自动释放
            synchronized (thread) {
                try {
                    thread.wait(); // 到底是谁通知 Thread -> thread.notify();
//                    LockSupport.park(); // 死锁发生
                } catch (Exception e) {
                    throw new RuntimeException(e);
                }
            }
```

### 3、屏障 BARRIERS

#### 基本版
请说明 CountDownLatch 与 CyclicBarrier 的区别？

**CountDownLatch** : 不可循环的，一次性操作（倒计时）。

```java
public class CountDownLatchQuestion {

    public static void main(String[] args) throws InterruptedException {

        // 倒数计数 5
        CountDownLatch latch = new CountDownLatch(5);

        ExecutorService executorService = Executors.newFixedThreadPool(5);

        for (int i = 0; i < 4; i++) {
            executorService.submit(() -> {
                action();
                latch.countDown(); // -1
            });
        }

        // 等待完成
        // 当计数 > 0，会被阻塞
        latch.await();

        System.out.println("Done");

        // 关闭线程池
        executorService.shutdown();
    }

    private static void action() {
        System.out.printf("线程[%s] 正在执行...\n", Thread.currentThread().getName());  // 2
    }

}
```

**CyclicBarrier**：可循环的， 先计数 -1，再判断当计数 > 0 时候，才阻塞。

```java
public class CyclicBarrierQuestion {

    public static void main(String[] args) throws InterruptedException {

        CyclicBarrier barrier = new CyclicBarrier(5); // 5

        ExecutorService executorService = Executors.newFixedThreadPool(5); // 3

        for (int i = 0; i < 20; i++) {
            executorService.submit(() -> {
                action();
                try {
                    // CyclicBarrier.await() = CountDownLatch.countDown() + await()
                    // 先计数 -1，再判断当计数 > 0 时候，才阻塞
                    barrier.await();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                } catch (BrokenBarrierException e) {
                    e.printStackTrace();
                }
            });
        }

        // 尽可能不要执行完成再 reset
        // 先等待 3 ms
        executorService.awaitTermination(3, TimeUnit.MILLISECONDS);
        // 再执行 CyclicBarrier reset
        // reset 方法是一个废操作
        barrier.reset();

        System.out.println("Done");

        // 关闭线程池
        executorService.shutdown();
    }

    private static void action() {
        System.out.printf("线程[%s] 正在执行...\n", Thread.currentThread().getName());  // 2
    }

}

```

#### 进阶版
请说明 Semaphore（信号量/灯） 的使用场景？

Semaphore 和Lock类似，比Lock灵活。其中有 acquire() 和 release() 两种方法，arg 都等于 1。acquire() 会抛出 InterruptedException，同时从 `sync.acquireSharedInterruptibly(arg:1)`可以看出是读模式（shared)； release()中可以计数，可以控制数量，permits可以传递N个数量。

[Java中Semaphore(信号量)的使用](https://blog.csdn.net/zbc1090549839/article/details/53389602)

#### 劝退版
请通过 Java 1.4 的语法实现一个 CountDownLatch?

```java
public class LegacyCountDownLatchDemo {

    public static void main(String[] args) throws InterruptedException {

        // 倒数计数 5
        MyCountDownLatch latch = new MyCountDownLatch(5);

        ExecutorService executorService = Executors.newFixedThreadPool(5);

        for (int i = 0; i < 5; i++) {
            executorService.submit(() -> {
                action();
                latch.countDown(); // -1
            });
        }

        // 等待完成
        // 当计数 > 0，会被阻塞
        latch.await();

        System.out.println("Done");

        // 关闭线程池
        executorService.shutdown();
    }

    private static void action() {
        System.out.printf("线程[%s] 正在执行...\n", Thread.currentThread().getName());  // 2
    }

    /**
     * Java 1.5+ Lock 实现
     */
    private static class MyCountDownLatch {

        private int count;

        private final Lock lock = new ReentrantLock();

        private final Condition condition = lock.newCondition();

        private MyCountDownLatch(int count) {
            this.count = count;
        }

        public void await() throws InterruptedException {
            // 当 count > 0 等待
            if (Thread.interrupted()) {
                throw new InterruptedException();
            }

            lock.lock();
            try {
                while (count > 0) {
                    condition.await(); // 阻塞当前线程
                }
            } finally {
                lock.unlock();
            }
        }

        public void countDown() {

            lock.lock();
            try {
                if (count < 1) {
                    return;
                }
                count--;
                if (count < 1) { // 当数量减少至0时，唤起被阻塞的线程
                    condition.signalAll();
                }
            } finally {
                lock.unlock();
            }
        }
    }

    /**
     * Java < 1.5 实现
     */
    private static class LegacyCountDownLatch {

        private int count;

        private LegacyCountDownLatch(int count) {
            this.count = count;
        }

        public void await() throws InterruptedException {
            // 当 count > 0 等待
            if (Thread.interrupted()) {
                throw new InterruptedException();
            }

            synchronized (this) {
                while (count > 0) {
                    wait(); // 阻塞当前线程
                }
            }
        }

        public void countDown() {
            synchronized (this) {
                if (count < 1) {
                    return;
                }
                count--;
                if (count < 1) { // 当数量减少至0时，唤起被阻塞的线程
                    notifyAll();
                }
            }
        }
    }
}

```

### 4、线程池 THREAD POOL

#### 基本版
请问 J.U.C 中内建了几种 ExceptionService 实现？

1.5：ThreadPoolExecutor、ScheduledThreadPoolExecutor

1.7：ForkJoinPool
```java
public class ExecutorServiceQuestion {

    public static void main(String[] args) {
        /**
         * 1.5
         *  ThreadPoolExecutor
         *  ScheduledThreadPoolExecutor :: ThreadPoolExecutor
         * 1.7
         *  ForkJoinPool
         */
        ExecutorService executorService = Executors.newFixedThreadPool(2);

        executorService = Executors.newScheduledThreadPool(2);

        // executorService 不再被引用，它会被 GC -> finalize() -> shutdown()
        ExecutorService executorService2 = Executors.newSingleThreadExecutor();
    }
}
```

#### 进阶版
请分别解释 ThreadPoolExecutor 构造器参数在运行时的作用？

```java
/**
 * Creates a new {@code ThreadPoolExecutor} with the given initial
 * parameters.
 *
 * @param corePoolSize the number of threads to keep in the pool, even
 *        if they are idle, unless {@code allowCoreThreadTimeOut} is set
 * @param maximumPoolSize the maximum number of threads to allow in the
 *        pool
 * @param keepAliveTime when the number of threads is greater than
 *        the core, this is the maximum time that excess idle threads
 *        will wait for new tasks before terminating.
 * @param unit the time unit for the {@code keepAliveTime} argument
 * @param workQueue the queue to use for holding tasks before they are
 *        executed.  This queue will hold only the {@code Runnable}
 *        tasks submitted by the {@code execute} method.
 * @param threadFactory the factory to use when the executor
 *        creates a new thread
 * @param handler the handler to use when execution is blocked
 *        because the thread bounds and queue capacities are reached
 * @throws IllegalArgumentException if one of the following holds:<br>
 *         {@code corePoolSize < 0}<br>
 *         {@code keepAliveTime < 0}<br>
 *         {@code maximumPoolSize <= 0}<br>
 *         {@code maximumPoolSize < corePoolSize}
 * @throws NullPointerException if {@code workQueue}
 *         or {@code threadFactory} or {@code handler} is null
 */
public ThreadPoolExecutor(int corePoolSize,
                          int maximumPoolSize,
                          long keepAliveTime,
                          TimeUnit unit,
                          BlockingQueue<Runnable> workQueue,
                          ThreadFactory threadFactory,
                          RejectedExecutionHandler handler);
```

**corePoolSize**: 核心线程池大小。这个参数是否生效取决于allowCoreThreadTimeOut变量的值，该变量默认是false，即对于核心线程没有超时限制，所以这种情况下，corePoolSize参数是起效的。如果allowCoreThreadTimeOut为true，那么核心线程允许超时，并且超时时间就是keepAliveTime参数和unit共同决定的值，这种情况下，如果线程池长时间空闲的话最终存活的线程会变为0，也即corePoolSize参数失效。

**maximumPoolSize**: 线程池中最大的存活线程数。这个参数比较好理解，对于超出corePoolSize部分的线程，无论allowCoreThreadTimeOut变量的值是true还是false，都会超时，超时时间由keepAliveTime和unit两个参数算出。

**keepAliveTime**: 超时时间。

**unit**: 超时时间的单位，秒，毫秒，微秒，纳秒等，与keepAliveTime参数共同决定超时时间。

**workQueue**: 线程等待队列。当调用execute方法时，如果线程池中没有空闲的可用线程，那么就会把这个Runnable对象放到该队列中。这个参数必须是一个实现BlockingQueue接口的阻塞队列，因为要保证线程安全。有一个要注意的点是，只有在调用execute方法是，才会向这个队列中添加任务，那么对于submit方法呢，难道submit方法提交任务时如果没有可用的线程就直接扔掉吗？当然不是，看一下AbstractExecutorService类中submit方法实现，其实submit方法只是把传进来的Runnable对象或Callable对象包装成一个新的Runnable对象，然后调用execute方法，并将包装后的FutureTask对象作为一个Future引用返回给调用者。Future的阻塞特性实际是在FutureTask中实现的，具体怎么实现感兴趣的话可以看一下FutureTask的源码。

**threadFactory**: 线程创建工厂。用于在需要的时候生成新的线程。默认实现是Executors.defaultThreadFactory()，即new 一个Thread对象，并设置线程名称，daemon等属性。

**handler**: 拒绝策略。这个参数的作用是当提交任务时既没有空闲线程，任务队列也满了，这时候就会调用handler的rejectedExecution方法。默认的实现是抛出一个RejectedExecutionException异常。

#### 劝退版
如何获取 ThreadPoolExecutor 正在运行的线程？

```java
public class ThreadPoolExecutorThreadQuestion {

    public static void main(String[] args) throws InterruptedException {

        // main 线程启动子线程，子线程的创造来自于 Executors.defaultThreadFactory()

        ExecutorService executorService = Executors.newCachedThreadPool();
        // 之前了解 ThreadPoolExecutor beforeExecute 和 afterExecute 能够获取当前线程数量

        Set<Thread> threadsContainer = new HashSet<>();

        setThreadFactory(executorService, threadsContainer);
        for (int i = 0; i < 9; i++) { // 开启 9 个线程
            executorService.submit(() -> {
            });
        }

        // 线程池等待执行 3 ms
        executorService.awaitTermination(3, TimeUnit.MILLISECONDS);

        threadsContainer.stream()
                .filter(Thread::isAlive)
                .forEach(thread -> {
                    System.out.println("线程池创造的线程 : " + thread);
                });

        Thread mainThread = Thread.currentThread();

        ThreadGroup mainThreadGroup = mainThread.getThreadGroup();

        int count = mainThreadGroup.activeCount();
        Thread[] threads = new Thread[count];
        mainThreadGroup.enumerate(threads, true);

        Stream.of(threads)
                .filter(Thread::isAlive)
                .forEach(thread -> {
                    System.out.println("线程 : " + thread);
                });

        // 关闭线程池
        executorService.shutdown();

    }

    private static void setThreadFactory(ExecutorService executorService, Set<Thread> threadsContainer) {

        if (executorService instanceof ThreadPoolExecutor) {
            ThreadPoolExecutor threadPoolExecutor = (ThreadPoolExecutor) executorService;
            ThreadFactory oldThreadFactory = threadPoolExecutor.getThreadFactory();
            threadPoolExecutor.setThreadFactory(new DelegatingThreadFactory(oldThreadFactory, threadsContainer));
        }
    }

    private static class DelegatingThreadFactory implements ThreadFactory {

        private final ThreadFactory delegate;

        private final Set<Thread> threadsContainer;

        private DelegatingThreadFactory(ThreadFactory delegate, Set<Thread> threadsContainer) {
            this.delegate = delegate;
            this.threadsContainer = threadsContainer;
        }

        @Override
        public Thread newThread(Runnable r) {
            Thread thread = delegate.newThread(r);
            // cache thread
            threadsContainer.add(thread);
            return thread;
        }
    }
}
```

### 5、FUTURE

#### 基本版
如何获取 Future 对象？

submit()

#### 进阶版
请举例 Future get() 以及 get(Long,TimeUnit) 方法的使用场景？

**超时等待**

**InterruptedException**

**ExcutionException**

**TimeOutException**

#### 劝退版
如何利用 Future 优雅地取消一个任务的执行？

```java
public class CancellableFutureQuestion {

    public static void main(String[] args) {

        ExecutorService executorService = Executors.newSingleThreadExecutor();

        Future future = executorService.submit(() -> { // 3秒内执行完成，才算正常
            action(5);
        });

        try {
            future.get(3, TimeUnit.SECONDS);
        } catch (InterruptedException e) {
            // Thread 恢复中断状态
            Thread.currentThread().interrupt();
        } catch (ExecutionException e) {
            throw new RuntimeException(e);
        } catch (TimeoutException e) {
            // 执行超时，适当地关闭
            Thread.currentThread().interrupt(); // 设置中断状态
            future.cancel(true); // 尝试取消
        }

        executorService.shutdown();
    }

    private static void action(int seconds) {
        try {
            Thread.sleep(TimeUnit.SECONDS.toMillis(seconds)); // 5 - 3
            // seconds - timeout = 剩余执行时间
            if (Thread.interrupted()) { // 判断并且清除中断状态
                return;
            }
            action();
        } catch (InterruptedException e) {
        }
    }

    private static void action() {
        System.out.printf("线程[%s] 正在执行...\n", Thread.currentThread().getName());  // 2
    }
}
```

### 6、VOLATILE 变量

#### 基本版
在 Java 中，volatile 保证的是可见性还是原子性？

**volatile** 既有可见性又有原子性（非我及彼），可见性是一定的，原子性是看情况的。对象类型和原生类型都是可见性，原生类型是原子性。

#### 进阶版
在 Java 中，volatile long 和 double 是线程安全的吗？

volatile long 和 double 是线程安全的。

#### 劝退版
在 Java 中，volatile 底层实现是基于什么机制？

**内存屏障**（变量 Lock）机制：一个变量的原子性的保证。

### 7、原子操作 ATOMIC

#### 基本版
为什么 AtomicBoolean 内部变量使用 int 实现，而非 boolean?

操作系统有 X86 和 X64，在虚拟机中，基于boolean 实现就是用 int 实现的，用哪一种实现都可以。虚拟机只有32位和64位的，所以用32位的实现。

#### 进阶版
在变量原子操作时，Atomic* CAS 操作比 synchronized 关键字哪个更重？

[Synchronization](https://wiki.openjdk.java.net/display/HotSpot/Synchronization)

同线程的时候，synchronized 刚快；而多线程的时候则要分情况讨论。

```java
public class AtomicQuestion {

    private static int actualValue = 3;

    public static void main(String[] args) {
        AtomicInteger atomicInteger = new AtomicInteger(3);
        // if( value == 3 )
        //     value = 5
        atomicInteger.compareAndSet(3, 5);
        // 偏向锁 < CAS 操作 < 重锁（完全互斥）
        // CAS 操作也是相对重的操作，它也是实现 synchronized 瘦锁(thin lock)的关键
        // 偏向锁就是避免 CAS（Compare And Set/Swap)操作
    }

    private synchronized static void compareAndSet(int expectedValue, int newValue) {
        if (actualValue == expectedValue) {
            actualValue = newValue;
        }
    }
}
```

#### 劝退版
Atomic* CAS 的底层是如何实现？

汇编指令：`cpmxchg` (Compare and Exchange)
