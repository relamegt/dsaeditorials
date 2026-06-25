# Nth Fibonacci Number - Solution

## Problem Statement

Given an integer `N`, find the `N`th Fibonacci number.

The Fibonacci sequence is defined as:

- `F(1) = 1`
- `F(2) = 1`
- `F(N) = F(N-1) + F(N-2)` for `N > 2`

Print the result modulo `10^9 + 7`.

### Input Format

A single integer `N`.

### Output Format

Print a single integer representing the `N`th Fibonacci number modulo `10^9 + 7`.

## Explanation

There are two common approaches to find the `N`th Fibonacci number.

- **Dynamic Programming using an Array:** Store every Fibonacci number from `1` to `N` in an array. Each new value is obtained by adding the previous two values.
- **Space Optimized Iterative Approach (Recommended):** Instead of storing all Fibonacci numbers, keep only the last two Fibonacci numbers since each term depends only on the previous two.

For example, when `N = 6`:

- `F(1) = 1`
- `F(2) = 1`
- `F(3) = 2`
- `F(4) = 3`
- `F(5) = 5`
- `F(6) = 8`

Output:
8

<approaches>
## Approach 1: Dynamic Programming using an Array

### Algorithm

1. Read the integer `N`.
2. If `N` is `1` or `2`, print `1`.
3. Create an array of size `N + 1`.
4. Initialize `fib[1] = 1` and `fib[2] = 1`.
5. Compute each Fibonacci number from `3` to `N` using:

- `fib[i] = (fib[i - 1] + fib[i - 2]) mod (10^9 + 7)`

1. Print `fib[N]`.

```C
#include <stdio.h>
#define MOD 1000000007

int main() {
    int N;
    scanf("%d", &N);

    if (N == 1 || N == 2) {
        printf("1");
        return 0;
    }

    long long fib[N + 1];
    fib[1] = fib[2] = 1;

    for (int i = 3; i <= N; i++) {
        fib[i] = (fib[i - 1] + fib[i - 2]) % MOD;
    }

    printf("%lld", fib[N]);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

const long long MOD = 1000000007;

int main() {
    int N;
    cin >> N;

    if (N == 1 || N == 2) {
        cout << 1;
        return 0;
    }

    long long fib[N + 1];
    fib[1] = fib[2] = 1;

    for (int i = 3; i <= N; i++) {
        fib[i] = (fib[i - 1] + fib[i - 2]) % MOD;
    }

    cout << fib[N];

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    static final long MOD = 1000000007;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        if (N == 1 || N == 2) {
            System.out.print(1);
            return;
        }

        long[] fib = new long[N + 1];
        fib[1] = fib[2] = 1;

        for (int i = 3; i <= N; i++) {
            fib[i] = (fib[i - 1] + fib[i - 2]) % MOD;
        }

        System.out.print(fib[N]);
    }
}
```
```Python
MOD = 1000000007

N = int(input())

if N == 1 or N == 2:
    print(1)
else:
    fib = [0] * (N + 1)
    fib[1] = fib[2] = 1

    for i in range(3, N + 1):
        fib[i] = (fib[i - 1] + fib[i - 2]) % MOD

    print(fib[N])
```
```C#
using System;

class Program
{
    const long MOD = 1000000007;

    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        if (N == 1 || N == 2)
        {
            Console.Write(1);
            return;
        }

        long[] fib = new long[N + 1];
        fib[1] = fib[2] = 1;

        for (int i = 3; i <= N; i++)
        {
            fib[i] = (fib[i - 1] + fib[i - 2]) % MOD;
        }

        Console.Write(fib[N]);
    }
}
```

### Output
For Input:
6
Output:
8

# Time Complexity
O(N)

# Space Complexity
O(N)

## Approach 2: Space Optimized Iterative Approach (Recommended)

### Algorithm

1. Read the integer `N`.
2. If `N` is `1` or `2`, print `1`.
3. Initialize two variables:

- `first = 1` (first Fibonacci number)
- `second = 1` (second Fibonacci number)

1. Repeat from the `3`rd Fibonacci number up to the `N`th Fibonacci number:

- Compute `current = (first + second) mod (10^9 + 7)`.
- Update `first = second`.
- Update `second = current`.

1. After the loop, `second` stores the `N`th Fibonacci number.
2. Print `second`.

```C
#include <stdio.h>
#define MOD 1000000007

int main() {
    int N;
    scanf("%d", &N);

    if (N == 1 || N == 2) {
        printf("1");
        return 0;
    }

    long long first = 1, second = 1, current;

    for (int i = 3; i <= N; i++) {
        current = (first + second) % MOD;
        first = second;
        second = current;
    }

    printf("%lld", second);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

const long long MOD = 1000000007;

int main() {
    int N;
    cin >> N;

    if (N == 1 || N == 2) {
        cout << 1;
        return 0;
    }

    long long first = 1, second = 1, current;

    for (int i = 3; i <= N; i++) {
        current = (first + second) % MOD;
        first = second;
        second = current;
    }

    cout << second;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    static final long MOD = 1000000007;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        if (N == 1 || N == 2) {
            System.out.print(1);
            return;
        }

        long first = 1;
        long second = 1;
        long current = 0;

        for (int i = 3; i <= N; i++) {
            current = (first + second) % MOD;
            first = second;
            second = current;
        }

        System.out.print(second);
    }
}
```
```Python
MOD = 1000000007

N = int(input())

if N == 1 or N == 2:
    print(1)
else:
    first = 1
    second = 1

    for i in range(3, N + 1):
        current = (first + second) % MOD
        first = second
        second = current

    print(second)
```
```C#
using System;

class Program
{
    const long MOD = 1000000007;

    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        if (N == 1 || N == 2)
        {
            Console.Write(1);
            return;
        }

        long first = 1;
        long second = 1;
        long current = 0;

        for (int i = 3; i <= N; i++)
        {
            current = (first + second) % MOD;
            first = second;
            second = current;
        }

        Console.Write(second);
    }
}
```

### Output
For Input:
6
Output:
8

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>

