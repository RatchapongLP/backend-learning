### Generic
- Helps prevent `ClassCastException` at runtime when working with collections.
- Built for type checking at compile time.
#### Type Erasure
- Compiler replaces the type parameters in bytecode:
    - **Unbounded type** parameters are replaced with `Object`, e.g. `List<String>` becomes `List<Object>`
    - **Bounded type** parameters are replaced with its first bound. e.g. `T extends Comparable<T>` becomes `Comparable`
- Inserts necessary type casts for type safety.
- No runtime specific type arguments of a generic type at runtime, e.g., `list instanceof List<String>` is not allowed.
- Cannot create new instances of a type parameter directly, e.g., `new T()`.