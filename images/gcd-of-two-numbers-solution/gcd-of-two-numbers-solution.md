# GCD of Two Numbers- Solution

## Problem Statement

Given two positive integers `A` and `B`, find their Greatest Common Divisor (GCD).

The GCD of two integers is the largest positive integer that divides both numbers without leaving a remainder.

### Input Format

A single line containing two space-separated integers `A` and `B`.

### Output Format

Print a single integer representing the GCD of `A` and `B`.

## Explanation

There are two common approaches to find the GCD of two numbers.

- **Brute Force:** Check every number from `1` to the smaller of the two numbers and keep track of the largest number that divides both.
- **Euclidean Algorithm (Recommended):** Repeatedly replace the larger number with the remainder obtained when it is divided by the smaller number. Continue this process until the remainder becomes `0`. The remaining number is the GCD.

For example, when `A = 12` and `B = 8`:

- `12 % 8 = 4`
- `8 % 4 = 0`

Since the remainder becomes `0`, the GCD is `4`.

Output:
4

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the integers `A` and `B`.
2. Find the smaller of the two numbers.
3. Initialize `gcd = 1`.
4. Check every integer from `1` to the smaller number.
5. If the current number divides both `A` and `B`, update `gcd`.
6. After checking all numbers, print `gcd`.

```C
#include <stdio.h>

int main() {
    long long A, B;
    scanf("%lld %lld", &A, &B);

    long long limit = (A < B) ? A : B;
    long long gcd = 1;

    for (long long i = 1; i <= limit; i++) {
        if (A % i == 0 && B % i == 0)
            gcd = i;
    }

    printf("%lld", gcd);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long A, B;
    cin >> A >> B;

    long long limit = min(A, B);
    long long gcd = 1;

    for (long long i = 1; i <= limit; i++) {
        if (A % i == 0 && B % i == 0)
            gcd = i;
    }

    cout << gcd;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long A = sc.nextLong();
        long B = sc.nextLong();

        long limit = Math.min(A, B);
        long gcd = 1;

        for (long i = 1; i <= limit; i++) {
            if (A % i == 0 && B % i == 0)
                gcd = i;
        }

        System.out.print(gcd);
    }
}
```
```Python
A, B = map(int, input().split())

limit = min(A, B)
gcd = 1

for i in range(1, limit + 1):
    if A % i == 0 and B % i == 0:
        gcd = i

print(gcd)
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] input = Console.ReadLine().Split();

        long A = long.Parse(input[0]);
        long B = long.Parse(input[1]);

        long limit = Math.Min(A, B);
        long gcd = 1;

        for (long i = 1; i <= limit; i++)
        {
            if (A % i == 0 && B % i == 0)
                gcd = i;
        }

        Console.Write(gcd);
    }
}
```

### Output
For Input:
12 8
Output:
4

# Time Complexity
O(min(A, B))

# Space Complexity
O(1)

## Approach 2: Euclidean Algorithm (Recommended)

### Algorithm

1. Read the integers `A` and `B`.
2. Repeat the following steps until `B` becomes `0`:

- Find the remainder when `A` is divided by `B` using `A % B`.
- Store the remainder in a temporary variable.
- Assign the value of `B` to `A`.
- Assign the remainder to `B`.

1. When `B` becomes `0`, the value stored in `A` is the GCD.
2. Print `A`.

```C
#include <stdio.h>

int main() {
    long long A, B;
    scanf("%lld %lld", &A, &B);

    while (B != 0) {
        long long temp = A % B;
        A = B;
        B = temp;
    }

    printf("%lld", A);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long A, B;
    cin >> A >> B;

    while (B != 0) {
        long long temp = A % B;
        A = B;
        B = temp;
    }

    cout << A;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long A = sc.nextLong();
        long B = sc.nextLong();

        while (B != 0) {
            long temp = A % B;
            A = B;
            B = temp;
        }

        System.out.print(A);
    }
}
```
```Python
A, B = map(int, input().split())

while B != 0:
    temp = A % B
    A = B
    B = temp

print(A)
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] input = Console.ReadLine().Split();

        long A = long.Parse(input[0]);
        long B = long.Parse(input[1]);

        while (B != 0)
        {
            long temp = A % B;
            A = B;
            B = temp;
        }

        Console.Write(A);
    }
}
```

### Output
For Input:
12 8
Output:
4

# Time Complexity
O(log(min(A, B)))

# Space Complexity
O(1)

</approaches>

