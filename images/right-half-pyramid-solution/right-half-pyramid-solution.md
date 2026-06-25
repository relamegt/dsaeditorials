# Right Half Pyramid - Solution

## Problem Statement

Given an integer `N`, print a right half pyramid pattern of stars (`*`) having exactly `N` rows.

In row `i` (1-indexed), print exactly `i` stars with no spaces between them.

Each row must be printed on a new line.

### Input Format

A single integer `N`.

### Output Format

Print `N` lines.

The `i-th` line should contain exactly `i` stars.

## Explanation

The pattern starts with one star in the first row.

For each subsequent row, increase the number of stars by `1`.

For example, when `N = 4`:

```Output
*
**
***
****
```

## Algorithm

1. Read the integer `N`.
2. Iterate from `1` to `N`.
3. For each row `i`, print exactly `i` stars (`*`) using an inner loop.
4. Move to the next line after printing each row.

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
    }
}
```
```Python
N = int(input())

for i in range(1, N + 1):
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

# Time Complexity
O(N²)

# Space Complexity
O(1)

