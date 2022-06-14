
## Q How can we remove a child from a dependency Hierarchy?
 
* using <exclusions> concept.

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