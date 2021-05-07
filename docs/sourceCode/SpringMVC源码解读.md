>当我们聊到SpringMVC的时候我们应该想到什么？给定几个核心的锚点，then go on...
- SpringMVC中的Bean容器有哪些？SpringMVC是如何创建、初始化、以及销毁这些Bean的容器的？
- SpringMVC是如何处理一次HTTP请求的？
- SpringMVC容器的生命周期，对我们业务代码设计应用会有什么帮助吗？

## SpringMVC中的Bean容器
一般情况，我们会在一个web应用中配置两个容器。一个容器用于加载web层的类，比如我们的接口Controller、HandlerMapping、ViewResolver等。我们把这个容器称为web容器；
另一个容器用于加载业务逻辑相关的类，比如 service、dao 层的一些类，我们把这个容器叫做业务容器，源码叫RootWebApplicationContext。
- 容器初始化的过程中，业务容器会先于web容器进行初始化。
- web 容器初始化时，会将业务容器作为父容器，因为web容器中的一些bean会依赖业务容器中的bean；比如我们controller层的接口通常会依赖service层的业务逻辑。
### 业务容器的创建过程
业务容器创建入口是ContextLoaderListener的contextInitialized(ServletContextEvent event)方法。顾名思义，ContextLoaderListener
实现了ServletContextListener接口，当Servlet容器（jetty或tomcat）启动时发送出ServletContextEvent事件，ContextLoaderListener可以监听该事件；同时继承了ContextLoader
加载器，可以在监听到容器启动后的ServletContext事件后就可以加载applicationContext.xml配置文件，并初始化root WebApplicationContext业务容器；

    <web-app>
        <listener>
            <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
        </listener>	
        <context-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:applicationContext.xml</param-value>
        </context-param>
        <!-- 省略其他  -->
    </web-app> 



### 业务容器的销毁过程
业务容器销毁的入口是ContextLoaderListener的contextDestroyed(ServletContextEvent event)方法。顾名思义，ContextLoaderListener是用来监听Servlet
容器（jetty或tomcat）启动时发送的ServletContextEvent事件；
### Web容器的创建过程

### Web容器的销毁过程


## SpringMVC处理HTTP请求




































