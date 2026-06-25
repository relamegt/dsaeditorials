# Half Diamond Star Pattern - Solution

## Problem Statement

Given an integer `N`, print a half diamond star pattern.

The pattern must first grow from `1` star to `N` stars and then shrink back to `1` star. The total number of rows must be `2 × N - 1`.

Each row must be printed on a new line.

### Input Format

A single integer `N`.

### Output Format

Print `2 × N - 1` lines.

- The first `N` lines contain `1` to `N` stars.
- The next `N - 1` lines contain `N - 1` down to `1` stars.

## Explanation

The pattern consists of two parts.

The first part prints an increasing right half pyramid from `1` star to `N` stars.

The second part prints a decreasing right half pyramid from `N - 1` stars back to `1` star.

For example, when `N = 4`:

```Output
*
**
***
****
***
**
*
```

## Algorithm

1. Read the integer `N`.
2. Print the first half of the pattern using an outer loop from `1` to `N`.
3. For each row in the first half, use an inner loop to print stars equal to the current row number.
4. After printing all the stars for the current row, move to the next line.
5. Print the second half of the pattern using another outer loop from `N - 1` down to `1`.
6. For each row in the second half, use an inner loop to print stars equal to the current row number.
7. After printing all the stars for the current row, move to the next line.
8. Repeat the process until both halves are printed, forming the complete half diamond pattern.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    for (int i = 1; i <= N; i++) {
        for (int j = 1; j <= i; j++) {
            printf("*");
        }
        printf("\n");
    }

    for (int i = N - 1; i >= 1; i--) {
        for (int j = 1; j <= i; j++) {
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
        for (int j = 1; j <= i; j++) {
            cout << "*";
        }
        cout << '\n';
    }

    for (int i = N - 1; i >= 1; i--) {
        for (int j = 1; j <= i; j++) {
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
            for (int j = 1; j <= i; j++) {
                System.out.print("*");
            }
            System.out.println();
        }

        for (int i = N - 1; i >= 1; i--) {
            for (int j = 1; j <= i; j++) {
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
    print("*" * i)

for i in range(N - 1, 0, -1):
    print("*" * i)
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
            {
                Console.Write("*");
            }
            Console.WriteLine();
        }

        for (int i = N - 1; i >= 1; i--)
        {
            for (int j = 1; j <= i; j++)
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
4
Output:
*
**
***
****
***
**
*

# Time Complexity
O(N²)

# Space Complexity
O(1)

