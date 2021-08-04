# Spring 的IOC
## 简要介绍
- **IOC 即控制反转**，原来由程序员控制的，现在通过配置文件，交由用户控制。根据用户的需要，创建不同的对象，采用不同的实现。
    > 比如说原来数据库由MySQL实现，现在用户想用Oracle实现，则程序员需要将每一个用DaoImplByMySQL实例化的Dao改为用DaoImplByOracle。工程大时，任务量将会特别大。但是Spring通过对属性的set方法实现的IOC则可以通过配置文件，选用相应的方法。  
- **DI（依赖注入）是实现Ioc的一种方法**  
    > 思路：原本需要程序员去控制的，用户需求变后，程序员要去改（如原来在Service中直接确定选用的DaoImpl，用户想法变后，程序员要去改service中选用的Dao）现在控制反转，交给用户去控制（在Service中，不直接确定DaoImpl，而是通过set方法，要用户去调用set方法，选择DaoImpl），现在由用户用set方法选择DaoImpl，所以即使用户想法改变，原来的Service也不需要变。  

*控制反转是一种通过描述（XML或注解）并通过第三方去生产或获取特定对象的方式。在Spring中实现控制反转的是IoC容器，其实现方法是依赖注入（Dependency Injection,DI).*  
参考博客：https://blog.csdn.net/qq_33369905/article/details/106647330

## IoC的实现方式
> Spring容器在初始化时先读取配置文件，根据配置文件或元数据创建与组织对象存入容器中，程序使用时再从Ioc容器中取出需要的对象。

### XML配置

### 使用注解

### 零配置实现IoC。


