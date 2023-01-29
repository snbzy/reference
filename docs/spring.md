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


### 容器扩展点
:-|-
:-|-
`BeanPostProcessor`    | 自定义 bean
`BeanFactoryPostProcessor`    | 自定义配置元数据
`FactoryBean`    | 自定义实例化逻辑


### 事务传播行为

### 循环依赖



Spring MVC
----

### 所有注解
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

另见
----

- [source-code-hunter](https://doocs.gitee.io/source-code-hunter/#/)
