# Java

## General Facts
- First version released in $1995$
- Initially developed by Sun Microsystems. In $2010$, Oracle acquired Sun Microsystems, including Java platform. 
- Compiled code (byte code) is not machine-executable, need to be translated again into machine code
- Platform independent compiled code (C, C++ need different compilers for OS's)
- Platform dependent runtime (C, C++ don't need runtime)
- Object-oriented language
- Familiar to C syntax

## Java Development and Execution
### Java byte code
- Instruction set meant for execution by JVM

### JVM
- Required for running byte code
- Platform dependent
- Contains byte code loader, verifier, interpreter, and Just-In-Time (JIT) compiler
    - **Interpreter** executes byte code instructions directly, translating byte code (.class)
      line-by-line into machine code, and hand it to the OS.
    - **JIT compiler** detects frequently executed sections of byte code (hotspots) at runtime,
      pre-compile them into machine code in advance before the line is reached by the interpreter,
      and place them in the memory for ease of access. This resulting in better performance compared
      to using interpreter alone.

### JRE
- Required for running Java applications
- Platform dependent
- Includes JVM
- Contains Java standard libraries
- Language agnostic: can run Groovy, Scala, Kotlin

### JDK
- Required for Java development
- Platform dependent
- Includes JRE
- Contains tools and utilities for development, compiling, packaging, distribution, etc.

### Pros and Cons of JVM model
#### Pros
- Platform independent compiled code
- Secure: JVM acts as a sandbox. It establishes boundaries between the code and the machine,
preventing the code from accessing or manipulating dangerous parts of the machine.

#### Cons
- A bit slow start up due to line-by-line interpretation (compensated with JIT optimization after start up)

### GraalVM
- GraalVM is a full-scale JDK distribution that follows the JVM specification and offers more.
- GraalVM JDK can simply be used as a drop-in replacement for other JDKs.
- Offers two ways of optimizing JVM (refer to the [official link](https://www.graalvm.org/why-graalvm/)) as:

1. #### Option 1: running compiled byte code using GraalVM as VM
- It uses the Java HotSpot VM as platform.
- GraalVM replaces the last-tier optimizing compiler in the HotSpot JVM (C2) with the Graal compiler, 
which includes several new optimizations. 
- GraalVM is itself written in Java (in contrary to Java Hotspot VM which is written in C, C++) 
which accelerates maintenance and delivering new optimizations.
- Several companies, such as Oracle Cloud, Twitter, and Facebook are running large-scale Java applications 
on GraalVM JDK to increase performance, reduce resource usage, and lower deployment costs. 

2. #### Option 2: running native executables compiled with 'Native Image'
- Native Image is a GraalVM tool that convert byte code into native executable of Java applications, 
that are self-contained and thus no longer require the JVM. 
- The image generation process employs static analysis to find all code reachable from the main Java method 
and then performs full ahead-of-time (AOT) compilation. At build time, it also performs snapshotting, 
so, at run time, the application starts much faster with pre-populated heap. 
- The resulting native binary contains the whole program in machine code form that is ready for 
execution instantly at startup with the following features:
  - Instant startup due to pre-initializing the JDK and user code at build time
  - Reduced memory and CPU usage due to minimized code execution overhead
  - Small packaging due to the AOT approach and slim runtime components
  - Reduced attack surface due to code elimination and the AOT approach



## Java Core

### General Facts
#### `public static void main(String[] args)`
Special method declaration that is recognized as the entry point for Java program.

#### `var`
- `var` can only be used for local variables, including loop variables in enhanced for loops and 
  resource variables in try-with-resources statements. It cannot be used for fields, method parameters, 
  or method return types.
- A `var` declaration **must** be initialized at the time of declaration.
- Java compiler automatically **refers** the variable's **static** type at **compile time** based on the 
type of the initializer expression assigned to the variable.

### Primitive Types
- **Integers:** `byte`, `short`, `int`, and `long`
- **Floating Points:** `float` and `double`
- **Character:** `char`
- **Boolean:** `boolean`

#### `byte`
- $8$-bit signed integer
- The leftmost bit (bit #8) - a.k.a. most significant bit (MSB) - determines whether the number is positive or negative.
  If MSB is $0$, the number is positive or zero. If MSB is $1$, the number is negative.
- The rest of $7$ bits makes up the number's absolute value.
- The maximum value is `Byte.MAX_VALUE` $= 2^{7}-1= 127$
- The minimum value is `Byte.MIN_VALUE` $= -2^{7}= -128$

#### `short`
- $16$-bit signed integer
- Follows MSB principle
- The maximum value is `Short.MAX_VALUE` $= 2^{15}-1= 32,767$
- The minimum value is `Short.MIN_VALUE` $= -2^{15}= -32,768$

#### `int`
- $32$-bit signed integer
- Follows MSB principle
- The maximum value is `Integer.MAX_VALUE` $= 2^{31}-1= 2,147,483,647$ (billions)
- The minimum value is `Integer.MIN_VALUE` $= -2^{31}= -2,147,483,648$

#### `long`
- $64$-bit signed integer
- Follows MSB principle
- The maximum value is `Long.MAX_VALUE` $= 2^{63}-1= 9,223,372,036,854,775,807$ (quintillion - $6$ commas)
- The minimum value is `Long.MIN_VALUE` $= -2^{63}= -9,223,372,036,854,775,808$

#### `float`
- $32$-bit single-precision floating-point number
- Follows MSB principle
- $23$ rightmost bits (bit $22$-$0$) represent the fractional part of the numbers (Significand/Mantissa).
- $8$ in-between bits (bit $30$-$23$) represent the exponent of the number.
- The maximum value is `Float.MAX_VALUE` $= 3.4028235\times 10^{38}$
- The minimum value is `-Float.MAX_VALUE` $= -3.4028235\times 10^{38}$
- The smallest positive value is `Float.MIN_VALUE` $=2^{-149} \approx 1.4\times 10^{-45}$

#### `double`
- $64$-bit double-precision floating-point number
- $52$ rightmost bits (bit $51$-$0$) represent the fractional part of the numbers (Significand/Mantissa).
- $11$ in-between bits (bit $62$-$52$) represent the exponent of the number.
- The maximum value is `Double.MAX_VALUE` $= 1.7976931348623157\times 10^{308}$
- The minimum value is `-Double.MAX_VALUE` $= -1.7976931348623157\times 10^{308}$
- The smallest positive value is `Double.MIN_VALUE` $=2^{-1074} \approx 4.94065645841247\times 10^{-324}$

#### `char`
- Stores a single character
- $16$-bit unsigned integer under the hood, corresponding to Unicode code units
- The maximum value is `Character.MAX_VALUE` $=$ `\uffff` $= 2^{16}-1 = 65,535$
- The minimum value is `Character.MIN_VALUE` $=$ `\u0000` $= 0$

#### `boolean`



### Access Modifier
### static vs instance