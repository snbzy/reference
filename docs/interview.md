Interview 备忘清单
===

这是一份Java常见面试题集合

Question
----
<!--rehype:body-class=cols-3-->

### 容器

1. List 和 Set 的区别？
2. ArrayList什么时候扩容？
3. 为什么Arrays生成的List不能增删
4. 如何在循环中删除元素而不触发并发修改异常？
5. HashSet 是如何保证不重复的
6. 使用过哪些map各有什么特点
7. HashMap put及扩容过程
8. HashMap扩容过程？
9. HashMap 是线程安全的吗，为什么不是线程安全的
10. HashMap 1.7 与 1.8 的 区别，说明 1.8 做了哪些优化，如何优化的？
11. HashMap 的长度为什么是2的幂次方?
12. HashMap树和链表转化的阈值
13. ConcurrentHashMap
14. LinkedHashMap的应用
15. 数组在内存中如何分配
16. 异常分类以及处理机制
17. cloneable接口实现原理
18. [设计模式详解](java.html#设计模式)
19. JDK 动态代理与 cglib 实现的区别

### JVM

1. 详细说明jvm内存模型
2. JVM内存结构
3. 各分区大小调节指令？
4. 讲讲什么情况下会出现内存溢出，内存泄漏？
5. JVM 年轻代到年老代的晋升过程的判断条件是什么呢？
6. JVM 出现 fullGC 很频繁，怎么去线上排查问题？
7. 类加载为什么采用双亲委派模式，什么场景打破了这个模式？
8. 类的加载顺序？
9. 类的实例化顺序
10. JVM垃圾回收机制，何时触发MinorGC等操作
11. hotspot虚拟机新生代回收算法（复制算法）
12. 老年代回收算法？
13. 何时触发FullGC？
14. JVM 中一次完整的 GC 流程（从 ygc 到 fgc）是怎样的
15. 各种回收器，各自优缺点，重点CMS. G1? serial new serial old,parollow
16. 判断对象是否可以回收？
17. 各种回收算法
18. OOM的七种原因及解决？

### JUC

1. synchronized 的实现原理以及锁优化？
2. volatile 的实现原理？
3. Java 的信号灯？
4. synchronized 在静态方法和普通方法的区别？
5. synchronized修饰代码块和普通方法的区别？
6. 怎么实现所有线程在等待某个事件的发生才会去执行？
7. CAS？CAS 有什么缺陷，如何解决？
8. synchronized 和 lock 有什么区别？
9. Hashtable 是怎么加锁的 ？
10. AQS
11. [如何检测死锁？怎么预防死锁？](juc.html#如何检查死锁)
12. 如何保证多线程下 i++ 结果正确？
13. 线程池的种类，区别和使用场景？
14. 分析线程池的实现原理和线程的调度过程？
15. 线程池如何调优，最大数目如何确认？
16. ExecutorService中execute和submit方法的区别？
17. ThreadLocal原理，用的时候需要注意什么？
18. [CountDownLatch 和 CyclicBarrier 的用法，以及区别?](juc.html#countdownlatch和cyclicbarrier)
19. LockSupport工具
20. Condition接口及其实现原理
21. [Fork/Join框架的理解](juc.html#forkjoin框架的理解)
22. 分段锁的原理,锁力度减小的思考
23. 八种阻塞队列以及各个阻塞队列的特性

### Spring

1. BeanFactory 和 FactoryBean？
2. BeanFactory 和 ApplicationContext？
3. Spring IOC 的理解，其初始化过程？
4. Spring Bean 的生命周期，如何被管理的？
5. Spring 的不同事务传播行为有哪些
6. spring 声明式事务原理，哪些场景会失效？
7. Spring MVC 的工作原理？
8. Spring 管理Bean的步骤？
9. Spring AOP的理解？
10. Springboot 自动配置原理
11. springboot启动流程

### Redis

1. Redis 为什么这么快？
2. Redis用过哪些数据数据，以及Redis底层怎么实现
3. 什么是缓存击穿、缓存穿透、缓存雪崩？
4. 什么是热 Key 问题，如何解决热 key 问题？
5. 如何使用Redis来实现分布式锁
6. Redis的并发竞争问题如何解决
7. Redis持久化的几种方式，优缺点是什么，怎么实现的
8. Redis的缓存过期策略和内存淘汰机制
9. 怎么实现 Redis 的高可用？(Redis 主从、哨兵、集群）
10. Redis6.0为何采用多线程？
11. MySQL 与 Redis 如何保证双写一致性？
12. 聊聊 Redis 事务机制

### 数据库

1. mysql分页有什么优化？
2. [mysql数据类型？](mysql.html#mysql-数据类型)
3. [Blob 和 text 有什么区别？](#blob和text有什么区别)
4. [索引分类？](#索引分类)
5. [索引哪些情况会失效?](#索引失效)
6. [什么情况下适合使用索引](#什么情况下适合使用索引)
7. [什么是组合索引以及最左前缀原则？](#组合索引与最左前缀)
8. [mysql 的表锁，页锁，行锁](#mysql几种锁)
9. [事务的特性和隔离级别](#事务的特性)
10. [mysql有哪几种日志](#mysql日志类型)
11. [事务是如何通过日志来控制的？](#事务是如何通过日志来实现的)
12. [数据库存储引擎介绍](#InnoDB与MyISAM对比)
13. [你是怎么优化 SQL 的?(步骤和方法)](#优化sql方法)
14. [如何选择合适的分布式主键方案？](#分布式主键生成方案)
15. [在高并发情况下，如何做到安全的修改同一行数据？](#如何安全的修改一行数据)
16. [select for update 有什么含义？](#select-for-update-有什么含义)
17. [一条 SQL 语句在 MySQL 中如何执行的？](#一条sql语句在-mysql中如何执行的)
18. [InnoDB完成一次更新操作日志层面的步骤](#InnoDB完成一次更新操作日志层面的步骤)
19. [mysql 中 int(20)和 char(20)以及 varchar(20)的 区别？](#int20与char20varchar20)
20. [drop、delete 与 truncate 的区别](#deletetruncate与-drop-的区别)
21. [MySQL 的复制原理以及流程](#主从复制原理)
22. MySQL系统逻辑架构图

### Mybatis

1. Mybatis原理
2. mybatis分页是怎么做的？
3. mybatis 属性名和表字段名不同该怎么处理？
4. mybatis四大接口？

### 分布式相关

1. 接口的幂等性的概念
2. 普通Hash和一致性Hash？
3. 分布式锁实现原理及方式？

### 消息中间件

1. RabbitMQ重启消息为什么会丢失？
2. RabbitMQ交换机类型和区别？
3. 消息队列如何解决消息丢失问题？
4. 消息队列有可能发生重复消费，如何避免，如何做到幂等？
5. 如何处理消息队列的消息积压问题？

MySQL
----
<!--rehype:body-class=cols-3-->

### 索引分类

- 主键索引(PRIMARY KEY)
- 唯一索引(UNIQUE)
- 全文索引(FULLTEXT)
- 空间索引(SPATIAL)
- 组合索引

### 什么情况下适合使用索引

- 表的某个字段值离散度越高，越适合选做索引字段
- 占用存储空间少的字段更适合选做索引
- 存储空间固定的字段更适合选做索引
- where语句中经常使用的字段

### 索引失效
<!--rehype:wrap-class=row-span-2-->
- 查询条件包含 or，可能导致索引失效
- 如何字段类型是字符串，where 时一定用引号括起来，否则索引失效
- like 通配符可能导致索引失效。
- 联合索引，查询时的条件列不是联合索引中的第一个列，索引失效。
- 在索引列上使用 mysql 的内置函数，索引失效。
- 对索引列运算（如，+、-、*、/），索引失效。
- 索引字段上使用（！= 或者 < >，not in）时，可能会导致索引失效。
- 索引字段上使用 is null， is not null，可能导致索引失效。
- 左连接查询或者右连接查询查询关联的字段编码格式不一样，可能导致索引失效。
- mysql 估计使用全表扫描要比使用索引快,则不使用索引。

### 组合索引与最左前缀

- `联合索引`，用户可以在多个列上建立索引,这种索引叫做联合索引。
因为 InnoDB 引擎中的索引策略的最左原则，所以需要注意联合索引中的顺序
- `最左前缀原则`，就是最左优先，在创建多列索引时，要根据业务需求，where
子句中使用最频繁的一列放在最左边。
- 当我们创建一个组合索引的时候，如(k1,k2,k3)，相当于创建了（k1）、
(k1,k2)和(k1,k2,k3)三个索引，这就是最左匹配原则

### Blob和text有什么区别？

- Blob主要存储二进制数据，text存储大字符串
- Blob 值被视为二进制字符串（字节字符串）,它们没有字符集，并且排序和比较基
  于列值中的字节的数值。
- text 值被视为非二进制字符串（字符字符串）。它们有一个字符集，并根据字符
  集的排序规则对值进行排序和比较

### select for update 有什么含义

select不会加锁，但是select for update则会加锁，具体加表锁还是行锁主要看是否使用索引：

- 用到索引，加行锁
- 未用到索引，加表锁

### 优化SQL方法

- 加索引
- 避免返回不必要的数据
- 适当分批量进行
- 优化 sql 结构
- 分库分表
- 读写分离

### 优化SQL步骤

- show status 命令了解各种 sql 的执行频率
- 通过慢查询日志定位那些执行效率较低的 sql 语句
- explain 分析低效 sql 的执行计划

### 隔离级别

- 读未提交
- 读已提交
- 可重复读
- 串行化

### 事务的特性
<!--rehype:wrap-class=col-span-2-->
特性 | 解释
:-|-
`原子性` | 事务作为一个整体被执行，包含在其中的对数据库的操作要么全部被执行，要么都不执行,`使用 undo log 来实现的`
`持久性` | 指在事务开始之前和事务结束以后，数据不会被破坏，假如 A 账户给 B 账户转 10 块钱，不管成功与否，A 和 B 的总金额是不变的,`使用 redo log 来实现`
`隔离性` | 多个事务并发访问时，事务之间是相互隔离的，即一个事务不影响其它 事务运行效果。简言之，就是事务之间是进水不犯河水的,`通过锁以及 MVCC,使事务相互隔离开`
`一致性` |  表示事务完成以后，该事务对数据库所作的操作更改，将持久地保存在 数据库之中,`通过回滚、恢复，以及并发情况下的隔离性，从而实现一致性`

### MySQL几种锁

- `表锁`： 开销小，加锁快；锁定力度大，发生锁冲突概率高，并发度最低;不会出现
死锁。
- `行锁`： 开销大，加锁慢；会出现死锁；锁定粒度小，发生锁冲突的概率低，并发
度高。
- `页锁`： 开销和加锁速度介于表锁和行锁之间；会出现死锁；锁定粒度介于表锁和
行锁之间，并发度一般

### 分布式主键生成方案

- 数据库自增长序列或字段。
- UUID。
- Redis 生成 ID
- Twitter 的 snowflake 算法
- 利用 zookeeper 生成唯一 ID
- MongoDB 的 ObjectId

### 如何安全的修改一行数据

- 悲观锁，如select for update
- 乐观锁，如版本号机制或 CAS 算法实现

### mysql日志类型

:-|-
:-|-
`redo log` |属于InnoDB存储引擎的日志，用来保证事务的持久性
`undo log` |属于InnoDB存储引擎的日志，用来保证事务的原子性
`bin log`  |主要用来备份数据，恢复数据
`slow query log` |慢查询日志，用来定位慢查询
`error log` |错误日志
`general log`
`relay log`

### 事务是如何通过日志来实现的

- 因为事务在修改页时，要先记 undo，在记 undo 之前要记 undo 的 redo， 然后
修改数据页，再记数据页修改的 redo。 Redo（里面包括 undo 的修改） 一定要
比数据页先持久化到磁盘。
- 当事务需要回滚时，因为有 undo，可以把数据页回滚到前镜像的 状态，崩溃恢复
时，如果 redo log 中事务没有对应的 commit 记录，那么需要用 undo 把该事务
的修改回滚到事务开始之前。
- 如果有 commit 记录，就用 redo 前滚到该事务完成时并提交掉。

### InnoDB与MyISAM对比

类型|InnoDB | MyISAM
:-|-|-
事务|支持 |不支持
外键|支持 |不支持
MVCC|支持 |不支持
全文索引|不支持(5.7之前) |支持
锁|表、行锁 |表锁
主键|必须有 |可没有
内存和空间|相对大 |相对小
<!--rehype:className=show-header-->

### 一条SQL语句在 MySQL中如何执行的

- 先检查该语句是否有权限
- 如果没有权限，直接返回错误信息
- 如果有权限，在 MySQL8.0 版本以前，会先查询缓存。
- 如果没有缓存，分析器进行词法分析，提取 sql 语句 select 等的关键元素。然后
判断 sql 语句是否有语法错误，比如关键词是否正确等等。
- 优化器进行确定执行方案
- 进行权限校验，如果没有权限就直接返回错误信息，如果有权限就会调用数据库引
擎接口，返回执行结果

### InnoDB完成一次更新操作日志层面的步骤

1. 开启事务
2. 查询待更新的记录到内存，并加 X 锁
3. 记录 undo log 到内存 buffer
4. 记录 redo log 到内存 buffer
5. 更改内存中的数据记录
6. 提交事务，触发 redo log 刷盘
7. 记录 bin log
8. 事务结束

### int(20)与char(20)、varchar(20)

- int(20) 表示字段是 int 类型，显示长度是 20
- char(20)表示字段是固定长度字符串，长度为 20
- varchar(20) 表示字段是可变长度字符串，长度为 20

### delete、truncate与 drop 的区别

选项 | delete| truncate| drop
:-|-|-|-
类型 | DML | DDL| DDL
回滚 | 可回滚 |不可回滚 |不可回滚
删除内容| 表结构还在，删除表的全部或者一部分数据行 |表结构还在，删除表中的所有数据 |从数据库中删除表，所有的数据行，索引和权限也会被删除
删除速度 |删除速度慢，逐行删除 |删除速度快 |删除速度最快
<!--rehype:className=show-header-->

### 主从复制原理

- 主数据库有个 bin-log 二进制文件，纪录了所有增删改 Sql 语句。（binlog 线程）
- 从数据库把主数据库的 bin-log 文件的 sql 语句复制过来。（io 线程）
- 从数据库的 relay-log 重做日志文件中再执行一次这些 sql 语句。（Sql 执行线程）

Java
----
<!--rehype:body-class=cols-3-->

### List 和 Set 的区别

1. list和set都继承自Collection接口
2. list是有序的可重复的，且允许值为null，set是无序的，有其值的hashcode决定的，虽然无序但位置是固定的
3. list支持for循环和迭代器遍历元素，set只能通过迭代器，无法通过下标获取值
4. set检索元素效率低，增删快，增删不会影响元素位置

### ArrayList什么时候扩容

- 空参构造的集合第一次添加元素扩容,空参生成的集合为空的数组，长度为0，第一次添加元素，长度变为10；
- 当前所需长度超出现有长度时扩容，扩容是原长度+原长度>>1

### 为什么Arrays生成的List不能增删

- 因为源码可知，Arrays.asList()生成的ArrayList只是一个内部类，继承自AbstractList,但是却没有重写其add()和remove()方法，因为调用时调用的AbstractList的add和remove方法，故会报错。

### 如何在循环中删除元素而不触发并发修改异常

- 使用迭代器去遍历，迭代器的删除方法,迭代器每次,最好使用list.listIterator()获取的ListIterator迭代器，因为ArrayList内部的迭代器只能删，不能增
- 使用list.removeIf("cat"::equals);
- 使用fori的逆序遍历
- 使用普通的for循环删除，手动去处理因删除操作导致集合大小变化的问题

### HashSet 是如何保证不重复的

- 其底层维护了HashMap结构，map保证不重复的原理是: 1.先通过hash计算该元素的位置，没有则直接插入，有值则通过equals和哈希判断两个值是否相等，如果相等，则会把这个元素返回

### HashMap为什么不安全

- 主要是put方法中resize()方法线程不安全，当多个线程同时开启扩容，会各自生成新的数组进行拷贝扩容，最终结果只有一个新数组被赋值给table变量，其他的线程均会丢失

JVM
----
<!--rehype:body-class=cols-3-->

JUC
----
<!--rehype:body-class=cols-3-->

Spring
----
<!--rehype:body-class=cols-3-->

Redis
----
<!--rehype:body-class=cols-3-->


### Redis数据结构及底层实现
<!--rehype:wrap-class=row-span-3-->
#### String
<!--rehype:style=color: #059669;-->
- 简介：String 是 Redis 最基础的数据结构类型，它是二进制安全的，可以存储图片
或者序列化的对象，值最大存储为 512M
- 简单使用举例: set key value、get key 等
- 应用场景：共享 session、分布式锁，计数器、限流。
- 内部编码有 3 种，int（8 字节长整型）/embstr（小于等于 39 字节字符串）/ raw（大于 39 个字节字符串）


#### List 
<!--rehype:style=color: #059669;-->
- 简介：列表（list）类型是用来存储多个有序的字符串，一个列表最多可以存储
2^32-1 个元素。
- 简单实用举例： lpush key value [value ...] 、lrange key start end
- 内部编码：ziplist（压缩列表）、linkedlist（链表）
- 应用场景： 消息队列，文章列表,

#### Hash
<!--rehype:style=color: #059669;-->
- 简介：在 Redis 中，哈希类型是指 v（值）本身又是一个键值对（k-v）结构
- 简单使用举例：hset key field value 、hget key field
- 内部编码：ziplist（压缩列表） 、hashtable（哈希表）
- 应用场景：缓存用户信息等。
- 注意点：如果开发使用 hgetall，哈希元素比较多的话，可能导致 Redis 阻塞，可以使用 hscan。而如果只是获取部分 field，建议使用 hmget。

#### Set
<!--rehype:style=color: #059669;-->
- 简介：集合（set）类型也是用来保存多个的字符串元素，但是不允许重复元素
- 简单使用举例：sadd key element [element ...]、smembers key
- 内部编码：intset（整数集合）、hashtable（哈希表）
- 注意点：smembers 和 lrange、hgetall 都属于比较重的命令，如果元素过多存在阻塞 Redis 的可能性，可以使用 sscan 来完成。
- 应用场景： 用户标签,生成随机数抽奖、社交需求。


#### ZSet
<!--rehype:style=color: #059669;-->
- 简介：已排序的字符串集合，同时元素不能重复
- 简单格式举例：zadd key score member [score member ...]，zrank key
member
- 底层内部编码：ziplist（压缩列表）、skiplist（跳跃表）
- 应用场景：排行榜，社交需求（如用户点赞）。

#### Geo
<!--rehype:style=color: #059669;-->
- Redis3.2 推出的，地理位置定位，用于存储地理位置信息，并对存储的信息进行操作

#### HyperLogLog
<!--rehype:style=color: #059669;-->
- 用来做基数统计算法的数据结构，如统计网站的 UV。

#### Bitmaps
<!--rehype:style=color: #059669;-->
- 用一个比特位来映射某个元素的状态，在 Redis 中，它的底层是基于
字符串类型实现的，可以把 bitmaps 成作一个以比特位为单位的数组

### Redis为什么这么快
<!--rehype:wrap-class=col-span-2-->
#### 1.基于内存实现
#### 2.高效的数据结构

#### 3.合理的数据编码
:-|-
:-|-
`String`| 如果存储数字的话，是用 int 类型的编码;如果存储非数字，小于等于 39 字节的字符串，是 embstr；大于 39 个字节，则是 raw 编码。
 `List`|如果列表的元素个数小于 512 个，列表每个元素的值都小于 64 字节 （默认），使用 ziplist 编码，否则使用 linkedlist 编码
`Hash`|哈希类型元素个数小于 512 个，所有值小于 64 字节的话，使用 ziplist 编码,否则使用 hashtable 编码。
`Set`|如果集合中的元素都是整数且元素个数小于 512 个，使用 intset 编码， 否则使用 hashtable 编码。
`ZSet`|当有序集合的元素个数小于 128 个，每个元素的值小于 64 字节时，使 用 ziplist 编码，否则使用 skiplist（跳跃表）编码
 <!--rehype:className=left-align-->

#### 4.合理的线程模型
I/O多路复用、单线程模型
#### 5.虚拟内存机制
通过VM功能可以实现冷热数据分离，使热数据仍在内存中、冷数据保存到磁盘



### 内存淘汰策略
<!--rehype:wrap-class=col-span-2-->
:- | :-
:- | :-
`volatile-lru`|当内存不足以容纳新写入数据时，从设置了过期时间的 key 中 使用 LRU（最近最少使用）算法进行淘汰；
`allkeys-lru` |当内存不足以容纳新写入数据时，从所有 key 中使用 LRU（最近 最少使用）算法进行淘汰。
`volatile-lfu`|4.0 版本新增，当内存不足以容纳新写入数据时，在过期的 key中，使用 LFU 算法进行删除 key。
`allkeys-lfu`|4.0 版本新增，当内存不足以容纳新写入数据时，从所有 key 中 使用 LFU 算法进行淘汰；
`volatile-random` | 当内存不足以容纳新写入数据时，从设置了过期时间的 key 中，随机淘汰数据；。
`allkeys-random` | 当内存不足以容纳新写入数据时，从所有 key 中随机淘汰 数据。
`volatile-ttl`|当内存不足以容纳新写入数据时，在设置了过期时间的 key 中， 根据过期时间进行淘汰，越早过期的优先被淘汰；
`noeviction`|默认策略，当内存不足以容纳新写入数据时，新写入操作会报错。
 <!--rehype:className=left-align-->

### Redis 持久化
<!--rehype:wrap-class=col-span-2-->
#### AOF（append only file）持久化
采用日志的形式来记录每个写操作，追加到
AOF 文件的末尾。Redis 默认情况是不开启 AOF 的。重启时再重新执行 AOF 文
件中的命令来恢复数据。它主要解决数据持久化的实时性问题。
AOF 是执行完命令后才记录日志的。为什么不先记录日志再执行命令呢？ 这是
因为 Redis 在向 AOF 记录日志时，不会先对这些命令进行语法检查，如果先记
录日志再执行命令，日志中可能记录了错误的命令，Redis 使用日志回复数据
时，可能会出错
#### RDB
RDB，就是把内存数据以快照的形式保存到磁盘上。和 AOF 相比，它记录的是
某一时刻的数据，，并不是操作。
什么是快照?可以这样理解，给当前时刻的数据，拍一张照片，然后保存下来。
RDB 持久化，是指在指定的时间间隔内，执行指定次数的写操作，将内存中的
数据集快照写入磁盘中，它是 Redis 默认的持久化方式。执行完操作后，在指
定目录下会生成一个 dump.rdb 文件，Redis 重启的时候，通过加载 dump.rdb
文件来恢复数据。RDB 触发机制主要有以下几种：
- 手动Save
- 手动bgsave
- 自动触发

#### 如何选择 RDB 和 AOF
- 如果数据不能丢失，RDB 和 AOF 混用
- 如果只作为缓存使用，可以承受几分钟的数据丢失的话，可以只使用 RDB。
- 如果只使用 AOF，优先使用 everysec 的写回策略
