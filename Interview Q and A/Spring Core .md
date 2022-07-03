
## 1.Which are the Spring framework modules?

1. Core module
2. Bean module
3. Context module
4. Expression Language module
5. JDBC module
6. ORM module
7. OXM module
8. Java Messaging Service(JMS) module
9. Transaction module
10. Web module
11. Web-Servlet module
12. Web-Struts module
13. Web-Portlet module

## 2.Explain the Core Container (Application context) module?

* This is the basic Spring module, which provides the fundamental functionality of the Spring framework.
* BeanFactory is the heart of any spring-based application. 
* Spring framework was built on the top of this module, which makes the Spring container.

## 3.What is the BeanFactory – BeanFactory implementation example?
* A BeanFactory is an implementation of the factory pattern that applies Inversion of Control to separate the application’s configuration and dependencies from the actual application code.
* The most commonly used BeanFactory implementation is the XmlBeanFactory class.

## 4.XMLBeanFactory?

* The most useful one is org.springframework.beans.factory.xml.XmlBeanFactory, which loads its beans based on the definitions contained in an XML file
* This container reads the configuration metadata from an XML file and uses it to create a fully configured system or application.

## 5.How can you configure Spring in your application?
There are 3 ways to do it.  
*     XML based configuration
*     Java based configuration
*     Annotation based configuration.
## 6.What is Spring XML based configuration?
* In Spring XML based configuration, you define all dependency in an XML file.
* You define all your beans with tag in XML file and all dependencies are read using this XML file.
* for example :Sample `ApplicationContext.xml` file
<!--?xml version="1.0" encoding="UTF-8"?-->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
 

```xml
  <bean id="CountryBean" class="org.arpit.javapostsforlearning.Country">
      <property name="countryName" value="India"/>
      <property name="capital" ref="CapitalBean"/>
  </bean>
  <bean id="CapitalBean" class="org.arpit.javapostsforlearning.Capital">
      <property name="capitalName" value="Delhi"/>
  </bean>
</beans>
```
You can read this `ApplicationContext.xml `using:


```java
ApplicationContext appContext = new ClassPathXmlApplicationContext("ApplicationContext.xml");
```
## 7.What is Spring java based configuration?

In Spring Java based configuration, you inject all dependencies using java class only. You can use `@Configuaration` and `@Bean` annotations to do it.


```
import org.arpit.java2blog.model.Country;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class ApplicationConfiguration {

  @Bean(name = "countryObj")
  public Country getCountry() {
    return new Country("India");
  }

}
```
Above file is equivalent to below spring `configuration xml`
 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context-3.0.xsd">
<context:annotation-config/>
<bean id="countryObj" class="org.arpit.java2blog.Country" >
  <property name="countryName" value="India"/>
</bean>
</beans>
 
```
To get above bean to application context, you need to use below code


```java

ApplicationContext appContext = new AnnotationConfigApplicationContext(ApplicationConfiguration.class);
Country countryObj = (Country) appContext.getBean("countryObj");
```

