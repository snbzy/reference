Spring 备忘清单
===

这是 Spring 的快速参考备忘单。 你可以在这里找到最常见的 Spring 命令。

Spring
----
<!--rehype:body-class=cols-3-->




### SpringIOC初始化过程
<!--rehype:wrap-class=col-span-2-->

AbstractApplicationContext refresh方法
表示 | 描述
:-|-
`1.prepareRefresh()` | 刷新前的预处理
`2. ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory()`| 获取BeanFactory；默认实现是DefaultListableBeanFactory 加载BeanDefition 并注册到 BeanDefitionRegistry
`3. prepareBeanFactory(beanFactory);`| BeanFactory的预准备⼯作（BeanFactory进⾏⼀些设置，⽐如context的类加载器等）
`4. postProcessBeanFactory(beanFactory)`| BeanFactory准备⼯作完成后进⾏的后置处理⼯作
`5. invokeBeanFactoryPostProcessors(beanFactory);`| 例化并调⽤实现了BeanFactoryPostProcessor接⼝的Bean
`6. registerBeanPostProcessors(beanFactory)` |注册BeanPostProcessor（Bean的后置处理器），在创建bean的前后等执⾏
`7. initMessageSource()`| 初始化MessageSource组件（做国际化功能；消息绑定，消息解析）；
`8. initApplicationEventMulticaster()`| 初始化事件派发器
`9. onRefresh()`|⼦类重写这个⽅法，在容器刷新的时候可以⾃定义逻辑
`10. registerListeners()`|注册应⽤的监听器。就是注册实现了ApplicationListener接⼝的监听器
`11. finishBeanFactoryInitialization(beanFactory)`|初始化所有剩下的⾮懒加载的单例bean 初始化创建⾮懒加载⽅式的单例Bean实例（未设置属性） 填充属性 初始化⽅法调⽤（⽐如调⽤afterPropertiesSet⽅法、init-method⽅法） 调⽤BeanPostProcessor（后置处理器）对实例bean进⾏后置处
`12. finishRefresh()`| 完成context的刷新。主要是调⽤LifecycleProcessor的onRefresh()⽅法，并且发布事件 （ContextRefreshedEvent）




### Bean生命周期
- 实例化（Instantiation）

  - 1.实例化bean实例

- 属性赋值（Populate）

  - 2.设置对象属性

- 初始化（Initialization）

  - 3.检查aware相关接口并设置属性
  - 4.BeanPostProcessor前置处理
  - 5.是否实现InitializationBean接口
  - 6.是否定义配置init-method接口
  - 7.BeanPostProcessor后置处理

- 销毁（Destruction）

  - 8.注册Destruction相关回调接口
  - 9.使用
  - 10.是否实现Disposable接口
  - 11.是否配置自定义的destroy-method接口
  

