# Spring Boot

> 作者: 潘深练
>
> 更新: 2022-03-10

## 一、springboot的原理

Spring Boot是一个基于Spring框架的开发工具，旨在简化Spring应用程序的创建和部署。它采用了约定优于配置的方式，使得开发者可以快速地搭建出一个基于Spring的应用程序，同时提供了许多默认的配置和集成，以减少开发者在应用程序开发和部署过程中的工作量。

Spring Boot的实现原理主要包括以下几个方面：

1、自动配置：Spring Boot通过对应用程序的类路径进行扫描，自动配置Spring应用程序。它通过预定义的默认值和规则，自动配置应用程序中的组件，包括Web服务器、数据源、缓存等。

2、起步依赖（Starter）：Spring Boot提供了一系列的“起步依赖”，它们是预定义的一组依赖库，可以方便地为应用程序添加所需的功能和组件。这些依赖库包括Web应用程序、数据访问、安全性等，而开发者可以根据需要，选择需要的依赖库。

3、嵌入式Web服务器：Spring Boot默认提供了Tomcat、Jetty和Undertow等Web服务器的嵌入式实现，它们可以作为Spring应用程序的默认Web服务器，从而避免了繁琐的配置过程。

4、注解驱动：Spring Boot通过大量的注解来简化配置，包括自动配置注解、组件扫描注解等。这些注解可以方便地将组件自动装配到应用程序中，减少了手动配置的工作量。

5、环境分离：Spring Boot支持在不同的环境中运行应用程序，如开发环境、测试环境和生产环境。它通过加载不同的配置文件，自动配置应用程序中的组件，以满足不同环境的需求。

6、Actuator：Spring Boot提供了Actuator组件，可以通过HTTP或JMX接口来监控和管理应用程序的运行状态。Actuator可以提供应用程序的健康检查、性能监控、日志查看等功能，方便应用程序的管理和维护。

总的来说，Spring Boot的原理就是通过：

- 自动配置
- 起步依赖（starter）
- 嵌入式Web服务器
- 注解驱动
- 环境分离
- Actuator

等特性，简化了Spring应用程序的开发和部署过程，提高了开发效率和应用程序的可维护性。

## 二、springboot的factories配置有什么用

Spring Boot的Factories机制是指在应用程序启动时自动加载并配置某些组件或对象的机制，这些组件或对象可以是任何类型，例如数据源、消息队列、缓存、Web服务器等等。

Factories机制的主要作用是使得应用程序更易于扩展和定制。Spring Boot提供了大量的内置的Factories，可以通过配置文件或注解来启用或禁用这些Factories，从而实现组件的自动配置和装配。

在Spring Boot中，Factories配置通常存储在META-INF/spring.factories文件中，其中包含了一组键值对，键表示要配置的组件类型，值表示要使用的具体实现。这些Factories可以自动注册到Spring应用程序上下文中，使得应用程序可以使用这些组件。

例如，如果我们需要在应用程序中使用JPA，只需要在pom.xml中添加spring-boot-starter-data-jpa依赖，并在配置文件中指定数据源的相关信息，Spring Boot就会自动配置JPA的相关组件。这是因为在spring-boot-starter-data-jpa中，包含了JPA的Factories配置，当应用程序启动时，这些Factories会被自动加载并配置相关的组件。

总的来说，Spring Boot的Factories机制可以使得应用程序更易于扩展和定制，减少了手动配置的工作量，提高了开发效率和可维护性。

## 三、springboot如何自定义starter

Spring Boot的Starter是一组依赖库的集合，它们被打包为一个单独的库，可以方便地被其他应用程序引用。自定义Starter可以使得应用程序更加模块化，提高应用程序的可维护性和可扩展性。

以下是自定义Spring Boot Starter的步骤：

定义Starter的名称和作用域：在项目的根目录下创建一个名为spring-boot-starter-{name}的模块，其中{name}是你自定义Starter的名称。该模块的作用域应该是provided，因为它不包含实现，只是用于管理依赖关系。

添加依赖：在Starter模块的pom.xml文件中，添加需要引入的依赖。这些依赖应该是一组相关的依赖，例如某个特定的库或组件。

添加自动配置：在Starter模块中添加一个spring.factories文件，指定自动配置类的全限定名。这些自动配置类应该定义了如何自动配置需要引入的依赖。

添加文档说明：添加一个README文件或者其他文档，说明该Starter的使用方式、提供的功能和限制等信息。

安装Starter到本地仓库：在Starter模块的根目录下运行mvn install命令，将该Starter安装到本地仓库。

在应用程序中使用Starter：在应用程序的pom.xml文件中，添加自定义的Starter依赖。Spring Boot会自动将Starter中定义的依赖引入到应用程序中，并根据自动配置类自动配置相关组件。

通过以上步骤，我们可以创建自己的Spring Boot Starter，并在应用程序中使用。自定义Starter可以使得应用程序更加模块化，提高应用程序的可维护性和可扩展性。

## 四、springboot执行流程

Spring Boot应用程序的执行流程可以大致分为以下几个步骤：

1、加载应用程序上下文

当Spring Boot应用程序启动时，它会加载应用程序上下文。应用程序上下文包含了Spring容器中的所有Bean定义和实例化对象。Spring Boot使用自动配置机制自动配置和装配容器中的组件，包括Web服务器、数据源、事务管理器等等。

2、执行CommandLineRunner和ApplicationRunner

Spring Boot提供了CommandLineRunner和ApplicationRunner接口，可以在应用程序启动后执行一些初始化操作。这些接口的实现类会被自动加载并执行。

3、启动Web服务器

如果应用程序是一个Web应用程序，Spring Boot会自动配置和启动内嵌的Web服务器，例如Tomcat、Jetty、Undertow等等。Web服务器可以通过配置文件进行定制化。

4、处理请求

一旦Web服务器启动，应用程序就可以开始接收和处理请求了。Spring Boot会根据应用程序的注解配置和URL匹配规则，将请求分发给对应的Controller进行处理。

5、响应请求

Controller处理完请求后，会返回一个响应结果。Spring Boot会将响应结果封装为HTTP响应格式，并将其发送给客户端。

6、关闭应用程序上下文

当应用程序停止时，Spring Boot会关闭应用程序上下文。应用程序上下文中的所有Bean都会被销毁，并执行一些清理工作。

总的来说，Spring Boot应用程序的执行流程包括加载应用程序上下文、执行初始化操作、启动Web服务器、处理和响应请求以及关闭应用程序上下文等步骤。这些步骤都是通过Spring Boot的自动配置机制和约定大于配置的设计思想来实现的，可以大大简化应用程序的开发和部署工作。

