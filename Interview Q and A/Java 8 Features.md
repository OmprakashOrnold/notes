
## 1. What New Features Were Added in Java 8?

* **Lambda Expressions** − a new language feature allowing treating actions as objects
* **Method Reference**s − enable defining Lambda Expressions by referring to methods directly using their names
* **Optional**− special wrapper class used for expressing optionality
* **Stream API** − a special iterator class that allows processing collections of objects in a functional manner
* **Functional Interface** – an interface with maximum one abstract method, implementation can be provided using a Lambda Expression
* **Default methods** − give us the ability to add full implementations in interfaces besides abstract methods
* **Nashorn, JavaScript Engine**− Java-based engine for executing and evaluating JavaScript code

## 2. What is the use of Functional Interface in Java 8?When to use Functional 
Interface in Java 8?
> An interface having only single abstract method is called as functional interface. Functional interface can have multiple default or static methods.

We can create a functional interface as below :

```java

public interface IConnection {

 public void connect();
 
  default void print() {
  System.out.println("in default method");
  }
 
  static void description() {
  System.out.println("in static method");
  }
}
```
> Functional interface can have only one abstract method(method without body) and can have many default and static methods.

## 3. What is the need of static method in Interface ?

Java 8 has added static methods in interface to provide utility methods on interface level without creating the object of the interface.
Some of the static methods of the java 8 are as below :
* Stream.of()
* Stream.iterate()
* Stream.empty()

## 4. What is the need of having a default method in an interface ?

* We can provide some default functionality with default methods.

* The benefit that default methods bring is that now it’s possible to add a new default method to the interface and it doesn’t break the old implementations. So that’s how java has added lots of default methods without breaking the implementation and provided the backward compatibility.

Some of the default methods available in Map interface :
* default V putIfAbsent(K key, V value)
* default boolean remove(Object key, Object value)

## 5. What is Lambda Expression in Java 8?
Lambda expression is a shorter way of writing an implementation of a single abstract method interface. Lambda expressions are used to create anonymous functions.

Syntax:
* (parameters) -> expression
or
* (parameters) -> { statements; }

Java 8 provide support for lambda expressions only with functional interfaces.

## 6. What is Method Reference in Java 8?

Java provides new feature called Method reference to call the single method of functional interface.

> Method reference is a short form of lambda expressions used on Functional Interface.


### Types of Method References in Java 8

#### 1. Reference to Static Method
Suppose that we have a static method to print the value as printMe. Now we have a stream some integers and we want to print even numbers in forEach block, Here we have used Lambda expression and passed the current value to printMe method as below :

**Without Method Reference :**

```java
import java.util.stream.Stream;

public class MethodReference {

 private static void printMe(Integer input) {
  System.out.println("Printing "+ input);
 }
 
 private static void staticReference_WithoutMethodRef() {
  Stream<Integer> stream = Stream.of(1,2,3,4,5,6,7,8,9);
  stream.filter(i -> i%2==0 )
   .forEach(i -> MethodReference.printMe(i));
 }
  
 public static void main(String[] args) {
  staticReference_WithoutMethodRef();  
 }
}
```

**With Method Reference :**


```java
private static void staticReference_WithMethodRef() {
    Stream<Integer> stream = Stream.of(1,2,3,4,5,6,7,8,9);
    stream.filter(i -> i%2==0 )
    .forEach(MethodReference::printMe);
}
```


#### 2. Reference to Instance Method from Class type
**Without Method Reference :**

```java
private static void instanceReferenceWithClass_WithoutMethodRef() {

 List<Student> students = JavaInputFixture.createList();
 
   Set<String> names = students.stream()
   .map(student -> student.getName()) // this will convert the Student Stream into String Stream by 
                   // applying the getName()
   .collect(Collectors.toSet());
 
 System.out.printf("Names of all students %sn", names);
}
```

**Without Method Reference :**

```java
private static void instanceReferenceWithClass_WithMethodRef() {

 List<Student> students = JavaInputFixture.createList();
 
 Set<String> names = students.stream()
   .map(Student::getName) // this will convert the Student Stream into String Stream by 
           // applying the getName()
   .collect(Collectors.toSet());
 
 System.out.printf("Names of all students %sn", names);
}
```

#### 3. Reference to Instance Method from instance


```java
**Without Method Reference :**
private static void instanceReference_WithoutMethodRef() {
 Stream<Integer> stream = Stream.of(1,2,3,4,5,6,7,8,9);
 stream.filter(i -> i%2==0 )
  .forEach((i -> System.out.println(i)));

```

