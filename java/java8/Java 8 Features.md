
## What are the three main features of Java 8 which make Java as a functional programming language?

Lambda expressions, functional interfaces and Stream API are the three main features of Java 8 which enables developers to write functional style of programming in Java also.


## What are lambda expressions? How this feature has changed the way you write code in Java? Explain with some before Java 8 and after Java 8 examples?

Lambda Expressions can be defined as methods without names i.e anonymous functions. Like methods, they also have parameters, a body, a return type and possible list of exceptions that can be thrown. But unlike methods, neither they have names nor they are associated with any particular class.

Lambda expressions are used where an instance of functional interface is expected. Before Java 8, anonymous inner classes are used for this purpose. After Java 8, you can use lambda expressions to implement functional interfaces.

These lambda expressions have changed the style of programming in Java significantly. They have made the Java code more clear, concise and readable than before. For example,

Below code shows how Comparator interface is implemented using anonymous inner class before Java 8.


```java
Comparator<Student> idComparator = new Comparator<Student>() {
            @Override
            public int compare(Student s1, Student s2) {
                return s1.getID()-s2.getID();
            }
        };
```
and after Java 8, above code can be written in a single line using Java 8 lambda expressions as below.


```java
Comparator<Student> idComparator = (Student s1, Student s2) -> s1.getID()-s2.getID();

```

## How the signature of lambda expressions are determined?

The signature of lambda expressions are derived from the signature of abstract method of functional interface. For example,

run() method of Runnable interface accepts nothing and returns nothing. Then signature of lambda expression implementing Runnable interface will be () -> void.

compare() method of Comparator interface takes two arguments of type Object and returns int. Then signature of lambda expression for implementing Comparator interface will be (Object, Object) -> int.

## How the compiler determines the return type of a lambda expression?
Compiler uses target type to check the return type of a lambda expression.

For example,	

```java
Runnable r = () -> System.out.println("Runnable Implementation Using Lambda Expressions");

```

In this example, target type of lambda expression is Runnable. Compiler uses run() method of Runnable interface to check the return type of lambda expression.



## What are the functional interfaces? Do they exist before Java 8 or they are the whole new features introduced in Java 8?

Functional interfaces are the interfaces which has exactly one abstract method. Functional interfaces provide only one functionality to implement.

There were functional interfaces exist before Java 8. It is not like that they are the whole new concept introduced only in Java 8. Runnable, ActionListener, Callable and Comaprator are some old functional interfaces which exist even before Java 8.

The new set of functional interfaces are introduced in Java 8 for writing lambda expressions. Lambda expressions must implement any one of these new functional interfaces.


## What are the new functional interfaces introduced in Java 8? In which package they have kept in?

Below is the list of new functional interfaces introduced in Java 8. They have kept in java.util.function package.

![](https://i0.wp.com/javaconceptoftheday.com/wp-content/uploads/2019/03/Java8FunctionalInterfaces.png?w=665&ssl=1)


## What is the difference between Predicate and BiPredicate?

Predicate is a functional interface which represents a boolean operation which takes one argument.

BiPredicate is also functional interface but it represents a boolean operation which takes two arguments


## What is the difference between Function and BiFunction?

Function is a functional interface which represents an operation which takes one argument of type T and returns result of type R.

BiFunction is also functional interface which represents an operation which takes two arguments of type T and U and returns a result of type R.


## Which functional interface do you use if you want to perform some operations on an object and returns nothing?

Consumer


## Which functional interface is the best suitable for an operation which creates new objects?

Supplier


## When you use UnaryOperator and BinaryOperator interfaces?

UnaryOperator performs same operation as Function but it is used when type of the argument and result should be of same type.

BinaryOperator performs same operation as BiFunction but it is used when type of the arguments and result should be of same type.
