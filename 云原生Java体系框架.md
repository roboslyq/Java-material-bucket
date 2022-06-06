# 微服务特性

## Red Hat 被称为“微服务特性（microservicility）”的内容

https://baijiahao.baidu.com/s?id=1714420255480846215&wfr=spider&for=pc

https://www.infoq.com/articles/microservicilities-quarkus/

微服务特性

“微服务特性（microservicility）”指的是除了业务逻辑之外，服务必须要实现的一个横切性关注点的列表，总结起来如下图所示：

![img](%E4%BA%91%E5%8E%9F%E7%94%9FJava%E4%BD%93%E7%B3%BB%E6%A1%86%E6%9E%B6/b58f8c5494eef01fd4f8a90633b6c92cbe317dd3.png)

业务逻辑可以使用任何语言（Java、Go 或 JavaScript）或任何框架（Spring Boot、Quarkus）来实现，但是围绕着业务逻辑，我们应该实现如下的关注点：

**API**：服务可以通过一组预先定义的 API 操作进行访问。例如，在采用 RESTful Web API 的情况下，会使用 HTTP 作为协议。此外，API 还可以使用像 Swagger 这样的工具实现文档化。

**发现（Discovery）**：服务需要能够发现其他的服务。

**调用（Invocation）**：在服务发现之后，需要使用一组参数来调用它，并且可能会返回一个响应。

**弹性（Elasticity）**：微服务架构很重要的特性之一就是每个服务都是有弹性的，这意味着它可以根据一些参数（比如系统的重要程度或当前的工作负载）独立地进行扩展和伸缩。

**回弹性（Resiliency）**：在微服务架构中，我们在开发时应该要考虑到故障，特别是与其他服务进行通信的时候。在单体架构中，应用会作为一个整体进行启动和关闭。但是，当我们把应用拆分成微服务架构之后，应用就变成由多个服务组成的，所有的服务会通过网络互相连接，这意味着应用的某些部分可能在正常运行，而其他部分可能已经出现了故障。在这种情况下，很重要的一点就是遏制故障，避免错误通过其他的服务进行传播。回弹性（或称为应用回弹性）是指一个应用 / 服务能够对面临的问题作出反应的能力，在出现问题的时候，依然能够提供尽可能最好的结果。

**管道（Pipeline）**：服务应该能够独立部署，不需要任何形式的部署编排。基于这一点，每个服务应该有自己的部署管道。

**认证（Authentication）**：在微服务架构中，涉及到安全性时，很重要的一个方面就是如何认证 / 授权内部服务之间的调用。Web token（以及通用的 token）是在内部服务之间声明安全性的首选方式。

**日志（Logging）**：在单体应用中，日志是很简单的事情，因为应用的所有组件都在同一个节点中运行。现在，组件以服务的形式分布在多个节点上，因此，为了全面了解日志跟踪的情况，我们需要一个统一的日志系统 / 数据收集器。

**监控（Monitoring）**：要保证基于微服务的应用正确运行，很重要的一个方面就是衡量系统的运行情况、理解应用的整体健康状况并在出现问题的时候发出告警。监控是控制应用程序的重要方面。

**跟踪（Tracing）**：跟踪用来可视化一个程序的流程和数据进展。当我们需要检查用户在整个应用中的操作时，它对开发人员或运维人员尤其有用。

Kubernetes 只能覆盖其中的三个

![img](%E4%BA%91%E5%8E%9F%E7%94%9FJava%E4%BD%93%E7%B3%BB%E6%A1%86%E6%9E%B6/7af40ad162d9f2d3be1b312564a4da1a6227cc40.png)

# Quarkus

https://quarkus.io/guides/

近几年由于云原生技术的普及，越来越多的用户开始使用容器来运行微服务应用。微服务架构的引入，使我们的服务颗粒度变得越来越小，轻量且能快速启动的应用能够更好的适应容器化环境。 以我们目前常规的Spring Boot应用来说，一般Restful服务的jar包大概是30M左右，如果我们将JDK以及相关应用打包成docker镜像文件大概是140M左右。而常规的Go语言的可执行程序生成镜像包一般不会超过50M。如何让臃肿的Java应用瘦身使他易于容器化，成为Java应用云原生化需要解决的问题。

红帽开源的Quarkus项目，借助开源社区的力量，通过对业界广泛使用的框架进行了适配，并结合云原生应用的特点，提供了一套端到端的Java云原生应用解决方案。虽然开源时间较短，但是生态方面也已经达到可用的状态，自身包含扩展框架，已经支持像Netty、Undertow、Hibernate、JWT等框架，足以用于开发企业级应用，用户也可以基于扩展框架自行扩展。

Quarkus定位为GraalVM*和OpenJDK HotSpot量身定制的一个Kurbernetes Native Java框架。

*GraalVM：JVM为了提升效率，借助JIT及时编译技术对解释执行的字节码进行局部优化，通过编译器生成本地执行代码提升应用执行效率。GraalVM是Oracle实验室开发的新一代的面向多种语言的JVM即时编译器，在性能以及多语言互操作性上有比较好的表现。与Java HotSpot VM相比，Graal借助内联，逃逸分析以及推出优化技术可以提升2至5倍的性能提升。

In March of 2019, after more than a year of internal development, Quarkus was introduced to the open source community. culminating in a 1.0 release within the open source community in October 2019. with a 2.0 community release in June 2021.

Among the specifications and technologies underlying Quarkus are Eclipse MicroProfile, Eclipse Vert.x, Contexts & Dependency Injection (CDI), Jakarta RESTful Web Services (JAX-RS), the Java Persistence API (JPA), the Java Transaction API (JTA), Apache Camel, and Hibernate, just to name a few.

