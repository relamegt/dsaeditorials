# Java FileReader Class

The `FileReader` class in Java (located in the `java.io` package) is a concrete subclass of `InputStreamReader`, which in turn extends the abstract `Reader` class. It is designed to read character-based text data from files. As a character-oriented stream, it automatically decodes raw bytes from disk into 16-bit Unicode characters using the system's default encoding or a specified charset, making it ideal for text files. For raw binary files (such as images, video clips, or compressed archives), `FileInputStream` should be used instead.

- **Character-Oriented Stream**: Reads stream bytes and maps them directly into 16-bit Unicode characters.
- **Automatic Encoding**: Translates native byte streams using default or explicit system charsets (e.g., UTF-8).
- **Stream Hierarchy Integration**: Extends `InputStreamReader` to inherit char-to-byte decoding features.

## Hierarchy & Declaration

The `FileReader` class inherits from `InputStreamReader` and is a descendant of `java.io.Reader`.

The class declaration is:

```java
public class FileReader extends InputStreamReader
```

## ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-filereader-class/1782055192291-74e9760d-35e9-4fdd-ae58-98aea360320d.png)

## Constructors of FileReader Class

The `FileReader` class provides several constructors to bind to files, path names, descriptors, and explicit character sets:

| Constructor | Parameter Type | Description |
| --- | --- | --- |
| `FileReader(String fileName)` | `String` | Creates a new FileReader to read from a file with the specified filepath name. |
| `FileReader(File file)` | `File` | Creates a new FileReader to read from the specified `File` object. |
| `FileReader(FileDescriptor fdObj)` | `FileDescriptor` | Creates a new FileReader bound to an existing active system file descriptor. |
| `FileReader(String fileName, Charset charset)` | `String`, `Charset` | Creates a new FileReader to read from the file using the specified character set encoding (Java 11+). |
| `FileReader(File file, Charset charset)` | `File`, `Charset` | Creates a new FileReader to read from the specified file using the specified character set encoding (Java 11+). |

## Methods of FileReader Class

| Method | Return Type | Description |
| --- | --- | --- |
| **read()** | `int` | Reads a single character and returns its integer value, or `-1` if the end of the file is reached. |
| **read(char[] cbuf, int off, int len)** | `int` | Reads up to `len` characters into a portion of the array `cbuf` starting at index `off`. Returns the number of characters read, or `-1`. |
| **ready()** | `boolean` | Checks if the stream is ready to be read (i.e., the input buffer is not empty). |
| **getEncoding()** | `String` | Returns the name of the character encoding currently used by this stream. |
| **close()** | `void` | Closes the stream and releases associated system resources. |

## Essential Concepts

### Character vs. Byte Streams

While `FileInputStream` reads raw 8-bit bytes (ideal for binary files like images), `FileReader` reads 16-bit characters. Reading binary files using `FileReader` can corrupt data because the decoder tries to map invalid byte sequences to Unicode character encodings, altering the raw binary layout.

### Explicit Charset Encoding (Java 11+)

Historically, `FileReader` constructors default to the host platform's native encoding, which can vary between operating systems (e.g., UTF-8 on Linux vs. Windows-1252 on Windows), causing platform-dependent decoding bugs. Since Java 11, `FileReader` supports passing a `Charset` parameter (e.g., `StandardCharsets.UTF_8`) to ensure consistent, cross-platform character decoding.

### Stream Cursor Exhaustion

Reading from a `FileReader` moves the stream cursor forward. Once the end of the file is reached (read methods return `-1`), subsequent reads will continue to return `-1` unless the stream is closed and a new instance is constructed. If you need to reread file content, you must reopen the stream.

## Expanded Java Implementation Examples

### 1. Reading File Contents Character by Character

The following program demonstrates opening a text file with `FileReader` and reading the file contents character-by-character using the `read()` method in a loop.

```java
import java.io.FileReader;
import java.io.IOException;

public class AlphaKnowledgeFileReaderCharByChar {
    public static void main(String[] args) {
        String filepath = "diagnostics.txt";
        System.out.println("Initiating AlphaKnowledge Char-by-Char FileReader...");

        try (FileReader reader = new FileReader(filepath)) {
            int charVal;
            // Read character by character until EOF (-1)
            while ((charVal = reader.read()) != -1) {
                System.out.print((char) charVal);
            }
            System.out.println();
        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        }
    }
}
```

### Output
Initiating AlphaKnowledge Char-by-Char FileReader...
AlphaKnowledge Diagnostic Report: Connection Stable.

*Note: For execution to run, a file named `diagnostics.txt` containing "AlphaKnowledge Diagnostic Report: Connection Stable." must exist in the working directory.*

### 2. High-Performance Buffered Reading using Character Array

To optimize I/O performance, this program reads file content into a character array buffer instead of invoking a system read operation for every character.

```java
import java.io.FileReader;
import java.io.IOException;

public class AlphaKnowledgeFileReaderArray {
    public static void main(String[] args) {
        String filepath = "diagnostics.txt";
        char[] buffer = new char[100];

        try (FileReader reader = new FileReader(filepath)) {
            // Read a block of characters into the array buffer
            int charactersRead = reader.read(buffer);
            System.out.println("Characters read: " + charactersRead);

            if (charactersRead > 0) {
                // Convert only the populated slice of the array to a String
                System.out.print(new String(buffer, 0, charactersRead));
            }
            System.out.println();
        } catch (IOException e) {
            System.out.println("Failed to read characters: " + e.getMessage());
        }
    }
}
```

### Output
Characters read: 52
AlphaKnowledge Diagnostic Report: Connection Stable.

# Summary

The Java FileReader class is a concrete class extending InputStreamReader designed for text-oriented file reading operations. By wrapping low-level system streams and converting bytes to 16-bit Unicode characters using default or explicit Java 11 Charset encodings, it ensures convenient text processing. It supports single-character and array buffer reads, as well as checking buffer readiness and retrieval of active encoding schemes. When managed using try-with-resources blocks, FileReader provides Java applications with a robust, platform-independent component to parse and process character text files securely.




