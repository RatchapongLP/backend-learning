# 📘 Effective Java – Item 2: Consider a builder when faced with many constructor parameters

## 🧪 Example:

```
// Builder Pattern
public class NutritionFacts {
    private final int servingSize;
    private final int servings;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;

    public static class Builder {
        // Required parameters
        private final int servingSize;
        private final int servings;

        // Optional parameters - initialized to default values
        private int calories      = 0;
        private int fat           = 0;
        private int sodium        = 0;
        private int carbohydrate  = 0;

        public Builder(int servingSize, int servings) {
            this.servingSize = servingSize;
            this.servings    = servings;
        }

        public Builder calories(int val) { 
            calories = val;      
            return this; 
        }
        public Builder fat(int val) { 
            fat = val;           
            return this; 
        }
        public Builder sodium(int val) { 
            sodium = val;        
            return this; 
        }
        public Builder carbohydrate(int val) { 
            carbohydrate = val;  
            return this; 
        }

        public NutritionFacts build() {
            return new NutritionFacts(this);
        }
    }

    private NutritionFacts(Builder builder) {
        servingSize  = builder.servingSize;
        servings     = builder.servings;
        calories     = builder.calories;
        fat          = builder.fat;
        sodium       = builder.sodium;
        carbohydrate = builder.carbohydrate;
    }
}

public class ClienApp {
    public void doWork() {
        NutritionFacts cocaCola = new NutritionFacts.Builder(240, 8)
                .calories(100).sodium(35).carbohydrate(27).build();
    }
}
```

## ❓What problem does it solve?
Creating instances with a large number of optional fields using regular techniques are not practical.
See the below examples.
1.  Using *constructors* are messy to implement. 
For the client use, it is bug prone, and reduces readability.
```
// Telescoping constructor pattern - does not scale well.
public class NutritionFacts {
    private final int servingSize; // (mL) required
    private final int servings; // (per container) required
    private final int calories; // (per serving) optional
    private final int fat; // (g/serving) optional
    private final int sodium; // (mg/serving) optional
    private final int carbohydrate; // (g/serving) optional
    
    // Total of five constructors need to be implemented.
    
    public NutritionFacts(int servingSize, int servings) {
        this(servingSize, servings, 0);
    }
    public NutritionFacts(int servingSize, int servings, int calories) {
        this(servingSize, servings, calories, 0);
    }
    public NutritionFacts(int servingSize, int servings, int calories, int fat) {
        this(servingSize, servings, calories, fat, 0);
    }
    public NutritionFacts(int servingSize, int servings, int calories, int fat, int sodium) {
        this(servingSize, servings, calories, fat, sodium, 0);
    }
    public NutritionFacts(int servingSize, int servings, int calories, int fat, int sodium, int carbohydrate) {
        this.servingSize = servingSize;
        this.servings = servings;
        this.calories = calories;
        this.fat = fat;
        this.sodium = sodium;
        this.carbohydrate = carbohydrate;
    }
}

public class ClientApp {
    public doWork() {
        // Constructor parameters are not semantic, hard to understand.
        // Extra work of passing in zeros values.
        NutritionFacts cocaCola = new NutritionFacts(240, 1, 100, 0, 0, 27);
    }
}
```

2. Using static factory methods is not very different from the constructors.
```
public class NutritionFacts {
    // Fields and constructors
    ...
    
    // Five static factory method need to be implemented
    public static NutritionFacts getInstance(int servingSize, int servings) {
        return new NutritionFacts(servingSize, servings);
    }
    public static NutritionFacts getInstance(int servingSize, int servings, int calories) {
        return new NutritionFacts(servingSize, servings, calories);
    }
    ...
}

public class ClientApp {
    public doWork() {
        // Static factory method parameters are not meaningful.
        // Extra work of passing in zeros values.
        NutritionFacts cocaCola = NutritionFacts.getInstance(240, 1, 100, 0, 0, 27);
    }
}
```

3. Using the *JavaBean* pattern makes it easier for the client to create instances and 
increases code readability. 
```
public class NutritionFacts {
    // Fields
    
    public void setServingSize(int val) {
        this.servingSize = val;
    }
    public void setServings(int val) {
        this.servings = val;
    }
    ...
}

public class ClientApp {
    public doWork() {
        // Meaningful setters.
        // Need not set zeros values.
        NutritionFacts cocaCola = new NutritionFacts();
        cocaCola.setServingSize(240);
        cocaCola.setServings(1);
        cocaCola.setCalories(100);
        cocaCola.setCarbohydrate(27);
    }
}
```
But it introduces new problems. Firstly, if we want to validate all the fields, we have to create a new method just for it,
which the user can forget to invoke.
```
public class NutritionFacts {
    // Fields
    // Setters
    
    public void validateAllFields() {
        if (this.servingSize < 1) throw new RuntimeException("servingSize cannot be less than 1");
        if (this.servings < 1) throw new RuntimeException("servings cannot be less than 1");
        if (this.calories < 0) throw new RuntimeException("calories cannot be less than 0");
        ...
    }
}

public class ClientApp {
    public doWork() {
        NutritionFacts cocaCola = new NutritionFacts();
        cocaCola.setServingSize(240);
        cocaCola.setCalories(-1);
        cocaCola.setCarbohydrate(27);
        
        // This will throw a RuntimeException due to the zero servings.
        // Can be accidentally forgotten by clumsy developers.
        cocaCola.validateAllFields(); 
    }
}
```
Also, the *JavaBean* class is mutable due to the setters, not good for ensuring thread safety.

But with *Builder* pattern, all the fields can be made `final`, and put the validation in the 
class' constructor, by which the `build()` method calls.
```
// Builder Pattern
public class NutritionFacts {
    // Final fields

    public static class Builder {
        ...
    }

    private NutritionFacts(Builder builder) {
        servingSize  = builder.servingSize;
        servings     = builder.servings;
        calories     = builder.calories;
        fat          = builder.fat;
        sodium       = builder.sodium;
        carbohydrate = builder.carbohydrate;
        
        validateAllFields();
    }
    
     private void validateAllFields() {
        if (this.servingSize < 1) throw new RuntimeException("servingSize cannot be less than 1");
        if (this.servings < 1) throw new RuntimeException("servings cannot be less than 1");
        if (this.calories < 0) throw new RuntimeException("calories cannot be less than 0");
        ...
    }
}
```
