# 1. IDEA如何搭建Maven

- 下载、安装、配置：<https://www.cnblogs.com/xihehua/p/9639045.html>



# 2. Maven基本概念

- Maven基于项目对象模型（POM，project object model）概念，Maven利用一个中央信息片段能管理一个项目的构建、报告和文档等步骤。
- Maven是一个项目管理和综合工具，可以对Java项目进行构建、依赖管理。
- 现在的JavaWeb项目中，绝大多数都是采用maven结构的项目，而对于maven支持最好的开发工具为IDEA。
- **为什么要用Maven**：
  - 在开发中经常需要依赖第三方的包，包与包之间存在依赖关系，版本间还有兼容性问题，有时还要将旧的包升级或降级，当项目复杂到一定程度时包管理变得非常重要。
  - Maven是当前最受欢迎的java项目管理构建自动化综合工具。
- **Maven主要做了两件事**：
  - 统一开发规范与工具
  - 统一管理jar包
- **Maven主要提供了三种功能**：
  1. **依赖的管理**：仅仅通过jar包的几个属性，就能确定唯一的jar包，在指定的文件pom.xml中，只要写入这些依赖属性，就会自动下载并管理jar包。
  2. **项目的构建**：内置很多插件与生命周期，支持多种任务，比如校验、编译、测试、打包、部署、发布...
  3. **项目的知识管理**：管理项目相关的其他内容，比如开发者信息，版本等等。

## 2.1 Maven功能

- 构建（Builds）
- 文档生成（Documentation）
- 报告（Reporting）
- 依赖（Dependencies）
- SCMs
- 发布（Releases）
- 分发（Distribution）
- 邮件列表（mailing list）

概括地说，Maven简化和标准化项目建设过程。处理编译、分配、文档、团队协作和其他任务的无缝连接。Maven增加可重用性并负责建立相关的任务。

## 2.2 Maven目标

Maven主要目标是提供给开发人员：

- 项目是可重复使用、易维护、更容易理解的一个综合模型。
- 插件或交互的工具，这种声明性的模式。

Maven项目的结构和内容在一个XML文件中声明，pom.xml项目对象模型（POM），这是整个Maven系统的基本单元。

## 2.3 约定配置

MavenProjectRoot(项目根目录)
   |----src
   |     |----main
   |     |         |----java ——存放项目的.java文件
   |     |         |----resources ——存放项目资源文件，如spring, hibernate配置文件
   |     |----test
   |     |         |----java ——存放所有测试.java文件，如JUnit测试类
   |     |         |----resources ——存放项目资源文件，如spring, hibernate配置文件
   |----target ——项目输出位置
   |----pom.xml ----用于标识该项目是一个Maven项目

| 目录                               | 目的                                                  |
| ---------------------------------- | ----------------------------------------------------- |
| ${basedir}                         | 存放pom.xml和所有子目录                               |
| ${basedir}/src/main/java           | 项目的Java源代码                                      |
| ${basedir}/src/main/resources      | 项目的资源，比如说property文件、springmvc.xml         |
| ${basedir}/src/test/java           | 项目的测试类，比如说Junit代码                         |
| ${basedir}/src/test/resources      | 测试用的资源                                          |
| ${basedir}/src/main/webapp/WEB-INF | web应用文件目录，web项目的信息，比如存放web.xml、图片 |
| ${basedir}/target                  | 打包输出目录                                          |
| ${basedir}/target/classes          | 编译输出目录                                          |
| ${basedir}/target/test-classes     | 测试编译输出目录                                      |
| Test.java                          | Maven只会自动运行符合该命名规则的测试类               |
| ~/.m2/repository                   | Maven默认的本地仓库目录位置                           |



# 3. 第一个Maven项目

1. 在D盘新建一个MavenProject文件夹
2. 在MavenProject文件夹中新建一个项目根文件夹Maven01
3. 在项目根文件夹Maven01中新建文件夹src->main->java；和一个pom.xml文件
4. 在Maven01->src->main->java中新建一个hello.java文件
5. win+R，cmd，enter进入命令行；进入Maven01文件夹
6. `mvn compile`；之后会在Maven01文件夹中看到target文件夹

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <!--所有的Maven项目都必须配置这四个配置项-->
    <modelVersion>4.0.0</modelVersion>
    <!--groupId指的是项目名的项目组，默认就是包名-->
    <groupId>cn.gacl.maven.hello</groupId>
    <!--artifactId指的是项目中的某一个模块，默认命名方式是"项目名-模块名"-->
    <artifactId>hello-first</artifactId>
    <!--version指的是版本，这里使用的是Maven的快照版本-->
    <version>SNAPSHOT-0.0.1</version>
	
	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<maven.compiler.source>1.8</maven.compiler.source>
		<maven.compiler.target>1.8</maven.compiler.target>
	</properties>
