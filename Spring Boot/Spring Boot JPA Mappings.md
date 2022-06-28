
## Association Mapping in JPA (HAS-A) with multiplicity (1...1/1... * / * ...1/ * ... * )

* Creating Relation between two tables, by using PrimaryKey(PK)-ForeignKey(FK) Concept
* One Table PK is taken as another table FK to create link b/w table using any multiplicity
* 1...* (meaning) = 1 row in one table are connected to many rows in another table
### Real Time Example
* 1...1 : Person --- VoterId/PanCard/Aadhar
* 1...* : Person -- BankAccount
* 1...* (and) *...1 = *...*Book --- Author
**Note:**
Incase of tables link using multiplicity, create FK Column(Extra Column)
   at many side (* side)  [for 1...  *  / * ...1]
### Non-Collection	
* 1...1 
* *...1                                     
### Collection	
* *...1  
* *...1      

## Association Mapping Implementation Steps:-

*  Apply HAS-A Relation between classes
*  Check for Collection Type (or not?), 
    if it is Collection then modify HAS-A variable as Collection variable.
*  Apply multiplicity Annotation at HAS-A Variable
*    1...1     @ManyToOne  (unique condition)
*    *...1     @ManyToOne
*    1...*     @OneToMany
*    * ... *   @ManyToMany

*  Apply JoinColumn (or) JoinTable at HAS-A Variable level
           
Code should be at parent model class (HAS-A variable level) only for any multiplicity

![](https://i.postimg.cc/m2G118cK/Spring-Boot7-AM-16102020.png)    

* => 2 Model classes
* => HAS-A Relation between them
* => Check for Collection Type or not?
* => Provide multiplicity annotation
* => Provide Join Column | Join Table
 
* => Define Repositories
* => Define Runner class for data insert
  
  1.   create objects
  2.    link based on relation
  3.    save into database


* => Check for tables for output.

Example code                                                             
### 1. Create Spring Starter Project

*  Name : SpringBoot2DataJpaManyToOneEx
*  Dep  : Spring Data Jpa, lombok, mysql


### 2. application.properties


```xml
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/boot7am
spring.datasource.username=root
spring.datasource.password=root

spring.jpa.show-sql=true
spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect
spring.jpa.hibernate.ddl-auto=create
```

### 3. Model class


```java
package in.nareshit.raghu.model;

import javax.persistence.Entity;
import javax.persistence.Id;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
@Entity
public class Dept {
	@Id
	private Integer id;
	private String code;
	
}
```

```java

package in.nareshit.raghu.model;

import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.JoinColumn;
import javax.persistence.ManyToOne;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
@Entity
public class Employee {
	@Id
	private Integer id;
	private String name;
	private Double sal;
	
	//       *...1
	//Employee---<> Dept
	@ManyToOne
	@JoinColumn(name="didFk")
	private Dept dob;
	
}
```

### 4. Repository Interface






```java
package in.nareshit.raghu.repo;
import org.springframework.data.jpa.repository.JpaRepository;
import in.nareshit.raghu.model.Dept;

public interface DeptRepository 
	extends JpaRepository<Dept, Integer> {
}
```

```java
package in.nareshit.raghu.repo;
import org.springframework.data.jpa.repository.JpaRepository;
import in.nareshit.raghu.model.Dept;

public interface DeptRepository 
	extends JpaRepository<Dept, Integer> {

}
```

### 5. Runner class


```java
package in.nareshit.raghu.runner;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

import in.nareshit.raghu.model.Dept;
import in.nareshit.raghu.model.Employee;
import in.nareshit.raghu.repo.DeptRepository;
import in.nareshit.raghu.repo.EmployeeRepository;

@Component
public class DataInsertRunner implements CommandLineRunner {
	@Autowired
	private DeptRepository drepo;
	@Autowired
	private EmployeeRepository erepo;
	
	@Override
	public void run(String... args) throws Exception {
		Dept d1 = new Dept(550, "DEV");
		Dept d2 = new Dept(551, "BA");
		
		Employee e1 = new Employee(10, "A", 3000.0, d1);
		Employee e2 = new Employee(11, "B", 4000.0, d1);
		
		Employee e3 = new Employee(12, "C", 5000.0, d2);
		Employee e4 = new Employee(13, "D", 6000.0, d2);
		
		//save objects
		drepo.save(d1);
		drepo.save(d2);
		
		erepo.save(e1);
		erepo.save(e2);
		erepo.save(e3);
		erepo.save(e4);
		
		
		
	}

}

```

