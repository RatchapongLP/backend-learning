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
- A bit slow start up due to line-by-line interpretation (compensated with JIT optimization)