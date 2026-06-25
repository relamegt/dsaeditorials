# Diamond Pattern - Solution

## Problem Statement

Given an integer `N`, print a centered diamond pattern of stars (`*`).

The upper half of the diamond, including the middle row, contains `N` rows, and the lower half contains `N - 1` rows. The number of stars increases by `2` in each row up to the middle row and then decreases by `2`.

Each row must be printed on a new line.

### Input Format

A single integer `N`.

### Output Format

Print `2 × N - 1` lines forming a centered diamond.

## Explanation

The pattern consists of two parts.

The first part prints a full pyramid where the number of stars increases by `2` in each row.

The second part prints an inverted full pyramid where the number of stars decreases by `2` in each row.

Combining these two parts forms a centered diamond.

For example, when `N = 3`:

**![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/diamond-pattern-solution/1782379350465-Screenshot_2026-06-25_145158.png)**

**Algorithm**

1. Read the integer `N`.
2. Print the upper half of the diamond using an outer loop from `1` to `N`.
3. For each row in the upper half, first print `N - row` leading spaces.
4. Then print `2 × row - 1` stars.
5. After printing all the spaces and stars for the current row, move to the next line.
6. Print the lower half of the diamond using another outer loop from `N - 1` down to `1`.
7. For each row in the lower half, first print `N - row` leading spaces.
8. Then print `2 × row - 1` stars.
9. After printing all the spaces and stars for the current row, move to the next line.
10. Repeat the process until both halves are printed, forming the complete centered diamond.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    for (int i = 1; i <= N; i++) {
        for (int j = 1; j <= N - i; j++) {
            printf(" ");
        }
        for (int j = 1; j <= (2 * i - 1); j++) {
            printf("*");
        }
        printf("\n");
    }

    for (int i = N - 1; i >= 1; i--) {
        for (int j = 1; j <= N - i; j++) {
            printf(" ");
        }
        for (int j = 1; j <= (2 * i - 1); j++) {
            printf("*");
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
        for (int j = 1; j <= (2 * i - 1); j++) {
            cout << "*";
        }
        cout << '\n';
    }

    for (int i = N - 1; i >= 1; i--) {
        for (int j = 1; j <= N - i; j++) {
            cout << " ";
        }
        for (int j = 1; j <= (2 * i - 1); j++) {
            cout << "*";
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
            for (int j = 1; j <= (2 * i - 1); j++) {
                System.out.print("*");
            }
            System.out.println();
        }

        for (int i = N - 1; i >= 1; i--) {
            for (int j = 1; j <= N - i; j++) {
                System.out.print(" ");
            }
            for (int j = 1; j <= (2 * i - 1); j++) {
                System.out.print("*");
            }
            System.out.println();
        }
    }
}
```
```Python
N = int(input())

for i in range(1, N + 1):
    print(" " * (N - i) + "*" * (2 * i - 1))

for i in range(N - 1, 0, -1):
    print(" " * (N - i) + "*" * (2 * i - 1))
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
            for (int j = 1; j <= (2 * i - 1); j++)
            {
                Console.Write("*");
            }
            Console.WriteLine();
        }

        for (int i = N - 1; i >= 1; i--)
        {
            for (int j = 1; j <= N - i; j++)
            {
                Console.Write(" ");
            }
            for (int j = 1; j <= (2 * i - 1); j++)
            {
                Console.Write("*");
            }
            Console.WriteLine();
        }
    }
}
```

### Output
For Input:
3
Output:
  *
 ***
*****
 ***
  *

# Time Complexity
O(N²)

# Space Complexity
O(1)

