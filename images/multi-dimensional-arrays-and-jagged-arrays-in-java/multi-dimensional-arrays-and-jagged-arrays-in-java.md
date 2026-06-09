# Multi-Dimensional Arrays and Jagged Arrays in Java

A multi-dimensional array in Java is an **array of arrays** that allows data to be stored in tabular form such as rows and columns. It is commonly used to represent matrices, tables, and grids in programs.

The most commonly used type is the **two-dimensional (2D) array**.

---

## Two-Dimensional Array (2D Array)

A 2D array represents data in **rows and columns**. It can be understood as an array of 1D arrays.

![2D - Arrays](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/multi-dimensional-arrays-and-jagged-arrays-in-java/1781019168273-2d_arrays.png)

### Syntax

```java
data_type[][] array_name = new data_type[rows][columns];
array_name[row_index][col_index] = value;
```

### Example 1: Direct Initialization

```java
public class Main {
    public static void main(String[] args) {
        // Array initialized and assigned
        int[][] arr = { { 1, 2 }, { 3, 4 } };

        // Printing the Array
        for (int i = 0; i < 2; i++) {
            for (int j = 0; j < 2; j++) {
                System.out.print(arr[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```

### Output
1 2 
3 4

### Example 2: Using Variables for Size

```java
public class Main {
    public static void main(String[] args) {
        int rows = 2;
        int cols = 2;

        int[][] arr = new int[rows][cols];

        int value = 1;
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                arr[i][j] = value;
                value++;
            }
        }

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                System.out.print(arr[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```

### Output
1 2 
3 4

### Accessing Elements of 2D Arrays

In a 2D array:

- `i` represents the **row index**
- `j` represents the **column index**
- Elements are accessed using `arr[i][j]`

Java uses **0-based indexing**:

- `arr[0][0]` → first row, first column
- Row index ranges from `0` to `rows-1`
- Column index ranges from `0` to `cols-1`

### Example

```java
public class Main {
    public static void main(String[] args) {
        int[][] arr = { { 1, 2 }, { 3, 4 } };

        System.out.println("arr : " + arr);[1]
    }
}
```

### Output
arr[1][1] : 4

---

