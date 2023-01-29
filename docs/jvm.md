JVM 备忘清单
===

这是 JVM 的快速参考备忘单。 你可以在这里找到最常见的 JVM 命令。

问答
----
<!--rehype:body-class=cols-3-->

### JVM内存结构
<!--rehype:wrap-class=col-span-2-->
![eee](https://img-blog.csdnimg.cn/fa88ead4fed448c8b1d30be1017580c2.png)

### OOM的七种原因及解决
<!--rehype:wrap-class=row-span-4-->
- 1.堆内存不足：java.lang.OutOfMemoryError: Java heap space

原因：

  1. 代码中可能存在大对象分配
  2. 可能存在内存泄露，导致在多次GC之后，还是无法找到一块足够大的内存容纳当前对象。

解决：

  1. 检查是否存在大对象的分配，最有可能的是大数组分配
  2. 通过jmap命令，把堆内存dump下来，使用mat工具分析一下，检查是否存在内存泄露的问题
  3. 如果没有找到明显的内存泄露，使用 -Xmx 加大堆内存
  4. 还有一点容易被忽略，检查是否有大量的自定义的 Finalizable 对象，也有可能是框架内部提供的，考虑其存在的必要性

- 2.元空间不足：java.lang.OutOfMemoryError: Metaspace

原因：

1. 在Java7之前，频繁的错误使用String.intern方法生成了大量的代理类，导致方法区被撑爆，无法卸载
2. 应用长时间运行，没有重启

解决：

1. 检查是否永久代空间或者元空间设置的过小
2. 检查代码中是否存在大量的反射操作
3. dump之后通过mat检查是否存在大量由于反射生成的代理类
4. 放大招，重启JVM

- 3.GC overhead limit exceeded：java.lang.OutOfMemoryError：GC overhead limit exceeded
- 4.方法栈溢出：java.lang.OutOfMemoryError : unable to create new native Thread
原因：出现这种异常，基本上都是创建的了大量的线程导致的，以前碰到过一次，通过jstack出来一共8000多个线程。
- 5.swap区溢出：java.lang.OutOfMemoryError: Out of swap space
- 6.分配超大数组：java.lang.OutOfMemoryError: Requested array size exceeds VM limit
- 7.本地方法溢出：java.lang.OutOfMemoryError: stack_trace_with_native_method

### JVM 年轻代到年老代的晋升过程
<!--rehype:wrap-class=col-span-2-->
- 部分对象会在From和To区域中复制来复制去,如此交换15次(由JVM参数MaxTenuringThreshold决定,这个参数默认是15),最终如果还是存活,就存入到老年代。
- 如果对象的大小大于Eden的二分之一会直接分配在old，如果old也分配不下，会做一次majorGC，如果小于eden的一半但是没有足够的空间，就进行minorgc也就是新生代GC。
- minor gc后，survivor仍然放不下，则放到老年代
- 动态年龄判断 ，大于等于某个年龄的对象超过了survivor空间一半 ，大于等于某个年龄的对象直接进入老年代

### JVM中创建对象完整流程
<!--rehype:wrap-class=col-span-2-->
![在这里插入图片描述](https://img-blog.csdnimg.cn/5762658fa08a483d8848f02f861cc77e.png)

### 垃圾收集器

![在这里插入图片描述](https://img-blog.csdnimg.cn/f3dd0092ff0c4d7d832d818553dc7a50.png)
