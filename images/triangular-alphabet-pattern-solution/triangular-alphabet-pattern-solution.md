# Triangular Alphabet Pattern - Solution

## Problem Statement

Given an integer `N`, print a triangular alphabet pattern with `N` rows using uppercase English letters.

In row `i` (1-indexed), print the first `i` uppercase letters of the English alphabet in order without spaces.

It is guaranteed that `N` does not exceed `26`.

Each row must be printed on a new line.

### Input Format

A single integer `N`.

### Output Format

Print `N` lines.

The `i-th` line should contain the first `i` uppercase letters from `A` onward.

## Explanation

The pattern contains `N` rows.

Each row starts from the letter `A` and prints consecutive uppercase letters. Every new row contains one more letter than the previous row.

For example, when `N = 4`:

```Output
A
AB
ABC
ABCD
```

## Algorithm

1. Read the integer `N`.
2. Since the pattern contains `N` rows, use an outer loop that runs from `1` to `N`.
3. For each row, use an inner loop that runs from `0` to `row - 1`.
4. During each iteration of the inner loop, print the character obtained by adding the loop index to the ASCII value of `'A'`.
5. Continue printing letters in order without spaces until the required number of letters for the current row is printed.
6. After printing all the letters for the current row, move to the next line.
7. Repeat the process until all `N` rows are printed.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    for (int i = 1; i <= N; i++) {
        for (int j = 0; j < i; j++) {
            printf("%c", 'A' + j);
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
        for (int j = 0; j < i; j++) {
            cout << char('A' + j);
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
            for (int j = 0; j < i; j++) {
                System.out.print((char)('A' + j));
            }
            System.out.println();
        }
    }
}
```
```Python
N = int(input())

for i in range(1, N + 1):
    for j in range(i):
        print(chr(ord('A') + j), end="")
    print()
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
            for (int j = 0; j < i; j++)
            {
                Console.Write((char)('A' + j));
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
A
AB
ABC
ABCD

# Time Complexity
O(N²)

# Space Complexity
O(1)

