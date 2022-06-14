
## **Q How can we remove a child from a dependency Hierarchy?**
     using <exclusions> concept.
```xml
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
