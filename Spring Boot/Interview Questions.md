## Q) How can we load a properties file in Spring/Spring Boot manuall
```
 @PropertySource("classpath:abcd.properties")
 @PropertySource("file:./abcd.properties")   [inside project folder]
 @PropertySource("file:d:/data/abcd.properties")  [inside D:/data folder
```
*  By using this annotation YAML files can not be loaded, only properties files  
*  YAML can be read using Snake YAML API only.
*  By default application.properties is loaded with priority.

## Q) How spring container will scan/find classes in project? 
*  By using: **@ComponentScan("") ** by default value is starter class package name.
*  We can even modify default value, then starter class package rule never works.

*  Multiple packages can also be provided:
*  @ComponentScan({"pack1","pack2","pack3","pack4",.....})

## Q)For which annotations Spring container creates object?

1. For StereoType Annotations [ @Component]
2. Java Config Annotations [ @Bean ]

    Some other types are sub type of @Component only : 
    @Repository, @Service, @Controller, @RestController..etc

## Q What is the difference between @Component and @Configuration?  
* **@Component** : Used for creating object to our classes only.[never works for pre-defined]
* **@Configuration ** :Is used to indicate Input file to Spring container that holds 
    object (@Bean) details. It is called as Java based configuration file.

     
## Q)What is the difference between @Bean and @Component? 
* **@Component **: Create object for Programmer defined classes.
* **@Bean**      : Create object For both pre and Programmer defined classes.
                But used mostly for pre-defined only.


## Q)What is the Type of Spring container used in Spring Boot? What are other types even?
* In Spring Boot Container type is : ApplicationContext
* other type is : BeanFactory(legacy) that supports only XML Configuration.

## Q) What are scopes in Spring? Which one is default? Why they are used
 Scope - in programming is life time/accessbility of data(variable/object..)

 singleton (default)
 prototype
 request
 session
 application 



## Q How can we remove a child from a dependency Hierarchy?
 
* using < exclusions > concept.

```java
         <dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context</artifactId>
			<version>5.2.8.RELEASE</version>
			<exclusions>
				<exclusion>
					<groupId>org.springframework</groupId>
					<artifactId>spring-aop</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
```

## Q) Why exclusions used in Realtime?
     
*   To avoid legacy APIs and add/migrate to new APIs (new concepts in place of old).
Ex: Remove junit-vintage-engine = JUnit 3/JUnit 4 support from Spring boot and add
    only JUnit5 support
  
```java
           <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
			<exclusions>
				<exclusion>
					<groupId>org.junit.vintage</groupId>
					<artifactId>junit-vintage-engine</artifactId>
				</exclusion>
			</exclusions>
		</dependency>

```

## Q) What are different Scopes in Maven ? Why they used?

* Scope - When a Jar is loaded/used.
* compile - Jar is used from compile time onwards
* test    - Jar used only for UnitTesting
* runtime - Jar used only at runtime, not a compile time
* provided - Jar is handled by Servers/Container/F/w
* system   - Jar loaded from System Drives (local folders)
* import - Only for <dependencyManagement>

## Q)How can we convert our project into JAR file/WAR file?
* build : maven clean  maven package (or) maven install
* build: Convert Project into final format (.jar/.war)
* need not to write: default <packaging>jar</packaging>
* for web applications: <packaging>war</packaging>

## Q)How Spring boot is handling jar/dependency versions?
* By using Spring Boot Parent Project as : dependencyManagement tag

## Q)How can we link our project with Spring Boot parent project?
* By using a tag called :  < parent > in pom.xml

```
<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.3.4.RELEASE</version>
       	</parent>
```

