# JAVA

JAVA的两个原则：

​	单一原则

​	开闭原则



懒加载: 用的时候才去加载，延迟加载

栈：一些基本类型的变量、数组和对象的引用

堆：对象

static:



链式继承：





jdbc (java database connection): 数据库连接

# 日志系统

Log4j:  直接记录日志的日志框架

jul:   java自带的一个日志记录的技术,直接使用

jcl: commons-logging    

​	在没有log4j的依赖情况下,是用jul

​	如果有了log4j则使用log4j

slf4j:

​	通过绑定器绑定一个具体的日志框架来完成日志记录

spring4 :

​	使用的是JCL  优先使用：Log4j， 然后 JUL

```
LOGGING_IMPL_LOG4J_LOGGER,
"org.apache.commons.logging.impl.Jdk14Logger",
"org.apache.commons.logging.impl.Jdk13LumberjackLogger",
"org.apache.commons.logging.impl.SimpleLog"
```

spring5:

​	使用的是 spring-jcl  --先使用的JUL

```
private static LogApi logApi = LogApi.JUL;
switch (logApi) {
   case LOG4J:
      return Log4jDelegate.createLog(name);
   case SLF4J_LAL:
      return Slf4jDelegate.createLocationAwareLog(name);
   case SLF4J:
      return Slf4jDelegate.createLog(name);
   default：
      return JavaUtilDelegate.createLog(name);
}
```

mybatis:

​	

```
日志使用顺序
    useSlf4jLogging();
    useCommonsLogging()
    useLog4J2Logging();
    useLog4JLogging();
    useJdkLogging();
    useNoLogging();
  
```

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



spring 的循环依赖：

​	



beanFactory

FactoryBean

beanDefinition

beanDefinitionRegistry

beanDefinitionReader

BeanPostProcessor:

BeanFactoryPostProcessor:



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





mybatis 解析mapper 有几种方式？

​	4种=》 url，class, resource, package





​	





spring 每次做完查询会关闭session

​	一级缓存： 基于sqlsession

​	二级缓存：



数据库不考虑事务 隔离性会出现的问题：

​	读的问题

​		脏读， 不可重复读， 幻读

​	写的问题

​		 丢失更新：多个人同时修改同一条数据，最后提交的会把之前的提交的数据覆盖

乐观锁：

​	主要解决的问题： 丢失更新

​	解决方案：执行更新之前，会检查本次数据的版本，版本一致则更新

​		



悲观锁（串行）：

​	











## 面试

## mybatis

### 1、mybatis的一级缓存的各种问题

#### 在和 spring整合之后为什么失效

​	    因为mybatis和spring的集成包中扩展了一个类SqlSessionTemplate，这个类在spring容器启动的时候注入给了mapper，这个类代替了原来的 DefaultSqlSession，SqlSessionTemplate的所有查询方法不是直接查询，而是经过一个代理，代理对象增强了查询方法，注意是关闭了session



#### 		2、mybatis的一级缓存技术的底层原理



# 其他



过滤器、拦截器：

​	filter 是servlet规范规定的

​	拦截器是spring容器内的





http：

rpc():

asm:



前后端分离开发：

前端： 页面（数据）显示



后端：操作数据



# 面试

1.我是xxx工作xxx年， 先后在xxx公司工作，先后做过多少项目

2、简单介绍项目：

​     为了解决什么问题，开发了一套什么系统。该系统有哪些部分组成。

​     先介绍项目的整体架构，参与某个模块的开发， 说一下 这个模块的业务设计

3、java的专业技能

4、最擅长什么，说下

 	对xxx有所研究



1、java的跨平台原理：

​		java通过不同系统，不同版本，不同位数的java虚拟机（jvm）,来屏蔽不同的系统指令集差异，

​		而对外提供统一的接口（java API）.

​		简化：java 通过jvm来屏蔽不同系统指令集的差异，通过通用api开发程序

2、java 中 int数据 占几个字节：

​		int 占 4个字节，32位

​		boolean 占  1位

3、面向对象的特性

​	封装、多态、继承、抽象

​	封装：将对象封装成高度自治和相对封闭的个体，一个类，属性私有，提供get和set方法

​    抽象：找出事物的相似和共性之处，抽象出公共属性。

​	继承：父子关系

​	多态：

​		实现机制：编译期间不确定调用对象，运行期间才会确定

​	原则：回答抽象的问题的时候，要举例说明



4、基本数据类型 和  包装类型

​		8中基本数据类型

​		每个基本数据类型，都会一一对应包装类型

​		装箱和拆箱

​		装箱：基本数据类型 -》 包装类型

​		拆箱：包装类型 --》基本数据类型

​		基本数据类型，不具备面向对象的特性

5、== 和equals

​	== : 判断两个变量的值是否相等。 基本数据类型变量 ==比较值==，引用数据类型比较引用==内存的首地址==

​	equals: 比较两个对象长的是否一样

6、String 和StringBuilder, StringBuffer

