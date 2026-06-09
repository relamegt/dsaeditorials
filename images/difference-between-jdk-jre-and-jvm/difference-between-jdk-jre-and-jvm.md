# Difference Between JDK, JRE, and JVM

JDK, JRE, and JVM are three basic parts of Java. They are related, but they do different jobs.

- **JDK** is used to develop Java programs
- **JRE** is used to run Java programs
- **JVM** is used to execute Java bytecode

![JDK, JRE and JVM](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/difference-between-jdk-jre-and-jvm/1781007710784-jvm_jdk_jre.png)

## JDK

JDK stands for **Java Development Kit**. It is mainly used by developers to write, compile, and test Java programs.

JDK includes:

- JRE
- Compiler (`javac`)
- Debugging and utility tools

Use JDK when you want to create Java applications.

## JRE

JRE stands for **Java Runtime Environment**. It gives the environment needed to run Java programs.

JRE includes:

- JVM
- Java class libraries
- Runtime files

Use JRE when you only want to run a Java application, not build one.

## JVM

JVM stands for **Java Virtual Machine**. It runs the compiled Java bytecode and converts it into machine-level instructions.

JVM is responsible for:

- Running bytecode
- Memory management
- Garbage collection
- Making Java platform-independent at the bytecode level

A Java program can run on any system that has a suitable JVM.

## Working of JVM

![JVM Working](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/difference-between-jdk-jre-and-jvm/1781007850904-jvm_working.png)

1. ****Loading:**** Class loader loads bytecode into memory.
2. ****Linking:**** Performs verification, preparation, and resolution.
3. ****Initialization:**** Executes class constructors and static initializers.
4. ****Execution:**** Interprets or compiles bytecode into native code.

## Simple Relationship

```text
JDK = JRE + Development Tools
JRE = JVM + Libraries
JVM = Runs Java Bytecode
```

## How They Work Together

1. You write Java code in a `.java` file
2. JDK compiles it into a `.class` file using `javac`
3. JRE provides the runtime environment
4. JVM runs the bytecode inside the `.class` file

## Quick Difference Table

| Part | Full Form | Main Use |
| --- | --- | --- |
| JDK | Java Development Kit | Develop and run Java programs |
| JRE | Java Runtime Environment | Run Java programs |
| JVM | Java Virtual Machine | Execute Java bytecode |

##



###
