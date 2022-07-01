
##  Serialization and Deserialization 

The basic concept is that we will convert the object into the form of a byte array and we will send that **byte array** to the server that we will again convert this byte array into the object.


> The process of converting the object into the byte stream is called **Serialization**


> when we convert the byte stream back to the object then we call it **Deserialization**


### Serialization

* Serialization is a process of writing the state of an object into a byte stream. We need to convert an object into a byte stream because the byte stream is **platform-independent**.

* So we can use this advantage by serializing an object on one platform and using the byte stream on different platforms. In order to serialize an object, we need to implement the **java.io.Serializable interface**.

To serialize an object into a byte stream, we need to call the writeObject() method of the ObjectOutputStream class.


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
      }
catch(Exception e)
{
System.out.println(e);  
     } 
} 
}   

```
