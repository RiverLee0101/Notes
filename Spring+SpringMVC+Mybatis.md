# 1. Spring框架

## 1.1 Spring框架基本概念

- Spring框架是Java应用最广的框架，它的成功来源于理念，而不是技术本身，它的理念包括**IOC（Inversion of Control，控制反转）**和 **AOP（Aspect Oriented Programming，面向切面编程）**

- **什么是Spring:**

  1. spring 是一个轻量级的**DI/IoC和AOP**容器的开源框架
  2. spring提倡以**最少侵入**的方式来管理应用中的代码，这意味着我们可以随时安装或者卸载spring

- **IoC（Inverse of Control，控制反转）：**

  - 读作“反转控制”，更好理解，不是什么技术，而是一种设计思想，就是讲原本在程序中手动创建对象的控制权，交由spring来管理。
  - **正控**：若要使用某个对象，需要自己去负责对象的创建
  - **反控**：若要使用某个对象，只需要从spring容器中获取需要使用的对象，不关心对象的创建过程，也就是把创建对象的控制反转给了spring框架

- Spring框架结构：

  ![img](https://upload-images.jianshu.io/upload_images/7896890-a7c003d175bd41af.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  - Data Access/Integration层包含有JDBC、ORM、OXM、JMS和Transaction
  - Web层包含了Web、Web-Servlet、WebSocket、Web-Porlet模块
  - AOP模块提供了一个符合AOP联盟标准的面向切面编程的实现
  - Core Container(核心容器)：包含有Beans、Core、Context和SpEL模块
  - Test模块支持使用JUnit和TestNG对Spring组件进行测试



## 1.2 IOC/DI基本概念

- IOC是spring的基础，全称控制反转（inversion of control），简单说就是创建对象以前由程序员自己new构造方法来调用，变成了交由spring创建对象

  ![img](http://how2j.cn/img/site/step/1876.png)

- DI，全称依赖注入（dependency inject），简单说就是拿到的对象的属性，已经被注入好相关值了，直接使用即可

  ```xml
  	<!--通过关键字“c”即可获取category类，这个类的name已经被注入"category 1"，id被注入“1”-->
  	<bean name="c" class="pojo.Category">
          <property name="name" value="category 1" />
          <property name="id" value="1" />
      </bean>
  
      <!--对product对象，注入一个category对象-->
      <bean name="p" class="pojo.Product">
          <property name="name" value="product 1"/>
          <property name="category" ref="c"/>
      </bean>
  ```

- 其他注解方式：<http://how2j.cn/k/spring/spring-annotation-ioc-di/1067.html>



## 1.3 AOP基本概念

- AOP即Aspect Oriented Program，面向切面编程。在面向切面编程思想里，把功能分为 **核心业务功能** 和 **周边功能**
  - **核心业务：**登录、增删改查数据等都叫核心业务
  - **周边功能：**性能统计、日志、事务管理等等
- 周边功能在spring的面向切面编程AOP思想里，即被定义为**切面**
- 核心业务功能和切面功能分别独立进行开发，然后把切面功能和核心业务功能编制在一起，这就叫AOP



# 2. SpringMVC框架

## 2.1 SpringMVC流程图

![æ­¤å¤è¾å¥å¾ççæè¿°](https://upload-images.jianshu.io/upload_images/226662-4e1e7fec34ec8787?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



## 2.2 Spring MVC工作原理

1. 客户端发送请求到DispatcherServlet（分发器）
2. 由DispatcherServlet控制器查询HanderMapping，找到处理请求的Controller
3. Controller调用业务逻辑处理后，返回ModelAndView
4. DispatcherServlet查询视图解析器，找到ModelAndView指定的视图
5. 视图负责将结果显示到客户端

## 2.3 DispatcherServlet组件类

- **Spring Web** 模型-视图-控制器（MVC）框架是围绕DispatcherServlet设计的，它处理所有的HTTP请求和响应。**Spring Web MVC DispatcherServlet** 的请求处理工作流程如下：

  ![img](http://www.yiibai.com/uploads/images/201701/18/451110124_66519.png)

- 以下是对应于到 **DispatcherServlet** 的传入HTTP请求的时间顺序：

  - 在接收到HTTP请求后，**DispatcherServlet** 会查询 **HandlerMapping** 以调用相应的 **Controller**
  - **Controller** 接受请求并根据使用的**GET** 或 **POST** 方法调用相应的服务方法。服务方法将基于定义的业务逻辑设置模型数据，并将视图名称返回给DispatcherServlet
  - **DispatcherServlet** 将从 **ViewResolver** 获取请求的定义视图
  - 当视图完成，**DispatcherServlet** 将模型数据传递到最终的视图，并在浏览器呈现

  所有上述组件，即：HandlerMapping，Controller 和 ViewResolver 是WebApplicationContext 的一部分，他是普通 ApplicationContext 的扩展，带有Web应用程序所需的一些额外功能。



## 2.4 SpringMVC项目结构

- 工程目录：

  ![1557369759930](C:\Users\11101453\AppData\Roaming\Typora\typora-user-images\1557369759930.png)

- ***web/WEB-INF/web.xml：***

  ```xml
  <servlet>
  	<servlet-name>dispatcher</servlet-name>
      <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
      <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
      <servlet-name>dispatcher</servlet-name>
      <url-pattern>/</url-pattern>
  </servlet-mapping>
  ```

  - 有关<servlet-mapping>的设置，通过这个设置，可以配置哪些类型的URL用哪些servlet来处理
  - 这里的这个<servlet-name>dispatcher要和web/WEB-INF/dispatcher-servlet.xml中的dispatcher对应
  - 这个web.xml的作用就是捕获所有的URL请求，全部交给dispatcher-servlet.xml来处理

- ***web/WEB-INF/dispatcher-servlet.xml：***

  ```xml
  <!--指定去com.springmvc.helloworl这个包里面找controller-->
  <context:component-scan base-package="com.springmvc.helloworld"/>
  
  <!--指定视图解析器-->
  <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
      <!-- 视图的路径 -->
      <property name="prefix" value="/WEB-INF/jsp/"/>
      <!-- 视图名称后缀  -->
      <property name="suffix" value=".jsp"/>
  </bean>
  ```

  - 这个dispatcher-servlet.xml是告诉servlet去哪里找Controller，这里是去com.springmvc.helloworld这个包里找controller
  - 视图解析器作用是把视图约定在/WEB-INF/jsp/***.jsp这个位置

- ***src/com.springmvc.helloworld/HiController.java：***

  ```java
  // controller判断不同的URL去到不同的view
  @Controller
  @RequestMapping("/hi")
  public class HiController {
      @RequestMapping("/say")
      public String say(Model model) { // 参数传入model
          model.addAttribute("name","lijiang"); // 指定model的值
          model.addAttribute("url","www.baidu.com"); // 指定model的值
          return "say";
      }
      @RequestMapping("/laugh")
      public String laugh(){
          return "laugh";
      }
  }
  ```

  - Controller 判断接收到的URL格式，然后决定去哪里找View
  - @Controller 注释将类定义为 Spring MVC 控制器
  - @RequestMapping("/hi") 表示收到的url地址的前面部分
  - @RequestMapping("/say") 表示收到的url地址的后面部分
  - return "say" 表示去到 web/WEB-INF/jsp/say.jsp（跳转view的绝对路径已经在dispatcher-servlet中配置过）

- ***web/WEB-INF/jsp/say.jsp：***

  ```html
  <html>
  <head>
      <title>Title</title>
  </head>
  <body>
  	hello world! I am ${name}<br/>${url}
  </body>
  </html>
  ```

  - Spring MVC 支持许多类型的视图用于不同的表示技术。包括JSP，HTML，PDF，EXCEL工作表，XML，Velocity模板，XSLT，JSON，Atom，和RSS源，JasperReports等。但最常见的是使用JSPL编写的JSP模板
  - 这里的 ${name} 和 ${url} 是在Controller 中设置的属性。可以在视图中显示多个属性



# 3. MyBatis框架

## 3.1 安装MySQL和WorkBench

- 下载MySQL：<https://dev.mysql.com/downloads/mysql/>，解压至文件夹：D:\Program Files\mysql-8.0.16-winx64

- 配置环境变量：

  - 新建 -> 变量名：MYSQL_HOME    变量值：D:\Program Files\mysql-8.0.16-winx64
  - 编辑Path，在结尾加上：%MYSQL_HOME%\bin;

- 以管理员身份运行cmd，输入：mysql -u root -p，回车

- 设置MySQL密码：alter user root@localhost identified by ‘12345’；

- 下载安装workbench

- 创建数据库test：create database test;

- 创建表product_：

  ```sql
  use test;
   
  CREATE TABLE product_ (
    id int(11) NOT NULL AUTO_INCREMENT,
    name varchar(30) ,
    price float ,
    PRIMARY KEY (id)
  ) DEFAULT CHARSET=UTF8;
  ```

- 常用cmd操作数据库命令：<https://blog.csdn.net/m0_37774790/article/details/81007192>



## 3.2 Mybatis框架基本概念

- Mybatis是一款优秀的持久层框架，它支持定制化SQL、储存过程以及高级映射。
- Mybatis避免了几乎所有JDBC代码和手动设置参数以及获取结果集。
- Mybatis可以使用简单的XML或注解来配置和映射原生类型、接口和java的POJO（plain old java object，普通老实java对象）为数据库中的记录。
- 使用Mybatis框架，只需要自己提供SQL语句，其他的工作，诸如建立连接、statement、JDBC相关异常处理等等都交给Mybatis去做了。
- 那些重复性的工作Mybatis也给做了，我们只需要关注在增删改查等操作层面上，把技术细节都封装在了我们看不见的地方。



## 3.3 Mybatis框架基本配置

- **mybatis项目基本结构：**

  ![1557456879099](C:\Users\11101453\AppData\Roaming\Typora\typora-user-images\1557456879099.png)

- ***实体类 Category.java:***

  ```java
  package com.how2java.pojo;
  public class Category {
      private int id;
      private String name;
      public int getId() {return id;}
      public void setId(int id) {this.id = id;}
      public String getName() {return name;}
      public void setName(String name) {this.name = name;}    
  }
  ```

  - 用于映射表 category_

- ***配置文件 mybatis-config.xml:***

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE configuration
          PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-config.dtd">
  <configuration>
      <typeAliases>
          <package name="com.how2java.pojo"/>
      </typeAliases>
      <environments default="development">
          <environment id="development">
              <transactionManager type="JDBC"/>
              <dataSource type="POOLED">
                  <property name="driver" value="com.mysql.jdbc.Driver"/>
                  <property name="url" value="jdbc:mysql://localhost:3306/test?characterEncoding=UTF-8"/>
                  <property name="username" value="root"/>
                  <property name="password" value="12345"/>
              </dataSource>
          </environment>
      </environments>
      <mappers>
          <mapper resource="com/how2java/pojo/Category.xml"/>
      </mappers>
  </configuration>
  ```

  - 配置文件 mybatis-config.xml 的作用：
    - 获取数据库连接实例的数据源（DataSource）和决定事务作用域和控制方式的事务管理器（TransactionManager）
    - environment 元素体中包含了事务管理和连接池的配置
    - mappers 元素则是包含一组映射器（mapper），这些映射器的XML映射文件包含了SQL代码和映射定义信息

- ***配置文件 Category.xml:***

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <mapper namespace="com.how2java.pojo">
      <select id="listCategory" resultType="Category">
          select * from   category_
      </select>
      <insert id="addCategory" parameterType="Category">
          insert into category_ (name) values (#{name})
      </insert>
      <delete id="deleteCategory" parameterType="Category" >
              delete from category_ where id= #{id}
      </delete>
      <select id="getCategory" parameterType="_int" resultType="Category">
              select * from   category_  where id= #{id}
      </select>
      <update id="updateCategory" parameterType="Category" >
              update category_ set name=#{name} where id=#{id}
      </update>
  </mapper>
  ```

  - namespace=“com.how2java.pojo”表示命名空间是com.how2java.pojo
  - sql 语句的 <id> 标识用以后续代码调用
  - resultType 表示返回的数据和Category关联起来

- ***测试类 TestMybatis:***

  ```java
  package com.how2java.pojo;
  import com.how2java.pojo.Category;
   
  public class TestMybatis {
      public static void main(String[] args) throws IOException {
          String resource = "mybatis-config.xml";
          InputStream inputStream = Resources.getResourceAsStream(resource);
          SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
          SqlSession session=sqlSessionFactory.openSession();
           
          List<Category> cs=session.selectList("listCategory");
          for (Category c : cs) {
              System.out.println(c.getName());
          }        
      }
  }
  ```

  - 根据配置文件 mybatis-config.xml 得到sqlSessionFactory
  - 然后根据 sqlSessionFactory 得到session
  - 最后通过session的增删改查等方法根据<id>调用Category.xml中的sql语句



# 4. Spring+Mybatis

## 4.1 Spring+Mybatis整合思路

1. 让Spring管理SqlSessionFactory

   ```xml
   <bean id="sqlSession" class="org.mybatis.spring.SqlSessionFactoryBean">
   	<property name="typeAliasesPackage" value="com.how2java.pojo" />
   	<property name="dataSource" ref="dataSource"/>
   	<property name="mapperLocations" value="classpath:com/how2java/mapper/*.xml"/>
   </bean>
   ```

   1. SqlSessionFactoryFactory有一个唯一的必要属性：用于JDBC的 ***dataSource***
   2. ***mapperLocations ***属性接受多个资源位置。这个属性可以用来指定MyBatis的映射器XML配置文件的位置

2. 让Spring管理mapper对象和dao

   ```xml
   <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
   	<property name="basePackage" value="com.how2java.mapper"/>
   </bean>
   ```

   1. 扫描Mapper类
   2. 自动开启事务，自动关闭sqlsession

3. 让Spring管理数据源（数据库连接池）

   ```xml
   <bean id="dataSource" 			class="org.springframework.jdbc.datasource.DriverManagerDataSource">  
   </bean>
   ```

   

## 4.2 项目结构

![1557567069422](C:\Users\11101453\AppData\Roaming\Typora\typora-user-images\1557567069422.png)





# 5. Spring+SpringMVC+MyBatis框架

## 5.1 SSM框架简介

- ssm框架是spring、spring MVC 和 mybatis 框架的整合，是标准的MVC模式，将整个系统划分为 **DAO层、service层、controller层、显示层** 四层。使用**spring MVC负责请求的转发和视图管理，spring实现业务对象管理，mybatis作为数据对象的持久化引擎**。



## 5.2 SSM框架的系统层次说明

- **项目结构**

​	![1557747265601](C:\Users\11101453\AppData\Roaming\Typora\typora-user-images\1557747265601.png) ![1557747641100](C:\Users\11101453\AppData\Roaming\Typora\typora-user-images\1557747641100.png)

- **持久层：DAO层（mapper）** —— `com.how2java.mapper`

  > DAO层主要做数据持久层的工作，负责 **与数据库进行联络** 的一些任务都封装在此。DAO层的设计首先是设计DAO的接口（`CategoryMapper.java`），然后在Spring的配置文件中定义此接口的实现类（在与此接口对应的xml文件中写sql语句对数据库进行操作），然后就可以在模块中调用此接口来进行数据业务的处理，而不用关心此接口的具体实现类是哪个类，显得结构非常清晰。DAO层的数据源配置，以及有关数据库连接的参数都在Spring的配置文件中进行配置。

- **业务层：Service层** —— `com.how2java.service`

  > Service层主要负责 **业务模块的逻辑应用设计**。首先设计接口（`CategoryService.java`），再设计其实现的类（`CategoryServiceImpl.java`），接着再在Spring的配置文件中配置其实现的关联。这样我们就可以在应用中调用Service接口来进行业务处理。Service层的业务实现，具体要求调用到已定义的DAO层的接口，封装Service层的业务逻辑有利于通用的业务逻辑的独立性和重复利用性，程序显得非常简洁。

- **控制层：Controller（Handler层）** —— `com.how2java.controller`

  > Controller层负责具体的业务模块流程的控制。在此层里面要**调用Service层的接口来控制业务流程**，控制的配置也同样是在Spring的配置文件中进行，针对具体的业务流程，会有不同的控制器，我们具体的设计过程中可以将流程进行抽象归纳，设计出可以重复利用的子单元流程模块，这样不仅使程序结构变得清晰，也大大减少了代码量。

- **显示层：View层 **—— `WEB-INF.jsp`

  > View层与控制层结合比较紧密，需要二者结合起来协同工作。View层主要负责前台jsp页面的表示。

- **各层联系**

  > DAO层，Service层这两个层次都可以单独开发，互相的耦合度很低，这样的一种模式在开发大项目的过程中有其有优势；Controller、View层因为耦合度比较高，因而要结合在一起开发，但是也可以看作一个整体独立于前两个层进行开发。这样，在层与层之间我们只需要知道接口的定义，调用接口即可完成所需要的逻辑单元应用，一切显得非常清晰简单。

- **Service逻辑层设计**

  > Service层是建立在DAO层之上的，建立了DAO层后才可以建立Service层，而Service层又是在Controller层之下的，因为Service层应该既调用DAO的接口，又要提供接口给Controller层的类来进行调用，它刚好处于一个中间层的位置。每个模型都有一个Service接口，每个接口分别封装自己的业务处理方法。



## 5.3 SSM框架整合

- **整合思路：**

  1. **整合dao层：**MyBatis和Spring整合，通过Spring管理Mapper接口。使用Mapper的扫描器自动扫描Mapper接口在Spring中进行注册。（详细见4.1）

     

  2. **整合Service层：**通过Spring管理Service接口。使用配置方式将Service接口配置在Spring配置文件中，实现事务控制。

     ```xml
     <context:component-scan base-package="com.how2java.service" />
     ```

  3. **整合SpringMVC：**由于SpringMVC是Spring的模块，不需要整合。



## 5.4 SSM框架执行流程

1. **`web.xml`**：容器先加载web.xml

2. **`web.xml`**：接着是 Spring 的配置文件 applicationContext.xml 在web.xml里的注册

   ```xml
   <!-- spring的配置文件-->
   <context-param>
   	<param-name>contextConfigLocation</param-name>
   	<param-value>classpath:applicationContext.xml</param-value>
       <!--spring加载多个配置文件-->
       <!-- <param-value>classpath:application-*.xml</param-value> -->
   </context-param>
   <listener>
   	<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
   </listener>
   ```

3. **`applicationContext.xml`**：spring配置文件进行数据库的连接、sqlSession的注册、mapper的扫描等

   ```xml
       <context:annotation-config />
   	<context:component-scan base-package="com.how2java.service" />
   
   	<bean id="dataSource"
             class="org.springframework.jdbc.datasource.DriverManagerDataSource">  
   	  <property name="driverClassName">  
             <value>com.mysql.jdbc.Driver</value>  
   	  </property>  
   	  <property name="url">  
   	      <value>jdbc:mysql://localhost:3306/test?characterEncoding=UTF-8</value>  
   	  </property>  
   	  <property name="username">  
   	      <value>root</value>  
   	  </property>  
   	  <property name="password">  
   	      <value>12345</value>  
   	  </property>  	
   	</bean>
   	
   	<bean id="sqlSession" class="org.mybatis.spring.SqlSessionFactoryBean">
   		<property name="typeAliasesPackage" value="com.how2java.pojo" />
   		<property name="dataSource" ref="dataSource"/>
   		<property name="mapperLocations" value="classpath:com/how2java/mapper/*.xml"/>
   	</bean>
   
   	<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
   		<property name="basePackage" value="com.how2java.mapper"/>
   	</bean>
   ```

4. **`web.xml`**：指定对应的URL去哪里找 dispatcher

   ```xml
   <!-- spring mvc核心：分发servlet -->
   <servlet>
   	<servlet-name>mvc-dispatcher</servlet-name>
   	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
   	<!-- spring mvc的配置文件 -->
   	<init-param>
   		<param-name>contextConfigLocation</param-name>
           <!--dispatcher的位置-->
   		<param-value>classpath:springMVC.xml</param-value>
   	</init-param>
   	<load-on-startup>1</load-on-startup>
   </servlet>
   <servlet-mapping>
   	<servlet-name>mvc-dispatcher</servlet-name>
       <!--包含 / 的URL统一交给上面的dispatcher来处理-->
   	<url-pattern>/</url-pattern>
   </servlet-mapping>
   ```

5. **`springMVC.xml`**：dispatcher 指定去哪里找controller。（根据包中的class的注解 @Controller）

   ```xml
   <context:component-scan base-package="com.how2java.controller">
             <context:include-filter type="annotation" 
             expression="org.springframework.stereotype.Controller"/>
   </context:component-scan>
   ```

6. **`Controller.java`**：controller根据URL决定执行service中的哪个方法，然后返回一个jsp页面

   ```java
       @Autowired
   	CategoryService categoryService;
   
   	@RequestMapping("listCategory")
   	public ModelAndView listCategory(String name){
   		ModelAndView mav = new ModelAndView();
   		Category c = new Category();
   		c.setName(name);
           // 执行service的操作
   		categoryService.addCategory(c);
   		List<Category> cs= categoryService.list();		
   		mav.addObject("cs", cs);	
   		mav.setViewName("listCategory");
   		return mav;
   	}
   ```

7. **`springMVC.xml`**：dispatcher对controller返回的结果进行解析，符合格式的，打开对应的jsp文件

   ```xml
   <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
   	<property name="viewClass"value="org.springframework.web.servlet.view.JstlView" />
       <property name="prefix" value="/WEB-INF/jsp/" />
       <property name="suffix" value=".jsp" />
   </bean>
   ```

   