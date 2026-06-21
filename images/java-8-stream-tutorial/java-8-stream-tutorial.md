# Java 8 Stream Tutorial

## Introduction to Streams

Java 8 introduced the **Stream API** within the `java.util.stream` package, which allows developers to process collections of data in a functional and declarative way. Streams make it easier to perform operations such as filtering, mapping, reducing, and collecting data without writing complex loops and nesting conditions.

A **Stream** is a sequence of elements that supports functional-style operations. Unlike standard collections, a Stream does not store data; it only processes it from a source (like a Collection, Array, or I/O channel) and returns the transformed results.

Key features of the Stream API include:

- **Declarative Style**: Write concise and readable code using functional expressions.
- **Lazy Evaluation**: Intermediate operations are not executed until a terminal operation is invoked.
- **Parallel Execution**: Supports concurrent operations via parallel streams to leverage multi-core processors.
- **Pipeline Structure**: Allows chaining of operations (e.g., `filter()`, `map()`, `sorted()`).
- **No Storage**: Streams do not store elements; they only carry and transform elements from a source.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-8-stream-tutorial/1782028922197-7b89d80c-f3ae-4335-9c30-95ddb3081a2c.png)

The internal workflow of a stream follows three steps:

1. **Create a Stream**: Establish a stream from collections, arrays, or static generator methods.
2. **Apply Intermediate Operations**: Transform the elements in the stream (e.g., `filter()`, `map()`, `distinct()`).
3. **Apply Terminal Operation**: Perform an aggregation or traversal to close the stream and return a result (e.g., `forEach()`, `collect()`, `reduce()`).

## Creation of Streams

Streams can be initialized from various sources:

- **From a Collection**: Create a stream directly from a `List`, `Set`, or any `Collection` using the `stream()` method.
- **From an Array**: Use `Arrays.stream(array)` to convert an array into a stream.
- **Using Stream.of()**: Create a stream from a fixed set of values.
- **Infinite Stream**: Generate unbounded sequences using `Stream.iterate()` or `Stream.generate()`, typically restricted with `limit()`.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Stream;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // 1. From a Collection
        List<String> list = Arrays.asList("Tesla", "BMW", "AlphaKnowledge");
        Stream<String> stream1 = list.stream();

        // 2. From an Array
        String[] arr = {"Tesla", "BMW", "AlphaKnowledge"};
        Stream<String> stream2 = Arrays.stream(arr);

        // 3. Using Stream.of()
        Stream<Integer> stream3 = Stream.of(1, 2, 3, 4, 5);

        // 4. Infinite Stream (limited to avoid infinite loop)
        Stream<Integer> stream4 = Stream.iterate(1, n -> n + 1).limit(5);
        stream4.forEach(System.out::println);
    }
}
```

### Output
1
2
3
4
5

### Explanation

- Displays the creation of streams from collections, arrays, fixed values, and infinite sequences.
- `Stream.iterate(1, n -> n + 1)` generates an infinite sequential stream of integers.
- `limit(5)` halts generation after five elements, and `forEach()` prints the values.

## Stream Pipeline

A Stream Pipeline defines the sequence of operations applied to the data. It consists of three parts:

### Source

The source provides the data for the stream pipeline (e.g., a collection, array, file, or generator).

```java
List<Integer> numbers = Arrays.asList(10, 20, 30, 40);
Stream<Integer> stream = numbers.stream(); // Source
```

### Intermediate Operations

Intermediate operations transform a stream into another stream. Common intermediate operations include:

- **filter()**: Filters elements based on a predicate condition.
- **map()**: Transforms elements into new values.
- **sorted()**: Sorts the elements.
- **distinct()**: Removes duplicate elements.
- **skip()**: Skips the first $n$ elements.

```java
import java.util.Arrays;
import java.util.List;

public class AlphaKnowledge {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(5, 10, 20, 10, 30, 40);

