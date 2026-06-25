# Hollow Rhombus Pattern - Solution

## Problem Statement

Given an integer `N`, print a hollow rhombus pattern of stars (`*`) with `N` rows and `N` columns.

The first and last rows must be completely filled with stars. In the middle rows, only the first and last positions of the rhombus body must be stars, and the inner positions must be spaces.

Each row must be printed on a new line.

### Input Format

A single integer `N`.

### Output Format

Print `N` lines forming a hollow rhombus.

## Explanation

The pattern consists of `N` rows.

Each row begins with leading spaces to create the rhombus shape. The first and last rows are completely filled with stars. For the remaining rows, only the first and last columns contain stars, while all inner positions are printed as spaces, creating a hollow rhombus.

For example, when `N = 5`:

**![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/hollow-rhombus-pattern-solution/1782380112394-Screenshot_2026-06-25_150438.png)**

**Algorithm**

1. Read the integer `N`.
2. Since the pattern contains `N` rows, use an outer loop that runs from `1` to `N`.
3. For each row, first print `N - row` leading spaces.
4. After printing the spaces, use an inner loop that runs from `1` to `N`.
5. If the current row is the first row or the last row, print a star (`*`) for every column.
6. Otherwise, if the current column is the first column or the last column, print a star (`*`).
7. If the current position is not on the border, print a space.
8. After printing all the characters for the current row, move to the next line.
9. Repeat the process until all `N` rows are printed, forming the complete hollow rhombus.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    for (int i = 1; i <= N; i++) {
        for (int j = 1; j <= N - i; j++) {
            printf(" ");
        }

        for (int j = 1; j <= N; j++) {
            if (i == 1 || i == N || j == 1 || j == N)
                printf("*");
            else
                printf(" ");
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

    for (int i = 1; i <= N; i++) {
        for (int j = 1; j <= N - i; j++) {
            cout << " ";
        }

        for (int j = 1; j <= N; j++) {
            if (i == 1 || i == N || j == 1 || j == N)
                cout << "*";
            else
                cout << " ";
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

        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= N - i; j++) {
                System.out.print(" ");
            }

            for (int j = 1; j <= N; j++) {
                if (i == 1 || i == N || j == 1 || j == N)
                    System.out.print("*");
                else
                    System.out.print(" ");
            }

            System.out.println();
        }
    }
}
```
```Python
N = int(input())

for i in range(1, N + 1):
    print(" " * (N - i), end="")

    for j in range(1, N + 1):
        if i == 1 or i == N or j == 1 or j == N:
            print("*", end="")
        else:
            print(" ", end="")

    print()
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        for (int i = 1; i <= N; i++)
        {
            for (int j = 1; j <= N - i; j++)
            {
                Console.Write(" ");
            }

            for (int j = 1; j <= N; j++)
            {
                if (i == 1 || i == N || j == 1 || j == N)
                    Console.Write("*");
                else
                    Console.Write(" ");
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
    *****
   *   *
  *   *
 *   *
*****

# Time Complexity
O(N²)

# Space Complexity
O(1)

