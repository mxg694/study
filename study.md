# JAVA

JAVA的两个原则：

​	单一原则

​	开闭原则



懒加载: 用的时候才去加载，延迟加载

栈：一些基本类型的变量、数组和对象的引用

堆：对象

static:



链式继承：







# 日志系统

Log4j:  直接记录日志的日志框架

jul:   java自带的一个日志记录的技术,直接使用

jcl: commons-logging    

​	在没有log4j的依赖情况下,是用jul

​	如果有了log4j则使用log4j

slf4j:

​	通过绑定器绑定一个具体的日志记录来完成日志记录

​	





# Spring

## IOC

spring IOC（控制反转） 和DI（依赖注入）的区别

​	DI是实现IOC的一种技术实现

​	IOC：是一种设计原则



​	依赖：A.class有个属性B.class  A依赖B      B是A的一个属性

​	注入：A.class有个属性B.class  B注入到A  B是A的一个属性

​		setter 注入：

​		constructor 注入：

​	自动装配：

​		byName：基于bean的名称

​		byType：  基于bean的类型



​	实现IOC的思路

​		利用配置描述类之间的依赖关系，由容器去解析配置关系，维护对象间的依赖关系



AOP和Spring AOP

​	AOP:是一种思想

​	spring AOP：是一种实现

AOP与OOP：

​	oop：面向对象编程

​	aop：面向切面编程

​	开发过程中会产生一些横切性问题，这些横切问题对主业务逻辑关系不大

​	这些横切问题不会影响到主逻辑，而且散落在代码的各个部分，难以维护

AOP的编程思想：

​	把这些横切性问题和主业务逻辑分开，达到与主业务逻辑解耦的过程





## 设计模式

### 代理

​	什么是代理：

​		增强一个对象的功能

​	代理的名词：

​		代理对象：增强的目标对象的对象

​		目标对象：被增强的对象（代理对象代理的对象）

​	java中实现代理的两种方式

​		静态代理

​			继承: 代理对象继承目标对象，重写需要增强的方法

​				缺点：代理类过多，非常复杂

​			聚合：目标对象和代理对象实现同一个接口，代理对象要包含目标对象

​				缺点：代理类过多，比继承少些

​		动态代理	

​			通过接口反射生成一个类文件，然后动态编译成class文件，然后利用classloader把动态编译的				class文件加载到jvm中，最后通过反射把类实例化

​		JDK动态代理：

​			通过接口反射得到字节码，然后把字节码转成class

​			



BeanFactory 和FactoryBean 的区别和联系

​	beanFactory:

​		是一个工厂，创建bean

​		在Spring中，所有的Bean都是由BeanFactory(也就是IOC容器)来进行管理的。

​	FactoryBean:  

​		是一个bean，是一个能生产或者修饰对象生成的工厂Bean

​		

​		如果一个类实现了FactoryBean,那么spring容器当中存在两个对象

​		一个是getObject()返回的对象，一个是当前对象

​		getObject() 得到对象存的是当前类的指定的名字

​		当前对象是 +"&" +当前类的名字



bean： 受到spring 管理的一个java对象

对象：  java对象





BeanDefination:

​	是spring bean的所有模板，其数据结构包含了springbean可能需要的所有属性

BeanPostProcessor:

​	后置处理器：



ImportSelector



full（@） :  全配置类， 会进行cglib 代理

lite:  部分配置类   不会进行cglib 代理



spring 对不同bean的处理

普通的bean:   扫描完成之后注册

importselector: 先放到configurationClasses中，然后注册， loadbean

Registar：   importBeanDefinitionRegistrars  然后注册

import普通类：





# mybatis:

spring 每次做完查询会关闭session

​	一级缓存： 基于sqlsession

​	二级缓存

# 其他



过滤器、拦截器：

​	filter 是servlet规范规定的

​	拦截器是spring容器内的





http：

rpc():

asm: