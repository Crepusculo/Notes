<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [SSH](#ssh)
- [S S H in SSH](#s-s-h-in-ssh)
- [S S H 在各层](#s-s-h-在各层)
- [Struts](#struts)
   - [Struts](#struts)
   - [M](#m)
   - [V](#v)
   - [C](#c)
- [Spring is](#spring-is)
   - [Spring loc](#spring-loc)
   - [Spring from Struts](#spring-from-struts)
   - [Spring AOP](#spring-aop)
- [Hibernate is](#hibernate-is)
- [ORM is](#orm-is)
- [JDBC is](#jdbc-is)
- [Why we need ORM ?](#why-we-need-orm)
- [ORM has:](#orm-has)
- [ORM's Advantages:](#orms-advantages)
- [Hibernate's Advantages:](#hibernates-advantages)
- [Hibernate Architecture:](#hibernate-architecture)
- [Hibernate properties](#hibernate-properties)
   - [Session Factory](#session-factory)
   - [Session](#session)
   - [Transaction](#transaction)
   - [Query](#query)
   - [Criteria](#criteria)
- [DAO](#dao)
- [CGI is](#cgi-is)
- [Servlet is](#servlet-is)
- [Why not CGI but servlet:](#why-not-cgi-but-servlet)
- [Servlet Architecture](#servlet-architecture)
- [JSP](#jsp)
- [JSP 与 Servlet 的关系](#jsp-与-servlet-的关系)
- [Servlet do:](#servlet-do)
- [MVC](#mvc)
- [MVC Advantages](#mvc-advantages)
- [MVP](#mvp)
- [MVVM](#mvvm)
- [Tomcat](#tomcat)
- [JNDI](#jndi)

<!-- /MDTOC -->
# SSH
struts + spring + hibernate
![4](/assets/4.gif)
# S S H in SSH
对象的调用流程是：
> jsp -> Action(Struts) -> Service(Struts) -> DAO -> Hibernate 。

数据的流向是 ActionFormBean 接受用户的数据，Action 将数据从 ActionFromBean 中取出，封装成 VO 或 PO,调用业务层的 Bean 类，完成各种业务处理后再 forward 。而业务层 Bean 收到这个 PO 对象之后，会调用 DAO 接口方法，进行持久化操作

简单的说：
struts 控制用的
hibernate 操作数据库的
spring 用解耦的

详细的说：
Struts 在 SSH 框架中起控制的作用, 其核心是 Controller, 即 ActionServlet, 而 ActionServlet 的核心就是 Struts-config.xml. 主要控制逻辑关系的处理.

Hibernate 是数据持久化层, 是一种新的对象、关系的映射工具, 提供了从 Java 类到数据表的映射，也提供了数据查询和恢复等机制, 大大减少数据访问的复杂度。把对数据库的直接操作, 转换为对持久对象的操作.

Spring 是一个轻量级的控制反转 (IoC) 和面向切面 (AOP) 的容器框架, 面向接口的编程, 由容器控制程序之间的（依赖）关系，而非传统实现中，由程序代码直接操控。这也就是所谓 “ 控制反转” 的概念所在：（依赖）控制权由应用代码中转到了外部容器，控制权的转移，是所谓反转。依赖注入，即组件之间的依赖关系由容器在运行期决定，形象的来说，即由容器动态的将某种依赖关系注入到组件之中

起到的主要作用是解耦
# S S H 在各层
1. struts 负责 web 层.
ActionFormBean 接收网页中表单提交的数据，然后通过 Action 进行处理，再 Forward 到对应的网页。
在 struts-config.xml 中定义`<action-mapping>`,ActionServlet 会加载。
2. spring 负责业务层管理，即 Service （或 Manager).
    1．service 为 action 提供统计的调用接口，封装持久层的 DAO.
    2．可以写一些自己的业务方法。
    3．统一的 javabean 管理方法
    4．声明式事务管理
    5. 集成 Hiberante
3. Hiberante 负责持久化层，完成数据库的 crud 操作
hibernate 为持久层，提供 OR/Mapping。
它有一组.hbm.xml 文件和 POJO, 是跟数据库中的表相对应的。然后定义 DAO, 这些是跟数据库打交道的类，它们会使用 PO。


# Struts
在 Struts 中，已经由一个名为ActionServlet的 Servlet 充当 控制器（Controller）的角色，根据描述模型、视图、控制器对应关系的struts-config.xml的配置文件，转发视图（View）的请求，组装响应数据模型（Model）。

在 MVC 的 模型（Model）部分，经常划分为两个主要子系统（系统的内部数据状态与改变数据状态的逻辑动作），这两个概念子系统分别具体对应 Struts 里的ActionForm与Action两个需要继承实现超类。在这里，Struts 可以与各种标准的数据访问技术结合在一起，包括 Enterprise Java Beans（EJB）, JDBC 与 JNDI。

在 Struts 的视图（View）端，除了使用标准的 JavaServer Pages（JSP）以外，还提供了大量的标签库使用，同时也可以与其他表现层组件技术（产品）进行整合，比如 Velocity Templates，XSLT 等。通过应用 Struts 的框架，最终用户可以把大部分的关注点放在自己的业务逻辑（Action）与 映射关系的配置文件（struts-config.xml）中。

## Struts
Struts = M + V + C
ActionServlet，这个类是 Struts 的核心控制器，负责拦截来自用户的请求。
Action，这个类通常由用户提供，该控制器负责接收来自 ActionServlet 的请求，并根据该请求调用模型的业务逻辑方法处理请求，并将处理结果返回给 JSP 页面显示。
## M
M = Model = ActionForm + JavaBean
由 ActionForm 和 JavaBean 组成，其中 ActionForm 用于封装用户的请求参数，封装成 ActionForm 对象，该对象被 ActionServlet 转发给 Action，Action 根据 ActionForm 里面的请求参数处理用户的请求。
JavaBean 则封装了底层的业务逻辑，包括数据库访问等。
## V
V = View = JSP
Struts 提供了丰富的标签库，通过标签库可以减少脚本的使用，自定义的标签库可以实现与 Model 的有效交互，并增加了现实功能。对应上图的 JSP 部分。
## C
C = Controller = 系统核心控制器 + 业务逻辑控制器。

controller 组件有两个部分组成——系统核心控制器，业务逻辑控制器。
系统核心控制器，对应上图的 ActionServlet。该控制器由 Struts 框架提供，继承 HttpServlet 类，因此可以配置成标注的 Servlet。该控制器负责拦截所有的 HTTP 请求，然后根据用户请求决定是否要转给业务逻辑控制器。
业务逻辑控制器，负责处理用户请求，本身不具备处理能力，而是调用 Model 来完成处理。对应 Action 部分。

# Spring is

__目的：__ 解决企业应用开发的复杂性
__功能：__ 使用基本的 JavaBean 代替 EJB，并提供了更多的企业应用功能
__范围：__ 任何 Java 应用

简单来说，Spring 是一个轻量级的控制反转 (IoC) 和面向切面 (AOP) 的容器框架。
2. __轻量__　从大小与开销两方面而言 Spring 都是轻量的。完整的 Spring 框架可以在一个大小只有 1MB 多的 JAR 文件里发布。并且 Spring 所需的处理开销也是微不足道的。此外，Spring 是非侵入式的：典型地，Spring 应用中的对象不依赖于 Spring 的特定类。
3. __控制反转__　Spring 通过一种称作控制反转（IoC）的技术促进了松耦合。当应用了 IoC，一个对象依赖的其它对象会通过被动的方式传递进来，而不是这个对象自己创建或者查找依赖对象。你可以认为 IoC 与 JNDI 相反——不是对象从容器中查找依赖，而是容器在对象初始化时不等对象请求就主动将依赖传递给它。
4. __面向切面__　Spring 提供了面向切面编程的丰富支持，允许通过分离应用的业务逻辑与系统级服务（例如审计（auditing）和事务（transaction）管理）进行内聚性的开发。应用对象只实现它们应该做的——完成业务逻辑——仅此而已。它们并不负责（甚至是意识）其它的系统级关注点，例如日志或事务支持。
5. __容器__　Spring 包含并管理应用对象的配置和生命周期，在这个意义上它是一种容器，你可以配置你的每个 bean 如何被创建——基于一个可配置原型（prototype），你的 bean 可以创建一个单独的实例或者每次需要时都生成一个新的实例——以及它们是如何相互关联的。然而，Spring 不应该被混同于传统的重量级的 EJB 容器，它们经常是庞大与笨重的，难以使用。
6. __框架__　Spring 可以将简单的组件配置、组合成为复杂的应用。在 Spring 中，应用对象被声明式地组合，典型地是在一个 XML 文件里。Spring 也提供了很多基础功能（事务管理、持久化框架集成等等），将应用逻辑的开发留给了你。

所有 Spring 的这些特征使你能够编写更干净、更可管理、并且更易于测试的代码。它们也为 Spring 中的各种模块提供了基础支持。

## Spring loc
Jsp 页面 ----Struts------Service（业务逻辑处理类）---Hibernate（左到右）

struts 负责控制 Service（业务逻辑处理类），从而控制了 Service 的生命周期，这样层与层之间的依赖和强。属于耦合。这时，使用 spring 框架就起到了控制 Action 对象（Strus 中的）和 Service 类的作用，两者之间的关系就松散了，Spring 的 Ioc 机制（控制反转和依赖注入）正是用在此处。
Spring 的 Ioc（控制反转和依赖注入）

控制反转：就是由容器控制程序之间的（依赖）关系，而非传统实现中，由程序代码直接操控

依赖注入：组件之间的依赖关系由容器在执行期决定 。由容器动态的将某种依赖关系注入到组件之中 。

简单的说，Spring 就是通过工厂 + 反射将我们的 bean 放到它的容器中的，当我们想用某个 bean 的时候，只需要调用 getBean("beanID") 方法。
原理简单介绍：
Spring 容器的原理，其实就是通过解析 xml 文件，或取到用户配置的 bean，然后通过反射将这些 bean 挨个放到集合中，然后对外提供一个 getBean() 方法，以便我们获得这些 bean。下面是一段简单的模拟代码：

## Spring from Struts
从上面我们不难看出：从头到尾 Action 不过充当了 Service 的控制工具。这些详细的业务方法是如何实现的。他根本就不会管，也不会问。他只要知道这些业务实现类所提供的方法接口就能够了。而在以往单独使用 Struts 框架的时候，全部的业务方法类的生命周期，甚至是一些业务流程都是由 Action 来控制的。
层与层之间耦合性太紧密了，既减少了数据訪问的效率又使业务逻辑看起来非常复杂。代码量也非常多。，Spring 容器控制全部 Action 对象和业务逻辑类的生命周期，由与上层不再控制下层的生命周期，层与层之间实现了全然脱耦，使程序执行起来效率更高，维护起来也方便。

## Spring AOP
使用 Spring 的第二个优点（AOP 应用）：
    事务的处理：
    在以往的 JDBCTemplate 中事务提交成功。异常处理都是通过 Try/Catch 来完毕，而在 Spring 中。Spring 容器集成了 TransactionTemplate，她封装了全部对事务处理的功能，包含异常时事务回滚，操作成功时数据提交等复杂业务功能。

这都是由 Spring 容器来管理，大大降低了程序猿的代码量。也对事务有了非常好的管理控制。

Hibernate 中也有对事务的管理，hibernate 中事务管理是通过 SessionFactory 创建和维护 Session 来完毕。

而 Spring 对 SessionFactory 配置也进行了整合，不须要在通过 hibernate.cfg.xml 来对 SessionaFactory 进行设定。这种话就能够非常好的利用 Sping 对事务管理强大功能。避免了每次对数据操作都要现获得 Session 实例来启动事务 / 提交 / 回滚事务还有繁琐的 Try/Catch 操作。这些也就是 Spring 中的 AOP（面向切面编程）机制非常好的应用。一方面使开发业务逻辑更清晰、专业分工更加 easy 进行。还有一方面就是应用 Spirng  AOP 隔离降低了程序的耦合性使我们能够在不同的应用中将各个切面结合起来使用大大提高了代码重用度。

# Hibernate is
Hibernate 是一个__高性能的对象 / 关系型持久化存储和查询的服务__，其遵循开源的 GNU Lesser General Public License (LGPL) 而且可以免费下载。
Hibernate 不仅关注于从 Java 类到数据库表的映射（也有 Java 数据类型到 SQL 数据类型的映射），另外也提供了数据查询和检索服务。从而极大地缩短的手动处理 SQL 和 JDBC 上的开发时间。

Hibernate 是一种 ORM

# ORM is
对象关系映射（英语：Object Relation Mapping，简称 ORM，或 O/RM，或 O/R mapping）

__简单__：以最基本的形式建模数据。
__传达性__：数据库结构被任何人都能理解的语言文档化。
__精确性__：基于数据模型创建正确标准化的结构。

# JDBC is
__Java Database Connectivity__
| JDBC 的优点	  | JDBC 的缺点  |
|---|---|
| 干净整洁的 SQL 处理|	大项目中使用很复杂
| 大数据下有良好的性能|	很大的编程成本
| 对于小应用非常好|	没有封装
| 易学的简易语法|	难以实现 MVC 的概念
| 查询需要指定| DBMS

# Why we need ORM ?
存在对象模型和关系数据库不匹配的问题。
| 不匹配	 |  描述 |
|---|---|
| __粒度__	| 有时你将会有一个对象模型，该模型类的数量比数据库中关联的表的数量更多
| __继承__	| RDBMSs 不会定义任何在面向对象编程语言中本来就有的继承
| __身份__	| RDBMS 明确定义一个'sameness' 的概念：主键。然而，Java 同时定义了对象判等（a==b）和 对象值判等（a.equals(b)）
| __关联__	| 面向对象的编程语言使用对象引用来表示关联，而一个 RDBMS 使用外键来表示对象关联
| __导航__	| 在 Java 中和在 RDBMS 中访问对象的方式完全不相同

# ORM has:
1. 一个 API 来在持久类的对象上实现基本的 CRUD 操作
2. 一个语言或 API 来指定引用类和属性的查询
3. 一个可配置的服务用来指定映射元数据
4. 一个技术和事务对象交互来执行 dirty checking, lazy association fetching 和其它优化的功能

# ORM's Advantages:
+ 使用业务代码访问对象而不是数据库中的表
+ 从面向对象逻辑中隐藏 SQL 查询的细节
+ 基于 JDBC 的'under the hood'
+ 没有必要去处理数据库实现
+ 实体是基于业务的概念而不是数据库的结构
+ 事务管理和键的自动生成
+ 应用程序的快速开发

# Hibernate's Advantages:
+ Hibernate __使用 XML 文件来处理映射 Java 类别到数据库表格中，并且不用编写任何代码。__
+ 为在数据库中直接储存和检索 Java 对象提供 __简单的 APIs__。
+ 如果在数据库中或任何其它表格中出现变化，那么仅需要改变 XML 文件属性。
+ __抽象不熟悉的 SQL 类型__，并为我们__提供工作中所熟悉的 Java 对象__。
+ Hibernate __不需要应用程序服务器__来操作。
+ 操控你数据库中对象复杂的关联。
+ 最小化与访问数据库的智能提取策略。
+ 提供简单的数据询问。

# Hibernate Architecture:
下面是一个非常高水平的 Hibernate 应用程序架构视图。
![hibernate_high_level](/assets/hibernate_high_level.jpg)
下面是一个详细的 Hibernate 应用程序体系结构视图以及一些重要的类。
![hibernate_architecture](/assets/hibernate_architecture.jpg)

# Hibernate properties
## Session Factory
## Session
## Transaction
## Query
## Criteria

# DAO
DAO(Data Access Object) 是一个数据访问接口，数据访问：顾名思义就是与数据库打交道。夹在业务逻辑与数据库资源中间。

在核心 J2EE 模式中是这样介绍 DAO 模式的：为了建立一个健壮的 J2EE 应用，应该将所有对数据源的访问操作抽象封装在一个公共 API 中。用程序设计的语言来说，就是建立一个接口，接口中定义了此应用程序中将会用到的所有事务方法。在这个应用程序中，当需要和数据源进行交互的时候则使用这个接口，并且编写一个单独的类来实现这个接口在逻辑上对应这个特定的数据存储。

# CGI is
通用网关接口（Common Gateway Interface/CGI）是一种重要的互联网技术，可以让一个客户端，从网页浏览器向执行在网络服务器上的程序请求数据。CGI 描述了服务器和请求处理程序之间传输数据的一种标准。
一般每次的 CGI 请求都需要新生成一个程序的副本来运行，这样大的工作量会很快将服务器压垮，因此一些更有效的技术像 mod_perl，可以让脚本解释器直接作为模块集成在 Web 服务器（例如：Apache）中，这样就能避免重复载入和初始化解释器。
# Servlet is
Servlet 为创建基于 web 的应用程序提供了基于组件、独立于平台的方法，可以不受 CGI 程序的性能限制。Servlet 有权限访问所有的 Java API，包括访问企业级数据库的 JDBC API。

Java Servlet 是运行在 Web 服务器或应用服务器上的程序，它是作为来自 Web 浏览器或其他 HTTP 客户端的请求和 HTTP 服务器上的数据库或应用程序之间的中间层。
使用 Servlet，您可以收集来自网页表单的用户输入，呈现来自数据库或者其他源的记录，还可以动态创建网页。

# Why not CGI but servlet:
Java Servlet 通常情况下与使用 CGI（Common Gateway Interface，公共网关接口）实现的程序可以达到异曲同工的效果。但是相比于 CGI，Servlet 有以下几点优势：
+ 性能明显更好。
+ Servlet 在 Web 服务器的地址空间内执行。这样它就没有必要再创建一个单独的进程来处理每个客户端请求。
+ Servlet 是独立于平台的，因为它们是用 Java 编写的。
+ 服务器上的 Java 安全管理器执行了一系列限制，以保护服务器计算机上的资源。因此，Servlet 是可信的。
+ Java 类库的全部功能对 Servlet 来说都是可用的。它可以通过 sockets 和 RMI 机制与 applets、数据库或其他软件进行交互。

# Servlet Architecture
![servlet-arch](/assets/servlet-arch.jpg)

# Servlet 生命周期
Servlet 通过调用 init () 方法进行初始化。
Servlet 调用 service() 方法来处理客户端的请求。
Servlet 通过调用 destroy() 方法终止（结束）。
最后，Servlet 是由 JVM 的垃圾回收器进行垃圾回收的。

在中间我们可以
- doGet()
- doPost()
- doDestory()

第一个到达服务器的 HTTP 请求被委派到 Servlet 容器。
Servlet 容器在调用 service() 方法之前加载 Servlet。
然后 Servlet 容器处理由多个线程产生的多个请求，每个线程执行一个单一的 Servlet 实例的 service() 方法。
![Servlet-LifeCycle](/assets/Servlet-LifeCycle.jpg)
# JSP
JavaServer Pages
JSP 技术是以 Java 语言作为脚本语言的，JSP 网页为整个服务器端的 Java 库单元提供了一个接口来服务于 HTTP 的应用程序。
JSP 使 Java 代码和特定的预定义动作可以嵌入到静态页面中。JSP 句法增加了被称为 JSP 动作的 XML 标签，它们用来调用内建功能。另外，可以创建 JSP 标签库，然后像使用标准 HTML 或 XML 标签一样使用它们。标签库提供了一种和平台无关的扩展服务器性能的方法。
JSP 被 JSP 编译器编译成 Java Servlets。一个 JSP 编译器可以把 JSP 编译成 JAVA 代码写的 servlet 然后再由 JAVA 编译器来编译成机器码，也可以直接编译成二进制码。
# JSP 与 Servlet 的关系
Servlet 是 Java 提供的用于开发 Web 服务器应用程序的一个组件，运行在服务器端，由 Servlet 容器所管理，用于生成动态的内容。Servlet 是平台独立的 Java 类，编写一个 Servlet，实际上就是按照 Servlet 规范编写一个 Java 类。
![jsp-servlet](/assets/jsp-servlet.gif)
如图所示，Java 提供一系列接口类
实际上 JSP 也是从 Servlet 继承而来。只不过它在 Servlet 当中又添加 / 修改了一些方法，作了新的封装。

它通过一个多重继承，分别从 Java 的 `HttpJspPage` 和 `HttpServlet` 两个类那里继承和实现一些方法，然后封装一个叫做 `HttpJspBase` 的类从而实现了一个通用化的 JSP 类，用户在开发自己的 JSP 时，只需要从 `HttpJspBase` 继承一个自己的类（如图中 `Hello_jsp` 类），然后根据需要去实现相应的方法即可。
# Servlet do:
+ __读取客户端（浏览器）发送的显式的数据。__ 这包括网页上的 HTML 表单，或者也可以是来自 applet 或自定义的 HTTP 客户端程序的表单。
+ __读取客户端（浏览器）发送的隐式的 HTTP 请求数据。__ 这包括 cookies、媒体类型和浏览器能理解的压缩格式等等。
+ __处理数据并生成结果。__ 这个过程可能需要访问数据库，执行 RMI 或 CORBA 调用，调用 Web 服务，或者直接计算得出对应的响应。
+ __发送显式的数据（即文档）到客户端（浏览器）。__该文档的格式可以是多种多样的，包括文本文件（HTML 或 XML）、二进制文件（GIF 图像）、Excel 等。
+ __发送隐式的 HTTP 响应到客户端（浏览器）。__ 这包括告诉浏览器或其他客户端被返回的文档类型（例如 HTML），设置 cookies 和缓存参数，以及其他类似的任务。

# MVC
![MVC-Process.svg](/assets/MVC-Process.svg.png)
__模型（Model）__ 用于封装与应用程序的业务逻辑相关的数据以及对数据的处理方法。“Model” 有对数据直接访问的权力，例如对数据库的访问。“Model” 不依赖 “View” 和 “Controller”，也就是说， Model 不关心它会被如何显示或是如何被操作。但是 Model 中数据的变化一般会通过一种刷新机制被公布。为了实现这种机制，那些用于监视此 Model 的 View 必须事先在此 Model 上注册，从而，View 可以了解在数据 Model 上发生的改变。（比较：观察者模式（软件设计模式））
__视图（View）__ 能够实现数据有目的的显示（理论上，这不是必需的）。在 View 中一般没有程序上的逻辑。为了实现 View 上的刷新功能，View 需要访问它监视的数据模型（Model），因此应该事先在被它监视的数据那里注册。
__控制器（Controller）__ 起到不同层面间的组织作用，用于控制应用程序的流程。它处理事件并作出响应。“事件” 包括用户的行为和数据 Model 上的改变。

+ Model 负责数据访问，较现代的 Framework 都会建议使用独立的数据对象 (DTO, POCO, POJO 等) 来替代弱类型的集合对象。数据访问的代码会使用 Data Access 的代码或是 ORM-based Framework，也可以进一步使用 Repository Pattern 与 Unit of Works Pattern 来切割数据源的相依性。
+ Controller 负责处理消息，较高级的 Framework 会有一个默认的实现来作为 Controller 的基础，例如 Spring 的 DispatcherServlet 或是 ASP.NET MVC 的 Controller 等，在职责分离原则的基础上，每个 Controller 负责的部分不同，因此会将各个 Controller 切割成不同的文件以利维护。
+ View 负责显示数据，这个部分多为前端应用，而 Controller 会有一个机制将处理的结果 (可能是 Model, 集合或是状态等) 交给 View，然后由 View 来决定怎么显示。例如 Spring Framework 使用 JSP 或相应技术，ASP.NET MVC 则使用 Razor 处理数据的显示。

# MVC Advantages
__首先，多个 View 能共享一个 Model 。__ 如今，同一个 Web 应用程序会提供多种用户界面，例如用户希望既能够通过浏览器来收发电子邮件，还希望通过手机来访问电子邮箱，这就要求 Web 网站同时能提供 Internet 界面和 WAP 界面。在 MVC 设计模式中， Model 响应用户请求并返回响应数据，View 负责格式化数据并把它们呈现给用户，业务逻辑和表示层分离，同一个 Model 可以被不同的 View 重用，所以大大提高了代码的可重用性。

__其次，Controller 是自包含（self-contained）指高独立内聚的对象，与 Model 和 View 保持相对独立，所以可以方便的改变应用程序的数据层和业务规则。__
例如，把数据库从 MySQL 移植到 Oracle，或者把 RDBMS 数据源改变成 LDAP 数据源，只需改变 Model 即可。一旦正确地实现了控制器，不管数据来自数据库还是 LDAP 服务器，View 都会正确地显示它们。由于 MVC 模式的三个模块相互独立，改变其中一个不会影响其他两个，所以依据这种设计思想能构造良好的少互扰性的构件。

__此外，Controller 提高了应用程序的灵活性和可配置性。__ Controller 可以用来连接不同的 Model 和 View 去完成用户的需求，也可以构造应用程序提供强有力的手段。给定一些可重用的 Model 、 View 和 Controller 可以根据用户的需求选择适当的 Model 进行处理，然后选择适当的的 View 将处理结果显示给用户。

# MVP
![mvp](/assets/mvp.png)
MVP 模式将 Controller 改名为 Presenter，同时改变了通信方向。
1. 各部分之间的通信，都是双向的。
2. View 与 Model 不发生联系，都通过 Presenter 传递。
3. View 非常薄，不部署任何业务逻辑，称为 "被动视图"（Passive View），即没有任何主动性，而 Presenter 非常厚，所有逻辑都部署在那里。

# MVVM
![mvvm](/assets/mvvm.png)
唯一的区别是，它采用双向绑定（data-binding）：View 的变动，自动反映在 ViewModel，反之亦然。Angular 和 Ember 都采用这种模式。

# Tomcat
按照 Sun Microsystems 提供的技术规范，实现了对 Servlet 和 JavaServer Page（JSP）的支持，并提供了作为 Web 服务器的一些特有功能，如 Tomcat 管理和控制平台、安全域管理和 Tomcat 阀等。由于 Tomcat 本身也内含了一个 HTTP 服务器，它也可以被视作一个单独的 Web 服务器。

但是，不能将 Tomcat 和 Apache Web 服务器混淆，Apache Web Server 是一个用 C 语言实现的 HTTP web server；这两个 HTTP web server 不是捆绑在一起的。Apache Tomcat 包含了一个配置管理工具，也可以通过编辑 XML 格式的配置文件来进行配置。

omcat 提供了一个 Jasper 编译器用以将 JSP 编译成对应的 Servlet。

Tomcat 的 Servlet 引擎通常与 Apache 或者其他 Web 服务器一起工作。除了用于开发过程中的调试以及那些对速度和事务处理只有很小要求的用户，很少会将 Tomcat 单独作为 Web 服务器。但随着版本的更新，正有越来越多的用户将其单独作为 Web 服务器用以那些对速度和可靠性有较高要求的环境中。

# JNDI
Java 命名和目录接口（Java Naming and Directory Interface，缩写 JNDI），是 Java 的一个目录服务应用程序界面（API），它提供一个目录系统，并将服务名称与对象关联起来，从而使得开发人员在开发过程中可以使用名称来访问对象。
