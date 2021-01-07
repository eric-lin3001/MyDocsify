# Collection vs Collections in Java with Example

Last Updated: 02-09-2020

**Collection:** Collection is a [interface](https://www.geeksforgeeks.org/interfaces-in-java/) present in java.util.package. It is used to represent a group of individual objects as a single unit. It is similar to the container in the [C++](https://www.geeksforgeeks.org/c-plus-plus/) language. The collection is considered as the root interface of the collection framework. It provides several classes and interfaces to represent a group of individual objects as a single unit. 

The [List](https://www.geeksforgeeks.org/list-interface-java-examples/), [Set](https://www.geeksforgeeks.org/set-in-java/), and [Queue](https://www.geeksforgeeks.org/queue-interface-java/) are the main sub-interfaces of the collection interface. The map interface is also part of the java collection framework, but it doesn’t inherit the collection of the interface. The **add()**, **remove()**, **clear()**, **size()**, and **contains()** are the important methods of the Collection interface.

**Declaration:**

```java
public interface Collection<E> extends Iterable<E>

Type Parameters: E - the type of elements returned by this iterator
```

**Collections:** Collections is a utility class present in java.util.package. It defines several utility methods like sorting and searching which is used to operate on collection. It has all static methods. These methods provide much-needed convenience to developers, allowing them to effectively work with [Collection Framework](https://www.geeksforgeeks.org/collections-in-java-2/). For example, It has a method *sort()* to sort the collection elements according to default sorting order, and it has a method *min()*, and *max()* to find the minimum and maximum value respectively in the collection elements.

**Declaration:**

```java
public class Collections extends Object
```

**Methods:**

1. Collections.copy(des,src); 
   - The destination list must be at least as long as the source list.
2. Collections.reverse(list);
3. Collections.fill(list,"X");
   - 将list中的每个元素替换为X（假设list的类型为list<String>）.

4. Collections.addAll(des,src);

   - des类型为list，src类型为T... elements，可以是array，但二者子类型必须相同。

   - 二者区别？

     ```java
     Collections.addAll(list2,a);
     Arrays.asList(a);
     ```

5. Collections.frequency(list,element);
   - returns counts of 'element' in the list

6. Collections.disjoint(list1,list2);
   - returns true if list1 & list2 has nothing in common.
   - returns false if list1 & list2 has at least one element in common.