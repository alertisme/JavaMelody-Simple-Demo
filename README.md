# 简介
JavaMelody-Simple-Demo 是使用 JavaMelody 监控 Java web 做性能分析的一个 Demo 项目主要目的是为了方便刚接触 JavaMelody 的童鞋能够快速上手，并且看到实际效果好做出决策是否使用该项目。
 
 # 关于[JavaMelody](#https://github.com/javamelody/javamelody/wiki)  
 JavaMelody 是一个开源项目，他的目标是监控 测试 & 生产环境中的 Java 或 Java EE 应用程序。根据用户对应用程序的使用情况来衡量和计算应用程序实际操作统计信息的工具。
 
 # 如何使用
 
 - 一 在 mavne 项目的 POM.xml 里面加入如下 Jar 包依赖
 ```XML
         <dependency>
             <groupId>net.bull.javamelody</groupId>
             <artifactId>javamelody-core</artifactId>
             <version>1.70.0</version>
         </dependency>
         <dependency>
             <groupId>org.jrobin</groupId>
             <artifactId>jrobin</artifactId>
             <version>1.5.9</version>
         </dependency>
```
 - 二 在 web.xml 里面加入如下内容，其中 applicationContext.xml 是你本来就有的 spring 配置文件，根据实际情况适当修改名字就好。这里有一点多说一句，就是由于监控信息属于敏感信息肯定线上不能谁都能看到，所以在这里加上用户认证。
 ```XML
 <context-param>
     <param-name>contextConfigLocation</param-name>
     <param-value>
       classpath:net/bull/javamelody/monitoring-spring-datasource.xml
       classpath:net/bull/javamelody/monitoring-spring-aspectj.xml
       classpath*:applicationContext.xml
     </param-value>
   </context-param>
 
   <listener>
     <listener-class>net.bull.javamelody.SessionListener</listener-class>
   </listener>
 
   <filter>
     <filter-name>javamelody</filter-name>
     <filter-class>net.bull.javamelody.MonitoringFilter</filter-class>
     <async-supported>true</async-supported>
     <!--========= 这里是设置访问性能监控页面的权限设置 ========-->
     <init-param>
       <param-name>authorized-users</param-name>
       <param-value>admin:123456, user:pwd</param-value>
     </init-param>
     <!--========= 这里是设置访问性能监控页面的权限设置 ========-->
   </filter>
 
   <filter-mapping>
     <filter-name>javamelody</filter-name>
     <url-pattern>/*</url-pattern>
     <dispatcher>REQUEST</dispatcher>
     <dispatcher>ASYNC</dispatcher>
   </filter-mapping>

```
 - 三 检查你的 Spring 配置文件里面是否配置了 AOP ，一般都会有的。
 ```xml
     <aop:aspectj-autoproxy/>
```
 
 ##  首页图表统计效果图
![首页图表统计](https://github.com/alertisme/JavaMelody-Simple-Demo/blob/master/src/main/webapp/static/imgs/main-chart.png "首页图表统计")
![首页图表统计](https://github.com/alertisme/JavaMelody-Simple-Demo/blob/master/src/main/webapp/static/imgs/main-chart2.png "首页图表统计")

 ##  统计列表数据效果图
![统计列表数据效果图](https://github.com/alertisme/JavaMelody-Simple-Demo/blob/master/src/main/webapp/static/imgs/main-list.png "统计列表数据效果图")
![统计列表数据效果图-详情](https://github.com/alertisme/JavaMelody-Simple-Demo/blob/master/src/main/webapp/static/imgs/main-list-info.png "统计列表数据效果图")
![统计列表数据效果图-详情-2](https://github.com/alertisme/JavaMelody-Simple-Demo/blob/master/src/main/webapp/static/imgs/main-list-info2.png "统计列表数据效果图")

##  JDBC 连接统计效果图
![JDBC 连接统计效果图](https://github.com/alertisme/JavaMelody-Simple-Demo/blob/master/src/main/webapp/static/imgs/jdbc.png "JDBC 连接统计效果图")
![JDBC 连接统计效果图 info](https://github.com/alertisme/JavaMelody-Simple-Demo/blob/master/src/main/webapp/static/imgs/jdbc2.png "JDBC 连接统计效果图 info")

##  DB 当前进程统计效果图
![DB 当前进程统计效果图](https://github.com/alertisme/JavaMelody-Simple-Demo/blob/master/src/main/webapp/static/imgs/db.png "DB 当前进程统计效果图")

##  Spring Bean 统计效果图 
![Spring Bean 统计效果图](https://github.com/alertisme/JavaMelody-Simple-Demo/blob/master/src/main/webapp/static/imgs/bean.png "Spring Bean 统计效果图")




