# Collections
- All types of collections extends from the `Collection` interface in Java, except for `Map`.
- All collections are generic types.

## `Collection` interface
- The root interface in the collection hierarchy.
- Extends `Iterable` interface.
- Defines basic methods for adding, removing, and checking elements in a collection.
- Commonly used subinterfaces:
    - `List`: An ordered collection (also known as a sequence) that allows duplicate elements.
    - `Set`: A collection that does not allow duplicate elements.
    - `Queue`: A collection designed for holding elements prior to processing, typically in a FIFO manner.
    - `Deque`: A double-ended queue that allows insertion and removal of elements from both ends.
- For `add`, some implementations may throw `UnsupportedOperationException` if the collection is unmodifiable.

## `equals()`
- Reflexivity: For any non-null reference value `x`, `x.equals(x)` should return `true`.
- Symmetry: For any non-null reference values `x` and `y`, `x.equals(y)` should return `true` if and only if `y.equals(x)` returns `true`.
- Transitivity: For any non-null reference values `x`, `y`, and `z`, if `x.equals(y)` returns `true` and `y.equals(z)` returns `true`, then `x.equals(z)` should return `true`.
- Consistency: For any non-null reference values `x` and `y`, multiple invocations of `x.equals(y)` should consistently return `true` or consistently return `false`, provided no information used in `equals` comparisons on the objects is modified.
- Non-nullity: For any non-null reference value `x`, `x.equals(null)` should return `false`.
- For properties equality checking of the object, they need not satisfy non-nullity if certain properties can be null.
- Example:
```java
@Override
public boolean equals(Object obj) {
    if (this == obj) return true;
    if (obj == null || getClass() != obj.getClass()) return false;
    MyClass other = (MyClass) obj;
    return Objects.equals(this.property1, other.property1) &&
            this.id == other.id;
}
```
- By default, any `Object` uses reference equality (i.e., `==` operator) for `equals()` method.

## `hashCode()`
- Consistency: The `hashCode` method must consistently return the same integer value, provided that the object is not modified in a way that affects `equals` comparisons.  
  This must hold:
> a.equals(b) == true → a.hashCode() == b.hashCode()
- Unequal objects can have the same hash code, but the reverse is not true. Because hash collisions can occur when different objects produce the same hash code.  
  This does ***not*** necessarily hold:
> a.hashCode() == b.hashCode() → a.equals(b) == true  

So collections like HashMap or HashSet rely on:
1. hashCode() → group objects into buckets
2. equals() → precisely check whether two objects are equal inside the bucket.

- By default, The Object.hashCode() method is a native method, which returns distinct integers for distinct objects. 
(This is typically implemented by converting the internal address of the object into an integer, 
but this implementation technique is not required by the JavaTM programming language.)
  
- `Objects` class provides hashing utility methods:

    - `Objects.hash(Object... values)`: 
  
      - Generates a hash code for a sequence of input values.
      - Uses Arrays.hashCode(Object[] a) internally, which implements in the same way as `List.hashCode()`.
      ```java
      int hashCode = 1;
      for (E e : list)
        hashCode = 31 * hashCode + (e == null ? 0 : e.hashCode());
      ```
      
    - `Objects.hashCode(Object o)`: 
      - Returns the hash code of the given object, or 0 if the object is null.
      - Calls `o.hashCode()` under the hood if `o` is not null.

## `Comparable<T>`
- An interface that defines a natural ordering for objects of a class.
- Contains the method `compareTo(T o)`, which compares the current object with the specified object.
- The `compareTo` method returns:
    - A negative integer if the current object is less than the specified object.
    - Zero if the current object is equal to the specified object.
    - A positive integer if the current object is greater than the specified object.
- Classes that implement `Comparable` can be sorted using sorting algorithms or data structures that rely on natural ordering (e.g., `TreeSet`, `TreeMap`).
- Example:
```java
public class MyClass implements Comparable<MyClass> {
    private int value;
    public MyClass(int value) {
        this.value = value;
    }
    @Override
    public int compareTo(MyClass other) {
        return Integer.compare(this.value, other.value);
    }
}
```

