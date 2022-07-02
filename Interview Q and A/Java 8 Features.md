
## 1. What New Features Were Added in Java 8?

* **Lambda Expressions** − a new language feature allowing treating actions as objects
* **Method Reference**s − enable defining Lambda Expressions by referring to methods directly using their names
* **Optional **− special wrapper class used for expressing optionality
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

**Witht Method Reference :**


```java
private static void instanceReference_WithMethodRef() {
 Stream<Integer> stream = Stream.of(1,2,3,4,5,6,7,8,9);
 stream.filter(i -> i%2==0 )
  .forEach(System.out::println);
}
```
