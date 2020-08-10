## Spring

### OK:

### NOT OK -> OK

1. 什么是Spring: Spring是一个轻量级的控制反转（IOC）和面向切面编程（AOP）的框架。

2. Spring 7大模块： https://www.cnblogs.com/xiaobaizhiqian/p/7616453.html

3. SpringBoot:

   3.1 构建一切

   3.2 基于SpringBoot可以快速开发单个微服务

   3.3 约定大于配置

   3.4 前提: 完全掌握Spring以及SpringMVC！

4. SpringCloud:

   4.1 SpringCloud是SpringBoot基于实现的。

   4.2 协调一切（多个微服务）。

5. Spring Ioc:

   5.1 Overview:

   ##### Spring init objects by configuration depending on whatever values we provide.

   ![image-20200423154805067](/Users/linzeyang/Library/Application Support/typora-user-images/image-20200423154805067.png)

   5.2 控制反转（IOC）： 主动性（控制）从程序员转移到用户。程序员不用去管理对象的创建，系统的耦合性大大降低，可以更加专注于业务上。

   ###### 比如A类依赖B类（要调用B类的构造方法），没有控制反转的话，如果业务上B类构造方法需要修改（比如入参增加一个变量），那A类相应的也要修改（程序员修改），否则在A中无法获得B新加的变量。有了控制反转，A类只注入B类，具体使用B类的哪个（构造）方法，可以抛给用户去决定。这样就实现了解耦。

   5.3 

   1）创建IOC容器：

   ```java
   ApplicationContext context = new ClassPathXmlApplicationContext("circleConfig.xml"); // step 1
   ```

   2）实现注入：

   XML CONFIG:

   ```XML
   <bean id="point1" class="com.lzy.brain.Point">
     <property name="x" value="1"/>
     <property name="y" value="2"/>
   </bean>
   ```

   ```java
   Point p = context.getBean("point1",Point.class); // step 2
   // 结合上一个代码块，context.getBean("point1",Point.class)执行后，对象p中的值x就被初始化为1，y被初始化为2
   ```

   3）Lazy-initialized Beans: 

   如果没有懒加载（默认），那么在容器创建时，spring就会去对应xml里找到对应的class，去初始化class（包括class的无参构造函数调用，预设值初始化。）

   4）The creation of the bean(无参构造函数调用，预设值初始化等) happens when the applicationContext(Spring Bean Factory) is initialized 

   (step 1), not when the 'getBean()' is happening (step 2)

   5）scope:

   - singleton: 无论getBean多少次，只要取的是同一个class，都只会生成同一个bean。如下：

     ![image-20200423171516058](/Users/linzeyang/Library/Application Support/typora-user-images/image-20200423171516058.png)

     “triangleBean”被创建2次，构造函数只被调用一次，且t1.setI(1)后，t2.getI()也等于1（而不是0）。t1,t2是同一个对象。

   - propotype：getBean多少次，就生成多少个不同的bean。

     ![image-20200423171725982](/Users/linzeyang/Library/Application Support/typora-user-images/image-20200423171725982.png)

     “triangleBean”被创建2次，构造函数被调用2次，且t1.setI(1)后，t2.getI()依然为null。t1,t2是2个不同的对象。

     ###### 当然可以用hashcode来判断t1,t2

     6）1.8(Container Extension Points): If you want to implement some custom logic after the Spring container finishes instantiating, configuring, and initializing a bean, you can plug in one or more custom `BeanPostProcessor` implementations.

     7) @Component注解： 代替XML中的BeanDefinition。如在Circle类头部加上 @Component,就不需要在XML中写如下：

   ```xml
   <bean id="circleBean" class="com.lzy.brain.Circle"/>
   ```

   Spring MVC中，@Controller,@Service,@Repository注解不仅告诉Spring这是个Bean，还提供额外信息（即这个Bean的角色），这个和AOP有关。

   6）注解：

   - @Autowired注解：我的理解是spring会自动扫描类中含有@Autowired的属性，方法或对象，并将xml配置文件中与这个属性对应的Bean自动注入到类中，不需要用户在xml写注入过程。

   - @Autowired注解在构造函数上：将构造函数入参中的Bean自动注入。

   - @Autowired注解在setter上：将setter入参中的Bean自动注入。

     ###### 当 Spring 容器启动时，AutowiredAnnotationBeanPostProcessor 将扫描 Spring 容器中所有 Bean，当发现 Bean 中拥有 @Autowired 注释时就找到和其匹配（默认按类型匹配）的 Bean，并注入到对应的地方中去。  

     ###### 按照上面的配置，Spring 将直接采用 Java 反射机制对 Boss 中的 car 和 office 这两个私有成员变量进行自动注入。所以对成员变量使用 @Autowired 后，您大可将它们的 setter 方法（setCar() 和 setOffice()）从 Boss 中删除。 

   - @Primary: 因为@Autowired默认是byType去注入bean,但是config中可能存在多个相同类型的bean，那么spring就不知道用哪个了。@Primary就是选个优先注入的。

   - @Quilifier: 使@Autowired也可以以byName的方式去注入Bean

   - @Resource: DI by Name.

   - @Resource的作用相当于@Autowired，只不过@Autowired按照byType自动注入。在注入类型为接口类型，而该接口有多个实现类时，用@Resource代替@Autowired很好用。具体见：https://www.cnblogs.com/think-in-java/p/5474740.html。

   7） 例子：

   1）@Autowired+XML:

   在java类中表明需要被自动装配的类，并且在xml中声明让spring去找所有的annotations。这样spring就去xml找到与@Autowired类型相同的bean config（这里是Point），然后注入到Circle Class中。如果XML里不止一个相同类型，可以用@Qualifier或者@Resource.

   ```java
   public Class Circle{
     @Autowired
   	Point point;
     ...
   }
   
   ```

   ```xml
   <context:annotation-config />
   
   <bean id="pointBean" class="com.lzy.brain.Point">
     <property name="x" value="0"></property>
     <property name="y" value="0"></property>
   </bean>
   
   ```

   上面代码相当于去掉以下注释部分：

   ```xml
       <bean id="circleBean" class="com.lzy.brain.Circle">
   <!--        <property name="point" ref="pointBean"></property>-->
       </bean>
   ```

   2) @Autowired+@Component+XML:

   如果想再把非注释部分也去掉，就可以用@Component注解，去声明一个Bean（Bean的Id即为类名首字母小写），但是需要在XML声明‘component-scan’，对应启动类getBean()也要改：

   ```java
   @Component
   public class Circle {
     @Autowired
   	Point point;
     ...
   }
   ```

   ```xml
   <context:component-scan base-package="com.lzy.brain"/>
   <context:annotation-config />
   ```

   ```java
   ApplicationContext context = new ClassPathXmlApplicationContext("myConfig.xml");
   Circle circleBean = context.getBean("circle",Circle.class);
   ```

   3) @Configuration+@Beans+Annotations

   xml里的声明如‘<context:annotation-config />’可以用一个@Configuration替代，‘<context:component-scan base-package="com.lzy.brain"/>’可以用@ComponentScan("com.lzy.brain")替代。这样就可以用一个类完全代替xml，这个类为配置类。如果想在这个类中初始化Bean，就用@Beans：

   ```java
   @Configuration
   @ComponentScan("com.lzy.brain")
   public class AppConfig {
       @Bean
       public Point point(){
           Point p =  new Point();
           p.setX(1);
           return p;
       }
     ...
   }
   ```

