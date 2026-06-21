# Java URL Class

The `URL` class in Java (located in the `java.net` package) represents a Uniform Resource Locator, which serves as a pointer to a specific resource on the World Wide Web. This class provides a high-level, platform-independent API to retrieve, parse, and interface with remote resources such as static web pages, binary files, dynamic documents, or REST APIs.

- **Resource Identification**: Identifies files, resources, and services hosted on internet or local servers.
- **Checked Exceptions**: Constructor calls validate string structures, throwing a `MalformedURLException` if specifications violate protocol syntaxes.
- **Component Access**: Exposes direct getter methods to retrieve protocol, host, port, file, and query parameters dynamically.

## Components of a URL

A standard URL consists of several core components that define how to locate and retrieve the remote resource.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-url-class/1782054006932-d4e61c31-e91a-4caf-b9e8-d82aa61163e8.png)

1. **rotocol**: The communication standard used (e.g., `http`, `https`, or `ftp`).
2. **Host**: The domain name or IP address of the server where the resource resides (e.g., `www.alphaknowledge.org`).
3. **Port**: An optional integer defining the specific socket port on the server host (e.g., `80` for HTTP or `443` for HTTPS). If omitted, the default port for the protocol is assumed.
4. **File/Path**: The location path of the resource on the host server (e.g., `/jvm-works-jvm-architecture/`).
5. **Query String**: An optional list of parameters passed to the web application following a `?` character.
6. **Reference Anchor**: An optional section identifier following a `#` character.

## Hierarchy & Declaration

The `URL` class is a final class extending `java.lang.Object` and implements `java.io.Serializable`.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-url-class/1782054124811-62ad05eb-56d9-4aca-b696-6312390195f6.png)

The class declaration is:

```java
public final class URL extends Object implements Serializable
```

## Constructors of URL Class

The `URL` class provides six constructors to instantiate URL objects from strings, relative specifications, and custom stream handlers:

| Constructor | Parameter Type | Description |
| --- | --- | --- |
| `URL(String spec)` | `String` | Creates a URL object from the specified absolute String representation. |
| `URL(String protocol, String host, String file)` | `String`, `String`, `String` | Creates a URL object from the specified protocol, host, and file path. |
| `URL(String protocol, String host, int port, String file)` | `String`, `String`, `int`, `String` | Creates a URL object from the specified protocol, host, port number, and file path. |
| `URL(URL context, String spec)` | `URL`, `String` | Creates a URL object by parsing the relative spec within the specified base context URL. |
| `URL(String protocol, String host, int port, String file, URLStreamHandler handler)` | `String`, `String`, `int`, `String`, `URLStreamHandler` | Creates a URL object with a custom stream handler. |
| `URL(URL context, String spec, URLStreamHandler handler)` | `URL`, `String`, `URLStreamHandler` | Creates a URL object by parsing a relative spec with a custom handler. |

*Note: All constructors throw `MalformedURLException` if the target string contains an unknown protocol or has syntax formatting errors.*

## Methods of URL Class

| Method | Return Type | Description |
| --- | --- | --- |
| **getAuthority()** | `String` | Returns the authority component of this URL (hostname and optional port), or `null`. |
| **getDefaultPort()** | `int` | Returns the default port number associated with the protocol (e.g., `443` for HTTPS). |
| **getFile()** | `String` | Returns the file path and query parameters combined. |
| **getHost()** | `String` | Returns the host name of the URL. |
| **getPath()** | `String` | Returns the path portion of this URL, excluding query arguments. |
| **getPort()** | `int` | Returns the port number explicitly defined in the URL, or `-1` if the default port is used. |
| **getProtocol()** | `String` | Returns the protocol name of this URL. |
| **getQuery()** | `String` | Returns the query string portion of this URL, or `null` if none exists. |
| **getRef()** | `String` | Returns the reference anchor portion (following the `#` symbol), or `null`. |
| **toString()** | `String` | Returns the complete string representation of the URL object. |

## Essential Concepts

### MalformedURLException Handling

Because network locations are dynamically configured, constructors parsing strings require explicit try-catch management for `MalformedURLException`. This is a checked subclass of `IOException` that enforces compile-time validation of protocol prefixes and port formats.

### Relative URL Parsing

The constructor `URL(URL context, String spec)` is extremely useful for resolving relative links found in documents. Passing a base URL context (such as `https://www.alphaknowledge.org/courses/`) and a relative specification (like `../post/3038131`) automatically resolves the relative path reference to an absolute destination.

