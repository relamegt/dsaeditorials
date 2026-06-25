# Largest Prime Factor - Solution

## Problem Statement

Given a positive integer `N`, find its largest prime factor.

### Input Format

A single integer `N`.

### Output Format

Print a single integer representing the largest prime factor of `N`.

## Explanation

There are two common approaches to find the largest prime factor of a number.

- **Brute Force:** Check every number from `2` to `N`. Whenever a number divides `N`, repeatedly divide `N` by it and update the largest prime factor found.
- **Check up to √N (Recommended):** A composite number always has a factor less than or equal to its square root. Therefore, check divisors only up to `√N`. Repeatedly divide by each divisor to remove all occurrences. If a number greater than `1` remains after the loop, it is itself the largest prime factor.

For example, when `N = 12`:

- `12` is divisible by `2`
- Divide: `12 → 6 → 3`
- The remaining number `3` is prime.

Hence, the largest prime factor is:

Output:
3

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the integer `N`.
2. Initialize `largest = 1`.
3. Traverse every integer from `2` to `N`.
4. For each integer:

- While it divides `N` exactly:
- Update `largest` with the current divisor.
- Divide `N` by the divisor.

1. After checking all numbers, print `largest`.

```C
#include <stdio.h>

int main() {
    long long N;
    scanf("%lld", &N);

    long long largest = 1;

    for (long long i = 2; i <= N; i++) {
        while (N % i == 0) {
            largest = i;
            N /= i;
        }
    }

    printf("%lld", largest);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long N;
    cin >> N;

    long long largest = 1;

    for (long long i = 2; i <= N; i++) {
        while (N % i == 0) {
            largest = i;
            N /= i;
        }
    }

    cout << largest;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();

        long largest = 1;

        for (long i = 2; i <= N; i++) {
            while (N % i == 0) {
                largest = i;
                N /= i;
            }
        }

        System.out.print(largest);
    }
}
```
```Python
N = int(input())

largest = 1
i = 2

while i <= N:
    while N % i == 0:
        largest = i
        N //= i
    i += 1

print(largest)
```
```C#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());

        long largest = 1;

        for (long i = 2; i <= N; i++)
        {
            while (N % i == 0)
            {
                largest = i;
                N /= i;
            }
        }

        Console.Write(largest);
    }
}
```

### Output
For Input:
12

Output:
3

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Check up to √N (Recommended)

### Algorithm

1. Read the integer `N`.
2. Initialize `largest = 1`.
3. Traverse every integer from `2` while `i × i ≤ N`.
4. For each integer:

- While it divides `N` exactly:
- Update `largest` with the current divisor.
- Divide `N` by the divisor.

1. After the loop, if `N` is greater than `1`, update `largest` with `N` because the remaining number is also a prime factor.
2. Print `largest`.

```C
#include <stdio.h>

int main() {
    long long N;
    scanf("%lld", &N);

    long long largest = 1;

    for (long long i = 2; i * i <= N; i++) {
        while (N % i == 0) {
            largest = i;
            N /= i;
        }
    }

    if (N > 1)
        largest = N;

    printf("%lld", largest);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long N;
    cin >> N;

    long long largest = 1;

    for (long long i = 2; i * i <= N; i++) {
        while (N % i == 0) {
            largest = i;
            N /= i;
        }
    }

    if (N > 1)
        largest = N;

    cout << largest;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();

        long largest = 1;

        for (long i = 2; i * i <= N; i++) {
            while (N % i == 0) {
                largest = i;
                N /= i;
            }
        }

        if (N > 1)
            largest = N;

        System.out.print(largest);
    }
}
```
```Python
N = int(input())

largest = 1
i = 2

while i * i <= N:
    while N % i == 0:
        largest = i
        N //= i
    i += 1

if N > 1:
    largest = N

print(largest)
```
```C#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());

        long largest = 1;

        for (long i = 2; i * i <= N; i++)
        {
            while (N % i == 0)
            {
                largest = i;
                N /= i;
            }
        }

        if (N > 1)
            largest = N;

        Console.Write(largest);
    }
}
```

### Output
For Input:
12

Output:
3

# Time Complexity
O(√N)

# Space Complexity
O(1)

</approaches>




