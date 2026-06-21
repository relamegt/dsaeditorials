# Java ServerSocket Class

The `ServerSocket` class in Java (located in the `java.io` package) is used to implement the server side of client-server network connections over TCP. It listens for incoming connection requests on a specified port, binds to a host address, and handles handshakes by spawning client-specific sockets for bidirectional communication.

- **System-Independent Execution**: Provides a unified API to manage socket port bindings across varying operating systems.
- **Backlog Management**: Supports connection queuing to hold incoming client requests before they are explicitly accepted.
- **NIO Integration**: Associated with a `ServerSocketChannel` when configured inside `java.nio.channels` for non-blocking I/O.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-serversocket-class/1782053765605-2f2396d3-05ff-4b00-a8a8-de85d73ed5ca.png)

## Hierarchy & Declaration

The `ServerSocket` class extends `java.lang.Object` and implements `java.lang.AutoCloseable` and `java.io.Closeable`.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-serversocket-class/1782053924208-e898d751-a10d-46f2-8b0d-2f025ab1b52a.png)

The class declaration is:

```java
public class ServerSocket implements Closeable
```

## Constructors of ServerSocket Class

The `ServerSocket` class provides several constructors to bind to specific ports and local addresses:

| Constructor | Parameter Type | Description |
| --- | --- | --- |
| `ServerSocket()` | None | Creates an unbound server socket. Must be bound using `bind()`. |
| `ServerSocket(int port)` | `int` (port number) | Creates a server socket bound to the specified port. Default backlog size is `50`. |
| `ServerSocket(int port, int backlog)` | `int`, `int` (backlog limit) | Creates a server socket bound to the specified port with a custom backlog limit. |
| `ServerSocket(int port, int backlog, InetAddress bindAddr)` | `int`, `int`, `InetAddress` | Creates a server socket bound to the specified port, backlog limit, and local IP address. |

## Methods of ServerSocket Class

| Method | Return Type | Description |
| --- | --- | --- |
| **accept()** | `Socket` | Listens for a connection to be made to this socket and accepts it. Blocks execution until a client connects. |
| **bind(SocketAddress endpoint)** | `void` | Binds the ServerSocket to a specific address (IP address and port number). |
| **bind(SocketAddress endpoint, int backlog)** | `void` | Binds the ServerSocket to a specific address and requests queue length. |
| **close()** | `void` | Closes this server socket, releasing port bindings. |
| **getChannel()** | `ServerSocketChannel` | Returns the unique ServerSocketChannel object associated with this socket, if any. |
| **getInetAddress()** | `InetAddress` | Returns the local IP address of this server socket. |
| **getLocalPort()** | `int` | Returns the port number on which this socket is listening. |
| **getLocalSocketAddress()** | `SocketAddress` | Returns the address of the endpoint this socket is bound to, or `null`. |
| **getReceiveBufferSize()** | `int` | Gets the value of the SO_RCVBUF option for this ServerSocket. |
| **getReuseAddress()** | `boolean` | Tests if SO_REUSEADDR option is enabled. |
| **getSoTimeout()** | `int` | Retrieves the setting for SO_TIMEOUT (milliseconds). |
| **implAccept(Socket s)** | `void` | Subclasses of ServerSocket use this method to override accept() and return custom sockets. |
| **isBound()** | `boolean` | Returns the binding state of the ServerSocket. |
| **isClosed()** | `boolean` | Returns the closed state of the ServerSocket. |
| **setPerformancePreferences(int connectionTime, int latency, int bandwidth)** | `void` | Sets performance preferences for connection time, latency, and bandwidth parameters. |
| **setReceiveBufferSize(int size)** | `void` | Sets the default receive buffer size SO_RCVBUF option for accepted client sockets. |
| **setReuseAddress(boolean on)** | `void` | Enables or disables the SO_REUSEADDR socket option. |
| **setSocketFactory(SocketImplFactory fac)** | `void` | Sets the server socket implementation factory for RMI or custom sockets. |
| **setSoTimeout(int timeout)** | `void` | Enables/disables SO_TIMEOUT with the specified timeout in milliseconds. |

## Essential Concepts

### Connection Backlog Queue

The `backlog` parameter represents the maximum number of pending client connection requests that the operating system can queue while the server is busy. If a client attempt arrives when the backlog queue is full, the connection request is rejected with a `ConnectException` (connection refused).