        numbers.stream()
               .filter(n -> n > 10)   // Keep elements > 10
               .map(n -> n * 2)       // Double each element
               .distinct()            // Remove duplicate entries
               .sorted()              // Sort in ascending order
               .forEach(System.out::println);
    }
}
```

### Output
40
60
80

### Explanation

- The numbers `20`, `30`, and `40` are kept because they are `> 10`.
- The values are mapped (doubled) to `40`, `60`, and `80`.
- `distinct()` removes any duplicate entries, and `sorted()` sorts them.

### Terminal Operations

Terminal operations execute all operations in the pipeline and produce a final, non-stream result. Common terminal operations include:

- **forEach()**: Iterates through elements.
- **collect()**: Gathers elements into collections like lists, sets, or maps.
- **reduce()**: Combines elements into a single aggregated value.
- **count()**: Returns the number of elements.
- **anyMatch() / allMatch() / noneMatch()**: Checks if elements match a predicate.
- **findFirst() / findAny()**: Retrieves the first or any element from the stream.

```java
import java.util.Arrays;
import java.util.List;
import java.util.Set;
import java.util.stream.Collectors;

public class AlphaKnowledge {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("mohit", "akash", "hemesh", "mohit");

        // Collect elements into a Set (removes duplicates)
        Set<String> uniqueNames = names.stream().collect(Collectors.toSet());
        System.out.println(uniqueNames);

        // Count names starting with 'm'
        long count = names.stream().filter(n -> n.startsWith("m")).count();
        System.out.println("Names starting with m: " + count);

        // Reduce (concatenate elements)
        String result = names.stream().reduce("", (a, b) -> a + b + " ");
        System.out.println(result.trim());
    }
}
```

### Output
[akash, hemesh, mohit]
Names starting with m: 2
mohit akash hemesh mohit

### Explanation

- `collect(Collectors.toSet())` returns unique names, filtering out the duplicate `"mohit"`.
- `count()` returns `2` because both `"mohit"` instances start with `"m"`.
- `reduce()` concatenates the elements with spaces.

## Types of Streams

Streams are categorized into several types based on execution styles and data types:

### 1. Sequential Stream

Processes elements sequentially in a single thread. It is created by calling `stream()`.

```java
import java.util.Arrays;
import java.util.List;

public class AlphaKnowledge {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("mohit", "akash", "hemesh");
        names.stream().forEach(System.out::println);
    }
}
```

### Output
mohit
akash
hemesh

### 2. Parallel Stream

Executes operations concurrently across multiple threads in the fork-join pool to speed up processing.

- Created by calling `parallel()` on a stream or `parallelStream()` on a collection.

```java
import java.util.Arrays;
import java.util.List;

public class AlphaKnowledge {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        numbers.parallelStream()
               .forEach(n -> System.out.println(n + " " + Thread.currentThread().getName()));
    }
}
```

### Output
3 main
4 ForkJoinPool.commonPool-worker-1
2 ForkJoinPool.commonPool-worker-2
5 ForkJoinPool.commonPool-worker-3
1 ForkJoinPool.commonPool-worker-4

### Explanation

- Parallel execution splits elements across workers. The order of output lines and thread names will vary.

### 3. Infinite Streams

Generates unbounded sequences. Use `limit()` to avoid infinite execution loops.

```java
import java.util.stream.Stream;

public class AlphaKnowledge {
    public static void main(String[] args) {
        Stream.iterate(1, n -> n + 1)
              .limit(5)
              .forEach(System.out::println);
    }
}
```

### Output
1
2
3
4
5

### 4. Primitive Streams

Java offers optimized streams for primitive data types to avoid boxing overhead:

- **IntStream**: For `int` values.
- **LongStream**: For `long` values.
- **DoubleStream**: For `double` values.

```java
import java.util.stream.IntStream;

