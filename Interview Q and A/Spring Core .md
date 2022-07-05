
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


## `@Primary` Annotation

* When we have multiple beans of the same type,
* we use `@Primary` to give higher preference to a particular bean
* For example, Let’s assume that we have two beans PermanentEmployee and ContractEmployee of type Employee. 
* Here, we want to give preference to PermanentEmployee. 
* Let’s observe below code to know how we will apply @Primary to give the preference.


```java
@Component  
@Primary
public class PermanentEmployee implements Employee {

 }

@Service
public class EmployeeService {
    @Autowired
    private Employee employee;
    public Employee getEmployee() {
         return employee;
    }
}
```

* Needless to say, in above EmployeeService class,
* PermanentEmployee will be injected via autowiring.


### **♥ Note :** 
* If we don’t provide @Primary in PermanentEmployee component and try to run the application, 
* Spring throws NoUniqueBeanDefinitionException. 
* However, to access beans of the same type we generally use @Qualifier(“beanName”) annotation.
* In fact we apply it at the injection point along with @Autowired. 
* In our case, as we selected the beans at the configuration phase so we can’t apply @Qualifier annotation here.

## @Qualifier Annotation

* The @Qualifier annotation provides additional information to @Autowired annotation 
* while resolving bean dependency. 
* If more than one bean of the same type is available in the container,
* we need to tell container explicitly which bean we want to inject, 
* otherwise the framework will throw an NoUniqueBeanDefinitionException, 
* indicating that more than one bean is available for autowiring. Here, 
* @Qualifier does the required job. For instance,
* let’s see how we can use the @Qualifier annotation to indicate the required bean.
Consider the below code:


```java
public interface PaymentService { }

@Service 
public class CardPaymentService implements PaymentService { }

@Service 
public class CashPaymentService implements PaymentService { }

@Controller
public class PaymentController {

    @Autowired
    @Qualifier("cardPaymentService")
    private PaymentService service;

    public void getPayment() {
    service.doPayment();
    }
}
```


## @Primary vs @Qualifier

* We can also use @Primary annotation when we need to decide which bean to inject in case of ambiguity. 
* Similar to @Qualifier, this annotation also defines a preference when multiple beans of the same type is present. 
* In that situation, the bean annotated with the @Primary will be used unless otherwise indicated. 
* However, this annotation is useful when we want to specify which bean of a certain type should be injected by default. 
* Mainly, we use @Primary in the sense of a default, 
* while @Qualifier in the sense of a very specific. 
* In case If both the @Qualifier and @Primary annotations are present, then the @Qualifier annotation will take precedence.
* In this case, we should place the @Primary annotation in one of the implementing classes
