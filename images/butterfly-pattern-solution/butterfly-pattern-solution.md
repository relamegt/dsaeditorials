# Butterfly Pattern - Solution

## Problem Statement

Given an integer `N`, print a butterfly star pattern with `2 × N - 1` rows.

In the upper half, the number of stars on the left and right wings increases from `1` to `N`, while the number of spaces between them decreases. In the lower half, the pattern mirrors back to `1` star.

Each row must be printed on a new line.

### Input Format

A single integer `N`.

### Output Format

Print `2 × N - 1` lines forming the butterfly pattern.

## Explanation

The pattern consists of two symmetric halves.

In the upper half, the number of stars on both wings increases by `1` in each row, while the spaces between them decrease by `2`.

In the lower half, the pattern is reversed, where the stars decrease by `1` in each row and the spaces increase by `2`, forming a butterfly shape.

For example, when `N = 4`:

```Output
*      *
**    **
***  ***
********
***  ***
**    **
*      *
```

## Algorithm

1. Read the integer `N`.
2. Print the upper half of the butterfly using an outer loop from `1` to `N`.
3. For each row, print stars equal to the current row number on the left wing.
4. Print `2 × (N - row)` spaces between the two wings.
5. Print stars equal to the current row number on the right wing.
6. After printing the complete row, move to the next line.
7. Print the lower half using another outer loop from `N - 1` down to `1`.
8. For each row, print stars equal to the current row number on the left wing.
9. Print `2 × (N - row)` spaces between the two wings.
10. Print stars equal to the current row number on the right wing.
11. After printing the complete row, move to the next line.
12. Repeat the process until both halves are printed, forming the complete butterfly pattern.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    for (int i = 1; i <= N; i++) {
        for (int j = 1; j <= i; j++)
            printf("*");

        for (int j = 1; j <= 2 * (N - i); j++)
            printf(" ");

        for (int j = 1; j <= i; j++)
            printf("*");

        printf("\n");
    }

    for (int i = N - 1; i >= 1; i--) {
        for (int j = 1; j <= i; j++)
            printf("*");

        for (int j = 1; j <= 2 * (N - i); j++)
            printf(" ");

        for (int j = 1; j <= i; j++)
            printf("*");

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
        for (int j = 1; j <= i; j++)
            cout << "*";

        for (int j = 1; j <= 2 * (N - i); j++)
            cout << " ";

        for (int j = 1; j <= i; j++)
            cout << "*";

        cout << '\n';
    }

    for (int i = N - 1; i >= 1; i--) {
        for (int j = 1; j <= i; j++)
            cout << "*";

        for (int j = 1; j <= 2 * (N - i); j++)
            cout << " ";

        for (int j = 1; j <= i; j++)
            cout << "*";

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
            for (int j = 1; j <= i; j++)
                System.out.print("*");

            for (int j = 1; j <= 2 * (N - i); j++)
                System.out.print(" ");

            for (int j = 1; j <= i; j++)
                System.out.print("*");

            System.out.println();
        }

        for (int i = N - 1; i >= 1; i--) {
            for (int j = 1; j <= i; j++)
                System.out.print("*");

            for (int j = 1; j <= 2 * (N - i); j++)
                System.out.print(" ");

            for (int j = 1; j <= i; j++)
                System.out.print("*");

            System.out.println();
        }
    }
}
```
```Python
N = int(input())

for i in range(1, N + 1):
    print("*" * i + " " * (2 * (N - i)) + "*" * i)

for i in range(N - 1, 0, -1):
    print("*" * i + " " * (2 * (N - i)) + "*" * i)
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
            for (int j = 1; j <= i; j++)
                Console.Write("*");

            for (int j = 1; j <= 2 * (N - i); j++)
                Console.Write(" ");

            for (int j = 1; j <= i; j++)
                Console.Write("*");

            Console.WriteLine();
        }

        for (int i = N - 1; i >= 1; i--)
        {
            for (int j = 1; j <= i; j++)
                Console.Write("*");

            for (int j = 1; j <= 2 * (N - i); j++)
                Console.Write(" ");

            for (int j = 1; j <= i; j++)
                Console.Write("*");

            Console.WriteLine();
        }
    }
}
```

### Output
For Input:
4
Output:
*      *
**    **
***  ***
********
***  ***
**    **
*      *

# Time Complexity
O(N²)

# Space Complexity
O(1)

