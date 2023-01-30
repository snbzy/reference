JVM 备忘清单
===

这是 JVM 的快速参考备忘单。 你可以在这里找到最常见的 JVM 命令。

问答
----
<!--rehype:body-class=cols-3-->

### JVM内存结构
<!--rehype:wrap-class=col-span-2-->
<img src="https://s2.loli.net/2023/01/29/4dHSmFVUnA1cMQk.png" width = 100%  alt="内存结构"/>

### JVM内存模型
<img src="https://s2.loli.net/2023/01/29/INzhfAp4Sx7Cwi9.png" width = 100%  alt="内存模型"/>

### JVM内存参数调整
<!--rehype:wrap-class=col-span-2 row-span-2-->

:-|:-|:-
:-|:-|:-
参数 | 说明| 示例
`-Xmx` |	设置最大堆大小|	-Xmx3550m，设置JVM最大可用内存为3550 MB
`-Xms` |	设置JVM初始内存|	-Xms3550m，设置JVM初始内存为3550 MB。此值建议与-Xmx相同，避免每次垃圾回收完成后JVM重新分配内存。
`-Xmn` |	设置年轻代大小|	-Xmn2g，设置年轻代大小为2 GB。整个JVM内存大小=年轻代大小+年老代大小+持久代大小。持久代一般固定大小为64 MB，所以增大年轻代后，将会减小年老代大小。此值对系统性能影响较大，Sun官方推荐配置为整个堆的3/8。
`-Xss` |	设置线程的栈大小|	-Xss128k，设置每个线程的栈大小为128 KB。
`-XX:NewRatio=n` |	设置年轻代和年老代的比值|	-XX:NewRatio=4，设置年轻代（包括Eden和两个Survivor区）与年老代的比值（除去持久代）。如果设置为4，那么年轻代与年老代所占比值为1:4，年轻代占整个堆栈的1/5。
`-XX:SurvivorRatio=n`	| 年轻代中Eden区与两个Survivor区的比值|	-XX:SurvivorRatio=4，设置年轻代中Eden区与Survivor区的大小比值。如果设置为4，那么两个Survivor区与一个Eden区的比值为2:4，一个Survivor区占整个年轻代的1/6。
`-XX:MaxPermSize=n`	| 设置持久代大小|	-XX:MaxPermSize=16m，设置持久代大小为16 MB。
`-XX:MaxTenuringThreshold=n`	| 设置垃圾最大年龄|	-XX:MaxTenuringThreshold=0，设置垃圾最大年龄。
`-XX:+UseParallelGC`	|选择垃圾收集器为并行收集器。|	-Xmx3800m -Xms3800m -Xmn2g -Xss128k -XX:+UseParallelGC -XX:ParallelGCThreads=20，-XX:+UseParallelGC此配置仅对年轻代有效，即在示例配置下，年轻代使用并发收集，而年老代仍旧使用串行收集。
<!--rehype:className=code-nowrap--> 
> 参考资料：https://help.aliyun.com/document_detail/148851.html

### 内存溢出与内存泄露
- 内存溢出：所需内存比可用内存大的时候，出现内存溢出
- 内存泄漏：申请的内存没有被回收

### JVM 年轻代到年老代的晋升过程

- 部分对象会在From和To区域中复制来复制去,如此交换15次(由JVM参数MaxTenuringThreshold决定,这个参数默认是15),最终如果还是存活,就存入到老年代。
- 如果对象的大小大于Eden的二分之一会直接分配在old，如果old也分配不下，会做一次majorGC，如果小于eden的一半但是没有足够的空间，就进行minorgc也就是新生代GC。
- minor gc后，survivor仍然放不下，则放到老年代
- 动态年龄判断 ，大于等于某个年龄的对象超过了survivor空间一半 ，大于等于某个年龄的对象直接进入老年代



### JVM中一次完整的GC流程
<!--rehype:wrap-class=col-span-2-->
<img src="https://img-blog.csdnimg.cn/5762658fa08a483d8848f02f861cc77e.png" width = 100%  alt="创建对象完整流程"/>

### 双亲委托机制
#### 双亲委托机制
如果一个类加载器收到类加载的请求，它首先不会自己去尝试加载这个类，而 是把这个请求委派给父类加载器完成。
每个类加载器都是如此，只有当父加载器在自己的搜索范围内找不到指定的类时（即ClassNotFoundException），子加载器才会尝试自己去加载。
#### 为什么
防止内存中出现多份同样的字节码
#### 如何打破机制
打破双亲委派机制则不仅要继承 ClassLoader 类，还要重写 loadClass 和 findClass 方法

### 类的加载顺序
加载、验证、准备、解析、初始化