## 2D Array with User Input

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of rows: ");
        int row = sc.nextInt();

        System.out.print("Enter number of columns: ");
        int col = sc.nextInt();

        int[][] arr = new int[row][col];

        System.out.println("Enter elements of array: ");

        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                arr[i][j] = sc.nextInt();
            }
        }

        System.out.println("Elements of array are: ");
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                System.out.print(arr[i][j] + " ");
            }
            System.out.println();
        }

        sc.close();
    }
}
```

---

## Three-Dimensional Array (3D Array)

A 3D array is a complex form of a multidimensional array. It can be seen as an **array of 2D arrays**.

![3D - Arrays](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/multi-dimensional-arrays-and-jagged-arrays-in-java/1781019212172-3d_arrays.png)

### Syntax

```java
data_type[][][] array_name = new data_type[arrays][rows][columns];
```

### Example: Creating and Printing 3D Array

```java
public class Main {
    public static void main(String[] args) {
        int[][][] arr = { 
            { { 1, 2 }, { 3, 4 } }, 
            { { 5, 6 }, { 7, 8 } } 
        };

        int n = arr.length;
        int m = arr.length;
        int o = arr.length;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                for (int k = 0; k < o; k++) {
                    System.out.println("arr[" + i + "][" + j + "][" + k + "] = " + arr[i][j][k]);
                }
            }
        }
    }
}
```

### Output
arr[0][0][0] = 1
arr[0][0][1] = 2
arr[0][1][0] = 3
arr[0][1][1] = 4
arr[1][0][0] = 5
arr[1][0][1] = 6
arr[1][1][0] = 7
arr[1][1][1] = 8

### Accessing 3D Array Elements

Elements in 3D arrays are referred by `arr[i][j][k]`:

- `i` → array number
- `j` → row number
- `k` → column number

---

## Jagged Array in Java

A **jagged array** is a multidimensional array where **each row can have a different number of columns**. The inner arrays can be of different lengths.

![Jagged Array](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/multi-dimensional-arrays-and-jagged-arrays-in-java/1781019255574-jagged_arrays.png)

### Declaration and Initialization

```java
data_type array_name[][] = new data_type[rows][];
array_name = new data_type[col1];
array_name = new data_type[col2];[1]
array_name = new data_type[col3];[2]
```

### Example 1: Basic Jagged Array

```java
public class Main {
    public static void main(String[] args) {
        int[][] arr = new int[];[2]

        arr = new int;[3]
        arr = new int;[1][2]

        int count = 0;
        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr[i].length; j++) {
                arr[i][j] = count++;
            }
        }

        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr[i].length; j++) {
                System.out.print(arr[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```

### Output
0 1 2 
3 4

### Example 2: Alternative Initialization Methods

```java
// Method 1
int[][] arr1 = new int[][] {
    new int[] {10, 20, 30, 40},
    new int[] {50, 60, 70, 80, 90, 100},
    new int[] {110, 120}
};

// Method 2
int[][] arr2 = {
    new int[] {10, 20, 30, 40},
    new int[] {50, 60, 70, 80, 90, 100},
    new int[] {110, 120}
};

// Method 3
int[][] arr3 = {
    {10, 20, 30, 40},
    {50, 60, 70, 80, 90, 100},
    {110, 120}
};
```

### Example 3: Row i Has i + 1 Columns

```java
public class Main {
    public static void main(String[] args) {
        int rows = 5;
        int[][] arr = new int[rows][];

        for (int i = 0; i < arr.length; i++) {
            arr[i] = new int[i + 1];
        }

        int count = 0;
        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr[i].length; j++) {
                arr[i][j] = count++;
            }
        }

        System.out.println("Contents of 2D Jagged Array");
        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr[i].length; j++) {
                System.out.print(arr[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```

### Output
Contents of 2D Jagged Array
0 
1 2 
3 4 5 
6 7 8 9 
10 11 12 13 14

### Example 4: User Input Jagged Array

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);

        System.out.print("Enter the number of sub-arrays: ");
        int numberOfArrays = scan.nextInt();

        int[][] jaggedArray = new int[numberOfArrays][];

        for (int i = 0; i < numberOfArrays; i++) {
            System.out.print("Enter the size of sub-array " + (i + 1) + ": ");
            int size = scan.nextInt();
            jaggedArray[i] = new int[size];
        }

        for (int i = 0; i < numberOfArrays; i++) {
            System.out.println("Enter the elements of sub-array " + (i + 1) + ":");
            for (int j = 0; j < jaggedArray[i].length; j++) {
                jaggedArray[i][j] = scan.nextInt();
            }
        }

        System.out.println("The jagged array is:");
        for (int i = 0; i < numberOfArrays; i++) {
            for (int j = 0; j < jaggedArray[i].length; j++) {
                System.out.print(jaggedArray[i][j] + " ");
            }
            System.out.println();
        }

        scan.close();
    }
}
```

---

## Size Calculation

For a multi-dimensional array:

```java
Total elements = product of all dimension sizes
```

### Example

```java
int[][][] x = new int;[4][5][3]
// Total elements = 3 × 5 × 7 = 105
```

---

## Advantages of Jagged Arrays

| Advantage | Explanation |
| --- | --- |
| Runtime Size | Decide row sizes at runtime |
| Memory Saving | Only create space for what you need |
| Variable Row Lengths | Work with data that has rows of different lengths |
| Faster Access | Only store what you need |

**Note:** Jagged arrays can make code harder to write and read, so use them only when really needed.

---

## Applications of Multi-Dimensional Arrays

- Store student records (roll number and marks)
- Represent images in matrix form
- Dynamic programming with 2D/3D states
- Matrix multiplication
- Adjacency matrix for graphs
- Grid traversal problems

---

## Complete Example with Names

```java
public class Main {
    public static void main(String[] args) {
        int[][] marks = {
            {85, 90, 78},    // Akash
            {92, 88, 95},    // Mohit
            {78, 82, 80}     // Abhiram
        };

        String[] students = {"Akash", "Mohit", "Abhiram"};

        System.out.println("Student Marks:");
        for (int i = 0; i < students.length; i++) {
            System.out.print(students[i] + ": ");
            for (int j = 0; j < marks[i].length; j++) {
                System.out.print(marks[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```

### Output
Student Marks:
Akash: 85 90 78 
Mohit: 92 88 95 
Abhiram: 78 82 80

---

##



###
