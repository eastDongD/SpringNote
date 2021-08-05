# Spring 的IOC
## 简要介绍
- **IOC 即控制反转**，原来由程序员控制的，现在通过配置文件，交由用户控制。根据用户的需要，创建不同的对象，采用不同的实现。
  > 比如说原来数据库由MySQL实现，现在用户想用Oracle实现，则程序员需要将每一个用DaoImplByMySQL实例化的Dao改为用DaoImplByOracle。工程大时，任务量将会特别大。但是Spring通过对属性的set方法实现的IOC则可以通过配置文件，选用相应的方法。  
- **DI（依赖注入）是实现Ioc的一种方法**  
  > 思路：原本需要程序员去控制的，用户需求变后，程序员要去改（如原来在Service中直接确定选用的DaoImpl，用户想法变后，程序员要去改service中选用的Dao）现在控制反转，交给用户去控制（在Service中，不直接确定DaoImpl，而是通过set方法，要用户去调用set方法，选择DaoImpl），现在由用户用set方法选择DaoImpl，所以即使用户想法改变，原来的Service也不需要变。  

*控制反转是一种通过描述（XML或注解）并通过第三方去生产或获取特定对象的方式。在Spring中实现控制反转的是IoC容器，其实现方法是依赖注入（Dependency Injection,DI).[参考博客](https://blog.csdn.net/qq_33369905/article/details/106647330)*

## IoC的实现方式
**实现IoC的思路**  
> 作用：原本类的实例必须通过new进行初始化，然后在其构造函数中对各个属性进行赋值。但是在web中，有很多初始化后的值是相似的，（可以理解为有一个学生类，但是web中就用3个学生的数据初始化类）。如果用new方法，一个学生长了一岁，则要去所有包含该学生对象的文件中，对new方法的参数进行修改。但是如果用Spring，则可以在配置文件中修改一次，其他获取该学生对象都是从配置文件中获取的，不用修改，给程序猿带来了春天。（总而言之就是通过配置中的内容对类直接进行初始化）

> Spring容器在初始化时先读取配置文件，根据配置文件或元数据创建与组织对象存入容器中，程序使用时再从Ioc容器中取出需要的对象。

**IoC的实现包括3中方式。首先是最基本的XML配置。然后为了方便查看，可以在类或者类的成员上写一个@属性名表示这个类或者对象用了xml配置文件中的某种方法。即通过注解代替了部分xml配置（需要在xml配置中添加注解支持）。最后是一种纯注解实现的方式，用注解表明当前类已经是\<beans>标签下,下面的注解相当于添加bean**
### 使用XML进行配置
#### 使用步骤
1. 在pom.xml中添加spring依赖。*这个可以直接从maven仓库中搜Spring web mvc 那一项，找个版本加入即可*
2. 正常写原来的实体类如Student。根据DI的注入方式不同，有的需要无参构造函数和set方法，有的需要有参构造函数
3. 在resources下新建xml配置文件（右键新建xml Spring 配置文件会自动生成<beans&#62;标签，接下来加入<bean&#62;即可）。对需要的类（类内部有参数的，或者作为其他类的成员的），在配置文件中通过<bean&#62;标签引入一套数据。  
    如：
   ```xml
       <bean id="school" class="com.dong.IoCByXML.School">
        <property name="name" value="XX中学"/>
        <property name="address" value="XX省XX市XX县"/>
      </bean>
   ```
4. 然后在service，test等类中获取时通过Spring获取容器中已经创建好的对象。
    ```java
        ApplicationContext context = new ClassPathXmlApplicationContext("IocByXML.xml");
        Student student = context.getBean("student", Student.class);
   ```
#### 标签说明
- <bean&#62; 代表new一个新的对象，其中的id属性代表对象的名字。class属性用于指向对象类型。value和ref用于对该对象的属性进行赋值。value用于基本类型，ref用于自己新建的类型。
- &#60;constructor-arg&#62;  代表用构造器方法进行注入  
- &#60;property&#62;  代表用set方法进行注入  
- index 代表按照位置进行赋值  
- name 代表按照名字进行赋值  
- type 代表按照类型进行赋值  
- value 用基本类型进行赋值
- ref 用新建的类型的对象进行赋值

***不用记这些，IDEA在xml有提示***  
***前面说了如何注入基本类型如String和自定义的类(value和ref），但是对于数组，list，Map等的注入稍有不同。其核心思路是在<property&#62;标签中不写value和ref，然后在两个<property&#62;之间写相应的注入，如<list&#62;对应List，<array&#62;对应数组。（打了<后，IDEA会提示怎么写）。***
#### 通过XML，用DI实现IOC的方式包括四种
- 构造器注入
  > 在&#60;bean&#62;中对成员变量进行赋值时用&#60;constructor-arg&#62;标签，要求有有参构造函数
- set注入
  > 在&#60;bean&#62;中对成员变量进行赋值时用&#60;property&#62;标签，同时要求必须有无参构造函数及成员变量的set方法（对set方法的方法名有要求，一般为set+属性首字母大写，对boolean类型稍有不同，但是用自动生成的set方法可以正常运行）。
- p注入
  > p代表property，指用set方法，需要有无参的构造函数才能用，并且要引入p命名空间。(IDEA上，输入xmlns:p=后会有提示的，不用记忆)
    ```xml
      xmlns:p="http://www.springframework.org/schema/p"  
      <bean id="simpleStudent4" class="com.dong.IoCByXML.SimpleStudent" p:name="小明p" p:school-ref="school"/>
    ```
- c注入
  > c代表constructor-arg，需要有有参的构造函数才能用，并且要引入c命名空间。(IDEA上，输入xmlns:c=后会有提示的，不用记忆)  
    ```xml
      xmlns:c="http://www.springframework.org/schema/c"  
      <bean id="simpleStudent5" class="com.dong.IoCByXML.SimpleStudent" c:name="小明c" c:school-ref="school"/>
    ```
  
#### 注意事项
- IOC通过beans.xml创建对象时机：
    ```java
    ApplicationContext context=new ClassPathXmlApplicationContext("beans.xml");
    ```
    执行这行代码时，会根据beans.xml的内容，创建所有的对象。一个<bean>调用一次构造函数，创建一个对象。

### 使用注解

### 零配置实现IoC。


