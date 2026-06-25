# Prime Factors - Solution

## Problem Statement

Given a positive integer `N`, print all its prime factors in ascending order. If a prime factor appears multiple times, print it multiple times.

### Input Format

A single integer `N`.

### Output Format

Print all prime factors of `N` in ascending order separated by spaces.

## Explanation

There are two common approaches to find the prime factors of a number.

- **Brute Force:** Check every number from `2` to `N`. If a number divides `N`, repeatedly divide `N` by that number until it no longer divides evenly, then continue with the next number.
- **Check up to √N (Recommended):** A composite number always has a factor less than or equal to its square root. Therefore, it is sufficient to test divisors only up to `√N`. Repeatedly divide by each divisor to extract all occurrences. If a number greater than `1` remains at the end, it is also a prime factor.

For example, when `N = 12`:

- `12` is divisible by `2`
- Divide: `12 → 6 → 3`
- `3` is also prime

Prime factors are:

`2 2 3`

Output:
2 2 3

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the integer `N`.
2. Traverse every integer from `2` to `N`.
3. For each integer:

- While it divides `N` exactly:
- Print the divisor.
- Divide `N` by the divisor.

1. Continue until all numbers have been checked.

```C
#include <stdio.h>

int main() {
    long long N;
    scanf("%lld", &N);

    for (long long i = 2; i <= N; i++) {
        while (N % i == 0) {
            printf("%lld ", i);
            N /= i;
        }
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

    for (long long i = 2; i <= N; i++) {
        while (N % i == 0) {
            cout << i << " ";
            N /= i;
        }
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

        for (long i = 2; i <= N; i++) {
            while (N % i == 0) {
                System.out.print(i + " ");
                N /= i;
            }
        }
    }
}
```
```Python
N = int(input())

i = 2

while i <= N:
    while N % i == 0:
        print(i, end=" ")
        N //= i
    i += 1
```
```C#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());

        for (long i = 2; i <= N; i++)
        {
            while (N % i == 0)
            {
                Console.Write(i + " ");
                N /= i;
            }
        }
    }
}
```

### Output
For Input:
12

Output:
2 2 3

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Check up to √N (Recommended)

### Algorithm

1. Read the integer `N`.
2. Traverse every integer from `2` while `i × i ≤ N`.
3. For each integer:

- While it divides `N` exactly:
- Print the divisor.
- Divide `N` by the divisor.

1. After the loop, if `N` is greater than `1`, print `N` because it is also a prime factor.
2. The printed numbers are the prime factors in ascending order.

```C
#include <stdio.h>

int main() {
    long long N;
    scanf("%lld", &N);

    for (long long i = 2; i * i <= N; i++) {
        while (N % i == 0) {
            printf("%lld ", i);
            N /= i;
        }
    }

    if (N > 1)
        printf("%lld", N);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long N;
    cin >> N;

    for (long long i = 2; i * i <= N; i++) {
        while (N % i == 0) {
            cout << i << " ";
            N /= i;
        }
    }

    if (N > 1)
        cout << N;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();

        for (long i = 2; i * i <= N; i++) {
            while (N % i == 0) {
                System.out.print(i + " ");
                N /= i;
            }
        }

        if (N > 1)
            System.out.print(N);
    }
}
```
```Python
N = int(input())

i = 2

while i * i <= N:
    while N % i == 0:
        print(i, end=" ")
        N //= i
    i += 1

if N > 1:
    print(N, end="")
```
```C#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());

        for (long i = 2; i * i <= N; i++)
        {
            while (N % i == 0)
            {
                Console.Write(i + " ");
                N /= i;
            }
        }

        if (N > 1)
            Console.Write(N);
    }
}
```

### Output
For Input:
12

Output:
2 2 3

# Time Complexity
O(√N)

# Space Complexity
O(1)

</approaches>




