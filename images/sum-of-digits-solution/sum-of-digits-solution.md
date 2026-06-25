# Sum of Digits - Solution

## Problem Statement

Given a non-negative integer `N`, find the sum of its digits.

Print the resulting sum as a single integer.

### Input Format

A single integer `N`.

### Output Format

Print a single integer representing the sum of all digits of `N`.

## Explanation

To find the sum of digits, repeatedly extract the last digit using the modulus (`%`) operator, add it to the sum, and remove the last digit using integer division (`/`).

For example, when `N = 1234`:

- Last digit = 4
- Last digit = 3
- Last digit = 2
- Last digit = 1

Sum = `1 + 2 + 3 + 4 = 10`

## Algorithm

1. Read the integer `N`.
2. Initialize `sum = 0`.
3. While `N` is greater than `0`:

- Extract last digit by `N % 10` and add that to `sum`.
- Remove last digit and update using `N = N / 10`.

Finally Print `sum`.

```C
#include <stdio.h>

int main() {
    unsigned long long N;
    scanf("%llu", &N);

    int sum = 0;

    while (N > 0) {
        sum += N % 10;
        N /= 10;
    }

    printf("%d", sum);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    unsigned long long N;
    cin >> N;

    int sum = 0;

    while (N > 0) {
        sum += N % 10;
        N /= 10;
    }

    cout << sum;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();
        int sum = 0;

        while (N > 0) {
            sum += N % 10;
            N /= 10;
        }

        System.out.print(sum);
    }
}
```
```Python
N = int(input())

sum = 0

while N > 0:
    sum += N % 10
    N //= 10

print(sum)
```
```C#
using System;

class Program
{
    static void Main()
    {
        ulong N = ulong.Parse(Console.ReadLine());

        int sum = 0;

        while (N > 0)
        {
            sum += (int)(N % 10);
            N /= 10;
        }

        Console.Write(sum);
    }
}
```

### Output
For Input:
1234
Output:
10

# Time Complexity
O(log₁₀N)

# Space Complexity
O(1)

