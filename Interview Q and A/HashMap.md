
# HashMap | Methods, Use, Example

> HashMap in is an unordered collection that stores elements (objects) in the form of key-value pairs (called entries).

* It is expressed as HashMap<Key, Value>, or HashMap<K, V>, where K stands for key and V for value
* Both Key and value are objects.
* HashMap uses an object to retrieve another object
* If the key is provided, its associated value can be easily retrieved from the HashMap.
* Keys in the map must be unique which means we cannot use duplicate data for keys in the HashMap

> HashMap class extends AbstractMap class and implements the Map interface


### HashMap class Declaration

```java

public class HashMap<K,V> extends AbstractMap<K,V> implements Map<K,V>, Cloneable, Serializable
```

### Features of Java HashMap class

* The underlying data structure of HashMap is HashTable.
* In simple words, HashMap internally uses hash table for storing entries. 
* That means accessing and adding an entry almost as fast as accessing an array.
* insertion order is not preserved (i.e. maintains no order). 
* It is based on the Hashcode of keys, not on the hash code of values
* HashMap contains only unique keys that means no duplicate keys are allowed but values can be duplicated. 
* We retrieve values based on the key.
* Heterogeneous objects are allowed for both keys and values.
* HashMap can have only one null key because duplicate keys are not allowed.
* Multiple null values are allowed in the HashMap.
* HashMap is not synchronized that means while using multiple threads on the HashMap object, we will get unreliable results.
*  HashMap implements Cloneable, and Serializable interfaces but not implements Random Access.
* HashMap is the best choice if our frequent operation is a search operation
* If no element exists in the HashMap, it will throw an exception named NoSuchElementException.
* Java HashMap stores only object references. Therefore, we cannot use primitive data types like double or int. We can use wrapper class like Integer or Double instead.

Example

```java
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map.Entry;

public class HashMapIterating1 {
	public static void main(String[] args) {
		HashMap<Character, String> hmap = new HashMap<>(); 

		hmap.put('V', "Violet");
		hmap.put('I', "Indigo");
		hmap.put('B', "Blue");
		hmap.put('G', "Green");
		hmap.put('Y', "Yellow");
		hmap.put('O', "Orange");
		hmap.put('R', "Red");

                Iterator<Entry<Character, String>> itr = hmap.entrySet().iterator(); // 
		System.out.println("Iterating Entries of HashMap");
		while (itr.hasNext()) {
			Object obj = itr.next();
			System.out.println(obj);
		}
		
		Iterator<Character> itr2 = hmap.keySet().iterator();
		System.out.println("Iterating Keys of HashMap");
		while (itr2.hasNext()) {
			Object keyView = itr2.next();
			System.out.println(keyView);
		}
		
		
		Iterator<String> itr3 = hmap.values().iterator(); // 
		System.out.println("Iterating Values of HashMap");
		while (itr3.hasNext()) {
			Object valuesView = itr3.next();
			System.out.println(valuesView);
		}
	}
}
```