6. Spring AOP:

   6.1 AOP HelloWorld!

​	1）导入AOP包

​	2）创建Aspect Class如下：

```java
package com.lzy.aop.aspect;

import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;

@Aspect
public class LoggingAspect {
    @Before("execution(public String getName())")
    public void loggingAdvice(){
        System.out.println("Advice Run! Get method called!");
    }
}
```

该类作用：loggingAdvice()方法会在public String getName()调用前被调用。

​    	 3）XML相关配置：将LoggingAspect声明为Spring Bean以及让Spring去扫描并解析@Aspect相关注解：

```xml
<aop:aspectj-autoproxy />
...
<bean name="LoggingAspect" class="com.lzy.aop.aspect.LoggingAspect">
</bean>
```

​		4）AOP：Aspect Oriented Programming. 可以看做是OOP的一种补充，也许OOP中很多个类都要去调用某公用方法，AOP则是创建一个Aspect Config类，将公用方法写到Aspect Config类中，以后无论哪个类中的那个方法需要调用该公用方法，就去Config类中注册。这样有2个好处，一个是不用在每个类中都调用公用方法，另一个是假设公用方法有修改，也不用在每个类中去改。

​	6.2 PointCuts & WildCards

​		1) PointCut: A predicate that matches join points. 。让Spring知道advice具体要执行到项目中的哪个方法上。

​        2) WildCards: 通配符，解决一个aspect 方法解决多个point的问题。

​	6.3 More pointcuts:

​        1) within: 在within内的所有类的方法，只要被触发，就会执行对应的aspect方法。

```java
@Aspect
public class LoggingAspect {
	@Pointcut("within(com.lzy.aop.*)")
	public void allAop() {
	}
	@Before("allAop()")
	public void loggingAdviceOne(){
	System.out.println("Advice One Run! Get method called!");
	}
}
```

​		2）多个pointCut作用于一个aspect方法，取并集：

```java
@Aspect
public class LoggingAspect {
	@Pointcut("within(com.lzy.aop.*)")
	public void allAop() {
	}
	@Before("allAop()")
	public void loggingAdviceOne(){
	System.out.println("Advice One Run! Get method called!");
	}
	@Before("allAop() && allSetters()")
	public void loggingAdviceOne(){
	System.out.println("Advice One Run! Get method called!");
	}
}
```

​		3) args:

​	如：

```java
@Before("args(s)")
public void allStrArgs(String s) {
  System.out.println("The param is "+ s);
}
```

以上代码做了2件事：一个是当程序执行的方法有且只有一个String类型的参数时，触发advice：allStrArgs。第二件事是获得该方法的参数，并作为该advice的参数并拿来使用。

6.4 JoinPoint

​	1)  In Spring AOP, a join point always represents a method execution.

​	2）Use the joinPoint to get the information about the method that triggered the advice：joinPoint.getTarget()方法即获得该方法的实例，并可以在advice中使用。

6.5 Spring AOP Advice Types:

-  @Before
- @After(无论是否异常，都会执行)
- @AfterReturning
- @AfterThrowing
- @Around

### STILL NOT OK：

##### 1.6.1

- ##### Startup and Shutdown Callbacks

- ##### Shutting Down the Spring IoC Container Gracefully in Non-Web Applications

#####  1.6.2

-  `ApplicationContextAware` and `BeanNameAware`

##### 1.6.3

- Other `Aware` Interfaces

##### 1.8.3

- FactoryBean

##### bean生命周期

![image-20200423232056463](/Users/linzeyang/Library/Application Support/typora-user-images/image-20200423232056463.png)

When to use XML as AOP config?(Tutorial34)