
# HashMap Internal Working

## HashMap

* HashMap in Java is basically an array of buckets (also known as bucket table of HashMap) 
* where each bucket uses linked list to hold elements.
* A linked list is a list of nodes where each node contains a key-value pair.

* In simple words, a bucket is a linked list of nodes where each node is an object of class Node<K,V>.
* The key of the node is used to obtain the hash value and this hash value is used to find the bucket from Bucket Table.

* HashMap works on the principle of hashing data structure or technique that uses an object’s hashcode to place that object inside the map.

* Hashing involves Bucket, Hash function (hashCode() method), and Hash value. It provides the best time complexity of O(1) for insertion and retrieval of objects.

* Therefore, it is the best-suited data structure for storing key-value pairs that later on can be retrieved in minimum time.


## Put Operation: How put() method of Hashmap works internally in Java?
> The put() method of HashMap is used to store the key-value pairs.
The syntax of put() method to add key/value pair is as follows:

```java
hashmap.put(key, value);

```

Let’s take an example where we will insert three (Key, Value) pairs in the HashMap.

```java

HashMap<String, Integer> hmap = new HashMap<>();  
 
 hmap.put("John", 20);  
 hmap.put("Harry", 5);  
 hmap.put("Deep", 10);
```
Let’s understand at which index the key-value pairs will be stored into HashMap.

* When we call the put() method to add a key-value pair to hashmap
* HashMap calculates hash code of key by calling its hashCode() method.
* HashMap uses that code to calculate the bucket index in which key/value pair will be placed.

The formula for calculating the index of bucket (where n is the size of an array of the bucket) is given below:

```
Index = hashCode(key) & (n-1);
```

Suppose the hash code value for “John” is 2657860. Then the index value for “John” is:


```
Index = 2657860 & (16-1) = 4
```
The value 4 is the computed index value where the key and value will be store in HashMap.

**Note:** Since HashMap allows only one null Key, the hash value returned by the hashCode(key) method will be 0 because the hashcode for null is always 0. The 0th bucket location will be used to place key/value pair


## How get() method in HashMap works internally in Java?
## Time Complexity of put() and get() methods
## Concept of Rehashing