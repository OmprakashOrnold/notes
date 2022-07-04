
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

* The get() method in HashMap is used to retrieve the value by its key. 
* If we don’t know the Key, it 
* will not fetch the value. The syntax for calling get() method is as follows:

```java
value = hashmap.get(key);
```

When the get(K Key) method takes a Key, it calculates the index of bucket using the method mentioned above. Then that bucket’s List is searched for the given key using equals() method and final result is returned.

## Time Complexity of put() and get() methods

HashMap stores a key-value pair in constant time which is O(1) for insertion and retrieval. 
But in the worst case, it can be O(n) when all node returns the same hash value and inserted into the same bucket.

The traversal cost of n nodes will be O(n) but after the changes made by Java 1.8 version, it can be maximum of O(log n).
## Concept of Rehashing

* Rehashing is a process that occurs automatically by HashMap when the number of keys in the map reaches the threshold value. 
* The threshold value is calculated as threshold = capacity * (load factor of 0.75).

* In this case, a new size of bucket array is created with more capacity and all the existing contents are copied over to it.
example


```
Load Factor: 0.75
Initial Capacity: 16 (Available Capacity initially)
Threshold = Load Factor * Available Capacity = 0.75 * 16 = 12
```
When 13th key-value pair is inserted into the HashMap, HashMap grows its bucket array size to 16*2 = 32.

Now Available capacity: 32


```
Threshold = Load Factor * Available Capacity = 0.75 * 32 = 24
```
Next time when 25th key-value pair is inserted into HashMap, HashMap grows its bucket array size to 32*2 = 64 and so on.