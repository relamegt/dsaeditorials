# Solid Rhombus Pattern - Solution

## Problem Statement

Given an integer `N`, print a solid rhombus pattern of stars (`*`) having `N` rows and `N` stars in each row.

The rhombus is formed by printing leading spaces that decrease diagonally from top to bottom.

Each row must be printed on a new line.

### Input Format

A single integer `N`.

### Output Format

Print `N` lines.

Each line must contain `N - i` leading spaces followed by `N` stars, where `i` is the row number from `1` to `N`.

## Explanation

The pattern contains `N` rows.

Each row has the same number of stars, but the number of leading spaces decreases by `1` in every row. This creates the appearance of a solid rhombus.

For example, when `N = 4`:

**![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/solid-rhombus-pattern-solution/1782379915957-Screenshot_2026-06-25_150120.png)**

**Algorithm**

1. Read the integer `N`.
2. Since the pattern contains `N` rows, use an outer loop that runs from `1` to `N`.
3. For each row, first calculate the number of leading spaces as `N - row`.
4. Use an inner loop to print the required number of spaces without moving to the next line.
5. After printing the spaces, use another inner loop to print exactly `N` stars.
6. After printing all the spaces and stars for the current row, move to the next line.
7. Repeat the process until all `N` rows are printed, forming the complete solid rhombus.

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
        for (int j = 1; j <= N; j++) {
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
            for (int j = 1; j <= N; j++) {
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
    print(" " * (N - i) + "*" * N)
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
  ****
 ****
****

# Time Complexity
O(N²)

# Space Complexity
O(1)

