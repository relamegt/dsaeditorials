# Reverse a Number - Solution

## Problem Statement

Given an integer `N`, reverse its digits and print the result.

Leading zeros in the reversed number should be omitted.

**Note:** If `N` is negative, reverse the digits of its absolute value and print the negative result.

### Input Format

A single integer `N`.

### Output Format

Print a single integer representing the reverse of `N`.

## Explanation

To reverse a number, repeatedly extract its last digit and append it to a new number.

- The last digit can be obtained using the modulus (`%`) operator.
- Before appending the extracted digit, multiply the reversed number by `10` to shift its digits one place to the left.
- Remove the last digit from the original number using integer division (`/`).
- If the original number is negative, reverse its absolute value and make the final answer negative.

For example, when `N = 12345`:

- Extract `5`, reverse becomes `5`
- Extract `4`, reverse becomes `54`
- Extract `3`, reverse becomes `543`
- Extract `2`, reverse becomes `5432`
- Extract `1`, reverse becomes `54321`

Output:
54321

## Algorithm

1. Read the integer `N`.
2. Check if `N` is negative. If yes, store this information and convert `N` to its absolute value.
3. Initialize `reverse = 0`.
4. Repeat the following steps until `N` becomes `0`:

- Extract the last digit using `N % 10`.
- Append the extracted digit to the reversed number by calculating `reverse = reverse × 10 + digit`.
- Remove the last digit from `N` using integer division (`N = N / 10`).

1. If the original number was negative, make the reversed number negative.
2. Print the reversed number.

```C
#include <stdio.h>

int main() {
    long long N;
    scanf("%lld", &N);

    int negative = 0;

    if (N < 0) {
        negative = 1;
        N = -N;
    }

    long long reverse = 0;

    while (N > 0) {
        int digit = N % 10;
        reverse = reverse * 10 + digit;
        N /= 10;
    }

    if (negative)
        reverse = -reverse;

    printf("%lld", reverse);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long N;
    cin >> N;

    bool negative = false;

    if (N < 0) {
        negative = true;
        N = -N;
    }

    long long reverse = 0;

    while (N > 0) {
        int digit = N % 10;
        reverse = reverse * 10 + digit;
        N /= 10;
    }

    if (negative)
        reverse = -reverse;

    cout << reverse;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();

        boolean negative = false;

        if (N < 0) {
            negative = true;
            N = -N;
        }

        long reverse = 0;

        while (N > 0) {
            long digit = N % 10;
            reverse = reverse * 10 + digit;
            N /= 10;
        }

        if (negative)
            reverse = -reverse;

        System.out.print(reverse);
    }
}
```
```Python
N = int(input())

negative = False

if N < 0:
    negative = True
    N = -N

reverse = 0

while N > 0:
    digit = N % 10
    reverse = reverse * 10 + digit
    N //= 10

if negative:
    reverse = -reverse

print(reverse)
```
```C#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());

        bool negative = false;

        if (N < 0)
        {
            negative = true;
            N = -N;
        }

        long reverse = 0;

        while (N > 0)
        {
            long digit = N % 10;
            reverse = reverse * 10 + digit;
            N /= 10;
        }

        if (negative)
            reverse = -reverse;

        Console.Write(reverse);
    }
}
```

### Output
For Input:
12345
Output:
54321

# Time Complexity
O(log₁₀N)

# Space Complexity
O(1)



###
