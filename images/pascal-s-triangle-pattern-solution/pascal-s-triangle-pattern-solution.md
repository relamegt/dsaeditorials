# Pascal's Triangle Pattern - Solution

## Problem Statement

Given an integer `N`, print the first `N` rows of Pascal's Triangle.

In Pascal's Triangle, the first and last numbers of every row are `1`, and every other number is the sum of the two numbers directly above it.

Each row must be printed on a new line.

### Input Format

A single integer `N`.

### Output Format

Print `N` lines.

In the `i-th` row, print the values of Pascal's Triangle separated by a single space.

## Explanation

The pattern contains `N` rows.

Every row starts and ends with `1`. The remaining values are calculated using the binomial coefficient formula, allowing each row to be generated efficiently without storing the entire triangle.

For example, when `N = 5`:

```Output
1
1 1
1 2 1
1 3 3 1
1 4 6 4 1
```

## Algorithm

1. Read the integer `N`.
2. Since the pattern contains `N` rows, use an outer loop that runs from `0` to `N - 1`.
3. For each row, initialize a variable `value` with `1`, which represents the first element of the current row.
4. Use an inner loop that runs from `0` to the current row number.
5. Print the current value followed by a space if it is not the last element of the row.
6. Update the value using the formula `value = value × (row - column) / (column + 1)` to generate the next element in the same row.
7. Continue this process until all values of the current row are printed.
8. After printing the complete row, move to the next line.
9. Repeat the process until all `N` rows are printed.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    for (int i = 0; i < N; i++) {
        long long value = 1;

        for (int j = 0; j <= i; j++) {
            printf("%lld", value);

            if (j != i)
                printf(" ");

            value = value * (i - j) / (j + 1);
        }

        printf("\n");
    }

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    int N;
    cin >> N;

    for (int i = 0; i < N; i++) {
        long long value = 1;

        for (int j = 0; j <= i; j++) {
            cout << value;

            if (j != i)
                cout << " ";

            value = value * (i - j) / (j + 1);
        }

        cout << '\n';
    }

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        for (int i = 0; i < N; i++) {
            long value = 1;

            for (int j = 0; j <= i; j++) {
                System.out.print(value);

                if (j != i)
                    System.out.print(" ");

                value = value * (i - j) / (j + 1);
            }

            System.out.println();
        }
    }
}
```
```Python
N = int(input())

for i in range(N):
    value = 1

    for j in range(i + 1):
        print(value, end="")

        if j != i:
            print(" ", end="")

        value = value * (i - j) // (j + 1)

    print()
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        for (int i = 0; i < N; i++)
        {
            long value = 1;

            for (int j = 0; j <= i; j++)
            {
                Console.Write(value);

                if (j != i)
                    Console.Write(" ");

                value = value * (i - j) / (j + 1);
            }

            Console.WriteLine();
        }
    }
}
```

### Output
For Input:
5
Output:
1
1 1
1 2 1
1 3 3 1
1 4 6 4 1

# Time Complexity
O(N²)

# Space Complexity
O(1)

