# 我的Spring学习笔记
## 目录简要说明
SpringIOC 介绍SpringIOC的作用及使用方法  
SpringAOP 介绍SpringAOp的作用及使用方法  
Note.md   介绍完整的Spring的作用及使用方法  
## Spring介绍
Spring理念 : 使现有技术更加实用 . 本身就是一个大杂烩 , 整合现有的框架技术.  
特点：控制反转（IOC） 和面向切面编程（AOP）  
官网 : http://spring.io/  
官方下载地址 :https://repo.spring.io/ui/native/libs-release-local/org/springframework/spring/  
GitHub: https://github.com/spring-projects  
**Spring Boot与Spring Cloud**

- Spring Boot 是 Spring 的一套快速配置脚手架，可以基于Spring Boot 快速开发单个微服务;
- Spring Cloud是基于Spring Boot实现的；
- Spring Boot专注于快速、方便集成的单个微服务个体，Spring Cloud关注全局的服务治理框架；
- Spring Boot使用了约束优于配置的理念，很多集成方案已经帮你选择好了，能不配置就不配置 , Spring Cloud很大的一部分是基于Spring Boot来实现，Spring Boot可以离开Spring Cloud独立使用开发项目，但是Spring Cloud离不开Spring Boot，属于依赖的关系。
- SpringBoot在SpringClound中起到了承上启下的作用，如果你要学习SpringCloud必须要学习SpringBoot。
## Spring使用
1. 首先从maven导入依赖包
   > 从maven中找Spring Web MVC，它会包括各种Spring，内容比较全，然后选用的最多的一个即可
   ```xml
   <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.2.0.RELEASE</version>
    </dependency>
   ```
   > 然后spring-jdbc也要导入。从maven搜，找用的最多的复制即可。
   ```xml
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.2.0.RELEASE</version>
    </dependency>
    ```
2. 在resources中新建xml配置文件
   
3. 在xml中对bean进行配置，也可以通过注解实现
4. 在java中进行调用
