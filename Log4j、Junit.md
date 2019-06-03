# 一、Log4j

## 1. Log4j 入门

- 写代码的过程中，免不了要输出各种调试信息。在没有使用任何日志工具之前，都会使用 **System.out.print()** 来输出相关信息。但是有很多缺点：

  1. 不知道打出来的信息是来自于哪个类，哪个线程；
  2. 不知道前后两句输出信息间隔了多少时间；
  3. 无法关闭调试信息，一旦System.out.print() 多了以后，到处都是输出，增加定位自己需要信息的难度。

- 使用 **Log4j** 进行日志输出，有如下好处：

  1. 知道是来自于哪个类里面的日志，比如：log4j.Log4jTest
  2. 知道是来自于哪个线程的日志，比如：[main]
  3. 日志级别可观察，一共有6个级别：TRACE DEBUG INFO WARN ERROR TATAL
  4. 日志输出级别范围可控制，如只输出高于DEBUG级别的，那么TRACE级别的日志就不会输出
  5. 每句日志消耗的毫秒数（最前面的数字）可观察，便于进行性能计算

- 代码讲解：

  ```java
  package log4j;
  
  import org.apache.log4j.BasicConfigurator;
  import org.apache.log4j.Level;
  import org.apache.log4j.Logger;
  
  public class Log4jTest {
      // 基于类的名称获取日志对象
  	static Logger logger = Logger.getLogger(Log4jTest.class);
  	public static void main(String[] args) throws InterruptedException {
  		BasicConfigurator.configure(); // 进行默认配置
  		logger.setLevel(Level.DEBUG); // 设置日志输出级别
          // 进行不同级别的日志输出
  		logger.trace("跟踪信息");
  		logger.debug("调试信息");
  		logger.info("输出信息");
  		Thread.sleep(1000);    // 为了便于观察前后日志输出的时间差
  		logger.warn("警告信息");
          logger.error("错误信息");
          logger.fatal("致命信息");
  	}
  }
  
  /*
  输出结果：
  0 [main] DEBUG log4j.Log4jTest  - 调试信息
  0 [main] INFO log4j.Log4jTest  - 输出信息
  1000 [main] WARN log4j.Log4jTest  - 警告信息
  1000 [main] ERROR log4j.Log4jTest  - 错误信息
  1000 [main] FATAL log4j.Log4jTest  - 致命信息
  */
  ```



## 2. Log4j.properties 配置讲解

- 在src目录下添加 log4j.properties 文件：

  - `log4j.rootLogger=debug, stdout, R`：设置日志输出的等级为debug，低于debug就不会输出了；设置日志输出到两种地方，分别叫做 stdout 和 R

  - ```
    log4j.appender.stdout=org.apache.log4j.ConsoleAppender
    log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
    log4j.appender.stdout.layout.ConversionPattern=%5p [%t] (%F:%L) - %m%n
    ```

    1. 第一个地方 stdout，输出到控制台
    2. 输出格式为：%5p [%t] (%F:%L) - %m%n

  - ```
    log4j.appender.R=org.apache.log4j.RollingFileAppender
    log4j.appender.R.File=example.log
    log4j.appender.R.MaxFileSize=100KB
    log4j.appender.R.MaxBackupIndex=5
    
    log4j.appender.R.layout=org.apache.log4j.PatternLayout
    log4j.appender.R.layout.ConversionPattern=%p %t %c - %m%n
    ```

    1. 第二个地方R，以滚动的方式输出到文件，文件名是example.log，文件最大100k，最多滚动5个文件
    2. 输出格式为：%p %t %c - %m%n

- **输出格式解释**：

  - %c：输出日志信息所属的类的全名
  - %d：输出日志的时间点的日期或时间，默认格式为ISO8601，也可以在其后指定格式，比如：%d{yyy-MM-dd HH:mm:ss}，输出类似：2002-10-18- 22：10：28
  - %f：输出日志信息所属的类的类名
  - %l：输出日志事件的发生位置，即输出日志信息的语句处于它所在的类的第几行
  - %m：输出代码中指定的信息，如 log(message)中的message
  - %n：输出一个回车换行符，windows平台为“rn”，Unix平台为“n”
  - %p：输出优先级，即 DEBUG INFO WARN ERROR FATAL
  - %r：输出自应用启动到输出该日志信息所耗费的毫秒数
  - %t：输出产生该日志事件的线程名
  - 所以：`%5p[%t](%F:%L) - %m%n` 表示：宽度是5的优先等级 [线程名称] (类名：行号) - 信息 换行

- 修改 Log4jTest.java

  ```java
  public class Log4jTest {
  	static Logger logger = Logger.getLogger(Log4jTest.class);
  
  	public static void main(String[] args) throws InterruptedException {
          // 配置方式不同，采用指定配置文件
  		PropertyConfigurator.configure("D:\\EclipseProject\\log4j\\log4j.properties");
  		for (int i = 0; i < 5000; i++) {
              logger.trace("跟踪信息");
              logger.debug("调试信息");
              logger.info("输出信息");
              logger.warn("警告信息");
              logger.error("错误信息");
              logger.fatal("致命信息");
          }
  	}
  }
  
  /*
  输出结果：
  ERROR [main] (Log4jTest.java:18) - 错误信息
  FATAL [main] (Log4jTest.java:19) - 致命信息
  DEBUG [main] (Log4jTest.java:15) - 调试信息
   INFO [main] (Log4jTest.java:16) - 输出信息
   WARN [main] (Log4jTest.java:17) - 警告信息
  */
  ```

  1. 输出在控制台，并且格式有所变化，如图所示，会显示哪个类的哪一行输出的信息
  2. 不仅仅在控制台有输出，日志也输出到了  "D:\\EclipseProject\\log4j\example.log" 位置



# 二、Junit

## 1. Junit 入门

- 最开始写代码都是用main() 函数来进行运行，测试所写的代码是否按期望运行，通过main()方法运行来进行测试有以下问题：比如新开发了一个方法，是对3个数求和，那么问题至少有两个：
  1. 要在原来测试的基础上修改，可能破坏原来的测试逻辑；
  2. 测试成功还是失败都不知道，只能通过肉眼观察，如果测试量很大，是很难看出来的。
- 为了应付测试的需求，我们就需要使用Junit测试框架来进行测试工作。
- Junit的好处：
  - 新增加的测试，对原来的测试没有影响；
  - 如果测试失败了，会立刻得到通知。

