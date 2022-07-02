
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
