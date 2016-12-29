<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [Hello world Sample](#hello-world-sample)   
   - [**1. 创建一个Spring项目**](#1-创建一个spring项目)   
   - [**2.Rewrite`build.gradle`**](#2rewritebuildgradle)   
   - [__3. Create a resource representation class(POJO)__](#__3-create-a-resource-representation-classpojo__)   
   - [__4. Create a resource controller__](#__4-create-a-resource-controller__)   
   - [__5. Make the application executable__](#__5-make-the-application-executable__)   
   - [6.__Build an executable jar__](#6__build-an-executable-jar__)   
   - [7.Test the service](#7test-the-service)   
- [Resource](#resource)   

<!-- /MDTOC -->
# Hello world Sample
Intellij IDEA + Windows + Gradle
[Building a RESTful Web Service](https://spring.io/guides/gs/rest-service/)

This guide walks you through the process of creating a "hello world" RESTful web service with Spring.

What you’ll build
You’ll build a service that will accept HTTP GET requests at:
```
http://localhost:8080/greeting
```
and respond with a JSON representation of a greeting:
```json
{"id":1,"content":"Hello, World!"}
```
You can customize the greeting with an optional name parameter in the query string:
```
http://localhost:8080/greeting?name=User
```
The name parameter value overrides the default value of "World" and is reflected in the response:
```json
{"id":1,"content":"Hello, User!"}
```
## **1. 创建一个Spring项目**
**1.1 By Gradle项目**
![spring-1](/assets/spring-1.jpg)
**1.2**
![spring-2](/assets/spring-2.jpg)
|   |   |
|---|---|
| GroupId  | nullable |
| ArtifactId | 和项目名保持一致 |
![spring-3](/assets/spring-3.jpg)
其它地方一路请确定就好。生成项目如下图所示:
![spring-4](/assets/spring-4.jpg)
最后在`settings.gradle`里的就是项目名
```
rootProject.name = 'SpringLearn'
```
## **2.Rewrite`build.gradle`**
```java
buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.4.3.RELEASE")
    }
}

apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'idea'
apply plugin: 'org.springframework.boot'

jar {
    baseName = 'gs-serving-web-content'
    version =  '0.1.0'
}

repositories {
    mavenCentral()
}

sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
    compile("org.springframework.boot:spring-boot-starter-thymeleaf")
    compile("org.springframework.boot:spring-boot-devtools")
    testCompile("junit:junit")
}
```
Don't forget `Sync` after update `build.gradle`

## __3. Create a resource representation class(POJO)__
`/greeting`接受`GET`请求, 可接受一个 `name` 参数。
`GET`请求返回一个 `200 OK`响应,并且返回如下所示的JSON
```json
{
    "id": 1,
    "content": "Hello, World!"
}
```
id是一个唯一的标识,content是内容。
To model the greeting representation, you create a resource representation class. Provide a POJO with fields, constructors, and accessors for the id and content data:
`src/main/java/hello/Greeting.java`
```java
package hello;

public class Greeting {

    private final long id;
    private final String content;

    public Greeting(long id, String content) {
        this.id = id;
        this.content = content;
    }

    public long getId() {
        return id;
    }

    public String getContent() {
        return content;
    }
}
```
## __4. Create a resource controller__
In Spring’s approach to building RESTful web services, HTTP requests are handled by a controller. These components are easily identified by the `@RestController` annotation, and the ``GreetingController`` below handles `GET` requests for `/greeting` by returning a new instance of the `Greeting` class:
`src/main/java/hello/GreetingController.java`

```java
package hello;

import java.util.concurrent.atomic.AtomicLong;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class GreetingController {

    private static final String template = "Hello, %s!";
    private final AtomicLong counter = new AtomicLong();

    @RequestMapping("/greeting")
    public Greeting greeting(@RequestParam(value="name", defaultValue="World") String name) {
        return new Greeting(counter.incrementAndGet(),
                            String.format(template, name));
    }
}
```
This controller is concise and simple, but there’s plenty going on under the hood. Let’s break it down step by step.

>As you see in steps below, Spring uses the Jackson JSON library to automatically marshal instances of type Greeting into JSON.

`@RequestMapping`确认了HTTP请求能够正确地从`/greeting`映射到`greetingg`方法。
> `@RequestMapping`默认会映射所有HTTP操作(`GET`,`PUT`,`POST`and so forth),我们可以使用`@RequestMapping(method=GET)`来缩小映射的范围。

`@RequestParam`将查询字符串中的参数`name`绑定到`greeting()`的参数`name`上
`@RequestParam`查询字符串的参数默认为`require=true`,如果查询请求中缺少参数的话会用`defaultValue`来填充

The implementation of the method body creates and returns a new `Greeting` object with `id` and `content` attributes based on the next value from the `counter`, and formats the given name by using the greeting `template`.
`id`和`content`如何产生, 很简单没必要翻了

__RESTful web service controller__ 和 __传统的 MVC controller__ 最大的区别在于 HTTP 响应内容创建的方式
__RESTful web service controller__ 没必要依赖一个[view technology](https://spring.io/understanding/view-templates)去将服务端的greeting内容渲染为HTML, 只需要简单地填充并且返回一个 Greeting 对象就行了, 这个对象将会被直接以JSON的形式直接写入HTTP响应。

`@RestController` 是 Spring 4 的新玩意儿, 可以将一个 class 标记为 controller。这样每个方法将会返回一个domain对象, 而不是一个view。是`@Controller`和`@ResponseBody`的合并玩意儿。

关于这个对象是怎么变成JSON的:
>The `Greeting` object must be converted to JSON. Thanks to Spring’s HTTP message converter support, you don’t need to do this conversion manually. Because Jackson 2 is on the classpath, Spring’s [`MappingJackson2HttpMessageConverter`](http://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/http/converter/json/MappingJackson2HttpMessageConverter.html) is automatically chosen to convert the `Greeting` instance to JSON.

## __5. Make the application executable__
虽然可以将此服务打包为用于部署到外部应用程序服务器的传统 WAR 文件, 但是下面演示我们可以用更简单的方法创建一个独立的应用程序。

我们可以把所有东西打包在一个 JAR 包里面, 通过一个传统的JAVA入口 `main()` 方法来前驱动, Spring将会通过内嵌的Tomcat servlet在HTTP运行时作为其容器而不是部署到外部实例。

`src/main/java/hello/Application.java`
```java
package hello;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

`@SpringBootApplication`方便地提供了一个下列Annotation的合集:
- `@Configuration` tags the class as a source of bean definitions for the application context.
- `@EnableAutoConfiguration` tells Spring Boot to start adding beans based on classpath settings, other beans, and various property settings.
- ormally you would add `@EnableWebMvc` for a Spring MVC app, but Spring Boot adds it automatically when it sees __spring-webmvc__ on the classpath. This flags the application as a web application and activates key behaviors such as setting up a `DispatcherServlet`.
- `@ComponentScan`tells Spring to look for other components, configurations, and services in the the `hello` package, allowing it to find the controllers.

`main()`函数使用 Spring Boot 的 `SpringApplication.run()` 方法启动新的 Application, 这种方法忽略了plumbing和infrastructure的配置, 不需要写任何XML


## 6.__Build an executable jar__
You can run the application from the command line with Gradle or Maven.

Or you can build a single executable JAR file that contains all the necessary dependencies, classes, and resources, and run that. This makes it easy to ship, version, and deploy the service as an application throughout the development lifecycle, across different environments, and so forth.

__Gradle__
If you are using Gradle, you can run the application using `./gradlew bootRun`. Or you can build the JAR file using `./gradlew build`. Then you can run the JAR file:
```
java -jar build/libs/gs-rest-service-0.1.0.jar
```
__Maven__
If you are using Maven, you can run the application using `./mvnw spring-boot:run`. Or you can build the JAR file with `./mvnw clean package`. Then you
 can run the JAR file:

`java -jar target/gs-rest-service-0.1.0.jar`

>The procedure above will create a runnable JAR. You can also opt to build a classic WAR file instead.

Logging output is displayed. The service should be up and running within a few seconds.

## 7.Test the service
启动服务后可以从Tomcat的默认端口8080查看结果
visit
http://localhost:8080/greeting
http://localhost:8080/greeting?name=User
# Resource
https://spring.io/guides/gs/rest-service/