Quarkus is also an ahead-of-time compilation (AOT) platform, optimizing code for the JVM as well as compiling to native code for improved performance. All of the underlying technologies are AOT-enabled, and Quarkus continually incorporates new AOT-enabled technologies, standards, and libraries.



Quarkus 集成了 MicroProfile 规范，将企业级 Java 生态系统转移到了微服务架构中。在下图中，我们可以看到构成 MicroProfile 规范的所有 API。其中有些 API 是基于 Jakarta EE（也就是以前的 Java EE）规范的，比如 CDI、JSON-P 和 JAX-RS，其他的则是由 Java 社区开发的。

## Start

https://code.quarkus.io/

 

https://mvnrepository.com/artifact/io.quarkus/quarkus-maven-plugin

mvn io.quarkus:quarkus-maven-plugin:2.9.0.Final:create \

-DprojectGroupId=com.redhat.cloudnative \

-DprojectArtifactId=inventory-quarkus \

-DprojectVersion=1.0.0-SNAPSHOT \

-DclassName="com.redhat.cloudnative.InventoryResource" \

-Dextensions="quarkus-resteasy,quarkus-junit5,rest-assured,quarkus-resteasy-jsonb,quarkus-hibernate-orm-panache,quarkus-jdbc-h2"

 

## Quarkus vs Spring

Quarkus-For-Spring-Developers-Red-Hat

https://github.com/quarkus-for-spring-developers/examples

|             | **Quarkus**              | **Spring**                                        |
| ----------- | ------------------------ | ------------------------------------------------- |
| **starter** | https://code.quarkus.io/ | https://start.aliyun.com/https://start.spring.io/ |
|             |                          |                                                   |

## *Common Quarkus extensions*

Maven quarkus:list-extensions

| **Quarkus extension**                   | **Spring Boot Starter**                                      |
| --------------------------------------- | ------------------------------------------------------------ |
| quarkus-resteasy-jackson                | spring-boot-starter-webspring-boot-starter-webflux           |
| quarkus-resteasy-reactive-jackson       | spring-boot-starter-webspring-boot-starter-webflux           |
| quarkus-hibernate-orm-panache           | spring-boot-starter-data-jpa                                 |
| quarkus-hibernate-orm-rest-data-panache | spring-boot-starter-data-rest                                |
| quarkus-hibernate-reactive-panache      | spring-boot-starter-data-r2dbc                               |
| quarkus-mongodb-panache                 | spring-boot-starter-data-mongodbspring-boot-starter-data-mongodb-reactive |
| quarkus-hibernate-validator             | spring-boot-starter-validation                               |
| quarkus-qpid-jms                        | spring-boot-starter-activemq                                 |
| quarkus-artemis-jms                     | spring-boot-starter-artemis                                  |
| quarkus-cache                           | spring-boot-starter-cache                                    |
| quarkus-redis-client                    | spring-boot-starter-data-redisspring-boot-starter-data-redis-reactive |
| quarkus-mailer                          | spring-boot-starter-mail                                     |
| quarkus-quartz                          | spring-boot-starter-quartz                                   |
| quarkus-oidc                            | spring-boot-starter-oauth2-resource-server                   |
| quarkus-oidc-client                     | spring-boot-starter-oauth2-client                            |
| quarkus-smallrye-jwt                    | spring-boot-starter-security                                 |

## Spring迁移到Quarkus的工具

It can analyze an existing Spring Boot application and offer suggestions for utilizing the Quarkus

Spring Extensions best to migrate the application to Quarkus.

https://developers.redhat.com/products/mta/overview

# Micronaut

https://micronaut.io/

https://launch.micronaut.io

Object Computing的一个团队开始重新思考如何从头开始设计 Java 框架。于是Micronaut框架诞生了，这是一个采用了不同做法的 Java 框架，它通过使用 Java 注释将框架的组装计算工作所转移到了编译阶段。这完全消除了传统 Java 框架使用的反射、运行时生成代理和复杂的动态类加载。

2018 年 4 月，Micronaut 框架首次公开发布。

# Spring Native

https://docs.spring.io/spring-native/docs/current/reference/htmlsingle/

https://start.spring.io/

 # Helidon

Oracle推出的开源框架[ Helidon ](https://helidon.io/)，该项目是一个用于创建基于微服务的应用程序的 Java 库集合。和[ Payara Micro ](https://www.payara.fish/payara_micro)、[ Thorntail ](https://thorntail.io/)（之前的[ WildFly Swarm ](http://wildfly-swarm.io/)）、[ OpenLiberty ](https://openliberty.io/)、[ TomEE ](http://tomee.apache.org/)等项目一样，该项目也加入了 MicroProfile 家族。

# Eclipse Microprofile

https://start.microprofile.io

Eclipse MicroProfile 是一个 Java 微服务开发的基础编程模型，它致力于定义企业 Java 微服务规范，MicroProfile 提供指标、API 文档、运行状况检查、容错、JWT、Open API 与分布式跟踪等能力，使用它创建的云原生微服务可以自由地部署在任何地方，包括 Service Mesh 架构，如 Istio。

> MicroProfile是一个规范，是将传统JavaEE轻量化以适应微服务时代的一个体系，不是一个具体的框架实现。![img](%E4%BA%91%E5%8E%9F%E7%94%9FJava%E4%BD%93%E7%B3%BB%E6%A1%86%E6%9E%B6/v2-e61c9ee72ed9115446e29adc0c87a925_1440w.jpg)

