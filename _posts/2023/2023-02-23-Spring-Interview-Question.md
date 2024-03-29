---
layout: post
title: Spring面试合集
category: 面试
---

# Spring面试合集

> 基于Spring Framework 4.x 总结的常见面试题，系统学习建议还是官方文档走起：[https://spring.io/projects/spring-framework#learn](https://spring.io/projects/spring-framework#learn)


## 一、一般问题

### 开发中主要使用 Spring 的什么技术 ?

1. IOC 容器管理各层的组件
2. 使用 AOP 配置声明式事务
3. 整合其他框架

### 使用 **Spring** 框架能带来哪些好处?

下面列举了一些使用 Spring 框架带来的主要好处:

- Dependency Injection(DI) 方法使得构造器和 JavaBean properties 文件中的依赖关系一 目了然。
- 与 EJB 容器相比较，IoC 容器更加趋向于轻量级。这样一来 IoC 容器在有限的内存和 CPU 资源的情况下进行应用程序的开发和发布就变得十分有利。
- Spring 并没有闭门造车，Spring 利用了已有的技术比如 ORM 框架、logging 框架、J2EE、Q uartz和JDK Timer，以及其他视图技术。
- Spring 框架是按照模块的形式来组织的。由包和类的编号就可以看出其所属的模块，开发者仅 仅需要选用他们需要的模块即可。
- 要测试一项用 Spring 开发的应用程序十分简单，因为测试相关的环境代码都已经囊括在框架中 了。更加简单的是，利用 JavaBean 形式的 POJO 类，可以很方便的利用依赖注入来写入测试 数据。
- Spring 的 Web 框架亦是一个精心设计的 Web MVC 框架，为开发者们在 web 框架的选择上 提供了一个除了主流框架比如 Struts、过度设计的、不流行 web 框架的以外的有力选项。
- Spring 提供了一个便捷的事务管理接口，适用于小型的本地事物处理(比如在单 DB 的环境 下)和复杂的共同事物处理(比如利用 JTA 的复杂 DB 环境)。

### Spring有哪些优点？

- **轻量级**：Spring在大小和透明性方面绝对属于轻量级的，基础版本的Spring框架大约只有2MB。
- **控制反转(IOC)**：Spring使用控制反转技术实现了松耦合。依赖被注入到对象，而不是创建或寻找依赖对象。
- **面向切面编程(AOP)**：Spring支持面向切面编程，同时把应用的业务逻辑与系统的服务分离开来。
- **容器**：Spring包含并管理应用程序对象的配置及生命周期。
- **MVC框架**：Spring的web框架是一个设计优良的web MVC框架，很好的取代了一些web框架。
- **事务管理**：Spring对下至本地业务上至全局业务(JAT)提供了统一的事务管理接口。
- **异常处理**：Spring提供一个方便的API将特定技术的异常(由JDBC, Hibernate, 或JDO抛出)转化为一致的、Unchecked异常。

### Spring模块

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gi8npk820uj30k00f0q3x.jpg#id=fy8tX&originHeight=540&originWidth=720&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

### 简述 AOP 和 IOC 概念

AOP：Aspect Oriented Program, 面向(方面)切面的编程;Filter(过滤器)也是一种 AOP. AOP 是一种新的 方法论, 是对传统 OOP(Object-OrientedProgramming, 面向对象编程) 的补充. AOP 的主要编程对象是切面(aspect),而切面模块化横切关注点.可以举例通过事务说明.

IOC：Invert Of Control, 控制反转. 也称为 DI(依赖注入)其思想是反转资源获取的方向. 传统的资源查找方式要求组件向容器发起请求查找资源.作为回应, 容器适时的返回资源. 而应用了 IOC 之后, 则是容器主动地将资源推送给它所管理的组件,组件所要做的仅是选择一种合适的方式来接受资源. 这种行为也被称为查找的被动形式

## 二、依赖注入

IoC（Inverse of Control:控制反转）是一种**设计思想**，就是 **将原本在程序中手动创建对象的控制权，交由Spring框架来管理。** IoC 在其他语言中也有应用，并非 Spring 特有。 **IoC 容器是 Spring 用来实现 IoC 的载体， IoC 容器实际上就是个Map（key，value）,Map 中存放的是各种对象。**

将对象之间的相互依赖关系交给 IoC 容器来管理，并由 IoC 容器完成对象的注入。这样可以很大程度上简化应用的开发，把应用从复杂的依赖关系中解放出来。 **IoC 容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，完全不用考虑对象是如何被创建出来的。** 在实际项目中一个 Service 类可能有几百甚至上千个类作为它的底层，假如我们需要实例化这个 Service，你可能要每次都要搞清这个 Service 所有底层类的构造函数，这可能会把人逼疯。如果利用 IoC 的话，你只需要配置好，然后在需要的地方引用就行了，这大大增加了项目的可维护性且降低了开发难度。

### 什么是 Spring IOC 容器？

Spring 框架的核心是 Spring 容器。容器创建对象，将它们装配在一起，配置它们并管理它们的完整生命周期。Spring 容器使用依赖注入来管理组成应用程序的组件。容器通过读取提供的配置元数据来接收对象进行实例化，配置和组装的指令。该元数据可以通过 XML，Java 注解或 Java 代码提供。

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gi8npp9px7j30du088743.jpg#id=xFOf6&originHeight=296&originWidth=498&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

### 什么是依赖注入？

**依赖注入（DI,Dependency Injection）是在编译阶段尚未知所需的功能是来自哪个的类的情况下，将其他对象所依赖的功能对象实例化的模式**。这就需要一种机制用来激活相应的组件以提供特定的功能，所以**依赖注入是控制反转的基础**。否则如果在组件不受框架控制的情况下，框架又怎么知道要创建哪个组件？

依赖注入有以下三种实现方式：

1. 构造器注入
2. Setter方法注入（属性注入）
3. 接口注入

### Spring 中有多少种 IOC 容器？

Spring 中的 org.springframework.beans 包和 org.springframework.context 包构成了 Spring 框架 IoC 容器的基础。

在 Spring IOC 容器读取 Bean 配置创建 Bean 实例之前，必须对它进行实例化。只有在容器实例化后， 才可以从 IOC 容器里获取 Bean 实例并使用

Spring 提供了两种类型的 IOC 容器实现

-  BeanFactory：IOC 容器的基本实现 
-  ApplicationContext：提供了更多的高级特性，是 BeanFactory 的子接口 

BeanFactory 是 Spring 框架的基础设施，面向 Spring 本身；ApplicationContext 面向使用 Spring 框架的开发者，几乎所有的应用场合都直接使用 ApplicationContext 而非底层的 BeanFactory；

无论使用何种方式, 配置文件是相同的。

### BeanFactory 和 ApplicationContext 区别
| BeanFactory | ApplicationContext |
| --- | --- |
| 懒加载 | 即时加载 |
| 它使用语法显式提供资源对象 | 它自己创建和管理资源对象 |
| 不支持国际化 | 支持国际化 |
| 不支持基于依赖的注解 | 支持基于依赖的注解 |


> BeanFactory 可以理解为含有 bean 集合的工厂类。BeanFactory 包含了种 bean 的定义，以便在接收到客户端请求时将对应的 bean 实例化。
>  
> BeanFactory 还能在实例化对象的时生成协作类之间的关系。此举将 bean 自身与 bean 客户端的 配置中解放出来。BeanFactory 还包含 了 bean 生命周期的控制，调用客户端的初始化方法 (initialization methods)和销毁方法(destruction methods)。
>  
> 从表面上看，application context 如同 bean factory 一样具有 bean 定义、bean 关联关系的设 置，根据请求分发 bean 的功能。但 applicationcontext 在此基础上还提供了其他的功能。
>  
> 1. 提供了支持国际化的文本消息
> 2. 统一的资源文件读取方式
> 3. 已在监听器中注册的bean的事件


**ApplicationContext**

ApplicationContext 的主要实现类：

- ClassPathXmlApplicationContext：从类路径下加载配置文件
- FileSystemXmlApplicationContext: 从文件系统中加载配置文件
- ConfigurableApplicationContext 扩展于 ApplicationContext，新增加两个主要方法：refresh() 和 close()， 让 ApplicationContext具有启动、刷新和关闭上下文的能力
- WebApplicationContext 是专门为 WEB 应用而准备的，它允许从相对于 WEB 根目录的路径中完成初始化工作
- ApplicationContext 在初始化上下文时就实例化所有单例的 Bean

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gi8npy9i8cj31300pwn0i.jpg#id=TyR6J&originHeight=932&originWidth=1404&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

**从 IOC 容器中获取 Bean**

- 调用 ApplicationContext 的 getBean() 方法

```java
ApplicationContext ctx = new ClassPathXmlApplicationContext("beans.xml");
HelloWorld helloWorld = (HelloWorld) ctx.getBean("helloWorld");
helloWorld.hello();
```

### 列举 IoC 的一些好处

- 它将最小化应用程序中的代码量；
- 它将使您的应用程序易于测试，因为它不需要单元测试用例中的任何单例或 JNDI 查找机制；
- 它以最小的影响和最少的侵入机制促进松耦合；
- 它支持即时的实例化和延迟加载服务

### Spring IoC 的实现机制

Spring 中的 IoC 的实现原理就是工厂模式加反射机制，示例：

```java
interface Fruit {
     public abstract void eat();
}
class Apple implements Fruit {
    public void eat(){
        System.out.println("Apple");
    }
}
class Orange implements Fruit {
    public void eat(){
        System.out.println("Orange");
    }
}
class Factory {
    public static Fruit getInstance(String ClassName) {
        Fruit f=null;
        try {
            f=(Fruit)Class.forName(ClassName).newInstance();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return f;
    }
}
class Client {
    public static void main(String[] a) {
        Fruit f=Factory.getInstance("priv.starfish.spring.Apple");
        if(f!=null){
            f.eat();
        }
    }
}
```

### 请举例说明如何在 **Spring** 中注入一个 **Java Collection**?

Spring 提供了以下四种集合类的配置元素:

- `<list>` : 该标签用来装配可重复的 list 值。
- `<set>` : 该标签用来装配没有重复的 set 值。
- `<map>`: 该标签可用来注入键和值可以为任何类型的键值对。
- `<props>` : 该标签支持注入键和值都是字符串类型的键值对。

```xml
<beans>
<!-- Definition for javaCollection -->
<bean id="javaCollection" class="com.howtodoinjava.JavaCollection">
      <!-- java.util.List -->
      <property name="customList">
        <list>
           <value>INDIA</value>
           <value>Pakistan</value>
           <value>USA</value>
           <value>UK</value>
        </list>
      </property>
     <!-- java.util.Set -->
     <property name="customSet">
        <set>
           <value>INDIA</value>
           <value>Pakistan</value>
           <value>USA</value>
           <value>UK</value>
        </set>
      </property>
     <!-- java.util.Map -->
     <property name="customMap">
        <map>
           <entry key="1" value="INDIA"/>
           <entry key="2" value="Pakistan"/>
           <entry key="3" value="USA"/>
           <entry key="4" value="UK"/>
</map>
    </property>
    <!-- java.util.Properties -->
    <property name="customProperies">
        <props>
            <prop key="admin">admin@nospam.com</prop>
            <prop key="support">support@nospam.com</prop>
        </props>
</property>
   </bean>
</beans>
```

## 三、Beans

### 什么是 Spring Beans？

- 它们是构成用户应用程序主干的对象
- Bean 由 Spring IoC 容器管理
- 它们由 Spring IoC 容器实例化，配置，装配和管理
- Bean 是基于用户提供给容器的配置元数据创建

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gi8nq56qklj30l602jjre.jpg#id=LIkx1&originHeight=91&originWidth=762&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

### Spring 提供了哪些配置方式？

-  基于 xml 配置
bean 所需的依赖项和服务在 XML 格式的配置文件中指定。这些配置文件通常包含许多 bean 定义和特定于应用程序的配置选项。它们通常以 bean 标签开头。例如： 
```xml
<bean id="studentbean" class="org.edureka.firstSpring.StudentBean">
 <property name="name" value="Edureka"></property>
</bean>
```
 

-  基于注解配置
您可以通过在相关的类，方法或字段声明上使用注解，将 bean 配置为组件类本身，而不是使用 XML 来描述 bean 装配。默认情况下，Spring 容器中未打开注解装配。因此，您需要在使用它之前在 Spring 配置文件中启用它。例如： 
```xml
<beans>
<context:annotation-config/>
<!-- bean definitions go here -->
</beans>
```
 

-  基于 Java API 配置
Spring 的 Java 配置是通过使用 [@Bean ](/Bean ) 和 [@Configuration ](/Configuration ) 来实现。  
   1.  [@Bean ](/Bean ) 注解扮演与 `<bean/>` 元素相同的角色。 
   2.  [@Configuration ](/Configuration ) 类允许通过简单地调用同一个类中的其他 [@Bean ](/Bean ) 方法来定义 bean 间依赖关系。  

例如：

```java
@Configuration
public class StudentConfig {
    @Bean
    public StudentBean myStudent() {
        return new StudentBean();
    }
}
```

### Spring Bean的作用域？

-  在 Spring 中, 可以在 <bean> 元素的 scope 属性里设置 Bean 的作用域。 
-  默认情况下，Spring 只为每个在 IOC 容器里声明的 Bean 创建唯一一个实例，整个 IOC 容器范围内都能共享该实例：所有后续的 `getBean()` 调用和 Bean 引用都将返回这个唯一的 Bean 实例。该作用域被称为 **singleton**，它是所有 Bean 的默认作用域。 

Spring 容器中的 bean 可以分为 5 个范围。所有范围的名称都是自说明的，但是为了避免混淆，还是让我们来解释一下：

1. **singleton**：这种bean范围是默认的，这种范围确保不管接受到多少个请求，每个容器中只有一个bean的实例，单例的模式由bean factory自身来维护。
2. **prototype**：原型范围与单例范围相反，为每一个bean请求提供一个实例。
3. **request**：每次HTTP请求都会创建一个新的bean，该作用于仅适用于WebApplicationContext环境，在请求完成以后，bean会失效并被垃圾回收器回收。
4. **Session**：同一个HTTP Session 共享一个bean，不同的 HTTP Session使用不同的bean。该作用于仅适用于WebApplicationContext环境，在session过期后，bean会随之失效。
5. **global-session**：全局session作用域，仅仅在基于portlet的web应用中才有意义，Spring5已经没有了。Portlet是能够生成语义代码(例如：HTML)片段的小型Java Web插件。它们基于portlet容器，可以像servlet一样处理HTTP请求。但是，与 servlet 不同，每个 portlet 都有不同的会话

全局作用域与Servlet中的session作用域效果相同。

### **Spring** 框架中的单例 **Beans** 是线程安全的么?

> Spring 容器中的Bean是否线程安全，容器本身并没有提供Bean的线程安全策略，因此可以说Spring容器中的Bean本身不具备线程安全的特性，但是具体还是要结合具体scope的Bean去研究。
>  
> 线程安全这个问题，要从单例与原型Bean分别进行说明。
>  
> **「原型Bean」**对于原型Bean,每次创建一个新对象，也就是线程之间并不存在Bean共享，自然是不会有线程安全的问题。
>  
> **「单例Bean」**对于单例Bean,所有线程都共享一个单例实例Bean,因此是存在资源的竞争。
>  
> ### **spring单例，为什么controller、service和dao确能保证线程安全？**
>  
> Spring中的Bean默认是单例模式的，框架并没有对bean进行多线程的封装处理。实际上大部分时间Bean是无状态的（比如Dao） 所以说在某种程度上来说Bean其实是安全的。
>  
> 但是如果Bean是有状态的 那就需要开发人员自己来进行线程安全的保证，最简单的办法就是改变bean的作用域 把  `singleton` 改为 `protopyte`， 这样每次请求Bean就相当于是 new Bean() 这样就可以保证线程的安全了。
>  
> - 有状态就是有[数据存储](https://cloud.tencent.com/product/cdcs?from=10680)功能
> - 无状态就是不会保存数据
> 
 
> controller、service和dao层本身并不是线程安全的，只是如果只是调用里面的方法，而且多线程调用一个实例的方法，会在内存中复制变量，这是自己的线程的工作内存，是安全的。


Spring 框架并没有对单例 bean 进行任何多线程的封装处理。关于单例 bean 的线程安全和并发问 题需要开发者自行去搞定。但实际上，大部分的 Spring bean 并没有可变的状态(比如 Serview 类 和 DAO 类)，所以在某种程度上说 Spring 的单例 bean 是线程安全的。如果你的 bean 有多种状 态的话(比如 View Model 对象)，就需要自行保证线程安全。
最浅显的解决办法就是将多态 bean 的作用域由“singleton”变更为“prototype”。

### Spring bean 容器的生命周期是什么样的？

Spring IOC 容器可以管理 Bean 的生命周期，Spring 允许在 Bean 生命周期的特定点执行定制的任务。

Spring bean 容器的生命周期流程如下：

1. Spring 容器根据配置中的 bean 定义实例化 bean；
2. Spring 使用依赖注入填充所有属性，如 bean 中所定义的配置；
3. 如果 bean 实现 BeanNameAware 接口，则工厂通过传递 bean 的 ID 来调用 setBeanName()；
4. 如果 bean 实现 BeanFactoryAware 接口，工厂通过传递自身的实例来调用 setBeanFactory()；
5. 与上面的类似，如果实现了其他 `*.Aware`接口，就调用相应的方法；
6. 如果存在与 bean 关联的任何 BeanPostProcessors，则调用 preProcessBeforeInitialization() 方法；
7. 如果为 bean 指定了 init 方法（`<bean>` 的 init-method 属性），那么将调用它；
8. 最后，如果存在与 bean 关联的任何 BeanPostProcessors，则将调用 postProcessAfterInitialization() 方法；
9. 如果 bean 实现 DisposableBean 接口，当 spring 容器关闭时，会调用 destory()；
10. 如果为 bean 指定了 destroy 方法（`<bean>` 的 destroy-method 属性），那么将调用它

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gi8nqbdmr2j30zp0u0n2x.jpg#id=Z0tkb&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

在 bean 初始化时会经历几个阶段，要与容器对 bean 生命周期的管理交互，可以实现  `InitializingBean` 和 `DisposableBean` 接口。容器对前者调用 `afterPropertiesSet()`，对后者调用 `destroy()`，以允许 bean 在初始化和销毁 bean 时执行某些操作。

官方不建议使用这两个接口，而是建议使用 `@PostConstruct` 和 `@PreDestroy`，或者 XML 配置中使用 `init-method`和`destroy-method` 属性

```xml
<bean id="exampleInitBean" class="examples.ExampleBean" init-method="init"/>
```

```java
public class ExampleBean {

    public void init() {
        // do some initialization work
    }
}
```

等价于

```java
public class AnotherExampleBean implements InitializingBean {

    public void afterPropertiesSet() {
        // do some initialization work
    }
}
```

> Spring Bean生命周期回调——初始化回调和销毁回调方法


实现 Bean 初始化回调和销毁回调各有三种方法，一是实现接口方法，二是在XML配置，三是使用注解

- 使用注解 `@PostConstruct` 和 `@PreDestroy`
- 实现  `InitializingBean` 和 `DisposableBean` 接口
- XML 中配置 `init-method` 和 `destroy-method`

在一个 bean 中，如果配置了多种生命周期回调机制，会按照上边从上到下的次序调用

### 在 Spring 中如何配置 Bean?

Bean 的配置方式: 通过全类名 （反射）、 通过工厂方法 （静态工厂方法 & 实例工厂方法）、FactoryBean

### 什么是 Spring 装配

当 bean 在 Spring 容器中组合在一起时，它被称为装配或 bean 装配，装配是创建应用对象之间协作关系的行为。 Spring 容器需要知道需要什么 bean 以及容器应该如何使用依赖注入来将 bean 绑定在一起，同时装配 bean。

依赖注入的本质就是装配，装配是依赖注入的具体行为。

注入是实例化的过程，将创建的bean放在Spring容器中，分为属性注入（setter方式）、构造器注入

### 什么是bean自动装配？

Spring 容器可以自动配置相互协作 beans 之间的关联关系。这意味着 Spring 可以自动配置一个 bean 和其他协作bean 之间的关系，通过检查 BeanFactory 的内容里有没有使用< property>元素。

在Spring框架中共有5种自动装配，让我们逐一分析

1.  **no**：这是Spring框架的默认设置，在该设置下自动装配是关闭的，开发者需要自行在beanautowire属性里指定自动装配的模式 
2.  **byName**：该选项可以根据bean名称设置依赖关系。当向一个bean中自动装配一个属性时，容器将根据bean的名称自动在在配置文件中查询一个匹配的bean。如果找到的话，就装配这个属性，如果没找到的话就报错。 
3.  **byType**：该选项可以根据bean类型设置依赖关系。当向一个bean中自动装配一个属性时，容器将根据bean的类型自动在在配置文件中查询一个匹配的bean。如果找到的话，就装配这个属性，如果没找到的话就报错。 
4.  **constructor**：构造器的自动装配和byType模式类似，但是仅仅适用于与有构造器相同参数的bean，如果在容器中没有找到与构造器参数类型一致的bean，那么将会抛出异常。 
5.  **autodetect**：Spring首先尝试通过 _constructor_ 使用自动装配来连接，如果它不执行，Spring 尝试通过 _byType_ 来自动装配 

### 自动装配有什么局限？

- 基本数据类型的值、字符串字面量、类字面量无法使用自动装配来注入。
- 装配依赖中若是出现匹配到多个bean（出现歧义性），装配将会失败

### 通过注解的方式配置bean | 什么是基于注解的容器配置

**组件扫描**(component scanning): Spring 能够从 classpath下自动扫描, 侦测和实例化具有特定注解的组件。

特定组件包括:

- [**@Component **](/Component )** **：基本注解，标识了一个受 Spring 管理的组件
- [**@Respository **](/Respository )** **：标识持久层组件
- [**@Service **](/Service )** **：标识服务层(业务层)组件
- [**@Controller **](/Controller )** **： 标识表现层组件

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gi8nqhucw4j31qq0j2aak.jpg#id=RTsFq&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

对于扫描到的组件,，Spring 有默认的命名策略：使用非限定类名，第一个字母小写。也可以在注解中通过 value 属性值标识组件的名称。

当在组件类上使用了特定的注解之后,，还需要在 Spring 的配置文件中声明 `<context:component-scan>`：

-  `base-package` 属性指定一个需要扫描的基类包，Spring 容器将会扫描这个基类包里及其子包中的所有类 
-  当需要扫描多个包时, 可以使用逗号分隔 
-  如果仅希望扫描特定的类而非基包下的所有类，可使用 `resource-pattern` 属性过滤特定的类，示例： 
```xml
<context:component-scan base-package="priv.starfish.front.web.controller"
	annotation-config="true" resource-pattern="autowire/*.class"/>
```
 

### 如何在 spring 中启动注解装配？

默认情况下，Spring 容器中未打开注解装配。因此，要使用基于注解装配，我们必须通过配置`<context：annotation-config />` 元素在 Spring 配置文件中启用它。

## 四、AOP

> 👴：描述一下Spring AOP 呗？
>  
> 		你有没有⽤过Spring的AOP? 是⽤来⼲嘛的? ⼤概会怎么使⽤？


### 什么是 AOP？

AOP(Aspect-Oriented Programming，面向切面编程)：是一种新的方法论，是对传统 OOP(Object-Oriented Programming，面向对象编程) 的补充。在 OOP 中, 我们以类(class)作为我们的基本单元，而 AOP 中的基本单元是 **Aspect(切面)**

AOP 的主要编程对象是切面(aspect)

在应用 AOP 编程时, 仍然需要定义公共功能，但可以明确的定义这个功能在哪里,，以什么方式应用,，并且不必修改受影响的类。这样一来横切关注点就被模块化到特殊的对象(切面)里。

AOP 的好处:

- 每个事物逻辑位于一个位置，代码不分散，便于维护和升级
- 业务模块更简洁, 只包含核心业务代码

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gi8nqrqcgvj30ov0hqq38.jpg#id=ezivW&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

### **AOP 术语**

- 切面（Aspect）：横切关注点（跨越应用程序多个模块的功能），被模块化的特殊对象
- 连接点（Joinpoint）：程序执行的某个特定位置，如类某个方法调用前、调用后、方法抛出异常后等。在这个位置我们可以插入一个 AOP 切面，它实际上是应用程序执行 Spring AOP 的位置

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gi8nqwua8mj31da0fqmxb.jpg#id=Macpo&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

- 通知（Advice）： 通知是个在方法执行前或执行后要做的动作，实际上是程序执行时要通过 SpringAOP 框架触发的代码段。Spring 切面可以应用五种类型的通知： 
   - before： 前置通知 ， 在一个方法执行前被调用
   - after：在方法执行之后调用的通知，无论方式执行是否成功
   - after-returning：仅当方法成功完成后执行的通知
   - after-throwing：在方法抛出异常退出时执行的通知
   - around：在方法执行之前和之后调用的通知

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gi8nr1x47wj30z20qi3yr.jpg#id=Ss7jX&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

- 目标（Target）：被通知的对象，通常是一个代理对象，也指被通知（advice）对象
- 代理（Proxy）：向目标对象应用通知之后创建的对象
- 切点（pointcut）：每个类都拥有多个连接点，程序运行中的一些时间点，例如一个方法的执行，或者是一个异常的处理。AOP 通过切点定位到特定的连接点。类比：连接点相当于数据库中的记录，切点相当于查询条件。切点和连接点不是一对一的关系，一个切点匹配多个连接点，切点通过 `org.springframework.aop.Pointcut` 接口进行描述，它使用类和方法作为连接点的查询条件
- 引入（Introduction）：引入允许我们向现有的类添加新方法或属性
- 织入（Weaving）：织入是把切面应用到目标对象并创建新的代理对象的过程

**Spring  AOP**

- **AspectJ：**Java 社区里最完整最流行的 AOP 框架
- 在 Spring2.0 以上版本中, 可以使用基于 AspectJ 注解或基于 XML 配置的 AOP

**在 Spring 中启用 AspectJ 注解支持**

- 要在 Spring 应用中使用 AspectJ 注解, 必须在 classpath 下包含 AspectJ 类库：`aopalliance.jar`、`aspectj.weaver.jar` 和 `spring-aspects.jar`
- 将 aop Schema 添加到 `<beans>` 根元素中.
- 要在 Spring IOC 容器中启用 AspectJ 注解支持, 只要在 Bean 配置文件中定义一个空的 XML 元素 `<aop:aspectj-autoproxy>`
- 当 Spring IOC 容器侦测到 Bean 配置文件中的`<aop:aspectj-autoproxy>` 元素时, 会自动为与 AspectJ切面匹配的 Bean 创建代理.

### 有哪写类型的通知（Advice） | 用 AspectJ 注解声明切面

-  要在 Spring 中声明 AspectJ切面, 只需要在 IOC 容器中将切面声明为 Bean 实例. 当在 Spring IOC 容器中初始化 AspectJ切面之后, Spring IOC 容器就会为那些与 AspectJ切面相匹配的 Bean 创建代理. 
-  在 AspectJ注解中, 切面只是一个带有 [@Aspect ](/Aspect ) 注解的 Java 类.  
-  通知是标注有某种注解的简单的 Java 方法. 
-  AspectJ支持 5 种类型的通知注解: 
   - @Before: 前置通知, 在方法执行之前执行
   - @After: 后置通知, 在方法执行之后执行
   - @AfterRunning: 返回通知, 在方法返回结果之后执行
   - @AfterThrowing: 异常通知, 在方法抛出异常之后
   - @Around: 环绕通知, 围绕着方法执行

### AOP 有哪些实现方式？

实现 AOP 的技术，主要分为两大类：

- 静态代理 - 指使用 AOP 框架提供的命令进行编译，从而在编译阶段就可生成 AOP 代理类，因此也称为编译时增强； 
   - 编译时编织（特殊编译器实现）
   - 类加载时编织（特殊的类加载器实现）。
- 动态代理 - 在运行时在内存中“临时”生成 AOP 动态代理类，因此也被称为运行时增强。 
   - JDK 动态代理
   - CGLIB

### Spring AOP 实现原理

`Spring`的`AOP`实现原理其实很简单，就是通过**动态代理**实现的。如果我们为`Spring`的某个`bean`配置了切面，那么`Spring`在创建这个`bean`的时候，实际上创建的是这个`bean`的一个代理对象，我们后续对`bean`中方法的调用，实际上调用的是代理类重写的代理方法。而`Spring`的`AOP`使用了两种动态代理，分别是**JDK的动态代理**，以及**CGLib的动态代理**。

**一）JDK动态代理**

**Spring默认使用JDK的动态代理实现AOP，类如果实现了接口，Spring就会使用这种方式实现动态代理**。熟悉`Java`语言的应该会对`JDK`动态代理有所了解。`JDK`实现动态代理需要两个组件，首先第一个就是`InvocationHandler`接口。我们在使用`JDK`的动态代理时，需要编写一个类，去实现这个接口，然后重写`invoke`方法，这个方法其实就是我们提供的代理方法。然后`JDK`动态代理需要使用的第二个组件就是`Proxy`这个类，我们可以通过这个类的`newProxyInstance`方法，返回一个代理对象。生成的代理类实现了原来那个类的所有接口，并对接口的方法进行了代理，我们通过代理对象调用这些方法时，底层将通过反射，调用我们实现的`invoke`方法。

**（二）CGLib动态代理**

`JDK`的动态代理存在限制，那就是被代理的类必须是一个实现了接口的类，代理类需要实现相同的接口，代理接口中声明的方法。若需要代理的类没有实现接口，此时`JDK`的动态代理将没有办法使用，于是`Spring`会使用`CGLib`的动态代理来生成代理对象。`CGLib`直接操作字节码，生成类的子类，重写类的方法完成代理。

> #### JDK的动态代理
>  
> **（一）实现原理**
>  
> `JDK`的动态代理是基于**反射**实现。`JDK`通过反射，生成一个代理类，这个代理类实现了原来那个类的全部接口，并对接口中定义的所有方法进行了代理。当我们通过代理对象执行原来那个类的方法时，代理类底层会通过反射机制，回调我们实现的`InvocationHandler`接口的`invoke`方法。**并且这个代理类是Proxy类的子类**（记住这个结论，后面测试要用）。这就是`JDK`动态代理大致的实现方式。
>  
> **（二）优点**
>  
> 1. `JDK`动态代理是`JDK`原生的，不需要任何依赖即可使用；
> 2. 通过反射机制生成代理类的速度要比`CGLib`操作字节码生成代理类的速度更快；
> 
 
> **（三）缺点**
>  
> 1. 如果要使用`JDK`动态代理，被代理的类必须实现了接口，否则无法代理；
> 2. `JDK`动态代理无法为没有在接口中定义的方法实现代理，假设我们有一个实现了接口的类，我们为它的一个不属于接口中的方法配置了切面，`Spring`仍然会使用`JDK`的动态代理，但是由于配置了切面的方法不属于接口，为这个方法配置的切面将不会被织入。
> 3. `JDK`动态代理执行代理方法时，需要通过反射机制进行回调，此时方法执行的效率比较低；
> 
 
> #### CGLib动态代理
>  
> **（一）实现原理**
>  
> `CGLib`实现动态代理的原理是，底层采用了`ASM`字节码生成框架，直接对需要代理的类的字节码进行操作，生成这个类的一个子类，并重写了类的所有可以重写的方法，在重写的过程中，将我们定义的额外的逻辑（简单理解为`Spring`中的切面）织入到方法中，对方法进行了增强。而通过字节码操作生成的代理类，和我们自己编写并编译后的类没有太大区别。
>  
> **（二）优点**
>  
> 1. 使用`CGLib`代理的类，不需要实现接口，因为`CGLib`生成的代理类是直接继承自需要被代理的类；
> 2. `CGLib`生成的代理类是原来那个类的子类，这就意味着这个代理类可以为原来那个类中，所有能够被子类重写的方法进行代理；
> 3. `CGLib`生成的代理类，和我们自己编写并编译的类没有太大区别，对方法的调用和直接调用普通类的方式一致，所以`CGLib`执行代理方法的效率要高于`JDK`的动态代理；
> 
 
> **（三）缺点**
>  
> 1. 由于`CGLib`的代理类使用的是继承，这也就意味着如果需要被代理的类是一个`final`类，则无法使用`CGLib`代理；
> 2. 由于`CGLib`实现代理方法的方式是重写父类的方法，所以无法对`final`方法，或者`private`方法进行代理，因为子类无法重写这些方法；
> 3. `CGLib`生成代理类的方式是通过操作字节码，这种方式生成代理类的速度要比`JDK`通过反射生成代理类的速度更慢；


### 有哪些不同的AOP实现

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gi8nr8kv0fj31kw0onwg3.jpg#id=ehbsU&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

### Spring AOP and AspectJ AOP 有什么区别？

- Spring AOP 基于动态代理方式实现，AspectJ 基于静态代理方式实现。
- Spring AOP 仅支持方法级别的 PointCut；提供了完全的 AOP 支持，它还支持属性级别的 PointCut。

### 过滤器和拦截器的区别

> [https://segmentfault.com/a/1190000022833940](https://segmentfault.com/a/1190000022833940)


拦截器它是链式调用，一个应用中可以同时存在多个拦截器`Interceptor`， 一个请求也可以触发多个拦截器 ，而每个拦截器的调用会依据它的声明顺序依次执行。

1.  实现方式不同
过滤器和拦截器 底层实现方式大不相同，`过滤器` 是基于函数回调的，`拦截器` 则是基于Java的反射机制（动态代理）实现的。 
2.  使用范围不同
我们看到过滤器 实现的是 `javax.servlet.Filter` 接口，而这个接口是在`Servlet`规范中定义的，也就是说过滤器`Filter` 的使用要依赖于`Tomcat`等容器，导致它只能在`web`程序中使用。
而拦截器(`Interceptor`) 它是一个`Spring`组件，并由`Spring`容器管理，并不依赖`Tomcat`等容器，是可以单独使用的。不仅能应用在`web`程序中，也可以用于`Application`、`Swing`等程序中。 
3.  触发时机不同
过滤器`Filter`是在请求进入容器后，但在进入`servlet`之前进行预处理，请求结束是在`servlet`处理完以后。
拦截器 `Interceptor` 是在请求进入`servlet`后，在进入`Controller`之前进行预处理的，`Controller` 中渲染了对应的视图之后请求结束。 
4.  拦截的请求范围不同 
5.  注入bean 情况不同 
6.  控制执行顺序不同 

## 五、数据访问

### Spring对JDBC的支持

JdbcTemplate简介

- 为了使 JDBC 更加易于使用, Spring 在 JDBC API 上定义了一个抽象层, 以此建立一个 JDBC 存取框架
- 作为 Spring JDBC 框架的核心， JDBCTemplate 的设计目的是为不同类型的 JDBC 操作提供模板方法。每个模板方法都能控制整个过程，并允许覆盖过程中的特定任务。通过这种方式，可以在尽可能保留灵活性的情况下，将数据库存取的工作量降到最低。

### Spring 支持哪些 ORM 框架

Hibernate、iBatis、JPA、JDO、OJB

## 六、事务

### Spring 中的事务管理

作为企业级应用程序框架,，Spring 在不同的事务管理 API 之上定义了一个抽象层，而应用程序开发人员不必了解底层的事务管理 API，就可以使用 Spring 的事务管理机制

Spring 既支持**编程式事务管理**，也支持**声明式的事务管理**

- 编程式事务管理：将事务管理代码嵌入到业务方法中来控制事务的提交和回滚，在编程式管理事务时，必须在每个事务操作中包含额外的事务管理代码，属于硬编码
- 声明式事务管理：大多数情况下比编程式事务管理更好用。它将事务管理代码从业务方法中分离出来，以声明的方式来实现事务管理。事务管理作为一种横切关注点，可以通过 AOP 方法模块化。Spring 通过 Spring AOP 框架支持声明式事务管理，**声明式事务又分为两种：** 
   - 基于XML的声明式事务
   - 基于注解的声明式事务

### 事务管理器

Spring 并不直接管理事务，而是提供了多种事务管理器，他们将事务管理的职责委托给 Hibernate 或者 JTA 等持久化机制所提供的相关平台框架的事务来实现。

Spring 事务管理器的接口是 `org.springframework.transaction.PlatformTransactionManager`，通过这个接口，Spring 为各个平台如 JDBC、Hibernate 等都提供了对应的事务管理器，但是具体的实现就是各个平台自己的事情了。

#### Spring 中的事务管理器的不同实现

**事务管理器以普通的 Bean 形式声明在 Spring IOC 容器中**

-  在应用程序中只需要处理一个数据源, 而且通过 JDBC 存取 
```java
org.springframework.jdbc.datasource.DataSourceTransactionManager
```
 

-  在 JavaEE 应用服务器上用 JTA(Java Transaction API) 进行事务管理 
```
org.springframework.transaction.jta.JtaTransactionManager
```
 

-  用 Hibernate 框架存取数据库 
```
org.springframework.orm.hibernate3.HibernateTransactionManager
```
 

**事务管理器以普通的 Bean 形式声明在 Spring IOC 容器中**

### 用事务通知声明式地管理事务

- 事务管理是一种横切关注点
- 为了在 Spring 2.x 中启用声明式事务管理，可以通过 tx Schema 中定义的 <tx:advice> 元素声明事务通知，为此必须事先将这个 Schema 定义添加到 <beans> 根元素中去
- 声明了事务通知后，就需要将它与切入点关联起来。由于事务通知是在 <aop:config> 元素外部声明的, 所以它无法直接与切入点产生关联，所以必须在 <aop:config> 元素中声明一个增强器通知与切入点关联起来.
- 由于 Spring AOP 是基于代理的方法，所以只能增强公共方法。因此, 只有公有方法才能通过 Spring AOP 进行事务管理。

### 用 [@Transactional ](/Transactional ) 注解声明式地管理事务 

- 除了在带有切入点，通知和增强器的 Bean 配置文件中声明事务外，Spring 还允许简单地用 [@Transactional ](/Transactional ) 注解来标注事务方法 
- 为了将方法定义为支持事务处理的，可以为方法添加 [@Transactional ](/Transactional ) 注解，根据 Spring AOP 基于代理机制， **只能标注公有方法.**
- 可以在方法或者类级别上添加 [@Transactional ](/Transactional ) 注解。当把这个注解应用到类上时， 这个类中的所有公共方法都会被定义成支持事务处理的 
- 在 Bean 配置文件中只需要启用 `<tx:annotation-driven>`元素, 并为之指定事务管理器就可以了
- 如果事务处理器的名称是 transactionManager, 就可以在 `<tx:annotation-driven>` 元素中省略 `transaction-manager` 属性，这个元素会自动检测该名称的事务处理器

### 事务传播属性

- 当事务方法被另一个事务方法调用时， 必须指定事务应该如何传播。例如：方法可能继续在现有事务中运行，也可能开启一个新事务，并在自己的事务中运行
- 事务的传播行为可以由传播属性指定，Spring 定义了 7  种类传播行为：
| 传播行为 | 意义 |
| --- | --- |
| PROPAGATION_MANDATORY | 表示该方法必须运行在一个事务中。如果当前没有事务正在发生，将抛出一个异常 |
| PROPAGATION_NESTED | 表示如果当前正有一个事务在进行中，则该方法应当运行在一个嵌套式事务中。被嵌套的事务可以独立于封装事务进行提交或回滚。如果封装事务不存在，行为就像PROPAGATION_REQUIRES一样。 |
| PROPAGATION_NEVER | 表示当前的方法不应该在一个事务中运行。如果一个事务正在进行，则会抛出一个异常。 |
| PROPAGATION_NOT_SUPPORTED | 表示该方法不应该在一个事务中运行。如果一个现有事务正在进行中，它将在该方法的运行期间被挂起。 |
| PROPAGATION_SUPPORTS | 表示当前方法不需要事务性上下文，但是如果有一个事务已经在运行的话，它也可以在这个事务里运行。 |
| PROPAGATION_REQUIRES_NEW | 表示当前方法必须在它自己的事务里运行。一个新的事务将被启动，而且如果有一个现有事务在运行的话，则将在这个方法运行期间被挂起。 |
| PROPAGATION_REQUIRES | 表示当前方法必须在一个事务中运行。如果一个现有事务正在进行中，该方法将在那个事务中运行，否则就要开始一个新事务。 |


### Spring 支持的事务隔离级别
| 隔离级别 | 含义 |
| --- | --- |
| ISOLATION_DEFAULT | 使用后端数据库默认的隔离级别。 |
| ISOLATION_READ_UNCOMMITTED | 允许读取尚未提交的更改。可能导致脏读、幻影读或不可重复读。 |
| ISOLATION_READ_COMMITTED | 允许从已经提交的并发事务读取。可防止脏读，但幻影读和不可重复读仍可能会发生。 |
| ISOLATION_REPEATABLE_READ | 对相同字段的多次读取的结果是一致的，除非数据被当前事务本身改变。可防止脏读和不可重复读，但幻影读仍可能发生。 |
| ISOLATION_SERIALIZABLE | 完全服从ACID的隔离级别，确保不发生脏读、不可重复读和幻影读。这在所有隔离级别中也是最慢的，因为它通常是通过完全锁定当前事务所涉及的数据表来完成的。 |


事务的隔离级别要得到底层数据库引擎的支持，而不是应用程序或者框架的支持；

Oracle 支持的 2 种事务隔离级别，Mysql支持 4 种事务隔离级别。

### 设置隔离事务属性

用 [@Transactional ](/Transactional ) 注解声明式地管理事务时可以在 [@Transactional ](/Transactional ) 的 isolation 属性中设置隔离级别 

在 Spring 事务通知中, 可以在 `<tx:method>` 元素中指定隔离级别

### 设置回滚事务属性

-  默认情况下只有未检查异常(RuntimeException和Error类型的异常)会导致事务回滚，而受检查异常不会。 
-  事务的回滚规则可以通过 [@Transactional ](/Transactional ) 注解的 rollbackFor和 noRollbackFor属性来定义，这两个属性被声明为 Class[] 类型的，因此可以为这两个属性指定多个异常类。  
   - rollbackFor：遇到时必须进行回滚
   - noRollbackFor： 一组异常类，遇到时必须不回滚

### 超时和只读属性

- 由于事务可以在行和表上获得锁， 因此长事务会占用资源，并对整体性能产生影响
- 如果一个事物只读取数据但不做修改，数据库引擎可以对这个事务进行优化
- 超时事务属性：事务在强制回滚之前可以保持多久，这样可以防止长期运行的事务占用资源
- 只读事务属性：表示这个事务只读取数据但不更新数据，这样可以帮助数据库引擎优化事务

**设置超时和只读事务属性**

- 超时和只读属性可以在 [@Transactional ](/Transactional ) 注解中定义，超时属性以秒为单位来计算 

列出两种方式的示例：

```java
@Transactional(propagation = Propagation.NESTED, timeout = 1000, isolation = Isolation.READ_COMMITTED, rollbackFor = Exception.class)
```

```xml
	<tx:advice id="txAdvice" transaction-manager="txManager">
		<!-- the transactional semantics... -->
		<tx:attributes>
			<!-- all methods starting with 'get' are read-only -->
			<tx:method name="get*" read-only="true" propagation="REQUIRES_NEW" isolation="READ_COMMITTED" timeout="30" no-rollback-for="java.lang.ArithmeticException"/>
			<!-- other methods use the default transaction settings (see below) -->
			<tx:method name="*"/>
		</tx:attributes>
	</tx:advice>

    <!-- ensure that the above transactional advice runs for any execution
        of an operation defined by the FooService interface -->
    <aop:config>
        <aop:pointcut id="fooServiceOperation" expression="execution(* x.y.service.FooService.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="fooServiceOperation"/>
    </aop:config>
```

## 七、MVC

### Spring MVC 框架有什么用？

Spring Web MVC 框架提供 **模型-视图-控制器** 架构和随时可用的组件，用于开发灵活且松散耦合的 Web 应用程序。 MVC 模式有助于分离应用程序的不同方面，如输入逻辑，业务逻辑和 UI 逻辑，同时在所有这些元素之间提供松散耦合。

### Spring MVC的优点

- 可以支持各种视图技术，而不仅仅局限于JSP
- 与Spring框架集成（如IoC容器、AOP等）
- 清晰的角色分配：前端控制器(dispatcherServlet) ，请求到处理器映射（handlerMapping)，处理器适配器（HandlerAdapter)， 视图解析器（ViewResolver）
- 支持各种请求资源的映射策略

### Spring MVC 的运行流程 | DispatcherServlet描述

在整个 Spring MVC 框架中， DispatcherServlet 处于核心位置，负责协调和组织不同组件以完成请求处理并返回响应的工作

SpringMVC 处理请求过程：

1. 若一个请求匹配 DispatcherServlet 的请求映射路径(在 web.xml中指定)，WEB 容器将该请求转交给 DispatcherServlet 处理
2. DispatcherServlet 接收到请求后, 将根据请求信息(包括 URL、HTTP方法、请求头、请求参数、Cookie 等)及 HandlerMapping 的配置找到处理请求的处理器(Handler)。可将 HandlerMapping 看成路由控制器， 将 Handler 看成目标主机
3. 当 DispatcherServlet 根据 HandlerMapping 得到对应当前请求的 Handler 后，通过 HandlerAdapter 对 Handler 进行封装，再以统一的适配器接口调用 Handler
4. 处理器完成业务逻辑的处理后将返回一个 ModelAndView 给 DispatcherServlet，ModelAndView 包含了视图逻辑名和模型数据信息
5. DispatcherServlet 借助 ViewResoler 完成逻辑视图名到真实视图对象的解析
6. 得到真实视图对象 View 后, DispatcherServlet 使用这个 View 对ModelAndView 中的模型数据进行视图渲染

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gi8nrg3furj316o0rs3zx.jpg#id=s2lH5&originHeight=1000&originWidth=1536&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

### Spring的Controller是单例的吗？多线程情况下Controller是线程安全吗？

controller默认是单例的，不要使用非静态的成员变量，否则会发生数据逻辑混乱。正因为单例所以不是线程安全的

```java
@Controller
//@Scope("prototype")
public class ScopeTestController {

    private int num = 0;

    @RequestMapping("/testScope")
    public void testScope() {
        System.out.println(++num);
    }

    @RequestMapping("/testScope2")
    public void testScope2() {
        System.out.println(++num);
    }

}
```

我们首先访问 `http://localhost:8080/testScope`，得到的答案是`1`；
然后我们再访问 `http://localhost:8080/testScope2`，得到的答案是 `2`。

接下来我们再来给`controller`增加作用多例 `@Scope("prototype")`

我们依旧首先访问 `http://localhost:8080/testScope`，得到的答案是`1`；
然后我们再访问 `http://localhost:8080/testScope2`，得到的答案还是 `1`。

**单例是不安全的，会导致属性重复使用**。

#### 解决方案

1. 不要在controller中定义成员变量
2. 万一必须要定义一个非静态成员变量时候，则通过注解@Scope(“prototype”)，将其设置为多例模式。
3. 在Controller中使用ThreadLocal变量

## 八、注解

### 什么是基于Java的Spring注解配置? 给一些注解的例子

基于Java的配置，允许你在少量的Java注解的帮助下，进行你的大部分Spring配置而非通过XML文件。

以[@Configuration ](/Configuration ) 注解为例，它用来标记类可以当做一个bean的定义，被Spring IOC容器使用。 

另一个例子是@Bean注解，它表示此方法将要返回一个对象，作为一个bean注册进Spring应用上下文。

```java
@Configuration
public class StudentConfig {
    @Bean
    public StudentBean myStudent() {
        return new StudentBean();
    }
}
```

### 怎样开启注解装配？

注解装配在默认情况下是不开启的，为了使用注解装配，我们必须在Spring配置文件中配置 `<context:annotation-config/>` 元素。

### Spring MVC 常用注解:

##### [@Controller ](/Controller ) 

在SpringMVC 中，控制器Controller 负责处理由DispatcherServlet 分发的请求，它把用户请求的数据经过业务处理层处理之后封装成一个Model ，然后再把该Model 返回给对应的View 进行展示。在SpringMVC 中只需使用[@Controller ](/Controller ) 标记一个类是Controller ，然后使用[@RequestMapping ](/RequestMapping ) 和[@RequestParam ](/RequestParam ) 等一些注解用以定义URL 请求和Controller 方法之间的映射，这样的Controller 就能被外界访问到。 

##### [@RequestMapping ](/RequestMapping ) 

RequestMapping是一个用来处理请求地址映射的注解，可用于类或方法上

##### [@RequestMapping ](/RequestMapping ) 

Spring Framework 4.3 之后引入的基于HTTP方法的变体

- `@GetMapping`
- `@PostMapping`
- `@PutMapping`
- `@DeleteMapping`
- `@PatchMapping`

##### [@PathVariable ](/PathVariable ) 

用于将请求URL中的模板变量映射到功能处理方法的参数上，即取出uri模板中的变量作为参数

##### [@RequestParam ](/RequestParam ) 

使用@RequestParam绑定请求参数值，在处理方法入参处使用@RequestParam可以把请求参数传递给请求方法

- value：参数名
- required：是否必须。默认为true, 表示请求参数中必须包含对应的参数，若不存在，将抛出异常

##### [@RequestBody ](/RequestBody ) 

[@RequestBody ](/RequestBody ) 表明方法参数应该绑定到HTTP请求体的值 

##### [@ResponseBody ](/ResponseBody ) 

[@Responsebody ](/Responsebody ) 表示该方法的返回结果直接写入HTTP response body中 

一般在异步获取数据时使用，在使用@RequestMapping后，返回值通常解析为跳转路径，加上@Responsebody后返回结果不会被解析为跳转路径，而是直接写入HTTP response body中。比如异步获取 json 数据，加上@Responsebody后，会直接返回 json 数据。

##### @Resource和[@Autowired ](/Autowired ) 

@Resource和@Autowired都是做bean的注入时使用，其实@Resource并不是Spring的注解，它的包是javax.annotation.Resource，需要导入，但是Spring支持该注解的注入。

- 共同点：两者都可以写在字段和 setter 方法上。两者如果都写在字段上，那么就不需要再写 setter 方法。
- 不同点 
   - [@Autowired ](/Autowired ) 为 Spring 提供的注解，[@Autowired ](/Autowired ) 注解是按照类型（byType）装配依赖对象，默认情况下它要求依赖对象必须存在，如果允许 null 值，可以设置它的 required 属性为 false。如果我们想使用按照名称（byName）来装配，可以结合 [@Qualifier ](/Qualifier ) 注解一起使用 
   - [@Resource ](/Resource ) 默认按照 ByName 自动注入，由 J2EE 提供，需要导入包 `javax.annotation.Resource`。[@Resource ](/Resource ) 有两个重要的属性：name 和 type，而 Spring 将@ Resource 注解的 name 属性解析为bean 的名字，而 type 属性则解析为 bean 的类型。所以，如果使用 name 属性，则使用 byName 的自动注入策略，而使用 type 属性时则使用 byType 自动注入策略。如果既不制定 name 也不制定 type 属性，这时将通过反射机制使用 byName 自动注入策略。 

##### [@ModelAttribute ](/ModelAttribute ) 

方法入参标注该注解后, 入参的对象就会放到数据模型中

##### [@SessionAttribute ](/SessionAttribute ) 

将模型中的某个属性暂存到**HttpSession**中，以便多个请求之间可以共享这个属性

##### [@CookieValue ](/CookieValue ) 

@CookieValue可让处理方法入参绑定某个Cookie 值

##### [@RequestHeader ](/RequestHeader ) 

请求头包含了若干个属性，服务器可据此获知客户端的信息，通过@RequestHeader即可将请求头中的属性值绑定到处理方法的入参中

### @Component, @Controller, @Repository, [@Service ](/Service ) 有何区别？ 

- @Component：将 java 类标记为 bean。它是任何 Spring 管理组件的通用构造型。Spring 的组件扫描机制可以将其拾取并将其拉入应用程序环境中
- @Controller：将一个类标记为 Spring Web MVC 控制器。标有它的 Bean 会自动导入到 IoC 容器中
- @Service：此注解是组件注解的特化。它不会对 [@Component ](/Component ) 注解提供任何其他行为。你可以在服务层类中使用 [@Service ](/Service ) 而不是 @Component，因为它以更好的方式指定了意图 
- @Repository：这个注解是具有类似用途和功能的 [@Component ](/Component ) 注解的特化。它为 DAO 提供了额外的好处。它将 DAO 导入 IoC 容器，并使未经检查的异常有资格转换为 Spring DataAccessException。 

### [@Required ](/Required ) 注解有什么作用 

这个注解表明bean的属性必须在配置的时候设置，通过一个bean定义的显式的属性值或通过自动装配，若@Required注解的bean属性未被设置，容器将抛出 BeanInitializationException。示例：

```java
public class Employee {
    private String name;
    @Required
    public void setName(String name){
        this.name=name;
    }
    public string getName(){
        return name;
    }
}
```

### [@Autowired ](/Autowired ) 注解有什么作用 

@Autowired默认是按照类型装配注入的，默认情况下它要求依赖对象必须存在（可以设置它required属性为false）。[@Autowired ](/Autowired ) 注解提供了更细粒度的控制，包括在何处以及如何完成自动装配。它的用法和@Required一样，修饰setter方法、构造器、属性或者具有任意名称和/或多个参数的PN方法。 

```java
public class Employee {
    private String name;
    @Autowired
    public void setName(String name) {
        this.name=name;
    }
    public string getName(){
        return name;
    }
}
```

### @Autowired和@Resource之间的区别

用途：做bean的注入时使用

-  @Autowired，属于Spring的注解，`org.springframework.beans.factory.annotation.Autowired` 
-  @Resource，不属于Spring的注解，JDK1.6支持的注解，`javax.annotation.Resource` 

共同点：都用来装配bean。写在字段上，或写在setter方法

不同点：[@Autowired ](/Autowired )  默认按类型装配。依赖对象必须存在，如果要允许null值，可以设置它的required属性为false  @Autowired(required=false)，也可以使用名称装配，配合@Qualifier注解 

@Resource默认是按照名称来装配注入的，只有当找不到与名称匹配的bean才会按照类型来装配注入

### [@Qualifier ](/Qualifier ) 注解有什么作用 

当创建多个相同类型的 bean 并希望仅使用属性装配其中一个 bean 时，可以使用 [@Qualifier ](/Qualifier ) 注解和 [@Autowired ](/Autowired ) 通过指定应该装配哪个确切的 bean 来消除歧义。 

### [@RequestMapping ](/RequestMapping ) 注解有什么用？ 

[@RequestMapping ](/RequestMapping ) 注解用于将特定 HTTP 请求方法映射到将处理相应请求的控制器中的特定类/方法。此注释可应用于两个级别： 

- 类级别：映射请求的 URL
- 方法级别：映射 URL 以及 HTTP 请求方法

---

## 九、其他问题

### Spring 框架中用到了哪些设计模式？

- **工厂设计模式** : Spring使用工厂模式通过 `BeanFactory`、`ApplicationContext` 创建 bean 对象。
- **代理设计模式** : Spring AOP 功能的实现。
- **单例设计模式** : Spring 中的 Bean 默认都是单例的。
- **模板方法模式** : Spring 中 `jdbcTemplate`、`hibernateTemplate` 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。
- **包装器设计模式** : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
- **观察者模式:** Spring 事件驱动模型就是观察者模式很经典的一个应用。
- **适配器模式** :Spring AOP 的增强或通知(Advice)使用到了适配器模式、spring MVC 中也是用到了适配器模式适配`Controller`。

## 参考与来源

[https://www.edureka.co/blog/interview-questions/spring-interview-questions/](https://www.edureka.co/blog/interview-questions/spring-interview-questions/)

[https://crossoverjie.top/2018/07/29/java-senior/ThreadPool/](https://crossoverjie.top/2018/07/29/java-senior/ThreadPool/)
