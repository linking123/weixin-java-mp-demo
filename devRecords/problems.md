
# 1. 说明

本文件记录开发过程中遇到的问题。包括但不限于编码问题。


# 2. 问题描述、原因及解决方法

## ajax request HTTP status 400

服务器返回400错误。

原因：form表单提交的字段名称与后端接收的model类型中字段 数据类型 不一致。

解决方式：form表单中字段用model类型的字段；保证类型一致，尤其是long和string。


## db.properties 中 jdbc.username 和 jdbc.password设反

注意反了，难找到。

## ModelAndView setview 页面不跳转，刷新后才跳转

Ajax请求不能用ModelAndView返回。

## Can't find bundle for base name system, locale zh_CN

```
private static final ResourceBundle BUNDLE = ResourceBundle.getBundle("system");
```

引入  system.property 文件


## com.mysql.jdbc.driver

注意引入 mysql-connect..jar

##  BeanNotOfRequiredTypeException... but was actually of type 'com.sun.proxy.$Proxy**'

- 解决方法

```
<!--开启基于注解的事务，使用xml配置形式的事务（必要主要的都是使用配置式）  -->  
<aop:config>  
    <!-- 切入点表达式 -->  
    <aop:pointcut expression="execution(* com.qihang.service..*(..))" id="txPoint"/>  
    <!-- 拦截器方式配置事务增强 txAdvice = tx:advice -->  
    <aop:advisor advice-ref="txAdvice" pointcut-ref="txPoint"/>  
</aop:config>  
<aop:aspectj-autoproxy  proxy-target-class="true"/>  
```

- 参考

http://blog.csdn.net/CSDN___LYY/article/details/76687588

- 错误信息：
```
Caused by: org.springframework.beans.factory.BeanNotOfRequiredTypeException: Bean named 'weixinService' is expected to be of type [com.suncreate.service.WeixinService] but was actually of type [com.sun.proxy.$Proxy23]
```


## At least one base package must be specified

- 原因

某些 service、controller、mapper、handler、config未扫描到。

- 解决方法

1.检查 web.xml contextConfigLocation 两处配置

```
# 引入需要 SpringMVC 扫描的xml文件 
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:spring-core.xml,classpath:spring-mybatis.xml,classpath:spring-redis.xml</param-value>
</context-param>

# servlet 配置 spring-mvc.xml
<init-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:spring-mvc.xml</param-value>
</init-param>
```

2. 检查修改项目结构，加入扫描路径。

```
<!-- 自动扫描(自动注入) -->
<context:component-scan base-package="com.suncreate.**.dao"/>
<context:component-scan base-package="com.suncreate.**.service"/>
<context:component-scan base-package="com.suncreate.handler"/>
<context:component-scan base-package="com.suncreate.config"/>
```


- 错误信息如下
```
[ERROR] 2018-01-18 18:43:37,924 [RMI TCP Connection(3)-127.0.0.1]:org.springframework.web.context.ContextLoader:351#initWebApplicationContext() Context initialization failed
java.lang.IllegalArgumentException: At least one base package must be specified
	at org.springframework.util.Assert.notEmpty(Assert.java:222)
	at org.springframework.context.annotation.ClassPathBeanDefinitionScanner.doScan(ClassPathBeanDefinitionScanner.java:245)
	at org.mybatis.spring.mapper.ClassPathMapperScanner.doScan(ClassPathMapperScanner.java:155)
	at org.mybatis.spring.annotation.MapperScannerRegistrar.registerBeanDefinit。。。
[INFO ] 2018-01-18 18:43:37,939 [RMI TCP Connection(3)-127.0.0.1]:org.springframework.web.context.support.XmlWebApplicationContext:982#doClose() Closing Root WebApplicationContext: startup date [Thu Jan 18 18:43:36 CST 2018]; root of context hierarchy
一月 18, 2018 6:43:37 下午 org.apache.catalina.core.StandardContext startInternal
严重: Error listenerStart
一月 18, 2018 6:43:37 下午 org.apache.catalina.core.StandardContext startInternal
严重: Context [] startup failed due to previous errors
[WARN ] 2018-01-18 18:43:37,955 [RMI TCP Connection(3)-127.0.0.1]:org.springframework.web.context.support.XmlWebApplicationContext:1000#doClose() Exception thrown from LifecycleProcessor on context close
java.lang.IllegalStateException: LifecycleProcessor not initialized - call 'refresh' before invoking lifecycle methods via the context: Root WebApplicationContext: startup date [Thu Jan 18 18:43:36 CST 2018]; root of context hierarchy
	at org.springframework.context.support.AbstractApplicationContext.getLifecycleProcessor(AbstractApplicationContext.java:416)
	at org.springframework.context.support.AbstractApplicationContext.doClose(AbstractApplicationContext.java:997)
	。。。
[DEBUG] 2018-01-18 18:43:37,971 [RMI TCP Connection(3)-127.0.0.1]:org.springframework.beans.factory.support.DefaultListableBeanFactory:512#destroySingletons() Destroying singletons in org.springframework.beans.factory.support.DefaultListableBeanFactory@7b0cb1e8: defining beans [wxProperties,org.springframework.context.support.PropertySourcesPlaceholderConfigurer#0,secuUserMapper,org.springframework.context.annotation.internalConfigurationAnnotationProcessor,org.springframework.context.annotation.internalAutowiredAnnotationProcessor,org.springframework.context.annotation.internalRequiredAnnotationProcessor,org.springframework.context.annotation.internalCommonAnnotationProcessor,org.springframework.context.event.internalEventListenerProcessor,org.springframework.context.event.inte
[2018-01-18 06:43:37,986] Artifact schoolManageWecht:war: Error during artifact deployment. See server log for details.
```

## redirect 和 forward运用

```
# forward 绝对路径
view.setViewName("forward: /propertyReport/toReportNav");
# forward 类内部路径
view.setViewName("forward: propertyReport/toReportNav");
# 差别在前面的`/`

# redirect 
view.setViewName("forward: /propertyReport/toReportNav");    
```

## 微信公众号子菜单url size超限

```
me.chanjar.weixin.common.exception.WxErrorException: 
{"errcode":40027,"errmsg":"invalid sub button url size hint: 
[GGFBJA0389vr24]"}
```

网友评论:
```
1. 微信服务器老爱抽风。
2. 这不是你们的问题，是微信服务器自身的问题，过一段时间了再试，直到成功。

```

参考链接：
1. https://www.cnblogs.com/zouke1220/p/7458878.html
2. [微信返回码查看](https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421141013)

发现问题：
```
我将 button23.setUrl(baseUrl + "frame");
写成了 button23.setPagePath(baseUrl + "frame");
```