public class AlphaKnowledge {
    public static void main(String[] args) {
        IntStream.range(1, 5).forEach(System.out::println);
    }
}
```

### Output
1
2
3
4

## Stream vs Collection Difference

- **Collections**: Memory-resident data structures storing elements. Focuses on data storage and access.
- **Streams**: Functional pipelines carrying elements from a source. Focuses on data processing and transformations. Does not store elements in memory.

## Java Stream: File Operation

Streams are integrated with Java NIO to perform file I/O operations.

### 1. File Read Operation

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class AlphaKnowledge {
    private static List<String> filterAndConvertToUpper(Stream<String> stream, int length) {
        return stream.filter(s -> s.length() == length)
            .map(String::toUpperCase)
            .collect(Collectors.toList());
    }

    public static void main(String[] args) {
        String fileName = "file.txt";

        // Create a Stream of lines from the file
        try (Stream<String> lines = Files.lines(Paths.get(fileName))) {
            List<String> filteredStrings = filterAndConvertToUpper(lines, 5);
            System.out.println("Filtered strings (length 5): " + filteredStrings);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### Output
Filtered strings (length 5): [MOHIT, AKASH, CODER]

### Explanation

- `Files.lines()` opens the file and returns a stream of lines.
- `filterAndConvertToUpper` filters lines of length 5 and maps them to uppercase.

### 2. File Write Operation

```java
import java.io.IOException;
import java.io.PrintWriter;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.stream.Stream;

public class AlphaKnowledge {
    public static void main(String[] args) {
        String[] words = {"Tesla", "BMW", "AlphaKnowledge", "Toyota", "Ford"};
        String fileName = "file.txt";

        try (PrintWriter pw = new PrintWriter(Files.newBufferedWriter(Paths.get(fileName)))) {
            // Write each word to the file
            Stream.of(words).forEach(pw::println);
            System.out.println("Words written to the file successfully.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### Output
Words written to the file successfully.

### Explanation

- A `PrintWriter` is opened.
- `Stream.of(words)` wraps the array, and `forEach(pw::println)` writes each word as a line.

## Real-World Example: Transaction Filtering

We can use streams to filter, sort, map, and collect transactional data dynamically.

```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;
import java.util.stream.Collectors;

class Transaction {
    private int id;
    private int value;
    private String type;

    public Transaction(int id, int value, String type) {
        this.id = id;
        this.value = value;
        this.type = type;
    }

    public int getId() {
        return id;
    }

    public int getValue() {
        return value;
    }

    public String getType() {
        return type;
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        List<Transaction> transactions = Arrays.asList(
            new Transaction(1, 100, "GROCERY"),
            new Transaction(3, 80, "GROCERY"),
            new Transaction(6, 120, "GROCERY"),
            new Transaction(7, 40, "ELECTRONICS"),
            new Transaction(10, 50, "GROCERY")
        );

        // Filter grocery transactions, sort descending by value, and collect IDs
        List<Integer> transactionIds = transactions.stream()
                .filter(t -> t.getType().equals("GROCERY"))
                .sorted(Comparator.comparing(Transaction::getValue).reversed())
                .map(Transaction::getId)
                .collect(Collectors.toList());

        System.out.println(transactionIds); 
    }
}
```

### Output
[6, 1, 3, 10]

### Explanation

- Groceries are kept (`1, 3, 6, 10`).
- Sorted descending by value: `6` (120), `1` (100), `3` (80), `10` (50).
- Mapped to IDs: `[6, 1, 3, 10]`.

# Summary

The Java 8 Stream API provides a powerful, functional, and declarative pipeline to query, transform, and aggregate data elements from collections, arrays, and standard file sources. Supported by features like lazy evaluation and parallel concurrent executions, it separates data-processing instructions from storage nodes, significantly simplifying loops and reducing boilerplate logic. By chaining intermediate mapping and filtering operations with terminal collections or counting calculations, the Stream API facilitates clean, thread-safe, and highly optimized data pipelines across enterprise Java developments.