<!--rehype:className=style-timeline-->
> 参考文章：[如何记忆 Spring Bean 的生命周期](https://juejin.cn/post/6844904065457979405)


### BeanFactory、FactoryBean和ApplicationContext
:-|:-
:-|:-
BeanFactory|
FactoryBean|
ApplicationContext|


### 依赖注入的两种方式
:-|:-
:-|:-
构造函数注入	|setter 注入
没有部分注入	|有部分注入
不会覆盖 setter 属性	|会覆盖 setter 属性
任意修改都会创建一个新实例	|任意修改不会创建一个新实例
适用于设置很多属性	|适用于设置少量属性

### 容器扩展点
:-|-
:-|-
`BeanPostProcessor`    | 自定义 bean
`BeanFactoryPostProcessor`    | 自定义配置元数据
`FactoryBean`    | 自定义实例化逻辑


### Spring 的事务隔离级别是如何做到和数据库不一致的？

比如数据库是可重复读，Spring 是读已提交，这是怎么实现的？

Spring 的事务隔离级别本质上还是通过数据库来控制的，具体是在执行事务前先执行命令修改数据库隔离级别

### 循环依赖
#### 定义
一个或多个对象实例之间存在直接或间接的依赖关系，这种依赖关系构成了构成一个环形调用。

#### 如何解决循环依赖
`通过Setter方式注入+三级缓存`：
- 当不需要代理时，只需要二级缓存即可解决循环依赖， 首先一级缓存是存放所有初始化好的bean
当采用Setter方式注入，首先需要实例化所需的bean,如A，B；但此时A，B仅实例化完成，并未完全初始化，故不能放入一级缓存，此时需要二级缓存，及实例化完成未完全初始化好的bean，然后采用Setter方式从二级缓存去取所需的bean，完成初始化。
- 当需要注入代理对象时，二级缓存不能满足要求，此时需要三级缓存
#### 三级缓存
- 第一级缓存（也叫单例池）：Map<String, Object> singletonObjects，存放已经初始化完成的 Bean 对象
- 第二级缓存：Map<String, Object> earlySingletonObjects，存放早期暴露出来的 Bean 对象，Bean 的生命周期未结束（属性还未填充完），可能是代理对象，也可能是原始对象
- 第三级缓存：Map<String, ObjectFactory<?>> singletonFactories，存放可以生成 Bean 的工厂，工厂主要用来生成 Bean 的代理对象
> `构造函数注入形成的循环依赖依赖不能被解决`

### spring声明式事务
<!--rehype:wrap-class=row-span-2-->
Spring 事务的底层实现主要使用的技术：AOP（动态代理） + ThreadLocal + try/catch。

动态代理：基本所有要进行逻辑增强的地方都会用到动态代理，AOP 底层也是通过动态代理实现。

ThreadLocal：主要用于线程间的资源隔离，以此实现不同线程可以使用不同的数据源、隔离级别等等。

try/catch：最终是执行 commit 还是 rollback，是根据业务逻辑处理是否抛出异常来决定。

Spring 事务的核心逻辑伪代码如下：
```java
public void invokeWithinTransaction() {
    // 1.事务资源准备
    try {
        // 2.业务逻辑处理，也就是调用被代理的方法
    } catch (Exception e) {
        // 3.出现异常，进行回滚并将异常抛出
    } finally {
        // 现场还原：还原旧的事务信息
    }
    // 4.正常执行，进行事务的提交
    // 返回业务逻辑处理结果
}

```
<img src="https://s2.loli.net/2023/02/01/dKwAhXMHvl8rmqE.png" width=100% alt=""/>

### 事务传播行为
1. required:（spring默认）如果当前没有事务，则自己新建一个事务，如果当前存在事务，则加入这个事务
2. supports:当前存在事务，则加入当前事务，如果当前没有事务，就以非事务方法执行
3. mondatory:当前存在事务，则加入当前事务，如果当前事务不存在，则抛出异常。
4. requires_new:创建一个新事务，如果存在当前事务，则挂起该事务。
5. not_supported:始终以非事务方式执行,如果当前存在事务，则挂起当前事务
6. never:不使用事务，如果当前事务存在，则抛出异常
7. nested:如果当前事务存在，则在嵌套事务中执行，否则和REQUIRED的操作一样（开启一个事务）

### Spring 事务失效场景



### Spring AOP实现原理

Spring MVC
----

### SpringMVC 的工作原理
<!--rehype:wrap-class=col-span-2-->
<img src="https://s2.loli.net/2023/02/01/xagnS8RY2ZPoCs4.png" width="100%" alt=""/>


### 所有注解
<!--rehype:wrap-class=row-span-2-->
:-|-
:-|-
`@Controller`  | 请求映射 
`@RestController`  | 请求映射 
`@RequestMapping`  | 请求映射 
`@GetMapping` | GET
`@PostMapping`| GET
`@PutMapping`| GET
`@DeleteMapping`| GET
`@PatchMapping`| GET
`@RequestParam`| GET
`@RequestHeader`| GET
`@CookieValue`| GET
`@ModelAttribute`| GET
`@SessionAttributes`| GET
`@SessionAttribute`| GET
`@RequestAttribute`| GET
`@RequestBody`| GET
`@RequestPart`| GET
`@ResponseBody`| GET
`@PathVariable`| GET
`@MatrixVariable`| GET
`@ExceptionHandler`| GET
`@ControllerAdvice`| GET
`@CrossOrigin`| GET




<!--rehype:body-class=cols-3-->

Spring WebFlux
----
<!--rehype:body-class=cols-3-->

SpringBoot
----
<!--rehype:body-class=cols-3-->

### Springboot自动配置原理

### Springboot启动流程

另见
----

- [source-code-hunter](https://doocs.gitee.io/source-code-hunter/#/)
