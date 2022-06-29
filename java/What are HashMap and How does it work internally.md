
## What is HashMap?
**HashMap** internally uses **HashTable** implementation. This HashMap class extends **AbstractMap** class that implements the **Map** interface.

###  important points to about HashMap :

* HashMap uses its static inner class **Node<K,V>** for storing the entries into the map.
* HashMap allows **at most one null key** and multiple **null values**.
* The HashMap class **does not preserve the order of insertion** of entries into the map.
* HashMap has multiple buckets or bins which contain a head reference to a singly linked list. That means there would be as many linked lists as there are buckets. Initially, it has a bucket size of 16 which grows to 32 when the number of entries in the map crosses the 75%. (That means after inserting in 12 buckets bucket size becomes 32)
* HashMap is almost similar to Hashtable except that it’s unsynchronized and allows at max one null key and multiple null values.
* HashMap uses hashCode() and equals() methods on keys for the get and put operations. So HashMap key objects should provide a good implementation of these methods.
* That’s why the Wrapper classes like Integer and String classes are a good choice for keys for HashMap as they are immutable and their object state won’t change over the course of the execution of the program.

**Note:** Java HashMap is not thread-safe and hence it should not be used in multithreaded application. For the multi-threaded application, we should use ConcurrentHashMap class.


### How to Initialize the Constructor with Our Own Capacity and Load factor?

There are mostly 4 different constructors that can be used while creating the hashmap.


```java
Map<String, Long> myPhoneBook = new HashMap<>();
        //Bucket size 16 and LD=0.75
        Map<String, Long> myPhoneBook = new HashMap<>(64);
        //Bucket size 64 and LD=0.75
        Map<String, Long> myPhoneBook = new HashMap<>(128, 0.90f);
        //Bucket size 16 and LD=0.9
        Map<String, Long> myPhoneBook = new HashMap<>(parentsPhoneBook);
        //Bucket copy the parentsPhoneBook to myPhoneBook
```

### Frequently Used Hashmap Methods:

* **public boolean containsKey(Object key):** Returns true if this map contains a mapping for the specified key.
* **public boolean containsValue(Object value):** Returns true if this map maps one or more keys to the specified value.
* **public V get(Object key):** Returns the value to which the specified key is mapped, or null if this map contains no mapping for the key.
* **public V put(K key, V value):** Associates the specified value with the specified key in this map (optional operation). If the map previously contained a mapping for the key, the old value is replaced by the specified value.
* **public void putAll(Map<? extends K, ? extends V> m):** Copies all of the mappings from the specified map to this map. These mappings will replace any mappings that this map had for any of the keys currently in the specified map.
* **public V remove(Object key):** Removes the mapping for a key from this map if it is present (optional operation).
* **public boolean isEmpty():** A utility method returning true if no key-value mappings are present in the map.
* **public int size():** Returns the number of key-value mappings in this map. If the map contains more than Integer.MAX_VALUE elements return Integer.MAX_VALUE.
* **public Set<K> keySet():** Returns a Set view of the keys contained in this map. The set is backed by the map, so changes to the map are reflected in the set, and vice-versa.
* **public Set<Map.Entry<K,V>> entrySet():** This method returns a Set view of the HashMap mappings. This set is backed by the map, so changes to the map are reflected in the set, and vice-versa.


### Let’s See an Example of Hashmap and Its Functions:


```java
import java.util.HashMap;
import java.util.Map;
import java.util.Set;

public class PhoneBookExample {

    public static void main(String args[]) {
        Map<String, Long> myPhoneBook = new HashMap<String, Long>(100, 0.9f);

        myPhoneBook.put("Vikram", 8149535110L);
        myPhoneBook.put("Mark", 7080535110L);
        myPhoneBook.put("John", 8923535110L);

        Set<Map.Entry<String, Long>> myPhoneBookSet = myPhoneBook.entrySet();
        System.out.println("---------: Contacts in my Phone List :----------");
        for (Map.Entry<String, Long> phoneEntry : myPhoneBookSet) {
            System.out.println("Name : " + phoneEntry.getKey() + " " + " Number : " + phoneEntry.getValue());
        }
        System.out.println("------------------------------------------------");
        System.out.println("No of contacts in myPhoneBook : " + myPhoneBook.size());
        System.out.println("Vikram's Contact number : " + myPhoneBook.get("Vikram"));
        System.out.println("Delete Mark's contact : " + myPhoneBook.remove("Mark"));
    }
}

```
**output**


```
 — — — — -: Contacts in my Phone List : — — — — — 
Name : John Number : 8923535110
Name : Vikram Number : 8149535110
Name : Mark Number : 7080535110
 — — — — — — — — — — — — — — — — — — — — — — — — 
No of contacts in myPhoneBook : 3
Contact number of Vikram : 8149535110
Delete Mark’s contact : 7080535110
```
