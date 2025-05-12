# 📘 Effective Java – Item 1: Consider static factory methods instead of constructors

## ✅ Advantages of static factory methods:
- Have semantic names corresponding to the distinct characteristic of each method, unlike overloaded constructors.
```
  // create or newInstance — Returns an instance that is described by its parameters.
  // Guarantees that each call returns a new instance, for example:
  Object newArray = Array.newInstance(classObject, arrayLen);

```
- Don’t require creating a new instance every invocation. Similar idea: Flyweight design pattern.
```
  public static Boolean valueOf(boolean b) {
    return b ? Boolean.TRUE : Boolean.FALSE;
  }

```
- Can return any subtype of the returning type. The actual return subtypes can be hidden (non-public).
```
  List<String> original = new ArrayList<>();
  List<String> unmodifiable = Collections.unmodifiableList(original);

  // Inside java.util.Collections
  private static class UnmodifiableList<E> implements List<E>, RandomAccess { ... }

```
- Actual return type can vary from call to call as a function of the input parameters.
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
- Actual return type need not exist yet when the class containing the method is written.  
  Example: In JDBC (*service provider framework*), ``DriverManager`` contains a static method - ``DriverManager.getConnection`` (*service access API*) - that returns ``Connection`` (*service interface*).
  The implementations of ``Connection`` can be created later by database vendors, e.g., MySQL, PostgreSQL, ORACLE that implement JDBC.

## 🔍 Limitations:
- Returned classes without public or protected constructors cannot be subclassed. Arguably this can be a blessing in disguise
because it encourages programmers to use composition instead of inheritance, and is required for immutable types.
- They are hard for programmers to find. They do not stand out in API documentation.

## 🧪 Example:  
public class Color {
    private final int red, green, blue;

    private Color(int r, int g, int b) {
        this.red = r; this.green = g; this.blue = b;
    }

    public static Color ofRGB(int r, int g, int b) {
        return new Color(r, g, b);
    }
}



Works great with enums and constants.