</project>
```

```java
public class hello{
	public static void main(String[] args){
         System.out.println("Hello Maven");
    }
}
```



# 4. Maven POM

## 4.1 POM 基础知识

- POM（project object model, 项目对象模型）是Maven工程的基本工作单元，是一个XML文件，包含了项目的基本信息，用于描述项目如何构建、声明项目依赖，等等。

- 我们需要什么jar包，都可以在pom.xml文件里面添加依赖，然后maven就会帮我们下载到本地仓库里面

- 执行任务或目标时，Maven会在当前目录中查找POM。它读取POM，获取所需的配置信息，然后执行目标，POM中可以指定以下配置：

  - 项目依赖
  - 插件
  - 执行目标
  - 项目构建profile
  - 项目版本
  - 项目开发者列表
  - 相关邮件列表信息

- 在创建POM之前，我们首先需要描述项目组（groupId），项目的唯一ID。所有POM文件都需要project元素和三个必要字段：groupId，artifactId，version。

  | 节点         | 描述                                                         |
  | ------------ | ------------------------------------------------------------ |
  | project      | 工程的根标签                                                 |
  | modelVersion | 模型版本需要设置为4.0                                        |
  | groupId      | 这是工程组的标识。它在一个组织或者项目中通常是唯一的。例如，一个银行组织：com.companyname.project-group拥有所有和银行相关的项目；vivo的外销搜索：com.vivo.oversea.appsearch |
  | artifactId   | 这是工程的标识，它通常是工程的名称，例如：oversea-appsearch。groupId和artifactId一起定义了artifact在仓库中的位置 |
  | version      | 这是工程的版本号。在artifact的仓库中，它用来区分不同的版本   |

## 4.2 父（super）POM

- 父（super）POM是Maven默认的POM。所有的POM都继承自一个父POM（无论是否显示定义了这个父POM）。父POM包含了一些可以被继承的默认设置。因此，当Maven发现需要下载POM中的依赖时，它会到super POM中配置的默认仓库http://repo1.maven.org/maven2 去下载。
- Maven使用effective pom（super pom加上工程自己的配置）来执行相关的目标，它帮助开发者在pom.xml中做尽可能少的配置，当然这些配置可以被重写。



# 5. 利用intellij IDEA 创建多模块Maven项目

- 开发工具：IntelliJ IDEA 2018.3.6
- maven版本：Apache Maven 3.6.1
- tomcat版本：Apache tomcat 9.0.19

## 5.1 项目结构

- multi-module-project 是主工程，里面包含两个模块（Module）:
  1. web-app是应用层，用于界面展示，依赖于web-service的服务；
  2. web-service层是服务层，用于给app层提供服务。

![img](https://images2015.cnblogs.com/blog/736876/201706/736876-20170605221648965-954838262.png)

## 5.2 构建项目

### 5.2.1 Parent Project

- 新建一个空白标准maven project（不要选择create from archetype），file -> new -> project -> 选中maven ->next
- 填写项目坐标：
  - groupId: com.cnblogs.kmpp
  - artifactId: multi-module
- project name: multi-module-project
- 得到一个标准的maven项目，因为该项目是作为一个parent project存在的，可以直接删除src文件夹

### 5.2.2 增加web-app模块（module）

- 右键点击主工程multi-module-project ->new -> module -> 选择maven -> 勾选create from archetype -> 选择org.apache.maven.archetypes:maven-archetype-webapp ->next
- GroupId和Version继承自parent project，这里只填写ArtifactId，填写：web-app 

### 5.2.3 增加web-service模块

- 用同样的方法创建web-service模块（该模块是一个空白maven项目，不要从archetype创建）。

### 5.2.4 最终的项目结构

![1557230704551](https://github.com/RiverLee0101/Notes/blob/master/images/maven-01.png)

## 5.3 添加项目依赖

- 右键点击主工程 -> 选择open module settings（或者F4快捷键）
- ![1557230942037](https://github.com/RiverLee0101/Notes/blob/master/images/maven-02.png)

- 上面的操作是添加web-app对web-service模块的依赖

- 在web-app的pom中添加对web-service的依赖：

  - ```xml
    <dependency>
        <groupId>com.cnblogs.kmpp</groupId>
        <artifactId>web-service</artifactId>
    	<version>1.0-SNAPSHOT</version>
    </dependency>
    ```


## 5.4 部署Tomcat

- 右键项目名 -> open module settings -> facets -> 加号添加一个web -> 修改deployment descriptor的path为web.xml所在路径 -> 修改web resources directories为webapp所在路径 -> 点击artifacts -> web application exploded -> from modules -> 选择刚才创建的项目
- 点击edit configurations -> 加号 - > tomcat server -> local -> deployment -> 加号Artifacts -> ok
- 点击debugger，浏览器中出现“Hello World”, 地址：<http://localhost:8080/TestDemo_war_exploded/>
