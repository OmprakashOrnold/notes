
# Association – Aggregation and Composition in Java

* What if there are two classes that have some kind of relationship between them?

* For example, the classes are **Library** and **Books** or **Teacher **and **Student**, don’t you think these two classes may be associated or connected with each other.

* We can establish a relationship between them using Java **Association**. This relationship can be any type like **one to one**, **one to many**, **many to one**, or **many to many**.

* Actually, these separate classes are connected with the help of their objects. 


## What is Association in Java?


> Association is a connection or relationship between two separate classes.

> how objects of two classes are associated with each other. The Association defines the multiplicity between objects. We can describe the Association as a has-a relationship between the classes.

It can be one-to-one, one-to-many, many-to-one, many-to-many.


### Let’s take a real-life example to understand these types:

#### 1. One-to-one

The best example of a one-to-one association is that one person or one individual can have only one passport. This is a one-to-one relationship between the person and the passport.


#### 2. One-to-many

Suppose, there is a Doctor and his patients. So, one doctor is associated with many patients. So this is an example of a one-to-many Association between a doctor and patients.

#### 3. Many-to-one
For example, there can be many books in one library, each book is associated with that library, and it can’t be a part of another library. So, many books are related to one library.

This is an example of a many-to-one Association between books and a library.

#### 4. Many-to-many
If we talk about a teacher and student, there can be many students associated with one teacher, and also, the teacher can be related to many students.

So, the relationship between a teacher and student can be many-to-many.

![](https://techvidvan.com/tutorials/wp-content/uploads/sites/2/2020/06/Association-in-Java.jpg)

## Types of Java Association

There are two special forms of Association in Java. They are:
1. Composition
2. Aggregation


### Example of Association in Java


```java

class Person {
  String name;
  long id;
  Person(String name, long id) {
    this.name = name;
    this.id = id;
  }
}
class Passport extends Person {
  String personName;
  Passport(String name, long id) {
    super(name, id);
    this.personName = name;
  }
}
public class GovernmentAgency {
  public static void main(String args[]) {
    Passport obj = new Passport("Divya", 99884444);
    System.out.println(obj.personName + " is a person with a passport number: " + obj.id);
  }
}
```
Output


```
Divya is a person with a passport number: 99884444
```
In the above example, there is a one to one association between two classes: Person and Passport. Both the classes represent two separate entities.


## Aggregation in Java
* Aggregation in Java is a special kind of association. 
* It represents the Has-A relationship between classes. 
* Java Aggregation allows only one-to-one relationships.
* If an object is destroyed, it will not affect the other object, i.e., both objects can work independently.

Let’s take an example. There is an Employee in a company who belongs to a particular Department. If the Employee object gets destroyed still the Department can work independently.

```java
class Employee {
  int id;
  String name;
  String dept;
  Employee(int id, String name, String dept) {
    this.id = id;
    this.name = name;
    this.dept = dept;
    System.out.println("\nEmployee name is " + name);
    System.out.println("Employee Id is " + id);
    System.out.println("Employee belongs to the " + dept + " Department");
  }
}
class Department {
  String deptName;
  int noOfemployees;
  Department(String name, int numberOfemployees) {
    this.deptName = name;
    this.noOfemployees = numberOfemployees;
  }
}
class University {
  String universityName;
  int noOfdepartments;
  University(String name, int departments) {
    this.universityName = name;
    this.noOfdepartments = departments;
  }
}
public class AggregationDemo {
  public static void main(String[] args) {
    Employee e1 = new Employee(101, "Rishi", "Engineering");
    Employee e2 = new Employee(167, "Rohan", "Management");
    Employee e3 = new Employee(125, "Sneha", "Accounts");
  }
}
```

## Composition in Java
* In this type of association, the entities are completely dependent on each other, unlike the aggregation. Composition allows for one-to-many relationships between objects.

* It represents a part-of relationship between two objects. One entity cannot exist without the other. Composition in Java represents a one-to-many relationship.

* Suppose, there is a House and inside the house, there are many rooms. We consider the relationship between the house and the rooms.

* A single house can have multiple rooms but a single room can not have multiple houses. And, if we delete the house, the rooms will automatically be deleted.

* So the two entities: house and rooms, are dependent on each other. Room is a part of the House and they two hold a relation of composition.


```java
import java.util. * ;
class Room {
  public String roomName;
  public int roomNo;
  Room(String name, int number) {
    this.roomName = name;
    this.roomNo = number;
  }
}
class House {
  private final List < Room > rooms;
  House(List < Room > rooms) {
    this.rooms = rooms;
  }
  public List < Room > getTotalRoomsInHouse() {
    return rooms;
  }
}
public class CompositionDemo {
  public static void main(String[] args) {
    Room room1 = new Room("Dining Room", 2);
    Room room2 = new Room("Bed Room", 5);
    Room room3 = new Room("Living Room", 3);
    List < Room > books = new ArrayList < Room > ();
    books.add(room1);
    books.add(room2);
    books.add(room3);
    House house = new House(books);
    List < Room > rooms = house.getTotalRoomsInHouse();
    for (Room room: rooms) {
      System.out.println("The Room Number of " + room.roomName + " is: " + room.roomNo);
    }
  }
}
```
