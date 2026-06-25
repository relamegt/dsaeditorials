# Nth Term of an Arithmetic Progression - Solution

## Problem Statement

Given the first term `A`, the common difference `D`, and an integer `N`, find the `N`th term of the arithmetic progression.

An arithmetic progression is a sequence in which the difference between consecutive terms is constant.

Print the value of the `N`th term.

### Input Format

A single line containing three space-separated integers `A`, `D`, and `N`.

### Output Format

Print a single integer representing the `N`th term of the arithmetic progression.

## Explanation

The `N`th term of an arithmetic progression can be calculated using the formula:

`Nth Term = A + (N - 1) × D`

This formula directly computes the required term without generating the entire sequence.

For example, when `A = 2`, `D = 3`, and `N = 4`:

Output:
11

## Algorithm

1. Read the integers `A`, `D`, and `N`.
2. Compute the `N`th term using the formula `A + (N - 1) × D`.
3. Print the result.

```C
#include <stdio.h>

int main() {
    long long A, D, N;
    scanf("%lld %lld %lld", &A, &D, &N);

    long long term = A + (N - 1) * D;

    printf("%lld", term);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long A, D, N;
    cin >> A >> D >> N;

    long long term = A + (N - 1) * D;

    cout << term;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long A = sc.nextLong();
        long D = sc.nextLong();
        long N = sc.nextLong();

        long term = A + (N - 1) * D;

        System.out.print(term);
    }
}
```
```Python
A, D, N = map(int, input().split())

term = A + (N - 1) * D

print(term)
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] input = Console.ReadLine().Split();

        long A = long.Parse(input[0]);
        long D = long.Parse(input[1]);
        long N = long.Parse(input[2]);

        long term = A + (N - 1) * D;

        Console.Write(term);
    }
}
```

### Output
For Input:
2 3 4
Output:
11

# Time Complexity
O(1)

# Space Complexity
O(1)

