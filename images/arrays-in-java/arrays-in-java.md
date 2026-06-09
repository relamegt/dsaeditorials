# Arrays in Java

An array is a collection of elements of the same data type stored in contiguous memory locations. It allows multiple values to be stored under a single name and accessed using an index.

In Java, arrays can hold:

- primitive types (`int`, `char`, `boolean`, etc.)
- object types (`String`, `Integer`, custom classes, etc.)

Important characteristics:

- array size is fixed after creation
- memory for arrays is allocated on the heap
- elements are automatically initialized:
- numeric types → `0`
- `boolean` → `false`
- reference types → `null`

## Declaring an Array

In Java, an array is declared by specifying the data type, followed by the array name, and empty square brackets `[]`.

![Declaring array](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/arrays-in-java/1781018139553-declaring_array.png)

### Syntax

```java
dataType[] arrayName;
// or
dataType arrayName[];
```

### Example

```java
int[] numbers;
String[] names;
```

## Initialization of an Array

When an array is declared, only a reference is created. Memory is allocated using the `new` keyword by specifying the array size.

![Initialising an array](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/arrays-in-java/1781018221760-initialising_an_array.png)

### Syntax

```java
int arr[] = new int[size];
```

### Example

```java
int[] arr = new int;[1]
```

After this line:

- `arr` has 5 elements
- all elements are initialized to `0`

## Initialization Using Array Literal

You can initialize an array using an array literal when declaring it. In this case, the `new` keyword is not required.

![Initialising using Array Literal](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/arrays-in-java/1781018323495-initialising_using_array_literal.png)

### Syntax

```java
int[] arr = {1, 2, 3};
```

The length of the array is determined by the number of values in the literal.

### Example

```java
int[] marks = {85, 90, 78, 92};
String[] students = {"Akash", "Mohit", "Abhiram"};
```

## Operations on Array Elements

### 1. Access Array Elements

Elements of an array are accessed by their index. In Java, indexing starts from `0`.

### Syntax

```java
arrayName[index]
```

### Example

```java
public class Main {
    public static void main(String[] args) {
        int[] arr = {2, 4, 8, 12, 16};

        // Accessing fourth element
        System.out.print(arr + " ");[2]

        // Accessing first element
        System.out.print(arr);
    }
}
```

### Output
12 2

**Important:**  
Index must be in the range:

```java
0 <= index <= size - 1
```

### 2. Update Array Elements

To update an element at a specific index, use the assignment operator `=`.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int[] arr = {2, 4, 8, 12, 16};

        // Updating first element
        arr = 90;
        System.out.println(arr);
    }
}
```

### Output
90

### 3. Traverse Array

Traversing an array means accessing each element one by one using a loop.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int[] arr = {2, 4, 8, 12, 16};

        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
        }
    }
}
```

### Output
2 4 8 12 16

### 4. Size of Array

To find the number of elements in an array, use the `length` property.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int[] arr = {2, 4, 8, 12, 16};
        System.out.println("Size of array: " + arr.length);
    }
}
```

### Output
Size of array: 5

## 

## 

## Primitive vs Non-Primitive Arrays

### Primitive Array

Stores primitive values directly in contiguous memory.

```java
public class Main {
    public static void main(String[] args) {
        int[] arr = {10, 20, 30, 40};
        int n = arr.length;

        System.out.print("Primitive Array -> ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
    }
}
```

### Output
Primitive Array -> 10 20 30 40

### Non-Primitive Array (String Objects)

Stores references to objects.

```java
public class Main {
    public static void main(String[] args) {
        String[] names = {"Akash", "Mohit", "Abhiram"};

        System.out.print("Non-Primitive Array -> ");
        for (int i = 0; i < names.length; i++) {
            System.out.print(names[i] + " ");
        }
    }
}
```

### Output
Non-Primitive Array -> Akash Mohit Abhiram

## Arrays of Objects in Java

An array of objects is created like an array of primitive-type data items.

### Example

```java
class Student {
    public int rollNo;
    public String name;

    Student(int rollNo, String name) {
        this.rollNo = rollNo;
        this.name = name;
    }
}

public class Main {
    public static void main(String[] args) {
        // declares an array of Student
        Student[] arr;

        // allocating memory for 5 objects of type Student
        arr = new Student;[1]

        // initialize the elements of the array
        arr = new Student(1, "Akash");
        arr = new Student(2, "Mohit");[3]
        arr = new Student(3, "Abhiram");[4]
        arr = new Student(4, "AlphaKnowledge");[2]
        arr = new Student(5, "Varun");[5]

        // accessing the elements of the array
        for (int i = 0; i < arr.length; i++) {
            System.out.println("Element at " + i + " : { "
                               + arr[i].rollNo + " "
                               + arr[i].name + " }");
        }
    }
}
```

### Output
Element at 0 : { 1 Akash }
Element at 1 : { 2 Mohit }
Element at 2 : { 3 Abhiram }
Element at 3 : { 4 AlphaKnowledge }
Element at 4 : { 5 Varun }

## What Happens If We Access Elements Outside the Array Size?

If you try to access an index that is negative or greater than or equal to `size - 1`, the JVM throws `ArrayIndexOutOfBoundsException`.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int[] arr = new int;[5]
        arr = 10;
        arr = 20;[3]
        arr = 30;[4]
        arr = 40;[2]

        System.out.println("Trying to access element outside the size of array");
        System.out.println(arr); // illegal index[1]
    }
}
```

### Output
Trying to access element outside the size of array
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 5

## Passing Arrays to Methods

Like variables, you can pass arrays to methods.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int[] arr = {3, 1, 2, 5, 4};

        // passing array to method sum
        sum(arr);
    }

    public static void sum(int[] arr) {
        int sum = 0;

        for (int i = 0; i < arr.length; i++) {
            sum += arr[i];
        }

        System.out.println("sum of array values : " + sum);
    }
}
```

### Output
sum of array values : 15

## Returning Arrays from Methods

A method can also return an array.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int[] arr = getArray();

        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
        }
    }

    public static int[] getArray() {
        return new int[]{1, 2, 3};
    }
}
```

### Output
1 2 3

## Advantages of Java Arrays

| Advantage | Explanation |
| --- | --- |
| Efficient Access | Access by index is fast: `O(1)` |
| Memory Management | Fixed size makes memory predictable |
| Data Organization | Structured storage for related elements |

## Limitations of Java Arrays

| Limitation | Explanation | Better Alternative |
| --- | --- | --- |
| Fixed Size | Cannot change size after creation | `ArrayList` |
| Type Homogeneity | Stores only same data type | `Object`, Collections, custom classes |
| Costly Insertion & Deletion | Requires shifting elements | `LinkedList` |

## Complete Example Combining Concepts

```java
public class Main {
    public static void main(String[] args) {
        int[] marks = {85, 90, 78, 92, 88};
        String[] students = {"Akash", "Mohit", "Abhiram", "AlphaKnowledge", "Varun"};

        System.out.println("Students and their marks:");

        for (int i = 0; i < marks.length; i++) {
            System.out.println(students[i] + " -> " + marks[i]);
        }

        System.out.println("\nTotal marks: " + sum(marks));
    }

    public static int sum(int[] arr) {
        int total = 0;
        for (int value : arr) {
            total += value;
        }
        return total;
    }
}
```

### Output
Students and their marks:
Akash -> 85
Mohit -> 90
Abhiram -> 78
AlphaKnowledge -> 92
Varun -> 88
Total marks: 433

##



###
