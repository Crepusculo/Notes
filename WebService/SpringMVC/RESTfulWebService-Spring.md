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
**1. 创建一个Spring项目**
**1.1 By Gradle项目**
![spring-1](/assets/spring-1_sppa2c0os.jpg)
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
**3.Rewrite`build.gradle`**
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


# Resource
https://spring.io/guides/gs/rest-service/
