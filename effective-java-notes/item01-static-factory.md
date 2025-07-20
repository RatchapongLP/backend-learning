# 📘 Effective Java – Item 1: Consider static factory methods instead of constructors

## 🧪 Example:
```
public class Color {
    private final int red, green, blue;

    // Hidden constructor
    private Color(int r, int g, int b) {
        this.red = r; this.green = g; this.blue = b;
    }

    // Static factory method
    public static Color ofRGB(int r, int g, int b) {
        return new Color(r, g, b);
    }
}

public class ClientApp {
    public void doWork() {
        Color turquoise = Color.ofRGB(64,224,208);
        // More work
    }
}
```

## ✅ Advantages

1. Have semantic names corresponding to the distinct characteristic of each method, unlike overloaded constructors.
```
  // Returns a new instance
  Object newArray = Array.newInstance(classObject, arrayLen);
  
  // Returns an instance with the provided value
  Integer num = Integer.valueOf(1);
```

2. Can return cached instances. Conceptually similar to the Flyweight design pattern.
```
  public static Boolean valueOf(boolean b) {
    return b ? Boolean.TRUE : Boolean.FALSE;
  }
```

3. The return types can be abstracted as interfaces or abstract classes. This has three main advantages.
  - Unlimited number of return subtypes can be created.
  - The return subtypes can be hidden from the outside (private).
    ```
      List<String> unmodifiable = Collections.unmodifiableList(original);
    
      // Actual returned subtype, defined inside java.util.Collections
      private static class UnmodifiableList<E> implements List<E>, RandomAccess { ... }
    ```
  - Return subtypes can be non-existing at time of static factory methods creations.  
    ```
    // JDBC framework
    Connection con = DriverManager.getConnection(...) 
  
    // Interface return type: Connection 
    // The implementations of 'Connection' can be created later by the database vendors, e.g., MySQL, PostgreSQL, ORACLE, which implement JDBC.
    ```
    **Terminology**
    - *service provider framework* - a framework that requires implementations to make it function, such as `JDBC`.
    - *service interface* - the contract to be implemented, such as `Connection`.
    - *service access API* - may allow clients to specify criteria for choosing an implementation, such as `DriverManager.getConnection`.
    - *service provider interface* - a factory object, produces instances of *service interface*, such as `Driver`.
    - *provider registration API* - providers use to register implementations, such as `DriverManager.registerDriver`.

4. Can use input parameter to determine the actual return type.
```
  enum HugeValueEnum {
      VALUE_1, VALUE_2, ..., VALUE_100;
  }
  
  // This will return an instance of JumboEnumSet, since the input enum type has over 64 constants.
  EnumSet<HugeValueEnum> set = EnumSet.range(HugeValueEnum.VALUE_1, HugeValueEnum.VALUE_10);

  enum SmallValueEnum {
      VALUE_1, VALUE_2, ..., VALUE_64;
  }

  // This will return an instance of RegularEnumSet, since the input enum type has no more than 64 constants.
  EnumSet<SmallValueEnum> set = EnumSet.range(SmallValueEnum.VALUE_1, SmallValueEnum.VALUE_10);

```


## ⚠️ Downsides
- The actual returned type cannot be subclassed. Because their constructors are `private`, and used internally by static methods. 
Arguably this can be a blessing in disguise because it encourages programmers to use composition instead of inheritance, 
which is required for immutable types.
- Static factory methods are hard to find in API documentation, as they do not stand out.


## 💡 Common usages
- Enums
- Constant classes.