**With Method Reference**


```java
private static void instanceReference_WithMethodRef() {
 Stream<Integer> stream = Stream.of(1,2,3,4,5,6,7,8,9);
 stream.filter(i -> i%2==0 )
  .forEach(System.out::println);
}
```
## 5.  Why to use Optional in Java 8?

* Java 8 introduced a new class java.util.Optional<T> which encapsulates a value. A container object which may or may not contain a non-null value. If a value is present, isPresent() will return true and get() will return the value.
* Additional methods that depend on the presence or absence of a contained value are provided, such as orElse(). The Optional may contain an Object or an empty instance of a class or a null value.
* For more methods of Optional please refer to below


```java
private static void getGraphicsCardSize(Lis) {
 String size = smartPhone.getGraphicsCard() 
    .map(GraphicsCard::getGraphicsMemory) // map returns the Optional of type passed as a parameter (here its string)
    .map(GraphicsMemory::getDedicatedMemory)
    .orElse("unkonwn");
 System.out.println("Size : " + size + ", for Object : "+smartPhone.toString());
}


```

## 6. What are different ways to create Optional?

1. **Optional.empty()** – This method will return an empty Optional object.

```java
Optional<GraphicsCard> card = Optional.empty();
```

2.**Optional.of()** – This method will return an Optional of object passed as an argument to the of method. Returns an Optional with the specified present non-null value.

```java
Optional<GraphicsCard> card = Optional.ofNullable(new GraphicsCard());
```

3.**Optional. ofNullable()** – Returns an Optional describing the specified value, if non-null,
otherwise returns an empty Optional

```java
Optional<GraphicsCard> card = Optional.ofNullable(null);
```

## 7. What is the Difference in between Optional.of() and Optional.ofNullable() ? Optional.of() vs Optional.ofNullable() ?

Optional.of() will return the object of Optional without null check. 

Let’s look at the interns of Optional.of() method:

```java
public static <T> Optional<T> of(T value) {
     return new Optional<>(value);
}
```
Optional.ofNullable() will return the object of Optional with a null check.

* If this method gets the null as an input then it will return the empty Optional otherwise it returns an Optional with the specified present non-null value

Let’s look at the interns of Optional.ofNullable() method:


```java
public static <T> Optional<T> ofNullable(T value) {
     return value == null ? empty() : of(value);
}
```

* Optional.of() should be used when you are sure that Optional will never have a null object and it will contain the object value or it will be empty but it will not be null. 
* Optional.of() can also throw a NullPointerEception if the Optional is created with a null value.
* Optional.ofNullable()- is used when there are chances that the object might be null.

## 8.What are methods available in Optional?
* isPresent() 
*  get()
* ifPresent(Consumer<? super T> consumer)
*  orElse(T other) 
* orElseThrow(Supplier<? extends X> exceptionSupplier)

## 9.How to filter the list of Student object who are from Pune?

filter allows you to filter the stream to process the stream.

```java
Syntax : Stream<T> filter(Predicate<? super T> predicate)
```
Lets see this with some examples :
Create a list of Student :

```java
private static List<Student> createList() {

   Student student1 = new Student("Saurabh", "Pune", 26);
   Student student2 = new Student("Robert", "Pune", 25);
   Student student3 = new Student("John", "Mumbai", 21);
   Student student4 = new Student("Roman", "Pune", 18);
   Student student5 = new Student("Randy", "Mumbai", 17);
   
   return Arrays.asList(new Student[] {student1, student2, student3, student4, student5});
}

private static void filter(List<Student> students) {
   System.out.println("Executing filter() :");
   // Print all the students who lives in Pune
   System.out.println("*** Students who lives in Pune *** ");
   students.stream()
         .filter(student -> "Pune".equals(student.getCity()))
         .forEach(System.out::println);
   
   // Find the student whose name is Saurabh and return null if not found
   System.out.println("*** Students whos name is Saurabh *** ");
   Student stud = students.stream()
         .filter(student -> SAURABH.equals(student.getName()))
         .findAny()
         .orElse(null); // it will return null if filter does find any object matching the criteria 
   
   System.out.println(stud);
   System.out.println("Ending the execution of filter()");
}
```
output


```
Executing filter()
*** Students who lives in Pune ***
Student [name=Saurabh, city=Pune, age=26]
Student [name=Robert, city=Pune, age=25]
Student [name=Roman, city=Pune, age=18]
```

