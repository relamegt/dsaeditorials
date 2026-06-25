# Greatest of Three Numbers - Solution

## Problem Statement

Given three integers **A**, **B**, and **C**, print the greatest among them.

If two or more values are equal and are the greatest, print that value.

### Input Format

A single line containing three space-separated integers **A**, **B**, and **C**.

### Output Format

Print a single integer — the greatest among the three numbers.

## Explanation

The task is to compare the three given integers and print the largest one.

If multiple integers are equal and have the greatest value, print that value.

## Algorithm

1. Read three integers **A**, **B**, and **C**.
2. Find the maximum among the three numbers.
3. Print the maximum value.

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int main() {
    long long A, B, C;
    cin >> A >> B >> C;

    cout << max(A, max(B, C));

    return 0;
}
```
```c
#include <stdio.h>

int main() {
    long long A, B, C;
    scanf("%lld %lld %lld", &A, &B, &C);

    long long greatest = A;

    if (B > greatest)
        greatest = B;
    if (C > greatest)
        greatest = C;

    printf("%lld\n", greatest);

    return 0;
}
```
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long A = sc.nextLong();
        long B = sc.nextLong();
        long C = sc.nextLong();

        System.out.println(Math.max(A, Math.max(B, C)));
    }
}
```
```python
A, B, C = map(int, input().split())
print(max(A, B, C))
```
```c#
using System;

class Program
{
    static void Main()
    {
        string[] input = Console.ReadLine().Split();

        long A = long.Parse(input[0]);
        long B = long.Parse(input[1]);
        long C = long.Parse(input[2]);

        Console.WriteLine(Math.Max(A, Math.Max(B, C)));
    }
}
```

### Output
For Input:
3 9 5
Output:
9

# Time Complexity
O(1)

# Space Complexity
O(1)

