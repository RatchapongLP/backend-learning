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