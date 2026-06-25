# Valid Triangle - Solution

## Problem Statement

Given three positive integers `a`, `b`, and `c` representing the sides of a triangle, determine whether they can form a valid triangle.

Three sides form a valid triangle if and only if the sum of any two sides is **strictly greater** than the third side.

### Input Format

A single line containing three space-separated integers `a`, `b`, and `c`.

### Output Format

Print `Yes` if the sides form a valid triangle, otherwise print `No`.

## Explanation

According to the **Triangle Inequality Theorem**, three sides can form a valid triangle only if all of the following conditions are satisfied:

- `a + b > c`
- `a + c > b`
- `b + c > a`

If even one of these conditions is false, the three sides cannot form a triangle.

For example, when `a = 3`, `b = 4`, and `c = 5`:

- `3 + 4 > 5` ✓
- `3 + 5 > 4` ✓
- `4 + 5 > 3` ✓

Since all three conditions are true, the sides form a valid triangle.

Output:
Yes

## Algorithm

1. Read the three integers `a`, `b`, and `c`.
2. Check whether `a + b > c`.
3. Check whether `a + c > b`.
4. Check whether `b + c > a`.
5. If all three conditions are true, print `Yes`.
6. Otherwise, print `No`.

```C
#include <stdio.h>

int main() {
    long long a, b, c;
    scanf("%lld %lld %lld", &a, &b, &c);

    if (a + b > c && a + c > b && b + c > a)
        printf("Yes");
    else
        printf("No");

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long a, b, c;
    cin >> a >> b >> c;

    if (a + b > c && a + c > b && b + c > a)
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long a = sc.nextLong();
        long b = sc.nextLong();
        long c = sc.nextLong();

        if (a + b > c && a + c > b && b + c > a)
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```
```Python
a, b, c = map(int, input().split())

if a + b > c and a + c > b and b + c > a:
    print("Yes")
else:
    print("No")
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] input = Console.ReadLine().Split();

        long a = long.Parse(input[0]);
        long b = long.Parse(input[1]);
        long c = long.Parse(input[2]);

        if (a + b > c && a + c > b && b + c > a)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}
```

### Output
For Input:
3 4 5
Output:
Yes

# Time Complexity
O(1)

# Space Complexity
O(1)