​		String: ==内容不可变，String 底层使用了一个不可变的字符数组==

​		StringBuilder：内容可变，底层使用的是可变的字符数组，==线程不安全，效率快==

​		StringBuffer：内容可变，底层使用的是可变的字符数组，==线程安全==

7、java中的集合

​		Collection(key)

​			List:  有序，可重复（根据equals和hashcode 方法）。

​			Set:  无序，不可重复，

​		Map（key-value）

8、ArrayList  和 LinkedList

​	ArrayList：

​		底层使用的是数组（是一块地址连续的内存），查询快，插入删改慢

​	LinkedList:

​		底层使用的是链表（是一块地址不连续的内存），查询慢，插入删改快

9、hashMap 和hashTable

​	共同点： 都可以存储key-value 数据

​	不同点：

​		hashMap：

​			null 可以为key,线程不安全，效率高

​		hashTable:

​			null 不可以为key,线程安全，效率低

​		concurrentHashMap: 线程安全，效率相对较高

10、拷贝文件的工具类使用字节流还是字符流

​	字符流： 只能是文本

​	字节流： 二进制数组

11、线程的几种实现方式：

​		继承thread类：扩展性差

​		实现runnable接口

12、线程池的作用：

​		限定线程个数，不会导致由于线程过多，导致系统运行缓慢或崩溃

13、常用设计模式：

​		设计模式：解决特定问题的设计方法

​		单例：		

​		工厂：springIOC

​			对象的创建，交给一个工厂

​		代理：springAOP

14、http Get post	

​	相同：

​		都是http 请求方式，get -》获取资源  post->修改资源

​	不同:

​		get：

​			提交请求会在地址栏中显示

​			传输数据大小有限制

​			安全性低

​		post：

​			提交请求不会在地址栏中显示

​			传输数据大小没有限制

​			安全性高

15、Servlet

​	server applet: 

​		服务器端程序，交互式的浏览和修改数据，生成动态web内容

​	cookie 和session:

​		cookie:

​			客户端记录信息

​		session:

​			服务器端记录信息

16：MVC   model  view  controller

​	

数据库：

关系型数据库三范式：

​	一：表中每一列都不可分割

​	二：主键

​	三：外键

反三范式：

​	为了效率查询，设置重复字段



事务（ACID）：操作序列

​	原子性：操作不可分割，要么都成功，要么都失败

​	一致性：要么都成功，要么都失败，失败要回滚

​	隔离性：事务开始后，不能受其他事务干扰

​	持久性：事务开始后，不能终止

# CSS

```
/*特殊情况， 块级元素 如果这个盒子啊，没有宽度 则padding 不会撑开盒子*/
```

# win10系统

	关于Windows10系统重装，您需要准备一个8G以上容量u盘，并按照以下步骤操作：
1 备份u盘原有数据并格式化u盘
2 在电脑上打开以下链接，点击立即下载工具，将微软官方Win10镜像工具下载到本地硬盘路径：https://dell.to/2ttJ6iS
3 双击运行下载的镜像工具程序，按照提示接收协议，并选中“为另一台电脑创建安装介质”选项，点击下一步
4 先取消勾选“对这台电脑使用推荐的选项”，手动选择版本为：中文（简体）---Windows10家庭中文版---64位（x64）
5 选择使用的介质为u盘并点击下一步，之后等待镜像下载到u盘中，下载完成后镜像工具会将u盘自动生成为系统安装介质
6 将u盘插入需要重装系统的电脑，开机后连续敲击F12键，然后选择UEFI Options下的usb选项，选择通过u盘启动进行系统重装

关于如何制作并使用win10 USB安装镜像, 图文教程参考：https://dell.to/3aIVKx8
视频教程请参考 http://v.youku.com/v_show/id_XMTMzODg4NTg3Mg==.html
【注意】重装系统的时候资料可能会丢失，需要提前做好备份呢





# springboot&springCloud

## eureka：

​	服务的注册与发现



CAP 定理

 Consistency  ---一致性

​	写操作之后的读操作，必须返回该值。（多台服务器，写操作之后的同步问题）

 Availability  ---可用性

​	要收到用户的请求，服务器就必须给出回应。（多台服务器，数据如果未同步完成，会导致数据有问题）

 Partition tolerance ---分区容错性

​	服务器（在不同的地区）之间通信是有可能出错的

C和A之间的矛盾

​		多台服务器无法同时做到一致性和可用性。系统设计时只能选择一个目标。如果追求一致性，那么无法保证所有节点的可用性；如果追求所有节点的可用性，那就没法做到一致性。



### eureka对比Zookeeper：

Zookeeper在设计的时候遵循的是CP原则

​	leader 选举，在选举期间，服务器处于不可用状态

 Eureka在设计的时候遵循的是AP原则

​	各个节点之间是平等的，只要有一台eureka可用，服务就可用



Hystrix：

​	



Oauth2.0

# 微信

微信appid ： wx5462f474f82923de

