
# Synchronized keyword in Java

* The process of allowing only a single thread to access the shared data or resource at a particular point of time is known as Synchronization.

* This helps us to protect the data from the access by multiple threads. Java provides the mechanism of synchronization using the synchronized blocks.


## Types of Synchronization in Java
There are two types of synchronization in Java. They are:

1. Process Synchronization
2. Thread Synchronization

### Process Synchronization

Process Synchronization is the term used to define Sharing the resources between two or more processes and meanwhile ensuring the inconsistency of data.

### Thread Synchronization

The concurrent execution of the critical resource by two or more Threads is termed as Thread Synchronization. Thread is the subroutine that can execute independently within a single process.

#### Example of Synchronized in Java

##### Synchronized Instance methods
*  When we use a synchronized block with the instance methods, then each object has its synchronized method.
*  There can be only one thread for each object, that can execute inside a method. If there is more than one object, then only a single thread can execute inside the block for each object.


```java
public class MyCounter {
  private int count = 0;
  public synchronized void increment(int value) {
    this.count += value;
  }
  public synchronized void decrement(int value) {
    this.count -= value;
  }
}
```
##### Synchronized Static methods

We can mark the Static methods as synchronized just like we mark the instance methods using the synchronized keyword.

```java
public static MyStaticCounter {
  private static int count = 0;
  public static synchronized void increment(int value) {
    count += value;
  }
}
```

##### Synchronized block inside Instance Methods

If you do not want to synchronize the whole method, you can just make a particular block inside the method as synchronized.

```java
public void increment(int value) {
  synchronized(this) {
    this.count += value;
  }
}
```

##### Synchronized block inside Static Methods

We can also use the Synchronized blocks inside the static methods. 


```java
public class MyClass {
  public static void print(String message) {
    synchronized(MyClass.class) {
      log.writeln(message);
    }
  }
```

## Example of Java synchronized in Multithreading

```java
// A Class used to send a message 
class Sender 
{ 
  public void sendMessage(String message)
  { 
    System.out.println("\nSending "  + message);
    try
    { 
      Thread.sleep(1000); 
    } 
    catch (Exception e) 
    { 
      System.out.println("Thread interrupted."); 
    } 
    System.out.println("\n" +message+ "Sent");
  }
} 
// Class for sending a message using Threads 
class SendUsingThreads extends Thread 
{ 
  private String message; 
  Sender sender; 

  // Receives a message object and a string message to be sent 
  SendUsingThreads(String msg, Sender object)
  { 
    message = msg;
    sender = object; 
  } 

  public void run() 
  { 
    // This will ensure that only one thread sends a message at a time. 
    synchronized(sender) 
    { 
      // synchronizing the send object 
      sender.sendMessage(message);
    } 
  } 
} 
// Driver class 
public class Demo
{ 
  public static void main(String args[]) 
  { 
    Sender sender = new Sender(); 
    SendUsingThreads sender1 = new SendUsingThreads( "Hello " , sender);
SendUsingThreads sender2 =  new SendUsingThreads( "Welcome to TechVidvan Tutorials ", sender);

    // Start two threads of SendUsingThreads type 
    sender1.start(); 
    sender2.start(); 

    // wait for threads to end 
    try
    { 
      sender1.join(); 
      sender2.join(); 
    } 
    catch(Exception e) 
    { 
      System.out.println("Interrupted"); 
    } 
  } 
} 
```


## Need for synchronized in Java

We use the Java synchronized keyword as it helps in performing various activities related to concurrent programming. Some of the essential features of the synchronized keyword are:

1. The synchronized keyword in Java provides the facility of locking, which ensures that no race condition occurs among threads.

2. The synchronized keyword also prevents the reordering of the program statements.

3. The synchronized keyword provides locking and unlocking. The thread needs to get the lock before getting inside the synchronized block. After getting the lock, it reads data from the main memory.

After reading the data, it flushes the write operation and then releases the lock.


## Important points of synchronized keyword in Java

1. Synchronized keyword in Java ensures that only a single thread can access shared data at a time.

2. Using Java synchronized keyword, we can only make a block or a method as synchronized.

3. A thread acquires a lock when it gets inside a synchronized block. And, after leaving that method, the thread releases that lock.

4. If we try to use a null object in the synchronized block then we may get a NullPointerException.

5. Using the Java synchronized keyword, we cannot use more than one JVM to provide access control to a shared resource.

6. The performance of the system can degrade due to the slow working of the synchronized keyword.


7. We should prefer to use the Java synchronized block rather than the Java synchronized method.

8. If we do not implement the synchronization properly in our code, then this might result in deadlock or starvation.

9. It is illegal to use a synchronized keyword with the constructor in Java. Also, you can not use the synchronized keyword with the variables in Java.

10. There are some important methods defined in the Object class that we can use while implementing synchronization in Java that are wait(), notify(), and notifyAll().
