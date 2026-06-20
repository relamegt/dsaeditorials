# Object Class in Java

## Introduction

The **Object** class, located in the `java.lang` package, is the absolute root of the Java class hierarchy. Every class in Java directly or indirectly inherits from `java.lang.Object`. If a class does not explicitly specify a parent class using the `extends` keyword, the Java compiler automatically inserts `extends java.lang.Object` at compile time.

This universal inheritance structure enables **polymorphism** at the highest level: a variable of type `Object` can hold a reference to an instance of any class (e.g., `Object obj = new Student("Mohit");`). The Object class defines 11 methods that provide baseline behaviors for all objects in Java:

- `toString()`: Returns a string representation of the object.
- `equals(Object obj)`: Compares two objects for logical equality.
- `hashCode()`: Returns a unique hash code integer value for the object.
- `clone()`: Creates and returns a copy of the object.
- `getClass()`: Returns the runtime Class metadata of the object.
- `finalize()`: Executed before garbage collection (deprecated since Java 9).
- `wait()`, `notify()`, `notifyAll()`: Coordinate thread execution (concurrency control).

Because every class extends Object, these methods are inherited by every Java class.

## Why is Object Class Important?

The Object class provides baseline, unified functionality that every Java class needs to participate in core language features:

- **Root of Inheritance**: Establishes a common type system, allowing generic frameworks (like the Java Collections Framework) to manipulate any object.
- **Logical Equality**: Enables collections to locate, compare, and remove elements using overridden logical comparison rules.
- **Hash-based Indexing**: Provides a contract for hash distribution, crucial for high-performance structures like `HashMap` and `HashSet`.
- **Reflection Entrypoint**: Supplies a way to inspect class details dynamically at runtime.
- **Thread Synchronization**: Offers intrinsic lock monitor operations directly on any object for concurrent coordination.

## Example: Object Class Methods

```java
class Student {
    String name;

    Student(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "Student{name='" + name + "'}";
    }

    public static void main(String[] args) {
        Student s = new Student("Mohit");
        System.out.println(s);
        System.out.println(s.hashCode());
    }
}
```

### Output
Student{name='Mohit'}
321001045

## 

## ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/object-class-in-java/1781952821067-9ba978c8-94eb-48b4-b5db-8f6c5d4f2f15.png)

## 

## Object Class Hierarchy

All classes in Java trace their lineage back to the Object class:

```text
Object
   ↑
Student
   ↑
EngineeringStudent
```

Even custom classes or built-in classes like `String`, `Integer`, or `ArrayList` are direct or indirect subclasses of `Object`.

## Common Object Class Methods

| Method | Signature | Purpose |
| --- | --- | --- |
| `toString()` | `public String toString()` | Converts an object to its string representation. |
| `equals()` | `public boolean equals(Object obj)` | Evaluates logical equality between two objects. |
| `hashCode()` | `public int hashCode()` | Computes an integer hash value for lookup optimization. |
| `clone()` | `protected Object clone() throws CloneNotSupportedException` | Creates a copy of the object (requires `Cloneable` interface). |
| `getClass()` | `public final Class<?> getClass()` | Returns runtime Class metadata for reflection. |
| `wait()` | `public final void wait() throws InterruptedException` | Forces the current thread to release the lock and wait. |
| `notify()` | `public final void notify()` | Wakes a single thread waiting on the object's monitor. |
| `notifyAll()` | `public final void notifyAll()` | Wakes all threads waiting on the object's monitor. |
| `finalize()` | `protected void finalize() throws Throwable` | Executed by Garbage Collector before reclamation (deprecated). |

## 1. toString() Method

The `toString()` method returns a string representation of an object. 

### Syntax

```java
public String toString()
```

### Default Implementation and the Value of Overriding

By default, the `toString()` method in the `Object` class returns a string consisting of the class name, followed by the "at" sign `@`, and the unsigned hexadecimal representation of the object's hash code:

