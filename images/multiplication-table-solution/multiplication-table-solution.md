# Multiplication Table - Solution

## Problem Statement

Given an integer `N`, print the multiplication table of `N` from `1` to `10`.

Each result must be printed on a new line in the exact format:

`N x i = value`    where `i` ranges from `1` to `10`.

### Input Format

A single integer `N`.

### Output Format

Print `10` lines.

For each `i` from `1` to `10`, print:

`N x i = N × i`

## Explanation

The multiplication table consists of `10` entries.

For each value from `1` to `10`, multiply it by `N` and print the result in the required format. The logic works correctly for both positive and negative integers.

For example, when `N = 5`:

```Output
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
5 x 4 = 20
5 x 5 = 25
5 x 6 = 30
5 x 7 = 35
5 x 8 = 40
5 x 9 = 45
5 x 10 = 50
```

## Algorithm

1. Read the integer `N`.
2. Use a loop that runs from `1` to `10`.
3. In each iteration, multiply `N` by the current loop value.
4. Print the current multiplication in the format `N x i = N × i`.
5. Move to the next line after printing each multiplication.
6. Repeat the process until all `10` multiples are printed.

```C
#include <stdio.h>

int main() {
    long long N;
    scanf("%lld", &N);

    for (int i = 1; i <= 10; i++) {
        printf("%lld x %d = %lld\n", N, i, N * i);
    }

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long N;
    cin >> N;

    for (int i = 1; i <= 10; i++) {
        cout << N << " x " << i << " = " << N * i << '\n';
    }

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();

        for (int i = 1; i <= 10; i++) {
            System.out.println(N + " x " + i + " = " + (N * i));
        }
    }
}
```
```Python
N = int(input())

for i in range(1, 11):
    print(f"{N} x {i} = {N * i}")
```
```C#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());

        for (int i = 1; i <= 10; i++)
        {
            Console.WriteLine($"{N} x {i} = {N * i}");
        }
    }
}
```

### Output
For Input:
5
Output:
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
5 x 4 = 20
5 x 5 = 25
5 x 6 = 30
5 x 7 = 35
5 x 8 = 40
5 x 9 = 45
5 x 10 = 50

# Time Complexity
O(1)

# Space Complexity
O(1)

