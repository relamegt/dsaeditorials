# Java Comparator Interface

## Introduction

The **Comparator** interface in Java is a utility interface used to define custom sorting logic for objects. Located in the `java.util` package, it allows sorting of user-defined classes without modifying their existing source code. It is especially useful when:

- **Multiple Sorting Strategies**: We need to sort objects based on different attributes (e.g., sorting employees by ID, name, or salary).
- **Decoupled Ordering**: Sorting logic should remain separate from the class definition.
- **Unmodifiable Classes**: Sorting logic must be defined for third-party classes whose source code cannot be edited.

Since the `Comparator` interface is a functional interface (having only one abstract method, `compare()`), it can be conveniently implemented using lambda expressions in Java 8 and later.

## Basic Code Demo

The following program defines a `Car` class and uses a `Comparator` (implemented via lambda expression) to sort a list of cars by their ID in ascending order.

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class Car {
    int id;
    String brand;

    Car(int id, String brand) {
        this.id = id;
        this.brand = brand;
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        ArrayList<Car> list = new ArrayList<>();
        list.add(new Car(2, "Tesla"));
        list.add(new Car(1, "BMW"));

        // Sort cars by id using Comparator
        Collections.sort(list, (c1, c2) -> Integer.compare(c1.id, c2.id));

        for (Car c : list) {
            System.out.println(c.id + " " + c.brand);
        }
    }
}
```

### Output
1 BMW
2 Tesla

### Explanation

- A custom class `Car` is defined with `id` and `brand` attributes.
- The `AlphaKnowledge` main program creates a list of cars and inserts two elements.
- `Collections.sort()` takes the list and a custom comparator (written as a lambda expression) to sort the cars in ascending order of their `id`.

## Hierarchy of Comparator

`Comparator` is a standalone utility interface in the `java.util` package that is used by collections to sort elements:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-comparator-interface/1782027840274-91478c3d-342a-4c62-84a4-7d5bdaf5a764.png)

## Methods in Comparator Interface

The `Comparator` interface specifies the following methods:

- **compare(T o1, T o2)**: Compares its two arguments for order. Returns a negative integer, zero, or a positive integer if the first argument is less than, equal to, or greater than the second.
- **equals(Object obj)**: Indicates whether some other object is equal to this comparator.

The contract of the `compare(T o1, T o2)` method is:

- **Negative value**: `o1` comes before `o2`.
- **Zero**: `o1` is equal to `o2`.
- **Positive value**: `o1` comes after `o2`.

## How Collections.sort() Works with Comparator

The `Collections.sort()` utility method uses a `Comparator` instance to determine the custom sorting sequence of elements in a `List`:

```java
public static <T> void sort(List<T> list, Comparator<? super T> c)
```

Internally, the sorting algorithm calls `compare()` to evaluate elements pair-wise and arrange them in the specified sequence.

## Example: Sorting by Multiple Fields (Name, then Age)

The following program creates a `Student` class and a `StudentComparator` class to sort student objects first by their name (lexicographical order), and then by their age if their names are identical.

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

class Student {
    String name;
    Integer age;

    Student(String name, Integer age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public Integer getAge() {
        return age;
    }

    @Override
    public String toString() {
        return name + " : " + age;
    }
}

class StudentComparator implements Comparator<Student> {
    public int compare(Student s1, Student s2) {
        int nameCompare = s1.getName().compareTo(s2.getName());
        int ageCompare = s1.getAge().compareTo(s2.getAge());
        return (nameCompare == 0) ? ageCompare : nameCompare;
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("mohit", 27));
        students.add(new Student("akash", 23));
        students.add(new Student("hemesh", 37));

        System.out.println("Original List:");
        for (Student s : students) {
            System.out.println(s);
        }

        // Sort by name, then by age
        Collections.sort(students, new StudentComparator());

        System.out.println("
After Sorting:");
        for (Student s : students) {
            System.out.println(s);
        }
    }
}
```

### Output
Original List:
mohit : 27
akash : 23
hemesh : 37

After Sorting:
akash : 23
hemesh : 37
mohit : 27

### Explanation

- The `Student` class holds name and age parameters.
- `StudentComparator` compares name strings using `compareTo()`. If they are the same (`nameCompare == 0`), it compares their age integers.
- `Collections.sort()` applies this comparator, sorting the students alphabetically.
- String comparison using `compareTo()` is case-sensitive (uppercase letters are sorted before lowercase letters). For case-insensitive sorting, use `compareToIgnoreCase()` or custom key extractor methods.

## Alternative Method: Using Comparator with Lambda

Java 8 offers a concise way to create comparators using `Comparator.comparing()` and `thenComparing()`, allowing chained comparisons in a single line.

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

class Student {
    String name;
    Integer age;

    Student(String name, Integer age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public Integer getAge() {
        return age;
    }

    @Override
    public String toString() {
        return name + " : " + age;
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();

        students.add(new Student("mohit", 27));
        students.add(new Student("akash", 23));
        students.add(new Student("hemesh", 37));

        System.out.println("Original List:");
        for (Student it : students) {
            System.out.println(it);
        }

        System.out.println();

        // Sort students by name, then by age using lambda chaining
        students.sort(Comparator.comparing(Student::getName).thenComparing(Student::getAge));

        System.out.println("After Sorting:");
        for (Student it : students) {
            System.out.println(it);
        }
    }
}
```

### Output
Original List:
mohit : 27
akash : 23
hemesh : 37

After Sorting:
akash : 23
hemesh : 37
mohit : 27

### Explanation

- `Comparator.comparing(Student::getName)` creates a primary comparator sorting by student names.
- `.thenComparing(Student::getAge)` chains a secondary comparison by age if names match.
- `students.sort()` executes the chained comparators directly on the list instance, producing clean, readable, and functional code.

# Summary

The Java Comparator interface represents a functional interface within the java.util package that defines custom ordering patterns for object collections without modifying the original class source code. Through its main abstract compare method, it allows developers to build multiple, distinct sorting strategies—ranging from basic integer attributes to complex multi-field properties—while cleanly separating comparison semantics from core domain entities. Whether applied through traditional standalone classes, anonymous inner classes, or modern Java 8 chained lambda expressions like comparing and thenComparing, the Comparator interface remains an essential component for custom object ordering, custom-keyed sets, and sorting tasks in enterprise Java systems.