```java
getClass().getName() + '@' + Integer.toHexString(hashCode())
```

For example, `Student@1a2b3c`. Because this default string is rarely useful to humans, overriding `toString()` is a highly recommended practice. In enterprise applications, overriding `toString()` allows you to output meaningful object states for system logging, diagnostics, and debugging.

### Example

```java
class Student {
    String name;
    int age;

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Student{name='" + name + "', age=" + age + "}";
    }

    public static void main(String[] args) {
        Student s = new Student("Mohit", 20);
        System.out.println(s);
    }
}
```

### Output
Student{name='Mohit', age=20}

### Example: AlphaKnowledge Course

```java
class Course {
    String courseName;

    Course(String courseName) {
        this.courseName = courseName;
    }

    @Override
    public String toString() {
        return "Course: " + courseName;
    }

    public static void main(String[] args) {
        Course c = new Course("AlphaKnowledge Java");
        System.out.println(c);
    }
}
```

### Output
Course: AlphaKnowledge Java

## 2. hashCode() Method

The `hashCode()` method returns an integer hash value for an object, which is used to distribute objects across hash-based collections.

### Syntax

```java
public int hashCode()
```

### Hashing and JVM Address Mapping

Hashing maps arbitrary object states to a 32-bit signed integer. In the default HotSpot JVM implementation, `hashCode()` is a native method that associates the object's identity with an internal memory reference structure or pseudo-random number generator (though it is not a direct memory address for security and garbage collector relocation reasons).

### Hash Collisions and Performance Impact

When objects are added to collections like `HashMap` or `HashSet`, the collection uses the object's hash code to determine which bucket it belongs to. If multiple distinct objects return the exact same hash code, a **hash collision** occurs. In Java 8 and later, if a bucket undergoes too many collisions (exceeding a threshold of 8), the JVM converts the underlying bucket structure from a linked list to a balanced red-black tree. This transition prevents performance degradation, upgrading worst-case search complexity from $O(N)$ back to $O(\log N)$, though keeping collisions low is still critical for optimal performance.

### Example

```java
class Student {
    int id;

    Student(int id) {
        this.id = id;
    }

    @Override
    public int hashCode() {
        // Multiply by a prime number to reduce collisions
        return id * 31;
    }

    public static void main(String[] args) {
        Student s = new Student(101);
        System.out.println(s.hashCode());
    }
}
```

### Output
3131

### Important Rule

If two objects are equal according to the `equals(Object)` method, they must return the same integer result when `hashCode()` is invoked.

```text
equals() == true
      ↓
hashCode() must be identical
```

## 3. equals() Method

The `equals()` method compares two objects for equality.

### Syntax

```java
public boolean equals(Object obj)
```

### Reference vs. Logical Equality

By default, the `equals()` method in the `Object` class uses the reference comparison operator (`==`). This means it only returns `true` if both variables point to the exact same object instance on the heap (reference identity). To compare the actual contents (states) of two distinct objects, you must override `equals()`.

### The 5 Equivalence Relation Rules

When overriding `equals()`, your implementation must satisfy the strict mathematical equivalence relation rules defined in the Java Specification:

1. **Reflexive**: For any non-null reference value `x`, `x.equals(x)` must return `true`.
2. **Symmetric**: For any non-null reference values `x` and `y`, `x.equals(y)` must return `true` if and only if `y.equals(x)` returns `true`.
3. **Transitive**: For any non-null reference values `x`, `y`, and `z`, if `x.equals(y)` is `true` and `y.equals(z)` is `true`, then `x.equals(z)` must return `true`.
4. **Consistent**: Multiple invocations of `x.equals(y)` must consistently return `true` or `false`, provided no state elements modified during evaluation have changed.
5. **Non-nullity**: For any non-null reference value `x`, `x.equals(null)` must return `false`.

### Without Overriding

