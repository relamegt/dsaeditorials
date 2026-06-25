# Floyd's Triangle Pattern - Solution

## Problem Statement

Given an integer `N`, print Floyd's Triangle containing `N` rows.

The triangle must start from `1` and continue with consecutive integers row by row. In row `i`, print exactly `i` integers separated by a single space.

Each row must be printed on a new line.

### Input Format

A single integer `N`.

### Output Format

Print `N` lines.

The `i-th` line should contain `i` consecutive integers separated by a single space.

## Explanation

The pattern contains `N` rows.

A number variable starts from `1` and increases continuously after every printed value. Each new row contains one more number than the previous row, forming Floyd's Triangle.

For example, when `N = 4`:

```Output
1
2 3
4 5 6
7 8 9 10
```

## Algorithm

1. Read the integer `N`.
2. Initialize a variable `num` with the value `1`.
3. Since the pattern contains `N` rows, use an outer loop that runs from `1` to `N`.
4. For each row, use an inner loop that runs from `1` to the current row number.
5. During each iteration of the inner loop, print the current value of `num` followed by a space.
6. Increment `num` after printing each value so that the numbers remain consecutive.
7. After printing all the numbers for the current row, move to the next line.
8. Repeat the process until all `N` rows are printed.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    int num = 1;

    for (int i = 1; i <= N; i++) {
        for (int j = 1; j <= i; j++) {
            printf("%d", num++);
            if (j != i)
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

    int num = 1;

    for (int i = 1; i <= N; i++) {
        for (int j = 1; j <= i; j++) {
            cout << num++;
            if (j != i)
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
        int num = 1;

        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print(num++);
                if (j != i)
                    System.out.print(" ");
            }
            System.out.println();
        }
    }
}
```
```Python
N = int(input())

num = 1

for i in range(1, N + 1):
    for j in range(1, i + 1):
        print(num, end="")
        if j != i:
            print(" ", end="")
        num += 1
    print()
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int num = 1;

        for (int i = 1; i <= N; i++)
        {
            for (int j = 1; j <= i; j++)
            {
                Console.Write(num++);
                if (j != i)
                    Console.Write(" ");
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
1
2 3
4 5 6
7 8 9 10

# Time Complexity
O(N²)

# Space Complexity
O(1)

