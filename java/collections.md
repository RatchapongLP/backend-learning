# Collections

## `Arrays.asList()`
- ### Fixed-size List:
    Because `Arrays.asList()` is 
***backed by the original array***. This means you cannot add or remove elements from this List, 
as these operations would change the size, which is not allowed for an array-backed List. 
Attempting to do so will result in an `UnsupportedOperationException`.
 
- ### Backed by the original array:
    Any modifications made to the elements of the returned List will directly reflect in 
the original array, and vice versa. This is because the List is a view of the array, not a separate copy.

- ### Allows null values:
    Unlike `List.of()`, `Arrays.asList()` permits null values within the array and consequently 
within the returned List.

- ### Handles primitive arrays differently:
    When used with an array of primitive types (e.g., `int[]`, `char[]`), Arrays.asList() treats 
the entire primitive array as a single element, creating a List containing only one element, 
which is the primitive array itself. To create a List of individual primitive values, you need 
to use wrapper classes (e.g., `Integer[]` instead of `int[]`).
```
Arrays.asList(new int[]{1, 2, 3}); // This gives a List of one element: [{1, 2, 3}]
Arrays.asList(new Integer[]{1, 2, 3}); // This gives a List of elements: [1, 2, 3]
```