```java
class Student {
    String name;

    Student(String name) {
        this.name = name;
    }

    public static void main(String[] args) {
        Student s1 = new Student("Mohit");
        Student s2 = new Student("Mohit");
        System.out.println(s1.equals(s2));
    }
}
```

### Output
false

### With Overriding

```java
class Student {
    String name;

    Student(String name) {
        this.name = name;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Student s = (Student) obj;
        return name != null ? name.equals(s.name) : s.name == null;
    }

    public static void main(String[] args) {
        Student s1 = new Student("Mohit");
        Student s2 = new Student("Mohit");
        System.out.println(s1.equals(s2));
    }
}
```

### Output
true

### Example: Comparing Team Members

```java
class Member {
    String name;

    Member(String name) {
        this.name = name;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Member m = (Member) obj;
        return name != null ? name.equals(m.name) : m.name == null;
    }

    public static void main(String[] args) {
        Member m1 = new Member("Akash");
        Member m2 = new Member("Akash");
        System.out.println(m1.equals(m2));
    }
}
```

### Output
true

## 4. getClass() Method

The `getClass()` method returns runtime Class metadata of the object.

### Syntax

```java
public final Class<?> getClass()
```

### Reflection and Metaspace Classes

The `getClass()` method returns a reference to the unique `java.lang.Class` object representing the object's class at runtime. This class metadata, loaded into the JVM's Metaspace, is the primary entry point for **Java Reflection**. Using the returned Class reference, applications can dynamically inspect class names, fields, declared methods, active constructors, annotations, and inheritance hierarchies at runtime.

### Final Keyword Constraints

The `getClass()` method is marked as `final` in the `Object` class. This prevents subclasses from overriding it, ensuring that no subclass can disguise its runtime identity. This constraint provides security and structural integrity within the runtime class-loading environment.

### Example

```java
public class Main {
    public static void main(String[] args) {
        Object obj = new String("AlphaKnowledge");
        System.out.println(obj.getClass().getName());
    }
}
```

### Output
java.lang.String

### Example

```java
class Student {

}

public class Main {
    public static void main(String[] args) {
        Student s = new Student();
        System.out.println(s.getClass().getName());
    }
}
```

### Output
Student

## 5. clone() Method

The `clone()` method creates and returns a copy of an object.

### Syntax

```java
protected Object clone() throws CloneNotSupportedException
```

### Marker Interface Cloneable and Runtime Behavior

The `clone()` method is declared as `protected` inside the `Object` class to restrict unauthorized cloning. To enable cloning, a class must implement the `java.lang.Cloneable` interface and override the `clone()` method to be `public`. `Cloneable` is a **marker interface**—it contains no methods or fields. If a class attempts to call `super.clone()` without implementing the `Cloneable` interface, the JVM throws a `CloneNotSupportedException` at runtime.

### Shallow Copy vs. Deep Copy

- **Shallow Copy (Default)**: By default, `super.clone()` performs a field-by-field copy. Primitives are copied directly. For reference variables, only the memory address (reference) is copied, meaning both the original object and the clone share the same nested mutable objects.
- **Deep Copy**: If your class contains references to mutable nested objects, you must manually clone those nested objects inside your overridden `clone()` method to ensure complete isolation between the original and the copied object.

### Example

```java
class Student implements Cloneable {
    String name = "Mohit";

    @Override
    public Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    public static void main(String[] args) throws Exception {
        Student s1 = new Student();
        Student s2 = (Student) s1.clone();
        System.out.println(s1.name);
        System.out.println(s2.name);
    }
}
```

### Output
Mohit
Mohit

### Example: AlphaKnowledge Clone

```java
class Course implements Cloneable {
    String course = "DSA Mastery";

    @Override
    public Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    public static void main(String[] args) throws Exception {
        Course c1 = new Course();
        Course c2 = (Course) c1.clone();
        System.out.println(c2.course);
    }
}
```

### Output
DSA Mastery

## 6. finalize() Method (Deprecated)