## 10.How to find the object meeting certain criteria?

* we can use findAny() / findFirst() on stream to find the object based on the criteria passed an an input.
* Here we are finding the Student whose name is Saurabh.


```java
private static List<Student> createList() {

   Student student1 = new Student("Saurabh", "Pune", 26);
   Student student2 = new Student("Robert", "Pune", 25);
   Student student3 = new Student("John", "Mumbai", 21);
   Student student4 = new Student("Roman", "Pune", 18);
   Student student5 = new Student("Randy", "Mumbai", 17);
   
   return Arrays.asList(new Student[] {student1, student2, student3, student4, student5});
}

private static void filter(List<Student> students) {
   System.out.println("Executing filter() :");
   // Find the student whose name is Saurabh and return null if not found
   System.out.println("*** Students whos name is Saurabh *** ");
   Student stud = students.stream()
         .filter(student -> SAURABH.equals(student.getName()))
         .findAny()
         .orElse(null); // it will return null if filter does find any object matching the criteria 
   
   System.out.println(stud);
   System.out.println("Ending the execution of filter()");
}

```


```
*** Students whos name is Saurabh ***
Student [name=Saurabh, city=Pune, age=26]
Ending the execution of filter()
```

## 11. How to use map method? What is the use of map method? Write a program to get the age of Student whose name is Saurabh

```
<R> Stream<R> map(Function<? super T, ? extends R> mapper);
```
* A stream consisting of the results of applying the given function to the elements of this stream. Map takes an input which describes how the value needs to be transformed into.
* Suppose we want to get the age of the Student whose name is Saurabh, till now we have only retrieved the complete object from the stream but how do we do this ?
We can use map() to transform the Student Stream into the age stream as below. 
```java
int age = students.stream()
    .filter(student -> SAURABH.equals(student.getName()))
    .map(Student::getAge)
    .findAny()
    .orElse(0);
System.out.printf("*** Age of %s is %dn",SAURABH, age)
```


## 12.What is the use of flatMap() in Java 8? What is the difference between map() and flatMap()?

Suppose we want to get all the courses available in students list then we can write the code as below:

```java
Set<String> courses = students.stream()
         .map(Student::getCourses)
         .collect(Collectors.toSet());
```
* Here we will get a compilation error as below
* Type mismatch: cannot convert from Set<String[]> to Set<String>
* To resolve this issue we use flatMap()

```java
Set<String> courses = students.stream()
         .map(Student::getCourses)
         .flatMap(Arrays::stream)
         .collect(Collectors.toSet());
```
## 13. What are short circuiting operations in Java 8?
 * Short-circuit operations are same as Boolean short circuiting in java,
 * where the second condition is executed or evaluated only if the first argument does not suffice to determine the value of the expression. For example:

```java
If(str != null && str.length>10)
```
In this condition, if we pass str as null then it will only execute the first condition and evaluate the result. The same concept of short circuiting java 8 uses in Stream.

## 14. What are different short circuiting operations in Java 8?


### 1. limit() in Java 8

it limits the stream elements to process, In below example we are printing only first 5 elements from the stream


```java
int [] arr = {1,2,3,4,5,6,7,8,9,11};
  
System.out.println("*** Printing the first 5 elements of stream :");
Arrays.stream(arr)
      .limit(5)
      .forEach(System.out::println);
```
Output :
```
*** Printing the first 5 elements of stream :
1
2
3
4
5
```

### 2. findFirst(), findAny() in Java 8

firstFist() will return the first element from the Stream where as findAny returns any element from the Stream. findAny may give different result everytime.


```java
int [] arr = {1,2,3,4,5,6,7,8,9};
  
Integer findFirst = Arrays.stream(arr).filter(i -> (i%2) == 0)
  .findFirst()
  .orElse(-1);

System.out.println("findFirst : " + findFirst);

Integer findAny = Arrays.stream(arr).filter(i -> (i%2) == 0)
  .findAny()
  .orElse(-1);

System.out.println("findAny : " + findAny);
```
Output :

```
findFirst : 2
findAny : 6
```


### 3. allMatch() anyMatch() noneMatch() in Java 8

* These short circuit operators returns true or false value depending on the condition being evaluated
* allMatch() – this will evaluate the condition for all the steams and will return a boolean value.
* anyMatch() – this will evaluate the condition in the stream until it finds its match and once it finds the match, It will exit the processing and retruns the rboolean value.
* noneMatch() – This is exact opposite of allMatch()
* Lets see their behavior through some practical example.