### 类的实例化顺序
- 父类静态成员和静态代码块
- 子类静态成员和静态代码块
- 父类非静态成员和非静态代码块
- 父类构造方法
- 子类非静态成员和非静态代码块
- 子类构造方法
<!--rehype:className=style-timeline-->
### 新生代回收算法
eden:from:to=8:1:1,当新的对象放eden内存不够时发生MinorGC，MinorGC发生时，To区一定是空的，所以MinorGC的主要区域是eden和from区，
eden区中的对象都会被复制到to区，而from区中的对象会根据对象年龄判断取向，年龄判别是根据参与GC的次数，默认达到15就被移到老年代，否则移到to区，
复制完成后，eden和from区会被清理，然后交换from区和to区，完成后to区再次变为空的。如果复制到to区过程，内存不够用，则需要内存担保，移动到老年代。

### 何时触发FullGC？
- 调用 System.gc 时，系统建议执 Full GC，但是不必然执行。
- 老年代空间不足。
- 方法区空间不足。
- 通过 Minor GC 后进入老年代的平均大小大于老年代的可用内存。
- 由 Eden 区、From 区向 To 区复制时，对象大小大于 To Space 可用内存，则把该对象转存到老年代，且老年代的可用内存小于该对象大小


### 垃圾收集器
<img src="https://img-blog.csdnimg.cn/f3dd0092ff0c4d7d832d818553dc7a50.png" width = 100%  alt="垃圾收集器"/>

:-|:-
:-|:-
名称|说明
serial |
parNew|
Parallel Scavenge|
Serial Old|
Parallel Old|
CMS|
G1|


### OOM的七种原因及解决
<!--rehype:wrap-class=col-span-2 row-span-2-->
`1.堆内存不足：java.lang.OutOfMemoryError: Java heap space`

- 原因：1. 代码中可能存在大对象分配 2. 可能存在内存泄露，导致在多次GC之后，还是无法找到一块足够大的内存容纳当前对象。

- 解决：1. 检查是否存在大对象的分配，最有可能的是大数组分配 2. 通过jmap命令，把堆内存dump下来，使用mat工具分析一下，检查是否存在内存泄露的问题 
3.如果没有找到明显的内存泄露，使用 -Xmx 加大堆内存 4.还有一点容易被忽略，检查是否有大量的自定义的 Finalizable 对象，也有可能是框架内部提供的，考虑其存在的必要性

`2.元空间不足：java.lang.OutOfMemoryError: Metaspace`

- 原因： 1.在Java7之前，频繁的错误使用String.intern方法生成了大量的代理类，导致方法区被撑爆，无法卸载 2. 应用长时间运行，没有重启

- 解决：1. 检查是否永久代空间或者元空间设置的过小 2. 检查代码中是否存在大量的反射操作 3. dump之后通过mat检查是否存在大量由于反射生成的代理类4. 放大招，重启JVM

`3.GC overhead limit exceeded：java.lang.OutOfMemoryError：GC overhead limit exceeded`

`4.方法栈溢出：java.lang.OutOfMemoryError : unable to create new native Thread`
  - 原因：出现这种异常，基本上都是创建的了大量的线程导致的，以前碰到过一次，通过jstack出来一共8000多个线程。 

`5.swap区溢出：java.lang.OutOfMemoryError: Out of swap space`

`6.分配超大数组：java.lang.OutOfMemoryError: Requested array size exceeds VM limit `

`7.本地方法溢出：java.lang.OutOfMemoryError: stack_trace_with_native_method`




### 各种回收算法
#### 标记清除：
分为两个阶段：第一阶段从引用根节点开始标记所有被引用的对象，第二阶段遍历整个堆，清除未被标记的对象。该算法的缺点是需要暂停整个应用，并且在回收以后未使用的空间是不连续，即内存碎片，会影响到存储。
#### 复制算法：
复制算法将可用内存按容量划分为相等的两部分，然后每次只使用其中的一块，当一块内存用完时，就将还存活的对象复制到第二块内存上，然后一次性清楚完第一块内存，再将第二块上的对象复制到第一块。但是这种方式，内存的代价太高，每次基本上都要浪费一半的内存。
#### 标记整理：
此算法结合了标记-清楚算法和复制算法的优点，也分为两个阶段，第一阶段从引用根节点开始标记所有被引用的对象，第二阶段遍历整个堆，在回收不存活的对象占用的空间后，会将所有的存活对象往左端空闲空间移动，并更新对应的指针。标记-整理算法是在标记-清除算法的基础上，又进行了对象的移动，因此成本更高，但是却解决了内存碎片的问题，按顺序排放，同时解决了复制算法所需内存空间过大的问题。


### 如何判断对象可以被回收
- 引用计数器法
- 可达性分析算法
