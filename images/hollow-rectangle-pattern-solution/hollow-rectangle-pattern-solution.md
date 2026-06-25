# Hollow Rectangle Pattern - Solution

## Problem Statement

Given two integers `R` and `C`, print a hollow rectangle pattern of stars (`*`) with `R` rows and `C` columns.

The border of the rectangle must be filled with stars, and all inner cells must be spaces.

Each row must be printed on a new line.

### Input Format

The first line contains two space-separated integers `R` and `C`.

### Output Format

Print `R` lines forming the hollow rectangle.

## Explanation

The pattern consists of `R` rows and `C` columns.

The first row, last row, first column, and last column form the border of the rectangle, so they are printed as stars. All remaining positions inside the border are printed as spaces, creating a hollow rectangle.

For example, when `R = 4` and `C = 5`:

```Output
*****
*   *
*   *
*****
```

## Algorithm

1. Read the integers `R` and `C`.
2. Since the rectangle contains `R` rows, use an outer loop that runs from `1` to `R`.
3. For each row, use an inner loop that runs from `1` to `C`.
4. For every position, check whether it belongs to the border of the rectangle.
5. If the current row is the first row or the last row, print a star (`*`).
6. Otherwise, if the current column is the first column or the last column, print a star (`*`).
7. If the current position is not on the border, print a space instead.
8. After completing each row, move to the next line.
9. Repeat the process until all `R` rows are printed.

```C
#include <stdio.h>

int main() {
    int R, C;
    scanf("%d %d", &R, &C);

    for (int i = 1; i <= R; i++) {
        for (int j = 1; j <= C; j++) {
            if (i == 1 || i == R || j == 1 || j == C)
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
    int R, C;
    cin >> R >> C;

    for (int i = 1; i <= R; i++) {
        for (int j = 1; j <= C; j++) {
            if (i == 1 || i == R || j == 1 || j == C)
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

        int R = sc.nextInt();
        int C = sc.nextInt();

        for (int i = 1; i <= R; i++) {
            for (int j = 1; j <= C; j++) {
                if (i == 1 || i == R || j == 1 || j == C)
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
R, C = map(int, input().split())

for i in range(1, R + 1):
    for j in range(1, C + 1):
        if i == 1 or i == R or j == 1 or j == C:
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
        string[] input = Console.ReadLine().Split();

        int R = int.Parse(input[0]);
        int C = int.Parse(input[1]);

        for (int i = 1; i <= R; i++)
        {
            for (int j = 1; j <= C; j++)
            {
                if (i == 1 || i == R || j == 1 || j == C)
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
4 5
Output:
*****
*   *
*   *
*****

# Time Complexity
O(R × C)

# Space Complexity
O(1)

