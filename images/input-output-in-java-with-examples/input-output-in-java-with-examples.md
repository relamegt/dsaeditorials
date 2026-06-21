# Input/Output in Java with Examples

Java I/O (Input/Output) is a collection of classes and streams in the `java.io` package that handles reading data from sources (like files, keyboard, or network) and writing data to destinations (like files, console, or sockets). It provides both byte and character streams to support all types of data.

- **Stream abstraction**: A stream is a sequence of data flowing from a source to a destination.
- **Directional streams**: Input streams are used for reading data, whereas output streams are used for writing data.
- **Data representation**: Supports both byte streams (for raw binary 8-bit data) and character streams (for 16-bit Unicode text data).

## Default/Standard Streams in Java

Java provides three default streams attached to the system console for standard input, standard output, and standard error operations. These are exposed as static members of the `System` class:

- **System.in**: The standard input stream, representing the keyboard by default.
- **System.out**: The standard output stream, representing the console monitor.
- **System.err**: The standard error stream, used to output error messages separately.

### 1. System.in

`System.in` is an instance of `InputStream`. It provides raw byte-level reading methods like `read()`. Usually, it is wrapped in helper classes like `BufferedReader` or `Scanner` for advanced text parsing.

#### Java Implementation (System.in Example)

The following example demonstrates reading a single character byte from the console using `System.in.read()`.

```java
import java.io.IOException;

public class SystemInExample {
    public static void main(String[] args) throws IOException {
        System.out.println("Enter a character:");

        // Reads a single byte from System.in
        int data = System.in.read();

        // Print the character and its ASCII value
        System.out.println("You entered: " + (char) data);
        System.out.println("ASCII Value: " + data);
    }
}
```

### 2. System.out

`System.out` is an instance of `PrintStream` used for writing standard program outputs to the console. It provides three primary methods:

- **print()**: Outputs text on the console without adding a newline at the end.
- **println()**: Outputs text on the console and appends a newline, moving the cursor to the next line.
- **printf()**: Outputs formatted text using format specifiers.

#### Java Implementation (print() Example)

The following example demonstrates printing strings on the same line.

```java
public class AlphaKnowledgePrint {
    public static void main(String[] args) {
        // using print() all are printed in the same line
        System.out.print("AlphaKnowledge! ");
        System.out.print("AlphaKnowledge! ");
        System.out.print("AlphaKnowledge! ");
    }
}
```

### Output
AlphaKnowledge! AlphaKnowledge! AlphaKnowledge!

#### Java Implementation (println() Example)

The following example demonstrates printing strings on separate lines.

```java
public class AlphaKnowledgePrintln {
    public static void main(String[] args) {
        // using println() all are printed in different lines
        System.out.println("AlphaKnowledge! ");
        System.out.println("AlphaKnowledge! ");
        System.out.println("AlphaKnowledge! ");
    }
}
```

### Output
AlphaKnowledge! 
AlphaKnowledge! 
AlphaKnowledge!

#### Java Implementation (printf() Example)

The following example demonstrates printing formatted outputs.

```java
public class AlphaKnowledgePrintf {
    public static void main(String[] args) {
        int x = 100;

        // Printing a simple integer
        System.out.printf("Printing simple integer: x = %d%n", x);

        // Printing a floating-point number with precision
        System.out.printf("Formatted with precision: PI = %.2f%n", Math.PI);

        float n = 5.2f;

        // Formatting a float to 4 decimal places
        System.out.printf("Formatted to specific width: n = %.4f%n", n);

        n = 2324435.3f;

        // Right-aligning and formatting a float to 20-character width
        System.out.printf("Formatted to right margin: n = %20.4f%n", n);
    }
}
```

### Output
Printing simple integer: x = 100
Formatted with precision: PI = 3.14
Formatted to specific width: n = 5.2000
Formatted to right margin: n =         2324435.2500

### 3. System.err

`System.err` is another `PrintStream` used exclusively for printing error messages. It works identically to `System.out` but writes to the standard error stream.

#### Java Implementation (System.err Example)

```java
public class AlphaKnowledgeError {
    public static void main(String[] args) {
        // Using print()
        System.err.print("This is an error message using print().\\n");

        // Using println()
        System.err.println("This is another error message using println().");

        // Using printf()
        System.err.printf("Error code: %d, Message: %s%n", 404, "Not Found");
    }
}
```

## Types of Streams in Java

Based on operations, Java streams are divided into two main categories:

- **Input Stream**: Used to read data from a source (such as files, memory arrays, or peripheral devices) into the application. Examples include `FileInputStream`, `BufferedInputStream`, and `ByteArrayInputStream`.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/input-output-in-java-with-examples/1782050877700-b8beb40c-52ba-4930-bddf-f94c274586e4_(1).png)

