JUC 备忘清单
===

这是 JUC 的快速参考备忘单

问答
----
<!--rehype:body-class=cols-3-->

### synchronized 的实现原理
<!--rehype:wrap-class=row-span-2-->
- synchronized 作用于「方法」或者「代码块」，保证被修饰的代码在同一时间只
能被一个线程访问。
- synchronized 修饰代码块时，JVM 采用「monitorenter、monitorexit」两个
指令来实现同步
- synchronized 修饰同步方法时，JVM 采用「ACC_SYNCHRONIZED」标记符来
实现同步
- monitorenter、monitorexit 或者 ACC_SYNCHRONIZED 都是「基于 Monitor
实现」的
- 实例对象里有对象头，对象头里面有 Mark Word，Mark Word 指针指向了
「monitor」
- Monitor 其实是一种「同步工具」，也可以说是一种「同步机制」。
- 在 Java 虚拟机（HotSpot）中，Monitor 是由「ObjectMonitor 实现」的。
ObjectMonitor 体现出 Monitor 的工作原理~

### synchronized锁膨胀

- 无锁态->偏向锁->轻量级锁->重量级锁的顺序膨胀

### volatile

- 为实现该语义，是在代码编译时期，会在指令序列添加对应内存屏障来禁止指令重排序，从而让线程访问对应变量时强制从主存中读取，写入时强制刷新回主存
- 作用：1.保证变量内存可见性 2.禁止指令重排序

### 线程池的种类
<!--rehype:wrap-class=col-span-2-->
:-|-
:-|-
`FixedThreadPool` |最小线程数等于最大线程数用户定义，存活时间为0，使用LinkedBlockingQueue队列
`SingleThreadExecutor` |最下最大线程数为1，存活时间为0，使用LinkedBlockingQueue队列
`CachedThreadPool` |最小线程数为0，最大线程数2^31-1,存活时间60秒，SynchronousQueue作为阻塞队列
`ScheduledThreadPool` |用户传入线程数，最大线程数为2^31-1,，存活时间为0，DelayedWorkQueue最为阻塞队列
`WorkStealingPool` |使用fork/join框架，采用双端队列，fork/join线程工厂

### 线程池原理

- 如果正在运行的线程数量小于 corePoolSize，那么马上创建线程运行这个任务；
- 如果正在运行的线程数量大于或等于 corePoolSize，那么将这个任务放入队列；
- 如果这时候队列满了，而且正在运行的线程数量小于 maximumPoolSize，那么还是要创建非核心线程立刻运行这个任务；
- 如果队列满了，而且正在运行的线程数量大于或等于 maximumPoolSize，那么线程池会抛出异常RejectExecutionException。
- 所有线程池的所有任务完成后，它最终会收缩到 corePoolSize 的大小

### 如何检查死锁

- 死锁：A线程持有1对象的锁，想获取2线程的锁，B线程则相反，因此两个线程都
- 可以使用jdk自带的命令jps，jstack或工具Jconsole
  - 1.jps打印所有进程，找到死锁的进程，
  - 2.使用jstack +进程id，打印堆栈信息
- 预防：
  - 资源一次性分配，确定每个资源交给哪个线程
  - 如果必须获取多个锁，我们就要考虑不同线程获取锁的顺序，

### CountDownLatch和CyclicBarrier

类型|CountDownLatch | CyclicBarrier
:-|-|-
计数方式|递减计数|加法计数
重复性 | 不可重复使用 |可重复使用
初始值 | N，N>0 |0
阻塞条件 | N>0,await一致阻塞 |N小于指定值
释放线程 | N=0 |达到指定N
<!--rehype:className=show-header-->

### Fork/Join框架的理解
<!--rehype:wrap-class=row-span-2-->
- fork/join框架每个线程会维护一个队列，fork是把大的任务划分成小的任务，join是把小的任务结果汇集
- fork方法：
  线程自己的任务在队首，采用后进先出的顺序，
  线程执行任务的同时，会窃取一个任务，该任务放在队列尾部，采用先进先出的顺序
- join方法：

1. 检查调用 join() 的线程是否是 ForkJoinThread 线程。如果不是（例如 main 线程），则阻塞当前线程，等待任务完成。如果是，则不阻塞。
2. 查看任务的完成状态，如果已经完成，直接返回结果。
3. 如果任务尚未完成，但处于自己的工作队列内，则完成它。
4. 如果任务已经被其他的工作线程偷走，则窃取这个小偷的工作队列内的任务（以 FIFO 方式），执行，以期帮助它早日完成欲 join 的任务。
5. 如果偷走任务的小偷也已经把自己的任务全部做完，正在等待需要 join 的任务时，则找到小偷的小偷，帮助它完成它的任务。
6. 递归地执行第5步。
