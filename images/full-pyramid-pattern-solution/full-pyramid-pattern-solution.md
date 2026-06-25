# Full Pyramid Pattern - Solution

## Problem Statement

Given an integer `N`, print a full pyramid pattern of stars (`*`) having exactly `N` rows.

The pyramid must be center-aligned. In row `i` (1-indexed), print `N - i` leading spaces followed by `2 × i - 1` stars.

Each row must be printed on a new line.

### Input Format

A single integer `N`.

### Output Format

Print `N` lines forming a center-aligned pyramid.

## Explanation

The pattern contains `N` rows.

For every row, the number of leading spaces decreases by `1`, while the number of stars increases by `2`. Since the number of stars is always odd (`2 × row - 1`), the pattern forms a centered pyramid.

For example, when `N = 4`:

**![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/full-pyramid-pattern-solution/1782378706363-Screenshot_2026-06-25_144111.png)**

**Algorithm**

1. Read the integer `N`.
2. Since the pattern contains `N` rows, use an outer loop that runs from `1` to `N`.
3. For each row, first calculate the number of leading spaces as `N - row`.
4. Use an inner loop to print the required number of spaces without moving to the next line.
5. After printing the spaces, calculate the number of stars for the current row using the formula `2 × row - 1`.
6. Use another inner loop to print the calculated number of stars without moving to the next line.
7. Once all spaces and stars for the current row are printed, move to the next line.
8. Repeat the process until all `N` rows are printed.

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
    }
}
```
```Python
N = int(input())

for i in range(1, N + 1):
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
    }
}
```

### Output
For Input:
4
Output:
   *
  ***
 *****
*******

# Time Complexity
O(N²)

# Space Complexity
O(1)

