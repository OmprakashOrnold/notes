
## OOPs Concepts – Object Oriented Programming

The main objective of the object-oriented paradigm is to implement real-world entities, like, Objects, Classes, Abstraction, Inheritance, Polymorphism, etc.


### What Is Object-Oriented Programming(OOP)?
* Object-Oriented Programming refers to programming that helps us to create the objects that we want and create methods to handle these objects. 
* The principle of OOP is to create objects, reuse the objects throughout the program, and manipulate these objects to get desired outputs.


### Benefits of Object-Oriented Programming

* Improved productivity during software development
* Improved software maintainability
* Faster development sprints
* Lower cost of development
* Higher quality software


### What is an Object?

* The object is a bundle of data and its behavior or methods. 
* Objects have two characteristics: states and behaviors.

**Object**: Student
**State**: name, age, gender
**Behavior**: study, play, run

So if we need to write a class based on states and behaviors of the Student. 


```java
class Student {
  //States as instance variables
  String name;
  String gender;
  int age;

  //Behavior as methods
  void study() {
    //Write code here
  }
  void play() {
    //Write code here
  }
  void run() {
    //code
  }
}
```

### What is Class in OOPs Concepts?

* A class is a blueprint that creates as many objects as we need. For example, we have a class Website that has two data members or fields or instance variables. This class is just a blueprint or a template. It does not represent any real website.

* But, using this class, we can create objects or instances of Website class that represent the websites. We created two objects in the below program. And, while creating objects we provided separate properties to the objects using a constructor.


```java
public class Website {
  //fields (or instance variable)
  String websiteName;
  int websiteAge;

  //constructor
  Website(String name, int age) {
    this.websiteName = name;
    this.websiteAge = age;
  }
  public static void main(String args[]) {
    //Creating objects
    Website obj1 = new Website("Techvidvan", 2);
    Website obj2 = new Website("Google", 18);

    //Accessing object data through reference
    System.out.println(“Website Name: “ + obj1.websiteName);
    System.out.println(“age: “ + obj1.websiteAge)
    System.out.println(“Website Name: “ + obj2.websiteName);
    System.out.println(“age: “ + obj2.websiteAge)
  }
}
```
output


```
Website Name: Techvidvan
age: 2
Website Name: Google
age: 18
```

### What is Method in OOP?

* A method in Java is a collection of statements that perform some specific task. The method returns the result of the statements inside it. A method can also perform some specific task without returning anything.
 
* Methods enable users to reuse the code without typing the code again. In Java, every method must belong to some class. We declare a method in Java as:


```java
accessSpecifier returnType methodName(argument-list)
```


```java
public int addNumbers(int num1, int num2)
```


## Java OOPs Concepts

After having an overview of Object-Oriented programming, let’s learn the concepts of OOPs.

 
### Abstraction 

> Abstraction is a process to represent only “relevant” or essential data and “hide” the unnecessary or background details of an object from the user.

* Let us take an example to understand abstraction. Suppose, You are driving a car. While driving, you only know the essential features of a car, such as gear handling, steering handling, use of the clutch, accelerator, brakes, etc. But while driving, do you get into the car’s internal details like wiring, motor working, etc.?

* You just change the gears or apply the brakes, etc. What is happening inside the car is hidden from you. This is an abstraction where you only know the essential things to drive a car without including the background details or explanations.

* Take another example of ‘switchboard’. You only press individual switches according to your requirement. What is happening inside, how it is happening, etc. You need not know. Again this is an abstraction; you know only the essential things to operate on the switchboard.


#### We can achieve abstraction in two ways:

a) Abstract Class
b) Interface

#### a. Abstract class
* An Abstract class in Java uses the ‘abstract’ keyword. 
* If we declare a class as abstract, we cannot instantiate it, which means we cannot create an abstract class object. 
* Also, In an abstract class, there can be abstract as well as concrete methods.

We can achieve 0-100% abstraction using abstract class.


```java
abstract class Person //abstract class
{
  abstract void talk(); //abstract method
  void walk() //non-abstract method
  {
    //code of method
  }
}

```

#### b. Interface

* An interface is a collection of abstract methods and static constants
* Each method in an interface is public and abstract, but there is no constructor. 
* Interfaces also help to achieve multiple inheritance in Java.* 


```java
public interface Car {
  //abstract methods
  abstract void run();
  Abstract void initSpeed();
}
```
