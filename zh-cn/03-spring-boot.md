# Spring Boot

![访问统计](https://visitor-badge.glitch.me/badge?page_id=senlypan.spring.03-spring-boot&left_color=blue&right_color=red)

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

1、定义Starter的名称和作用域：在项目的根目录下创建一个名为spring-boot-starter-{name}的模块，其中{name}是你自定义Starter的名称。该模块的作用域应该是provided，因为它不包含实现，只是用于管理依赖关系。

2、添加依赖：在Starter模块的pom.xml文件中，添加需要引入的依赖。这些依赖应该是一组相关的依赖，例如某个特定的库或组件。

3、添加自动配置：在Starter模块中添加一个spring.factories文件，指定自动配置类的全限定名。这些自动配置类应该定义了如何自动配置需要引入的依赖。

4、添加文档说明：添加一个README文件或者其他文档，说明该Starter的使用方式、提供的功能和限制等信息。

5、安装Starter到本地仓库：在Starter模块的根目录下运行mvn install命令，将该Starter安装到本地仓库。

6、在应用程序中使用Starter：在应用程序的pom.xml文件中，添加自定义的Starter依赖。Spring Boot会自动将Starter中定义的依赖引入到应用程序中，并根据自动配置类自动配置相关组件。

通过以上步骤，我们可以创建自己的Spring Boot Starter，并在应用程序中使用。自定义Starter可以使得应用程序更加模块化，提高应用程序的可维护性和可扩展性。

## 四、springboot启动流程

Spring Boot 是一个基于 Spring 框架的开发框架，其启动流程主要包括以下几个步骤：

1、加载配置文件：Spring Boot 启动时会加载项目中的配置文件，如 application.properties 或 application.yml 等，这些文件包含了应用程序的配置信息，如数据库连接信息、端口号等。

2、创建 Spring 应用上下文：Spring Boot 会创建一个 Spring 应用上下文，用于管理所有的 Bean。Spring 应用上下文可以通过注解或者 XML 文件来定义。

3、扫描注册 Bean：Spring Boot 会扫描项目中的包，查找带有特定注解的类，并将它们注册为 Bean。默认情况下，Spring Boot 会扫描启动类所在的包以及其子包。

4、自动装配：Spring Boot 会自动装配 Bean，将它们注入到需要的地方。自动装配是 Spring Boot 的一个重要特性，它可以大大减少配置工作。

5、运行应用程序：Spring Boot 会启动嵌入式的 Tomcat 服务器，并将应用程序部署到服务器上，从而使应用程序可以响应请求。

总的来说，Spring Boot 的启动流程可以归纳为加载配置文件、创建应用上下文、扫描注册 Bean、自动装配和运行应用程序等步骤。这些步骤是自动化的，让开发者可以更加专注于业务逻辑的开发，从而提高开发效率。

## 五、springboot执行流程

Spring Boot应用程序的执行流程可以大致分为以下几个步骤：

1、加载应用程序上下文

当Spring Boot应用程序启动时，它会加载应用程序上下文。应用程序上下文包含了Spring容器中的所有Bean定义和实例化对象。Spring Boot使用自动配置机制自动配置和装配容器中的组件，包括Web服务器、数据源、事务管理器等等。

2、执行CommandLineRunner和ApplicationRunner

Spring Boot提供了CommandLineRunner和ApplicationRunner接口，可以在应用程序启动后执行一些初始化操作。这些接口的实现类会被自动加载并执行（run方法）。

3、启动Web服务器

如果应用程序是一个Web应用程序，Spring Boot会自动配置和启动内嵌的Web服务器，例如Tomcat、Jetty、Undertow等等。Web服务器可以通过配置文件进行定制化。

4、处理请求

一旦Web服务器启动，应用程序就可以开始接收和处理请求了。Spring Boot会根据应用程序的注解配置和URL匹配规则，将请求分发给对应的Controller进行处理。

5、响应请求

Controller处理完请求后，会返回一个响应结果。Spring Boot会将响应结果封装为HTTP响应格式，并将其发送给客户端。

6、关闭应用程序上下文

当应用程序停止时，Spring Boot会关闭应用程序上下文。应用程序上下文中的所有Bean都会被销毁，并执行一些清理工作。

总的来说，Spring Boot应用程序的执行流程包括加载应用程序上下文、执行初始化操作、启动Web服务器、处理和响应请求以及关闭应用程序上下文等步骤。这些步骤都是通过Spring Boot的自动配置机制和约定大于配置的设计思想来实现的，可以大大简化应用程序的开发和部署工作。

## 六、SmartLifecycle  和 CommandLineRunner 的区别？

SmartLifecycle 和 CommandLineRunner 都是 Spring 框架中的接口，用于在应用启动时执行一些初始化操作。它们的区别在于：

- 生命周期控制方式不同

SmartLifecycle 接口提供了更细粒度的生命周期控制方式，可以通过实现 isRunning() 方法返回组件当前是否处于运行状态，Spring 容器会根据返回值来判断是否执行 start() 或 stop() 方法。

而 CommandLineRunner 接口没有生命周期控制方式，只能在应用启动时执行一次，无法做到类似 SmartLifecycle 中的运行状态控制。

- 方法签名不同

SmartLifecycle 接口中定义了 start()、stop()、isRunning() 和 getPhase() 方法，需要实现这些方法，才能完成相应的功能。

CommandLineRunner 接口只有一个 run() 方法，需要实现这个方法，才能完成初始化操作。

- 初始化方式不同

SmartLifecycle 接口的初始化是在 Spring 容器启动时自动注册并执行，无需手动调用。

而 CommandLineRunner 接口需要手动在 Spring 容器启动后调用，或者通过 SpringApplication.run() 方法的参数来指定。

总的来说，SmartLifecycle 和 CommandLineRunner 都可以用于在应用启动时执行一些初始化操作，但是 SmartLifecycle 提供了更细粒度的生命周期控制方式，可以根据组件的运行状态来控制启动和停止时的操作，适用于需要长期运行的任务；而 CommandLineRunner 适用于只需要在应用启动时执行一次的任务。

> Apollo 配置组件就可以通过创建了一个 ConfigChangeListener 的 bean，用于监听配置变化，再创建了一个 ApolloRefreshInitializer 的 bean，它实现了 SmartLifecycle 接口的 bean，在应用启动时注册 ConfigChangeListener，并在应用关闭时取消注册。这样就可以实现在 apollo 配置发生变化时，ConfigChangeListener 会自动执行刷新操作。

例如：

```java
@Configuration
public class ApolloConfig {

    @Bean
    public ConfigChangeListener configChangeListener() {
        return changeEvent -> {
            // 配置发生变化，执行刷新操作
            // ...
        };
    }

    @Bean
    public ApolloRefreshInitializer apolloRefreshInitializer(
        ConfigChangeListener configChangeListener) {
        return new ApolloRefreshInitializer(configChangeListener);
    }

}
```

## 七、SpringBoot中application和bootstrap配置文件的区别

在Spring Boot框架中，application和bootstrap指的是不同的配置文件，它们的加载顺序也有所不同。

bootstrap配置文件是Spring Boot框架用来配置 **系统级别** 的属性的文件，例如日志的级别、加密算法、SSL证书等。bootstrap文件是在Spring Boot启动时 **最先加载** 的配置文件，因为它需要先配置系统级别的属性，以便后续的操作可以正确地执行。

application配置文件则是用来配置 **应用程序级别** 的属性，例如数据库连接、服务器端口等。application配置文件会在bootstrap配置文件加载之后加载，因为它需要依赖bootstrap配置文件中的一些系统级别的属性来正确地配置应用程序级别的属性。

在Spring Boot中，默认情况下，bootstrap文件应该被命名为bootstrap.properties或bootstrap.yml，并且放置在类路径根目录下。而application文件则应该被命名为application.properties或application.yml，同样放置在类路径根目录下。如果需要自定义bootstrap或application文件的位置，可以在启动时通过spring.config.name和spring.config.location属性来指定。

总之，在Spring Boot框架中，bootstrap文件是最先加载的配置文件，用来配置系统级别的属性，而application文件是在bootstrap文件加载之后加载的，用来配置应用程序级别的属性。这种加载顺序可以确保系统级别的属性先被正确配置，以便后续的操作可以正确执行。


1、加载顺序

- bootstrap.yml（bootstrap.properties）先加载
- application.yml（application.properties）后加载

2、二者不同

跟 application 相比，bootstrap 配置文件具有以下几个特性：

- bootstrap 由父 ApplicationContext 加载，比 application 优先加载
- bootstrap 里面的属性不能被覆盖

3、应用场景

- application：
    - 主要用于 springboot 项目的自动化配置
- bootstrap：
    - 使用spring Cloud config 配置中心时，这时需要在bootstrap 配置文件中添加连接到配置中心的配置属性来加载外部配置中心的配置信息
    - 一些固定的不能被覆盖的配置
    - 一些加密/解密的场景

> 注意：一旦 bootStrap 被加载，则内容不会被覆盖，即便后期加载的 application 的内容标签与 bootstrap 的标签一致，application 也不会覆盖 bootstrap, 而 application 里面的内容可以动态替换。
