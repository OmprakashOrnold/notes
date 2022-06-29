
# Singleton design pattern

>               

A Singleton class allows only one instance to be created and provides global access to all other classes through this single object or instance.

> 


* The primary purpose of Single class is to restrict the limit of the number of object creation to only one



## To design a singleton class, we need to do the following things:

*  Firstly, declare the constructor of the Singleton class with the private keyword.
*  We declare it as private so that no other classes can instantiate or make objects from it.
*  A private static variable of the same class that is the only instance of the class.
*  Declare a static factory method with the return type as an object of this singleton class.


## There are two forms of singleton design pattern, which are:

* **Early Instantiation:** The object creation takes place at the load time.
*  **Lazy Instantiation:** The object creation is done according to the requirement


### Early Instantiation


```java
public class EagerInitialization
{
  //Instance will be created at load time
  private static EagerInitialization obj = new EarlyInitialization();
  public String string;

  //Creating private constructor
  private EagerInitialization()
  {
    string = "Welcome to TechVidvan's Tutorial of Java";
  }

  //Declaring static method
  public static EagerInitialization getInstance()
  {
    return obj;
  }

  public static void main(String args[])
  {
    EagerInitialization text = EagerInitialization.getInstance();
    //original string
    System.out.println("Original String:");
    System.out.println(text.string);

    //text in upper case
    System.out.println("String in Upper Case:");
    text.string = (text.string).toUpperCase();
    System.out.println(text.string);
  }
}
```


### LazyInitialization


```java
public class LazyInitialization
{
  // private instance, so that it can be
  // accessed by only by getInstance() method
  private static LazyInitialization instance;
  public String string;
  private LazyInitialization ()
  {
    // private constructor
    string = "Welcome to TechVidvan's Tutorial of Java";
  }
  //method to return instance of class
  public static LazyInitialization getInstance()
  {
    if (instance == null)
    {
      // if instance is null, initialize
      instance = new LazyInitialization ();
    }
    return instance;
  }
  public static void main(String args[])
  {
    LazyInitialization text = LazyInitialization .getInstance();
    //original string
    System.out.println("The String is:");
    System.out.println(text.string);
  }
}

```

[Click Referance From Here](https://techvidvan.com/tutorials/java-singleton-class/)