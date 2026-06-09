# Arrays Class in Java and Final Arrays

This article covers two important topics:

1. The `Arrays` class in `java.util` — a utility class for array operations
2. Final arrays in Java — what `final` means when applied to an array

---

## Arrays Class in Java

The `Arrays` class in `java.util` is a **utility class** that provides **static methods** to perform operations like:

- sorting
- searching
- comparing
- filling
- converting arrays

The `Arrays` class:

- cannot be instantiated
- is used only for utility purposes
- implicitly extends `Object`
- is declared as `final`

### Class Declaration

```java
public final class Arrays extends Object
```

### To Use Arrays Class

```java
Arrays.<functionName>(arguments);
Arrays.sort(arrayName);
```

---

## Why Do We Need the Arrays Class?

Java provides `java.util.Arrays` to help developers perform common array operations easily and efficiently, such as:

- fill an array with a particular value
- sort an array
- search in an array
- compare arrays
- convert array to list
- and many more

---

## Complete Summary of All Arrays Class Methods

| Method | Action Performed |
| --- | --- |
| `asList()` | Returns a fixed-size list backed by the specified array |
| `binarySearch()` | Searches for the specified element in the array using the Binary Search Algorithm |
| `binarySearch(array, fromIndex, toIndex, key, Comparator)` | Searches a range of the specified array for the specified object using the Binary Search Algorithm |
| `compare(array1, array2)` | Compares two arrays lexicographically: returns negative, 0, or positive if the first array is smaller, equal, or greater respectively |
| `copyOf(originalArray, newLength)` | Copies the specified array, truncating or padding with the default value (if necessary) so the copy has the specified length |
| `copyOfRange(originalArray, fromIndex, endIndex)` | Copies the specified range of the specified array into a new array |
| `deepEquals(Object[] a1, Object[] a2)` | Returns true if the two specified arrays are deeply equal to one another |
| `deepHashCode(Object[] a)` | Returns a hash code based on the "deep contents" of the specified array |
| `deepToString(Object[] a)` | Returns a string representation of the "deep contents" of the specified array |
| `equals(array1, array2)` | Checks if both the arrays are equal or not |
| `fill(originalArray, fillValue)` | Assigns the fill value to each index of the array |
| `hashCode(originalArray)` | Returns an integer hashCode of this array instance |
| `mismatch(array1, array2)` | Finds and returns the index of the first unmatched element between the two specified arrays |
| `parallelPrefix(originalArray, fromIndex, endIndex, functionalOperator)` | Performs parallelPrefix for the given range of the array with the specified functional operator |
| `parallelPrefix(originalArray, operator)` | Performs parallelPrefix for the complete array with the specified functional operator |
| `parallelSetAll(originalArray, functionalGenerator)` | Sets all the elements of this array in parallel, using the provided generator function |
| `parallelSort(originalArray)` | Sorts the specified array using parallel sort |
| `setAll(originalArray, functionalGenerator)` | Sets all the elements of the specified array using the generator function provided |
| `sort(originalArray)` | Sorts the complete array in ascending order |
| `sort(originalArray, fromIndex, endIndex)` | Sorts the specified range of array in ascending order |
| `sort(T[] a, int fromIndex, int toIndex, Comparator<super T> c)` | Sorts the specified range of the specified array of objects according to the order induced by the specified comparator |
| `sort(T[] a, Comparator<super T> c)` | Sorts the specified array of objects according to the order induced by the specified comparator |
| `spliterator(originalArray)` | Returns a Spliterator covering all of the specified array |
| `spliterator(originalArray, fromIndex, endIndex)` | Returns a Spliterator of the type of the array covering the specified range of the specified arrays |
| `stream(originalArray)` | Returns a sequential stream with the specified array as its source |
| `toString(originalArray)` | Returns a string representation of the array, where elements are enclosed in square brackets `[]` and separated by a comma and a space |

---

## Important Methods in the Arrays Class with Examples

### 1. `asList()` Method

Converts an array into a **fixed-size list**.

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] intArr = {10, 20, 15, 22, 35};

        System.out.println("int Array as List: " + Arrays.asList(intArr));
    }
}
```

**Note:** `asList()` does not work properly with **primitive arrays** like `int[]`, `char[]`. It treats the entire array as a single element instead of converting each value into a list. It works correctly with object arrays like `Integer[]`, `String[]`.

---

### 2. `binarySearch()` Method

Searches for a specified element in a **sorted array** using the binary search algorithm.

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] intArr = {10, 20, 15, 22, 35};

        Arrays.sort(intArr);

        int key = 22;

        System.out.println(key + " found at index = " + Arrays.binarySearch(intArr, key));
    }
}
```