The `finalize()` method was historically invoked by the garbage collector on an object when it determined that there were no more active references to the object.

### Deprecation and Modern Resource Reclamation

The `finalize()` method has been deprecated since Java 9 and removed entirely in later releases due to serious design flaws:

- **Unpredictable Execution**: The JVM does not guarantee when (or if) the garbage collector will run. Consequently, critical resource cleanups inside `finalize()` can delay indefinitely, causing starvation and system leaks.
- **Performance Overhead**: Objects overriding `finalize()` slow down the GC processes, requiring multiple collection cycles for memory reclamation.
- **Resurrection Flaw**: An object can "resurrect" itself inside `finalize()` by assigning `this` back to an active reference, leading to severe memory management issues.

### Modern Alternatives

For robust resource management, developers must use:

1. **`try-with-resources`**: Along with classes implementing the `java.lang.AutoCloseable` or `java.io.Closeable` interface.
2. **`java.lang.ref.Cleaner` API**: A lightweight, thread-safe, and isolated alternative to finalize blocks.

### Example

```java
class Demo {
    @Override
    protected void finalize() {
        System.out.println("Cleanup performed");
    }

    public static void main(String[] args) {
        Demo d = new Demo();
        d = null;
        System.gc(); // Requesting garbage collection
        System.out.println("Program End");
    }
}
```

### Possible Output

Program End

Cleanup performed

> [NOTE] The exact output timing is not guaranteed because garbage collection schedules are dependent on the JVM implementation.

## 7. wait() Method

The `wait()` method causes the current thread to release its lock on the object's monitor and wait until another thread wakes it up.

### Syntax

```java
public final void wait() throws InterruptedException
public final void wait(long timeoutMillis) throws InterruptedException
```

### Monitor Locks and Thread Coordination

Java objects have an associated internal **monitor lock** (intrinsic lock). The `wait()` method suspends thread execution and releases ownership of this monitor lock. The thread remains in a blocked waiting state until another thread holding the same monitor lock calls `notify()` or `notifyAll()`.

### Synchronization Requirements

The `wait()`, `notify()`, and `notifyAll()` methods must be called **only** from within a synchronized context (a `synchronized` block or method). If a thread attempts to call these methods without holding the target object's monitor lock, the JVM throws an `IllegalMonitorStateException` at runtime.

### Example

```java
class Demo {
    public static void main(String[] args) throws Exception {
        Object obj = new Object();
        synchronized(obj) {
            System.out.println("Waiting...");
            obj.wait(2000); // Wait for 2 seconds
            System.out.println("Resumed");
        }
    }
}
```

### Output
Waiting...
Resumed

## 8. notify() Method

The `notify()` method wakes up a single thread that is currently waiting on the object's monitor lock.

### Syntax

```java
public final void notify()
```

### Synchronization Flow

If multiple threads are waiting on the object's monitor queue, calling `notify()` wakes up exactly one thread. The selection is arbitrary and JVM-dependent. The awakened thread will not proceed until the notifying thread releases the synchronized monitor lock.

### Example

```java
obj.notify(); // Invoked within a synchronized block
```

## 9. notifyAll() Method

The `notifyAll()` method wakes up all threads currently waiting on the object's monitor queue.

### Syntax

```java
public final void notifyAll()
```

### Execution Advantages

Unlike `notify()`, `notifyAll()` wakes up every thread waiting in the monitor queue. The threads then compete to acquire the monitor lock. This method is preferred in multi-threaded producer-consumer problems to prevent deadlock conditions.

### Example

```java
obj.notifyAll(); // Invoked within a synchronized block
```

## equals() vs ==

Understanding the distinction between `equals()` and the `==` operator is a fundamental concept in Java memory allocation:

- **Stack Memory**: Contains reference pointers (memory addresses) pointing to objects on the heap.
- **Heap Memory**: Contains the actual instances (states and data) of classes.

