# Java FilePermission Class

The `FilePermission` class in Java (located in the `java.io` package) represents access control authorization to system files or directories. It is parameterized by a target filepath path and a list of permitted operations. This class is utilized by the legacy Java security manager framework to validate and restrict operations such as reading, writing, executing, and deleting files.

- **Action Bounds**: Supports standard actions including `read`, `write`, `execute`, `delete`, and `readlink`.
- **Wildcard Matching**: Supports wildcards to specify permissions recursively or across directory boundaries.
- **Hierarchy Integration**: Extends `java.security.Permission` and implements `java.io.Serializable`.

## Hierarchy & Declaration

The `FilePermission` class inherits from `java.security.Permission`, implementing `java.io.Serializable`.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-filepermission-class/1782052975271-ba8c1e45-6f79-4022-a74f-33a1d7b4dfb8.png)

The class declaration is:

```java
public final class FilePermission extends Permission implements Serializable
```

## Constructors of FilePermission Class

The `FilePermission` class provides a constructor to define file-level permissions:

| Constructor | Parameter Type | Description |
| --- | --- | --- |
| `FilePermission(String path, String actions)` | `String`, `String` | Creates a new FilePermission object with the specified file or directory path and permitted actions. |

### Constructor Parameters:

- **path**: The path to a file or directory. Pathnames can end with `/*` (all files in that directory) or `/-` (all files and subdirectories recursively). The special path `<<ALL FILES>>` matches any file in the system.
- **actions**: A comma-separated list of actions (e.g., `"read,write"`).

## Methods of FilePermission Class

| Method | Return Type | Description |
| --- | --- | --- |
| **equals(Object obj)** | `boolean` | Compares two FilePermission objects for equality. Returns `true` if and only if both the path and the actions are equal. |
| **getActions()** | `String` | Returns the canonical string representation of the actions, which are normalized and sorted alphabetically. |
| **hashCode()** | `int` | Returns the hash code value for this FilePermission object, consistent with its equality logic. |
| **implies(Permission p)** | `boolean` | Checks if this FilePermission object implies the specified permission. Returns `true` if the actions and path of `p` are covered. |
| **newPermissionCollection()** | `PermissionCollection` | Returns a new `PermissionCollection` object designed to hold FilePermission objects. |

## Supported Actions

The action string passed to the constructor represents a comma-separated list of permissions:

- **read**: Permission to read the file contents (corresponds to `File.exists()`, `FileInputStream`, etc.).
- **write**: Permission to write/modify the file contents (corresponds to `FileOutputStream`, `FileWriter`, etc.).
- **execute**: Permission to execute a physical system binary file (corresponds to `Runtime.exec()`).
- **delete**: Permission to delete files or folders (corresponds to `File.delete()`).
- **readlink**: Permission to read symbolic links on platforms supporting link files.

## Essential Concepts

### Actions Canonicalization

When you construct a `FilePermission` object, the order of action inputs does not affect its internal state. The `getActions()` method returns actions in a standardized, canonical format: sorted alphabetically and separated by commas. For example, passing `"write,read"` to the constructor will yield `"read,write"` when calling `getActions()`.

### Wildcard Path Matching

Paths specified in a `FilePermission` support wildcard logic:

- `"/tmp/*"`: Grants access to all files inside the `/tmp` directory, but not subdirectories.
- `"/tmp/-"`: Grants recursive access to all files and subdirectories within the `/tmp` directory.
- `"*"`: Matches any file in the current working directory.
- `"-"`: Matches any file in the current directory and subdirectories recursively.

### Implication Logic

The `implies()` method evaluates whether one permission implicitly grants another. For instance, if user policy grants a `FilePermission` for `"/tmp/-"` with actions `"read,write"`, it implies permission to `"read"` a specific file like `"/tmp/diagnostics/report.txt"`. Implication logic evaluates both the hierarchy of paths and the subset of actions.

## Expanded Java Implementation Examples

### 1. Action Canonicalization and Equality Checks

The following program demonstrates how `FilePermission` normalizes incoming actions, verifying that different action configurations point to identical permission states.

```java
import java.io.FilePermission;

public class AlphaKnowledgePermissionVerifier {
    public static void main(String[] args) {
        System.out.println("AlphaKnowledge Permission Verifier Running...");

        // Define permissions with different action ordering
        FilePermission fp1 = new FilePermission("ALPHAKNOWLEDGE.txt", "write,read");
        FilePermission fp2 = new FilePermission("ALPHAKNOWLEDGE.txt", "read,write");

        // Display canonicalized actions
        System.out.println("fp1 Canonical Actions: " + fp1.getActions());
        System.out.println("fp2 Canonical Actions: " + fp2.getActions());

        // Check equality (canonical matching)
        System.out.println("Are fp1 and fp2 equal? " + fp1.equals(fp2));
    }
}
```

### Output
AlphaKnowledge Permission Verifier Running...
fp1 Canonical Actions: read,write
fp2 Canonical Actions: read,write
Are fp1 and fp2 equal? true

### 2. Wildcard Path and Actions Implication

This program illustrates how a directory-level recursive permission logically implies a file-level permission for deep nested files.

```java
import java.io.FilePermission;

public class AlphaKnowledgePermissionImplication {
    public static void main(String[] args) {
        // Directory recursive wildcard permission
        FilePermission parentDirPermission = new FilePermission("C:\\AlphaKnowledge\\-", "read,write");

        // Specific target file permission in nested subfolder
        FilePermission targetFilePermission = new FilePermission("C:\\AlphaKnowledge\\diagnostics\\report.bin", "read");

        // Evaluate implication logic
        boolean isImplied = parentDirPermission.implies(targetFilePermission);
        System.out.println("Does directory permission imply file permission? " + isImplied);
    }
}
```

### Output
Does directory permission imply file permission? true

### 3. Permissions Collection Verification

This example shows how to group several `FilePermission` instances inside a `PermissionCollection` container.

```java
import java.io.FilePermission;
import java.security.PermissionCollection;

public class AlphaKnowledgePermissionCollection {
    public static void main(String[] args) {
        FilePermission fpRead = new FilePermission("AK_DATA.txt", "read");
        FilePermission fpWrite = new FilePermission("AK_DATA.txt", "write");

        // Construct custom collection container
        PermissionCollection pc = fpRead.newPermissionCollection();
        pc.add(fpRead);
        pc.add(fpWrite);

        // Verify presence of elements in the collection
        boolean hasElements = pc.elements().hasMoreElements();
        System.out.println("AlphaKnowledge Collection contains entries: " + hasElements);
    }
}
```

### Output
AlphaKnowledge Collection contains entries: true

# Summary

The Java FilePermission class is a concrete class extending Permission that regulates access control boundaries for files and directories. By wrapping a file path target and a comma-separated action list, it interfaces with the SecurityManager system to authorize read, write, execute, delete, and readlink operations. It features built-in path wildcard matching (directory and recursive subdirectories) and alphabetical action canonicalization to ensure accurate evaluation in permission queries. Through implications checks and standard collection containment, FilePermission provides Java applications with a robust programmatic security check layer.