### Output
22 found at index = 3

**Explanation:**  
If the element is found, it returns its index. If not found, it returns a negative value indicating the insertion point.

---

### 3. `compare(array1, array2)` Method

Compares two arrays **lexicographically**.

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] intArr = {10, 20, 15, 22, 35};
        int[] intArr1 = {10, 15, 22};

        System.out.println("int Arrays on comparison: " + Arrays.compare(intArr, intArr1));
    }
}
```

### Output
Integer Arrays on comparison: 1

**Returns:**

- `0` if arrays are equal
- negative if first array is smaller
- positive if first array is greater

---

### 4. `fill(array, value)` Method

Assigns a fill value to **each index** of the array.

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] arr = new int;[1]

        Arrays.fill(arr, -1);

        for (int val : arr) {
            System.out.print(val + " ");
        }
    }
}
```

### Output
-1 -1 -1 -1 -1

---

### 5. `sort(array)` Method

Sorts the complete array in **ascending order**.

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] arr = {35, 10, 22, 15, 20};

        Arrays.sort(arr);

        for (int val : arr) {
            System.out.print(val + " ");
        }
    }
}
```

### Output
10 15 20 22 35

---

### 6. `toString(array)` Method

Returns a **string representation** of the array.

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] arr = {10, 20, 30};

        System.out.println(Arrays.toString(arr));
    }
}
```

### Output
[10, 20, 30]

---

### 7. `equals(array1, array2)` Method

Checks if both arrays are **equal**.

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] arr1 = {10, 20, 30};
        int[] arr2 = {10, 20, 30};

        System.out.println(Arrays.equals(arr1, arr2));
    }
}
```

### Output
true

---

### 8. `copyOfRange(originalArray, fromIndex, toIndex)` Method

Copies a **range** of the specified array into a new array.

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] arr = {10, 20, 30, 40, 50};

        int[] copy = Arrays.copyOfRange(arr, 1, 4);

        for (int val : copy) {
            System.out.print(val + " ");
        }
    }
}
```

### Output
20 30 40

---

## Final Arrays in Java

In Java, the `final` keyword makes a variable's **reference constant**, not its **contents**. When an array is declared as `final`:

- you **cannot** reassign it to point to a new array
- you **can** still modify the elements within the array

### Key Points

- A `final` array must be initialized once and cannot be reassigned later
- Helps maintain a **fixed reference**, improving code safety and predictability

### Syntax Example

```java
final int[] arr = {10, 20, 30};
```

### What You Can Do

```java
arr = 99;  // Allowed - modify element[2]
```

### What You Cannot Do

```java
arr = new int[]{600, 700, 800};  // Compilation error - reassign reference
```

---

## Examples of Final Arrays

### Example 1: Modifying Elements of a Final Array

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        final int[] arr = {10, 20, 30};

        arr = 99;[2]

        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
        }
    }
}
```

### Output
10 20 99

---

### Example 2: Attempting Reassignment (Compilation Error)

```java
public class Main {
    public static void main(String[] args) {
        final int[] arr1 = {1, 2, 3, 4, 5};
        int[] arr2 = {10, 20, 30, 40, 50};

        arr2 = arr1;  // Allowed
        arr1 = arr2;  // Compilation error - cannot reassign final reference
    }
}
```

---

### Example 3: Final Array with Names

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        final String[] students = {"Akash", "Mohit", "Abhiram"};

        // Allowed - modify element
        students = "AlphaKnowledge";

        System.out.println("Array after modifying: " + Arrays.toString(students));

        // Not allowed - reassign reference
        // students = new String[]{"Varun", "Rahul"};  // Compilation error
    }
}
```

### Output
Array after modifying: [AlphaKnowledge, Mohit, Abhiram]

---

## What We Can and Cannot Do with Final Arrays

| Operation | Allowed? | Explanation |
| --- | --- | --- |
| Modify element in final array | **Yes** | Array contents are mutable |
| Reassign final array to new array | **No** | Reference is final |
| Modify object state in final variable | **Yes** | Object fields can be updated |
| Reassign final object reference | **No** | Final variables cannot point to new instances |

---

## Final Keyword Meaning for Arrays

When the `final` keyword is applied to an array:

- **C** is correct: *The reference to the array cannot be changed*
- The array is **not** completely immutable
- Elements **inside** the array can still be modified
- The array can still store any number of elements (not limited to 10)



###