- **Output Stream**: Used to write data from the application to a destination (such as files, socket channels, or console streams). Examples include `FileOutputStream`, `BufferedOutputStream`, and `ByteArrayOutputStream`.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/input-output-in-java-with-examples/1782050975805-dfc461ae-bcac-4c38-93ed-2e3b114c1774_(1).png)

## Byte Streams vs Character Streams

Depending on the format of the data being read or written, Java classifies streams into Byte Streams and Character Streams:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/input-output-in-java-with-examples/1782050938023-b8beb40c-52ba-4930-bddf-f94c274586e4.png)

### 1. Byte Streams

Byte streams process data in 8-bit bytes. They are suitable for reading and writing raw binary data like images, compressed zip archives, audio, and executable binaries. The root classes are the abstract `InputStream` and `OutputStream` classes.

| Stream Class | Description |
| --- | --- |
| **BufferedInputStream** | Improves input reading efficiency by maintaining a memory buffer. |
| **DataInputStream** | Allows reading Java primitive types directly from binary streams. |
| **FileInputStream** | Provides mechanisms to read byte streams from a file source. |
| **FileOutputStream** | Enables writing byte streams directly to a target file. |

#### Java Implementation (Byte Stream File Copy)

The following example copies the contents of a source file to a destination file byte by byte using byte streams.

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class AlphaKnowledgeByteCopy {
    public static void main(String[] args) throws IOException {
        FileInputStream sourceStream = null;
        FileOutputStream targetStream = null;

        try {
            sourceStream = new FileInputStream("sourcefile.txt");
            targetStream = new FileOutputStream("targetfile.txt");

            // Reading source file and writing content to target file byte by byte
            int temp;
            while ((temp = sourceStream.read()) != -1) {
                targetStream.write((byte) temp);
            }
        } finally {
            if (sourceStream != null) {
                sourceStream.close();
            }
            if (targetStream != null) {
                targetStream.close();
            }
        }
    }
}
```

### 2. Character Streams

Character streams process data in 16-bit Unicode characters. They are designed for textual reading and writing operations, handling text files and translating byte-to-character encoding patterns automatically. The root classes are the abstract `Reader` and `Writer` classes.

| Stream Class | Description |
| --- | --- |
| **BufferedReader** | Buffers input character readings, supporting efficient line-by-line reading. |
| **FileReader** | Provides character-reading capabilities from a text file. |
| **FileWriter** | Provides character-writing capabilities to a text file. |
| **InputStreamReader** | Acts as a bridge, translating byte streams to character streams. |

#### Java Implementation (Character Stream File Read)

The following example reads a text file character by character using a character reader and prints it to the console.

```java
import java.io.FileReader;
import java.io.IOException;

public class AlphaKnowledgeCharRead {
    public static void main(String[] args) throws IOException {
        FileReader sourceStream = null;

        try {
            sourceStream = new FileReader("test.txt");

            // Reading text file character by character.
            int temp;
            while ((temp = sourceStream.read()) != -1) {
                System.out.print((char) temp);
            }
        } finally {
            if (sourceStream != null) {
                sourceStream.close();
            }
        }
    }
}
```

## Scanner vs BufferedReader

Java provides multiple ways to read input from standard input or files. The two most common utilities are `Scanner` and `BufferedReader`.

- **BufferedReader**: Reads text from a character-input stream, buffering characters to provide efficient reading of characters, arrays, and lines. It is fast because it has a larger default buffer (8KB) and is synchronized (thread-safe).
- **Scanner**: A simple text scanner which can parse primitive types and strings using regular expressions. It is slower due to parsing overhead and has a smaller default buffer (1KB). It is not thread-safe.

| Feature | BufferedReader | Scanner |
| --- | --- | --- |
| **Parsing** | Reads text as String only (requires manual conversion). | Can parse primitives directly (`nextInt()`, `nextFloat()`, etc.). |
| **Speed** | Extremely fast (8KB buffer). | Slower (1KB buffer, parsing overhead). |
| **Thread Safety** | Thread-safe (synchronized). | Not thread-safe. |
| **Exceptions** | Mandates handling of `IOException`. | Hides `IOException` (accessible via `ioException()`). |

### Java Implementation (Scanner Example)

The following example demonstrates reading structured tokenized input using a `Scanner`.

```java
import java.util.Scanner;

