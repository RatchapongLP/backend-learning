# Java

## General Facts
- First version released in 1995
- Initially developed by Sun Microsystems
- Oracle acquired Sun Microsystems, including Java platform, in 2010
- Compiled code (byte code) is not machine-executable, need to be translated again into machine code
- Platform independent compiled code (C, C++ need different compilers for OS's)
- Platform dependent runtime (C, C++ don't need runtime)

## Java byte code
- Instruction set meant for execution by JVM

## JVM
- Required for running byte code
- Platform dependent
- Contains byte code loader, verifier, interpreter, and Just-In-Time (JIT) compiler
    - **Interpreter** executes byte code instructions directly, translating byte code (.class)
      line-by-line into machine code, and hand it to the OS.
    - **JIT compiler** detects frequently executed sections of byte code (hotspots) at runtime,
      pre-compile them into machine code in advance before the line is reached by the interpreter,
      and place them in the memory for ease of access. This resulting in better performance compared
      to using interpreter alone.

## JRE
- Required for running Java applications
- Platform dependent
- Includes JVM
- Contains Java standard libraries
- Language agnostic: can run Groovy, Scala, Kotlin

## JDK
- Required for Java development
- Platform dependent
- Includes JRE
- Contains tools and utilities for development, compiling, packaging, distribution, etc.

## Pros and Cons of JVM model
### Pros
- Platform independent compiled code
- Secure: JVM acts as a sandbox. It establishes boundaries between the code and the machine,
preventing the code from accessing or manipulating dangerous parts of the machine.

### Cons
- A bit slow start up due to line-by-line interpretation (compensated with JIT optimization after start up)

## GraalVM
- GraalVM is a full-scale JDK distribution that follows the JVM specification and offers more.
- GraalVM JDK can simply be used as a drop-in replacement for other JDKs.
- Offers two ways of optimizing JVM (refer to the [official link](https://www.graalvm.org/why-graalvm/)) as:

1. ### Option 1: running compiled byte code using GraalVM as VM
- It uses the Java HotSpot VM as platform.
- GraalVM replaces the last-tier optimizing compiler in the HotSpot JVM (C2) with the Graal compiler, 
which includes several new optimizations. 
- GraalVM is itself written in Java (in contrary to Java Hotspot VM which is written in C, C++) 
which accelerates maintenance and delivering new optimizations.
- Several companies, such as Oracle Cloud, Twitter, and Facebook are running large-scale Java applications 
on GraalVM JDK to increase performance, reduce resource usage, and lower deployment costs. 

2. ### Option 2: running native executables compiled with 'Native Image'
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