```java
int [] arr = {1,2,3,4,5,6,7,8,9,11};
    
System.out.println("All numbers are less than 12 : " + Arrays.stream(arr).allMatch(i-> i < 12));
System.out.println("Contains any numbers greater than 10 : " + Arrays.stream(arr).anyMatch(i-> i == 8));
System.out.println("All numbers are less than 10 : " + Arrays.stream(arr).noneMatch(i-> i > 10));
```
Output :

```
All numbers are less than 12 : true
Contains any numbers greater than 10 : true
All numbers are less than 10 : false
```
## 15.What is Intermediate and Terminal Operations of Stream in Java 8?
![](https://i1.wp.com/onlyfullstack.com/wp-content/uploads/2020/11/img_5fbbc595ddb92.png?resize=678%2C135&ssl=1)


### Stream
We can create stream from object with the help of Stream.of() method.

### Intermediate Operations in Java 8
* Intermediate operation will transform a stream into another stream, they are composed forming a Pipeline of Stream execution and will not be able to execute until some terminal operation is invoked
* Intermediate Operations are lazy, so they don’t get executed until  the actual processing is required.
* Every Intermediate Operation will return the new Stream and traversal of each Stream does not begin until the terminal operation of the pipeline is executed.

Lets see how intermediate operations are lazy ?

* We have a map() function in which we are printing the current student name. These names will only be printed if we apply a terminal operator to it. In below example we have applied the collect(terminal operator) and the map() prints the student names after the thread comes into running state. This is how intermediate operations works.


```java
private static void lazyIntermediateOperations(List<Student> students) throws InterruptedException {
 System.out.println("######## Executing lazyIntermediateOperations() : ######## ");
 Stream<String> studentStream = students.stream()
            .map(student -> {
           System.out.printf("In Map : %sn", student.getName());
           return student.getName().toUpperCase();
      });
 
 System.out.println("After map statement");
 Thread.sleep(5000);
 System.out.println("Thread is in Running state now");
 studentStream.collect(Collectors.toList());
 System.out.println("######## Ending the execution of lazyIntermediateOperations() ######## ");
}
```

Output

```
######## Executing lazyIntermediateOperations() : ########
After map statement
Thread is in Running state now
In Map : Saurabh
In Map : Robert
In Map : John
In Map : Roman
In Map : Randy
######## Ending the execution of lazyIntermediateOperations() ########
```

### Intermediate Operations available in Java 8 :

•    filter(Predicate<T>)
•    map(Function<T>)
•    flatmap(Function<T>)
•    sorted(Comparator<T>)
•    peek(Consumer<T>)
•    distinct()
•    limit(long n)
•    skip(long n)

### Terminal Operations in Java 8
Terminal operations produces a non-stream (cannot be chained) result such as primitive value, a collection or no value at all.
* forEach
* toArray
* reduce
* collect
* min
* max
* count

### Short Circuiting Terminal Operations available in Java 8 :
* anyMatch
* allMatch
* noneMatch
* findFirst
* findAny

Last 5 are short-circuiting terminal operations.

## 16.Difference between Intermediate and Terminal Operations in Java 8Intermediate vs Terminal Operations in Java 8
![](https://i.ibb.co/KDh4k2z/diff.png)

## 18.Advance collectors in Java 8

### 1. joining() in Java 8

Collectors.joining will join all the results with delimiter specified in the parameter.


```java
private static void joiningCollector(List<Student> students) {
 System.out.println("######## Executing joiningCollector() : ######## ");
 String allStudents = students.stream()
   .map(Student::getName)
   .collect(Collectors.joining(" | "));
 System.out.println("Collectors.joining() : "+allStudents);
 System.out.println("######## Ending the execution of joiningCollector() ######## "); 
}

```
Output

```
######## Executing joiningCollector() : ########
Collectors.joining() : Saurabh | Robert | John | Roman | Randy
######## Ending the execution of joiningCollector() ########
```


### 2. summaryStatistics() in Java 8
It is used to calculate the sum, min, max, avg and total count of the elements passed to this method. In below example we are finding the sum, min, max of the Students age.


```java
private static void summaryStatisticsCollector(List<Student> students) {
 System.out.println("######## Executing summaryStatisticsCollector() : ######## ");
 DoubleSummaryStatistics statistics = students.stream()
   .mapToDouble(Student::getAge)
   .summaryStatistics();
 
 System.out.println("summaryStatistics() : "+statistics);
 System.out.println("Total Count : "+statistics.getCount());
 System.out.println("Total Sum : " + statistics.getSum());
 System.out.println("Minimum Age : " + statistics.getMin());
 System.out.println("Maximum Age : " + statistics.getMax());
 System.out.println("Average Age : " + statistics.getAverage());
 System.out.println("######## Ending the execution of summaryStatisticsCollector() ######## ");
}
```

Output

```
######## Executing summaryStatisticsCollector() : ########
summaryStatistics() : DoubleSummaryStatistics{count=5, sum=107.000000, min=17.000000, average=21.400000, max=26.000000}
Total Count : 5
Total Sum : 107.0
Minimum Age : 17.0
Maximum Age : 26.0
Average Age : 21.4
######## Ending the execution of summaryStatisticsCollector() ########

```


### 3. partitioningBy() in Java 8

* We can partition a set of stream in two based on certain condition. 
* So it will create two streams – one which satisfies the condition and another which does not satisfies the conditions.
* Lets see below, suppose we want to divide the students who lives in Pune and who does not live in Pune.
* partitioningBy will return a map containing two keys
* true – which holds the stream which satisfy the condition.
* false – which holds the stream which does not satisfy the condition


```java
private static void partitioningByCollector(List<Student> students) {
 System.out.println("######## Executing partitioningByCollector() : ######## ");
 Map<Boolean,List<Student>> partition = students.stream()
   .collect(Collectors.partitioningBy(stud -> stud.getCity().equals("Pune")));
 
 System.out.println("Students living in Pune : "+partition.get(true));
 System.out.println("Students not living in Pune : "+partition.get(false));
 System.out.println("######## Ending the execution of partitioningByCollector() ######## ");
}
```
Output

```
######## Executing summaryStatisticsCollector() : ########
Students living in Pune : [Student [name=Saurabh, city=Pune, age=26], Student [name=Robert, city=Pune, age=25], Student [name=Roman, city=Pune, age=18]]
Students not living in Pune : [Student [name=John, city=Mumbai, age=21], Student [name=Randy, city=Mumbai, age=17]]
######## Ending the execution of summaryStatisticsCollector() ########
```

### 4.groupingBy() in Java 8

* partitioningBy() is very simple form of grouping the stream into two, but in real life we might need more than that. groupingBy() is used to group the stream based on the condition passed to the groupingBy().
* In below example we are passing the city as an input to the groupingBy() which will split the stream into total number of cities available in the stream and will return a map as `Map<String,List<Student>>`

```java

private static void groupingByCollector(List<Student> students) {
 System.out.println("######## Executing groupingByCollector() : ######## ");
 Map<String,List<Student>> groupBy = students.stream()
   .collect(Collectors.groupingBy(Student::getCity));
 
 System.out.println("groupingByCollector : "+groupBy);
 System.out.println("######## Ending the execution of groupingByCollector() ######## ");
}
```

Output

```
######## Executing groupingByCollector() : ########
groupingByCollector : {Pune=[Student [name=Saurabh, city=Pune, age=26], Student [name=Robert, city=Pune, age=25], Student [name=Roman, city=Pune, age=18]], Mumbai=[Student [name=John, city=Mumbai, age=21], Student [name=Randy, city=Mumbai, age=17]]}
######## Ending the execution of groupingByCollector() ########
```

### 5. mappingBy() in Java 8

* `groupingBy()` splits the stream into set of groups but it collects the complete object on which groupingBy is done
* Like in above example of `groupingBy()`, we got the `Map<String,List<Student>>` where we gets the key as grouping factor and value as List<Student> objects, but what if we want to collect the names of Students or age of Students ? In this case` mappingBy()` comes into picture, `mappingBy()` allows us to pick the particular property of the Object to store into map rather than storing the complete Object.


```java
private static void mappingByCollector(List<Student> students) {
 System.out.println("######## Executing mappingByCollector() : ######## ");
 Map<String,Set<String>> mappingBy = students.stream()
   .collect(Collectors.groupingBy(Student::getCity, 
      Collectors.mapping(Student::getName, Collectors.toSet())));
 
 System.out.println("mappingByCollector : "+mappingBy);
 System.out.println("######## Ending the execution of mappingByCollector() ######## ");
}
```

Output

```
######## Executing mappingByCollector() : ########
mappingByCollector : {Pune=[Robert, Roman, Saurabh], Mumbai=[Randy, John]}
######## Ending the execution of mappingByCollector() ########

```
