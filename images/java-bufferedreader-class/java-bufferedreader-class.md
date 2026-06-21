# Java BufferedReader Class

The `BufferedReader` class in Java (located in the `java.io` package) is a concrete subclass of the abstract `Reader` class. It is designed to read character streams efficiently by caching individual characters in a memory buffer. This buffering mechanism reduces the number of direct I/O queries to the underlying stream (such as a file or network socket), resulting in significantly faster and smoother read performance.

- **Buffered Reading**: Reads large segments of characters from the disk or source stream at once into memory, minimizing expensive system I/O calls.
- **Line-Oriented Support**: Exposes the convenient `readLine()` method, allowing character streams to be processed line by line.
- **Decorator Pattern Usage**: Wraps other `Reader` instances (such as `FileReader` or `InputStreamReader`) to enrich them with buffering capabilities.

## Hierarchy & Declaration

The `BufferedReader` class extends `java.io.Reader`, implementing the `AutoCloseable` and `Readable` interfaces.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-bufferedreader-class/1782052679760-95907baf-206f-409d-b8da-050196bff051.png)

The class declaration is:

```java
public class BufferedReader extends Reader
```

## Constructors of BufferedReader Class

The `BufferedReader` class provides two constructors to bind to character streams:

| Constructor | Parameter Type | Description |
| --- | --- | --- |
| `BufferedReader(Reader in)` | `Reader` (character input stream) | Creates a buffered character input stream using the default buffer size (typically 8,192 characters). |
| `BufferedReader(Reader in, int sz)` | `Reader`, `int` (buffer size) | Creates a buffered character input stream with a custom buffer size defined by `sz`. |

## Methods of BufferedReader Class

| Method | Return Type | Description |
| --- | --- | --- |
| **close()** | `void` | Closes this stream and releases any associated system resources. Further reads or skips will throw an `IOException`. |
| **mark(int readAheadLimit)** | `void` | Marks the current position in the stream. Subsequent calls to `reset()` will reposition the stream to this marked point. |
| **markSupported()** | `boolean` | Checks if the stream supports the `mark()` operation (always returns `true` for `BufferedReader`). |
| **read()** | `int` | Reads and returns a single character as an integer, or `-1` if the end of the stream has been reached. |
| **read(char[] cbuf, int off, int len)** | `int` | Reads up to `len` characters into a portion of character array `cbuf` starting at index `off`. Returns the number of characters read, or `-1`. |
| **readLine()** | `String` | Reads and returns a line of text, terminated by a newline (`\n`), carriage return (`\r`), or carriage return followed by newline (`\r\n`). Returns `null` if EOF is reached. |
| **ready()** | `boolean` | Checks if the stream is ready to be read without blocking. |
| **reset()** | `void` | Resets the stream's position to the most recently marked location. |
| **skip(long n)** | `long` | Skips over and discards up to `n` characters from the stream, returning the actual number of characters skipped. |

## Essential Concepts

### How Buffering Works

Without buffering, each invocation of `read()` or `read(char[])` on a character stream triggers a direct disk read or network system call, which is highly inefficient. `BufferedReader` contains an internal character buffer array (`char[] cb`). When a read operation occurs, it reads a large chunk of characters into the buffer at once. Subsequent character reads are served directly from the buffer in RAM until the buffer is exhausted, at which point it loads the next chunk.

### Stream Chaining & Decoration

Because `BufferedReader` is a decorator, it is rarely used alone. It is chained with raw stream decoders. For example:

- `new BufferedReader(new FileReader("file.txt"))` wraps a file reader.
- `new BufferedReader(new InputStreamReader(System.in))` wraps the console input byte stream, converting incoming bytes to Unicode characters and wrapping them in a buffer.

### The readLine() Lifecycle

The `readLine()` method reads characters until it encounters a carriage return (`\r`) or line feed (`\n`). The returned string contains the line content but excludes the line-termination characters. If the end of the stream is reached without reading any characters, `readLine()` returns `null`, which serves as the standard loop termination condition.

## Expanded Java Implementation Examples

### 1. Reading Text from a File Line by Line

The following program demonstrates opening a text file using `BufferedReader`, wrapping it around a `FileReader`, and printing its contents line-by-line using a standard read loop.

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class AlphaKnowledgeBufferedReaderFile {
    public static void main(String[] args) {
        String filepath = "sample.txt";

        // Try-with-resources to automatically close the stream
        try (BufferedReader reader = new BufferedReader(new FileReader(filepath))) {
            String line;
            System.out.println("Initiating AlphaKnowledge Buffered File Reader...");

            // Read the file line by line until EOF is reached
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.out.println("An error occurred while reading the file: " + e.getMessage());
        }
    }
}
```

### Output
Initiating AlphaKnowledge Buffered File Reader...
Line 1: Diagnostic data segment loaded.
Line 2: AlphaKnowledge execution test completed.

*Note: For the program to run successfully, a text file named `sample.txt` containing the output lines must exist in the runtime directory.*

### 2. Reading Custom Inputs from Standard Console Stream

This program illustrates wrapped byte-to-character conversion and buffering to read user inputs dynamically from the terminal console.

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class AlphaKnowledgeBufferedReaderConsole {
    public static void main(String[] args) {
        System.out.println("AlphaKnowledge Console Diagnostics System Initialized.");

        // Wrapping System.in (InputStream) in InputStreamReader, then BufferedReader
        try (BufferedReader reader = new BufferedReader(new InputStreamReader(System.in))) {
            System.out.print("Enter diagnostic signature code: ");
            String code = reader.readLine();

            System.out.println("Signature accepted: " + code);
        } catch (IOException e) {
            System.out.println("I/O error during console reading: " + e.getMessage());
        }
    }
}
```

### Output
AlphaKnowledge Console Diagnostics System Initialized.
Enter diagnostic signature code: AK-9988
Signature accepted: AK-9988

# Summary

The Java BufferedReader class is a concrete subclass of Reader designed to optimize character stream input through internal buffer array caching. By loading large chunks of text from underlying sources into memory, it minimizes direct disk system calls, enhancing execution efficiency. It supports essential navigation methods (read, readLine, ready, skip, reset) and is commonly chained around low-level reader decoders like FileReader and InputStreamReader. Through try-with-resources resource management and robust stream chaining, BufferedReader provides Java applications with a robust utility to process character text streams smoothly.




