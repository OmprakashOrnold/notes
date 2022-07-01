
##  Serialization and Deserialization 

The basic concept is that we will convert the object into the form of a byte array and we will send that **byte array** to the server that we will again convert this byte array into the object.


> The process of converting the object into the byte stream is called **Serialization**


> when we convert the byte stream back to the object then we call it **Deserialization**


### Serialization

* Serialization is a process of writing the state of an object into a byte stream. We need to convert an object into a byte stream because the byte stream is **platform-independent**.

* So we can use this advantage by serializing an object on one platform and using the byte stream on different platforms. In order to serialize an object, we need to implement the **java.io.Serializable interface**.


> To serialize an object into a byte stream, we need to call the writeObject() method of the ObjectOutputStream class.



> To deserialize a byte stream into an object is readObject() method of ObjectInputStream class.



#### java.io.Serializable Interface

The java.io.Serializable is a marker interface that adds a Serializable behavior to a class that implements it.


### Java Serialization Example

```java
import java.io.Serializable;  
public class Teacher implements Serializable
{  
   int id;  
   String name;  
   public Teacher(int id, String name)
   {  
      this.id = id;  
      this.name = name;  
   }  
} 
```
 


```java
import java.io.*;  
public class Serialization
{  
   public static void main(String args[])
{  
     try
       {  
        //Creating the object  of Teacher class
        Teacher t1 = new Teacher(101," John");  

        //Creating the byte stream and writing the object into a file 
        FileOutputStream file = new FileOutputStream("myFile.txt");  

        ObjectOutputStream output = new ObjectOutputStream(file);  
        output.writeObject(t1);  
        output.flush();  
        
        //closing the stream  
        output.close();  
        System.out.println("Successfully created a byte stream and written it in the specified file");  
        }catch(Exception e){
          System.out.println(e);  
     } 
} 
}   

```


### Example of Deserialization


```java
import java.io.*;
public class Deserialization {
  public static void main(String args[]) {
    try {
      //Creating stream to read the object  
      ObjectInputStream input = new ObjectInputStream(new FileInputStream("myFile.txt"));
      Teacher teacher = (Teacher) input.readObject();

      //printing the data of the serialized object  
      System.out.println(“The id of the teacher is: ”+teacher.id);
      System.out.println(“The name of the teacher is: ”+teacher.name);

      //closing the stream  
      input.close();
    } catch (Exception e) {
      System.out.println(e);
    }
  }
} 
```

### Java Serialization with the static data member


> If our class contains any static data member, it will not be serialized because static is the part of the class not the object.


```java
import java.io.*;
class Student implements Serializable {
  int id;
  String name;
  static String collegename = "SVV University"; //We can’t serialize the static member

  public Student(int id, String name) {
    this.id = id;
    this.name = name;
  }
}
```

### Java Serialization with transient Keyword


> There are some cases when you don’t want to serialize any data member of a class but also include it in the code of serialization. In this case, you can mark or declare that member with the transient keyword which will restrict the member from being serialized.


```java
import java.io.*;
class Student implements Serializable {
  transient int id; //Making id transient so that it cant be serialized
  String name;

  public Student(int id, String name) {
    this.id = id;
    this.name = name;
  }
}
```

> Now, the transient member id can not be serialized. When we deserialize the object, then you will get the values of only name or other non-transient members. But the value of id as default will be returned. In our case, it will return 0 as default value as id is of int type.

### Java Serialization with SerialVersionUID

* The serialization process at runtime associates an id with each Serializable class which is known as SerialVersionUID. It is used to verify the sender and receiver of the serialized object. The sender and receiver must be the same. To verify it, SerialVersionUID is used.

* The sender and receiver must have the same SerialVersionUID, otherwise, InvalidClassException will be thrown when you deserialize the object. We can also declare our own SerialVersionUID in the Serializable class.

* To do so, you need to create a field SerialVersionUID and assign a value to it. It must be of the long type with static and final. It is suggested to explicitly declare the serialVersionUID field in the class and have it private also.

```java

import java.io.Serializable;
class Student implements Serializable {
  private static final long serialVersionUID = 123 L;
  int id;
  String name;

  public Student(int id, String name) {
    this.id = id;
    this.name = name;
  }
}
```
