# Inverted Right Half Pyramid Pattern - Solution

## Problem Statement

Given an integer `N`, print an inverted right half pyramid pattern of stars (`*`) having exactly `N` rows.

In the first row, print exactly `N` stars. Each subsequent row must contain one fewer star than the previous row.

Each row must be printed on a new line.

### Input Format

A single integer `N`.

### Output Format

Print `N` lines.

The `i-th` line should contain exactly `N - i + 1` stars.

## Explanation

The pattern begins with `N` stars in the first row.

For every new row, decrease the number of stars by `1` until only one star remains.

For example, when `N = 4`:

```Output
****
***
**
*
```

## Algorithm

1. Read the integer `N`.
2. Since the pattern contains `N` rows, use an outer loop that starts from `N` and decreases to `1`.
3. During each iteration of the outer loop, the current loop value represents the number of stars to be printed in that row.
4. For every row, use an inner loop that starts from `1` and runs up to the current row value.
5. In each iteration of the inner loop, print one star (`*`) without moving to the next line.
6. After the inner loop finishes, all stars for the current row have been printed. Move the cursor to the next line.
7. Continue the process until the outer loop reaches `1`, producing the complete inverted right half pyramid.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    for (int i = N; i >= 1; i--) {
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

    for (int i = N; i >= 1; i--) {
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

        for (int i = N; i >= 1; i--) {
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

for i in range(N, 0, -1):
    print("*" * i)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        for (int i = N; i >= 1; i--)
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
****
**
**
*

# Time Complexity
O(N²)

# Space Complexity
O(1)