## `Comparator<T>`
- An interface that defines a custom ordering for objects of a class.
- Contains the method `compare(T o1, T o2)`, which compares two objects.
- The `compare` method returns the same results as `compareTo`.
- `Comparator` can be used to define multiple orderings for a class, unlike `Comparable`, which defines a single natural ordering.
- Example:
```java
public class MyClassComparator implements Comparator<MyClass> {
    @Override
    public int compare(MyClass o1, MyClass o2) {
        return Integer.compare(o1.getValue(), o2.getValue());
    }
}
```

## `Iterable<T>` interface
- The root interface for all iterable collections in Java.
- Defines the method `iterator()`, which returns an `Iterator` over elements of type `T`.
- Allows the use of enhanced for-loops (for-each loops) to iterate over collections.
```java
for (T element : collection) {
    System.out.println(element);
}
```
- **fail-fast iterator**: 
    - If the collection is modified structurally, e.g., adding or removing elements, *after* the iterator is created, 
    the iterator will throw a `ConcurrentModificationException` on the next `iterator.next()` on a best-effort basis.
    - This behavior comes from the `modCount` field in collection implementations, an internal modification counter.

## `List<T>`
- An ordered collection (also known as a sequence)
- Allows duplicate elements.
- Typically allows multiple null elements if allows null elements at all.
- Common implementations: `ArrayList`, `LinkedList`, `Vector`, `Stack`, `CopyOnWriteArrayList`.
- Supports iteration in the order of insertion and also reverse iteration.
- Methods:
    - `add(int index, T element)`: Inserts the specified element at the specified position, *shifts all the subsequent elements to the right8.
    - `remove(int index)`: Removes the element at the specified position, *shifts any subsequent elements to the left*.
    - `indexOf(Object o)`: Returns the index of the first occurrence of the specified element, or -1 if not found.

### `ArrayList<T>`
- A resizable array implementation of the `List` interface.
- Used an array under the hood.
- Provides $O(1)$ time complexity for add, get, set, etc. on general. 
- Provides amortized constant time complexity for `add(T element)` operation.

### `LinkedList<T>`
- A doubly-linked list implementation of the `List` and `Deque` interfaces.
- Each element (node) contains a reference to the previous and next node.
- Provides $O(n)$ time complexity for add, get, set, etc. on general.
- Provides $O(1)$ for appending and removing at the end of the list,

### `Vector<T>`
- Exists since Java 1.0, before the introduction of the Collections Framework in Java 2 (Java 1.2).
- A synchronized (thread-safe) implementation of the `List` interface.
- Similar to `ArrayList`, but with synchronized methods.
- Generally slower than `ArrayList` due to synchronization overhead.
- For multi-threaded environments, consider using `Collections.synchronizedList()` or `CopyOnWriteArrayList` instead.

## `Arrays.asList()`
- ***Fixed-size List:***
    Because `Arrays.asList()` is 
***backed by the original array***. This means you cannot add or remove elements from this List, 
as these operations would change the size, which is not allowed for an array-backed List. 
Attempting to do so will result in an `UnsupportedOperationException`.
 
- ***Backed by the original array:***
    Any modifications made to the elements of the returned List will directly reflect in 
the original array, and vice versa. This is because the List is a view of the array, not a separate copy.

- ***Allows null values:***
    Unlike `List.of()`, `Arrays.asList()` permits null values within the array and consequently 
within the returned List.

- ***Handles primitive arrays differently:***
    When used with an array of primitive types (e.g., `int[]`, `char[]`), Arrays.asList() treats 
the entire primitive array as a single element, creating a List containing only one element, 
which is the primitive array itself. To create a List of individual primitive values, you need 
to use wrapper classes (e.g., `Integer[]` instead of `int[]`).
```
    Arrays.asList(new int[]{1, 2, 3}); // This gives a List of one element: [{1, 2, 3}]
    Arrays.asList(new Integer[]{1, 2, 3}); // This gives a List of elements: [1, 2, 3]
```
## `Arrays.asList()` vs `List.of()`
A practical summary of an answer in a [Stack Overflow thread](https://stackoverflow.com/questions/46579074/what-is-the-difference-between-list-of-and-arrays-aslist):

[//]: # (<img src="images/arrays_aslist_vs_list_of.jpg" width="450">)
![](images/arrays_aslist_vs_list_of.jpg)