### accept() blocking and SO_TIMEOUT

By default, the `accept()` method block holds execution indefinitely until a client connection handshake finishes. Developers can configure a timeout limit using `setSoTimeout(int timeout)`. If the timeout expires without an incoming request, the method throws a `SocketTimeoutException`, permitting the server thread to verify state flags or resume loop runs.

### Performance Preferences

The `setPerformancePreferences()` method allows applications to hint to the JVM how to optimize socket resources. Passing integer weights for connection time, latency, and bandwidth instructs the native network interface to select optimal protocol parameters.

## Client-Side Interaction

To interact with a `ServerSocket`, client applications configure a standard client-side `Socket` referencing the server's IP address and port.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-serversocket-class/1782053870232-78f88075-79a9-4a80-87c3-998b066613fe.png)

## Expanded Java Implementation Examples

### 1. Basic TCP Server-Client Exchange

This program demonstrates a server-side `ServerSocket` listening on port `6666`, accepting a connection, reading a string payload from a client, and printing it.

#### Server Side Program

```java
import java.io.DataInputStream;
import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;

public class AlphaKnowledgeServer {
    public static void main(String[] args) {
        int port = 6666;
        System.out.println("Starting AlphaKnowledge Server...");

        try (ServerSocket serverSocket = new ServerSocket(port)) {
            System.out.println("Server started. Listening on port " + port + "...");

            // Wait and accept client connection
            try (Socket clientSocket = serverSocket.accept();
                 DataInputStream dataIn = new DataInputStream(clientSocket.getInputStream())) {

                System.out.println("Client connected successfully!");
                String clientMessage = dataIn.readUTF();
                System.out.println("Message from client: " + clientMessage);
            }
        } catch (IOException e) {
            System.out.println("Server Exception: " + e.getMessage());
        }
    }
}
```

#### Client Side Program

```java
import java.io.DataOutputStream;
import java.io.IOException;
import java.net.Socket;

public class AlphaKnowledgeClient {
    public static void main(String[] args) {
        String host = "localhost";
        int port = 6666;

        try (Socket socket = new Socket(host, port);
             DataOutputStream dataOut = new DataOutputStream(socket.getOutputStream())) {

            // Write message to the server
            dataOut.writeUTF("Hello AlphaKnowledge Readers!");
            dataOut.flush();

            System.out.println("Message sent successfully.");
        } catch (IOException e) {
            System.out.println("Client Error: " + e.getMessage());
        }
    }
}
```

### Output
Starting AlphaKnowledge Server...
Server started. Listening on port 6666...
Client connected successfully!
Message from client: Hello AlphaKnowledge Readers!

### 2. Configuring ServerSocket Accept Timeout

The following example demonstrates how configuring a `SoTimeout` on `ServerSocket` handles idle listen locks cleanly by raising a `SocketTimeoutException`.

```java
import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;
import java.net.SocketTimeoutException;

public class AlphaKnowledgeTimeoutServer {
    public static void main(String[] args) {
        int port = 7777;
        int timeoutMs = 3000; // 3 seconds timeout

        try (ServerSocket serverSocket = new ServerSocket(port)) {
            // Configure timeout on accept blocking operation
            serverSocket.setSoTimeout(timeoutMs);
            System.out.println("Server listening on port " + port + " with timeout " + timeoutMs + "ms");

            try {
                Socket socket = serverSocket.accept();
                System.out.println("Connected to: " + socket.getRemoteSocketAddress());
                socket.close();
            } catch (SocketTimeoutException e) {
                System.out.println("AlphaKnowledge Diagnostic: Server accept timed out cleanly.");
            }
        } catch (IOException e) {
            System.out.println("I/O error occurred: " + e.getMessage());
        }
    }
}
```

### Output
Server listening on port 7777 with timeout 3000ms
AlphaKnowledge Diagnostic: Server accept timed out cleanly.

# Summary

The Java ServerSocket class is a concrete class in java.net that implements server-side TCP stream endpoints. By listening on assigned ports and configuring optional backlog limits and local IP addresses, it blocks client attempts via the accept method, spawning active socket instances upon successful connection handshake resolutions. It supports comprehensive socket options, including accept timeouts (SoTimeout), receive buffers, and performance weighting configurations. When paired with standard client-side Socket instances, ServerSocket provides Java applications with a robust, platform-independent component to host network services securely.