public class AlphaKnowledgeScanner {
    public static void main(String[] args) {
        String inputData = "AlphaKnowledge 100 95.5";
        Scanner scanner = new Scanner(inputData);

        // Read and parse string and primitive tokens
        String siteName = scanner.next();
        int rank = scanner.nextInt();
        double rating = scanner.nextDouble();

        System.out.println("Site: " + siteName);
        System.out.println("Rank: " + rank);
        System.out.println("Rating: " + rating);

        scanner.close();
    }
}
```

### Output
Site: AlphaKnowledge
Rank: 100
Rating: 95.5

### Java Implementation (BufferedReader Example)

The following example demonstrates reading text input line-by-line using a `BufferedReader`.

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class AlphaKnowledgeReader {
    public static void main(String[] args) throws IOException {
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        System.out.println("Enter your platform name:");

        // Reading line input
        String name = reader.readLine();
        System.out.println("Welcome to " + name + "!");
    }
}
```

## File Operations in Java (The File Class)

The `File` class in the `java.io` package represents file and directory pathnames. It provides methods to create, delete, inspect properties, and list files.

### Java Implementation (File Management)

The following program demonstrates verifying file existence, creating a new file, and querying its access properties.

```java
import java.io.File;
import java.io.IOException;

public class AlphaKnowledgeFileOps {
    public static void main(String[] args) {
        File file = new File("ak_diagnostic.txt");

        try {
            // Create file if it does not exist
            if (file.createNewFile()) {
                System.out.println("File created: " + file.getName());
            } else {
                System.out.println("File already exists.");
            }

            // Inspecting metadata attributes
            System.out.println("Path: " + file.getAbsolutePath());
            System.out.println("Writable: " + file.canWrite());
            System.out.println("Readable: " + file.canRead());
            System.out.println("Size in Bytes: " + file.length());

        } catch (IOException e) {
            System.out.println("An error occurred during file operations.");
        }
    }
}
```

### Output
File created: ak_diagnostic.txt
Path: C:\Users\chmoh\Downloads\aaa\ak_diagnostic.txt
Writable: true
Readable: true
Size in Bytes: 0

## Serialization and Deserialization

- **Serialization**: The process of converting an object's state into a byte stream, allowing it to be written to persistent storage or sent over a network. The class must implement the `Serializable` interface.
- **Deserialization**: The reverse process of recreating the Java object from the serialized byte stream.
- **Transient Keyword**: Variables declared with the `transient` keyword are skipped during serialization.

### Java Implementation (Serialization Demo)

The following example shows how to serialize and deserialize an object representing a diagnostic report.

```java
import java.io.*;

class DiagnosticReport implements Serializable {
    private static final long serialVersionUID = 1L;
    String serviceName;
    transient int secretKey; // will not be serialized

    public DiagnosticReport(String serviceName, int secretKey) {
        this.serviceName = serviceName;
        this.secretKey = secretKey;
    }
}

public class AlphaKnowledgeSerialization {
    public static void main(String[] args) {
        DiagnosticReport report = new DiagnosticReport("AlphaKnowledge", 9901);
        String filename = "report.ser";

        // Serialization
        try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream(filename))) {
            out.writeObject(report);
            System.out.println("Object serialized successfully.");
        } catch (IOException e) {
            System.out.println("IOException during serialization: " + e.getMessage());
        }

        // Deserialization
        try (ObjectInputStream in = new ObjectInputStream(new FileInputStream(filename))) {
            DiagnosticReport deserializedReport = (DiagnosticReport) in.readObject();
            System.out.println("Object deserialized successfully.");
            System.out.println("Service Name: " + deserializedReport.serviceName);
            System.out.println("Secret Key (transient): " + deserializedReport.secretKey);
        } catch (IOException | ClassNotFoundException e) {
            System.out.println("Exception during deserialization: " + e.getMessage());
        }
    }
}
```

### Output
Object serialized successfully.
Object deserialized successfully.
Service Name: AlphaKnowledge
Secret Key (transient): 0

# Summary

Java Input/Output (I/O) is a comprehensive set of classes and streams in the java.io package designed to coordinate data transfer between applications and physical storage or peripheral interfaces. It divides stream classes into InputStreams and OutputStreams based on direction, and into Byte Streams and Character Streams based on data representation. Byte streams are optimized for 8-bit binary data processing, whereas Character streams are optimized for 16-bit Unicode textual data processing. By leveraging buffered wrappers and standard streams like System.in, System.out, and System.err, developers can implement robust, resource-efficient, and highly scalable data reading and writing routines. In addition, utilities like Scanner and BufferedReader simplify console and text file ingestion, the File class provides extensive path and metadata control, and Object Serialization enables saving and recreating active object states efficiently.