When you use the `==` operator, Java compares the address values stored in Stack memory (reference identity). When you call `equals()`, it evaluates the state values stored in Heap memory (logical equality, assuming the method has been overridden).

| Feature | `equals()` Method | `==` Operator |
| --- | --- | --- |
| Compares | Content / State (logical equality). | Memory references (reference identity). |
| Customization | Can be overridden for custom class logic. | Behavior cannot be modified. |
| Use Case | Comparing string contents or entity properties. | Checking null references or comparing primitives. |

### Example

```java
public class Main {
    public static void main(String[] args) {
        String s1 = new String("Java");
        String s2 = new String("Java");

        System.out.println(s1 == s2);
        System.out.println(s1.equals(s2));
    }
}
```

### Output
false
true

## hashCode() Contract

When overriding `equals()`, you must also override `hashCode()`. Failing to maintain this contract breaks collections like `HashMap`, `HashSet`, and `Hashtable`.

### The Three Contract Rules

1. **Consistency**: Multiple invocations of `hashCode()` on the same object must return the same integer value during execution, provided the state used in the `equals()` comparison remains unchanged.
2. **Equal Objects**: If two objects are equal according to `equals(Object)`, invoking `hashCode()` on both objects must produce the same integer result.
3. **Unequal Objects**: If two objects are unequal according to `equals(Object)`, it is **not** required that their `hashCode()` values be different. However, generating unique hash codes for unequal objects improves performance in hash structures.

If you violate this contract, objects will be stored in incorrect buckets inside collections, causing `HashSet.contains()` or `HashMap.get()` to return incorrect results or create duplicate entries.

## Real-Life Example

### Student Registration with Valid Equality Contracts

This example demonstrates how to implement a custom class that overrides `toString()`, `equals()`, and `hashCode()` to meet Java specification standards.

```java
import java.util.Objects;

class Student {
    String name;
    int rollNo;

    Student(String name, int rollNo) {
        this.name = name;
        this.rollNo = rollNo;
    }

    @Override
    public String toString() {
        return "Student: " + name + " (Roll No: " + rollNo + ")";
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Student s = (Student) obj;
        return rollNo == s.rollNo && Objects.equals(name, s.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, rollNo);
    }

    public static void main(String[] args) {
        Student s1 = new Student("Mohit", 101);
        Student s2 = new Student("Mohit", 101);

        System.out.println(s1);
        System.out.println("Is s1 equal to s2? " + s1.equals(s2));
        System.out.println("s1 Hash Code: " + s1.hashCode());
        System.out.println("s2 Hash Code: " + s2.hashCode());
    }
}
```

### Output
Student: Mohit (Roll No: 101)
Is s1 equal to s2? true
s1 Hash Code: 74751433
s2 Hash Code: 74751433

## Object Class Methods Summary

| Method | Purpose |
| --- | --- |
| `toString()` | Converts an object to a readable string representation. |
| `equals()` | Compares two objects for state-based logical equality. |
| `hashCode()` | Generates a hash value used in hash-based search structures. |
| `clone()` | Creates a shallow or deep copy of the object. |
| `getClass()` | Accesses the runtime metadata of the object class. |
| `wait()` | Releases lock and puts the current thread in a waiting state. |
| `notify()` | Awakens a single thread waiting on the object monitor queue. |
| `notifyAll()` | Awakens all threads waiting on the object monitor queue. |
| `finalize()` | Performs resource cleanup before garbage reclamation (deprecated). |

## Summary

The Object class serves as the foundation of Java's inheritance hierarchy, and every class automatically inherits its methods. It provides essential functionality such as object comparison (`equals()`), hashing (`hashCode()`), string representation (`toString()`), cloning (`clone()`), runtime type information (`getClass()`), and thread communication (`wait()`, `notify()`, `notifyAll()`). Understanding Object class methods is crucial because they are used extensively in collections, multithreading, debugging, and real-world Java applications.




