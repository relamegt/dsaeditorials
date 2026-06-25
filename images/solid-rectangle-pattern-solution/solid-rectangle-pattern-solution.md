# Solid Rectangle Pattern - Solution

## Problem Statement

Given two integers `R` and `C`, print a solid rectangle pattern of stars (`*`) with `R` rows and `C` columns.

Every row must contain exactly `C` stars.

Each row must be printed on a new line.

### Input Format

The first line contains two space-separated integers `R` and `C`.

### Output Format

Print `R` lines.

Each line must contain exactly `C` stars.

## Explanation

The pattern consists of `R` rows and `C` columns.

Each row contains the same number of stars, so a nested loop can be used. The outer loop prints the rows, while the inner loop prints `C` stars for each row.

For example, when `R = 3` and `C = 5`:

```Output
*****
*****
*****
```

## Algorithm

1. Read the integers `R` and `C`.
2. Since the rectangle contains `R` rows, use an outer loop that runs from `1` to `R`.
3. For each row, use an inner loop that runs from `1` to `C`.
4. During each iteration of the inner loop, print one star (`*`) without moving to the next line.
5. After printing `C` stars for the current row, move to the next line.
6. Repeat the process until all `R` rows are printed, forming the complete solid rectangle.

```C
#include <stdio.h>

int main() {
    int R, C;
    scanf("%d %d", &R, &C);

    for (int i = 1; i <= R; i++) {
        for (int j = 1; j <= C; j++) {
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
    int R, C;
    cin >> R >> C;

    for (int i = 1; i <= R; i++) {
        for (int j = 1; j <= C; j++) {
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

        int R = sc.nextInt();
        int C = sc.nextInt();

        for (int i = 1; i <= R; i++) {
            for (int j = 1; j <= C; j++) {
                System.out.print("*");
            }
            System.out.println();
        }
    }
}
```
```Python
R, C = map(int, input().split())

for i in range(R):
    print("*" * C)
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
                Console.Write("*");
            }
            Console.WriteLine();
        }
    }
}
```

### Output
For Input:
3 5
Output:
*****
*****
*****

# Time Complexity
O(R × C)

# Space Complexity
O(1)