### Authority vs Host

- `getHost()` returns only the hostname or IP address of the target machine (e.g., `www.alphaknowledge.org`).
- `getAuthority()` returns the host name along with the port if it is explicitly declared in the specification string (e.g., `www.alphaknowledge.org:8080`).

## Expanded Java Implementation Examples

### 1. Parsing and Breakdown of Complex URLs

The following example demonstrates instantiating URLs using various constructors, parsing complex query links containing parameter arrays and anchors, and outputting their parsed components.

```java
import java.net.MalformedURLException;
import java.net.URL;

public class AlphaKnowledgeURLParser {
    public static void main(String[] args) {
        System.out.println("AlphaKnowledge URL Diagnostics System Initialized...");

        try {
            // Instantiating a URL from an absolute string containing query arguments and an anchor
            URL u1 = new URL("https://www.google.co.in/?gfe_rd=cr&ei=ptYqWK26I4fT8gfth6CACg#q=alpha+knowledge+java");

            // Instantiating a URL specifying protocol, hostname, and path separately
            URL u2 = new URL("http", "www.alphaknowledge.org", "/jvm-works-jvm-architecture/");

            // Instantiating a search query URL with multiple parameter segments
            URL u3 = new URL("https://www.google.co.in/search?q=gnu&rlz=1C1CHZL_enIN714IN715&ie=UTF-8#q=alpha+knowledge+java");

            System.out.println("u1: " + u1);
            System.out.println("u2: " + u2);
            System.out.println();
            System.out.println("Components breakdown of u3:");
            System.out.println("Protocol: " + u3.getProtocol());
            System.out.println("Hostname: " + u3.getHost());
            System.out.println("Default Port: " + u3.getDefaultPort());
            System.out.println("Query: " + u3.getQuery());
            System.out.println("Path: " + u3.getPath());
            System.out.println("File: " + u3.getFile());
            System.out.println("Reference: " + u3.getRef());
        } catch (MalformedURLException e) {
            System.out.println("Invalid URL target specified: " + e.getMessage());
        }
    }
}
```

### Output
u1: https://www.google.co.in/?gfe_rd=cr&ei=ptYqWK26I4fT8gfth6CACg#q=alpha+knowledge+java
u2: http://www.alphaknowledge.org/jvm-works-jvm-architecture/

Components breakdown of u3:
Protocol: https
Hostname: www.google.co.in
Default Port: 443
Query: q=gnu&rlz=1C1CHZL_enIN714IN715&ie=UTF-8
Path: /search
File: /search?q=gnu&rlz=1C1CHZL_enIN714IN715&ie=UTF-8
Reference: q=alpha+knowledge+java

```Code
+------------------------------------------------------------+
|                     [IMAGE PLACEHOLDER]                    |
| Title: Console Output Screenshot                           |
| Source Image: image attached                               |
| Description: Screenshot showing execution output inside the|
|              Java terminal environment.                    |
+------------------------------------------------------------+
```

### 2. Relative URL Resolution

This program demonstrates how passing a base URL context and a relative specification dynamically resolves paths using relative parent references.

```java
import java.net.MalformedURLException;
import java.net.URL;

public class AlphaKnowledgeRelativeURLResolver {
    public static void main(String[] args) {
        try {
            URL baseUrl = new URL("https://www.alphaknowledge.org/courses/");

            // Resolving spec relative to the base directory parent
            URL relativeUrl = new URL(baseUrl, "../post/3038131");

            System.out.println("Base URL: " + baseUrl);
            System.out.println("Relative URL Spec: ../post/3038131");
            System.out.println("Resolved Absolute URL: " + relativeUrl);
        } catch (MalformedURLException e) {
            System.out.println("URL resolution error: " + e.getMessage());
        }
    }
}
```

### Output
Base URL: https://www.alphaknowledge.org/courses/
Relative URL Spec: ../post/3038131
Resolved Absolute URL: https://www.alphaknowledge.org/post/3038131

# Summary

The Java URL class is a final class in the java.net package representing a Uniform Resource Locator. By supporting flexible constructors parsing string specifications, relative contexts, and custom stream handlers, it permits seamless validation of internet addresses. It offers structured getter methods to extract essential components such as protocol, host, port, file path, query parameters, and anchor references. Chained with checked MalformedURLException controls, the URL class provides Java applications with a robust, platform-independent component to reference and locate network resources securely.




