# Generics
- Helps prevent `ClassCastException` at runtime when working with collections.
- Built for type checking at compile time.
- Generic types used *without* any type arguments are called *raw types*.
- Type arguments are associated with *expressions/variables* not *instances*.

## Type Erasure
- Compiler replaces the type parameters in bytecode:
    - **Unbounded type** parameters are replaced with `Object`, e.g. `List<String>` becomes `List<Object>`
    - **Bounded type** parameters are replaced with its first bound. e.g. `T extends Comparable<T>` becomes `Comparable`
- Inserts necessary type casts for type safety ***if*** the value is used, e.g. assigned, printed, passed to another method, etc.
  For example, if the result from `<list>.get()` is ignored, no cast is generated.
- No runtime specific type arguments of a generic type at runtime, e.g., `<object_reference> instanceof List<String>` is not allowed.
- Cannot create new instances of a type parameter directly, e.g., `new T()`.

## Generics vs Array
- Generics is *compile time* construct, while array is *runtime* construct.
- Which means that a declared generic type *cannot* be cast into a different type argument like this:
  ```java
  List<Integer> integerList = new ArrayList<>();
  List<Number> numberList = (List<Number>) integerList; // Not compilable
  ```
- But the runtime information on the actual parameterized type is actually absence as `List`.
- While an array can be cast into wider array type like this:
  ```java
  Integer[] integerArr = {1, 2, 3};
  Number[] numberArr = (Number[]) integerArr; // Compilable, redundant cast
  ```
- But the runtime of the actual array instance is always array of `Integer`

> In other words, 
Arrays are not statically sound but are dynamically checked.<br>
While generics are statically sound and not dynamically checked.

See this [Stack Overflow thread](https://stackoverflow.com/questions/2927391/whats-the-reason-i-cant-create-generic-array-types-in-java) 
for Generics array topic.

## Bounded Type Parameters
### Upper Bounded Wildcards
- Use `extends` keyword to set an upper bound for a type parameter.
- Can have multiple bounds using `&` operator.
- When multiple bounds are specified, the first bound can be a class, and the rest must be interfaces.
- Example:
  ```java
  public <T extends Number & Comparable<T>> void process(T value) {
        Number num = value;
  }
  ```
- Here, `T` is bounded by `Number` and `Comparable<T>`, meaning that `T` must be a subclass of `Number` and implement `Comparable<T>`.
- Use bounded type parameters to restrict the types that can be used with generics. Especially when the method
  *produces* values that are of the extended type.

### Lower Bounded Wildcards
- Use `super` keyword to set a lower bound for a wildcard type.
- Example:
  ```java
  public void addNumbers(List<? super Integer> list) {
      list.add(1);
      list.add(2);
  }
  ```
- Here, `<? super Integer>` means that the list can accept `Integer` and any of its supertypes,e.g., `Number`, `Object`.
- Use lower bounded wildcards if the method involves modifying the input parameter, a.k.a. *consuming*. 
  Because the passed objects are always wider than the `super`ed-type value that modifies.

### PECS (Producer Extends, Consumer Super)
- An acronym to help remember when to use `extends` and `super` in generics
- **Producer Extends:** If a parameterized type is producing values (i.e., you are retrieving values from it), use `extends`.
- **Consumer Super:** If a parameterized type is consuming values (i.e., you are adding values to it), use `super`.