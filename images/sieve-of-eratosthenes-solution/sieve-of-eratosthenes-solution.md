# Sieve of Eratosthenes - Solution

## Problem Statement

Given a positive integer `N`, print all prime numbers from `2` to `N` (inclusive) in ascending order.

### Input Format

A single integer `N`.

### Output Format

Print all prime numbers from `2` to `N` separated by spaces on a single line. If no primes exist, print nothing.

## Explanation

There are two common approaches to print all prime numbers up to `N`.

- **Check Every Number for Primality:** For every number from `2` to `N`, check whether it is prime by testing divisibility up to its square root. If it is prime, print it.
- **Sieve of Eratosthenes (Recommended):** Initially assume every number is prime. Starting from `2`, mark all multiples of each prime number as non-prime. After marking is complete, the remaining unmarked numbers are prime.

For example, when `N = 20`:

- Start with all numbers from `2` to `20`.
- Mark multiples of `2`: `4, 6, 8, ...`
- Mark multiples of `3`: `6, 9, 12, ...`
- Mark multiples of `5`: `10, 15, ...`

The remaining prime numbers are:

`2 3 5 7 11 13 17 19`

Output:
2 3 5 7 11 13 17 19

<approaches>
## Approach 1: Check Every Number for Primality

### Algorithm

1. Read the integer `N`.
2. Traverse every number from `2` to `N`.
3. For each number:

- Assume it is prime.
- Check divisibility from `2` while `j × j ≤ current number`.
- If any divisor is found, it is not prime.

1. If the number is prime, print it.
2. Continue until all numbers are checked.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    for (int i = 2; i <= N; i++) {
        int prime = 1;

        for (int j = 2; j * j <= i; j++) {
            if (i % j == 0) {
                prime = 0;
                break;
            }
        }

        if (prime)
            printf("%d ", i);
    }

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    int N;
    cin >> N;

    for (int i = 2; i <= N; i++) {
        bool prime = true;

        for (int j = 2; j * j <= i; j++) {
            if (i % j == 0) {
                prime = false;
                break;
            }
        }

        if (prime)
            cout << i << " ";
    }

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        for (int i = 2; i <= N; i++) {
            boolean prime = true;

            for (int j = 2; j * j <= i; j++) {
                if (i % j == 0) {
                    prime = false;
                    break;
                }
            }

            if (prime)
                System.out.print(i + " ");
        }
    }
}
```
```Python
N = int(input())

for i in range(2, N + 1):
    prime = True

    j = 2
    while j * j <= i:
        if i % j == 0:
            prime = False
            break
        j += 1

    if prime:
        print(i, end=" ")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        for (int i = 2; i <= N; i++)
        {
            bool prime = true;

            for (int j = 2; j * j <= i; j++)
            {
                if (i % j == 0)
                {
                    prime = false;
                    break;
                }
            }

            if (prime)
                Console.Write(i + " ");
        }
    }
}
```

### Output
For Input:
20

Output:
2 3 5 7 11 13 17 19

# Time Complexity
O(N√N)

# Space Complexity
O(1)

## Approach 2: Sieve of Eratosthenes (Recommended)

### Algorithm

1. Read the integer `N`.
2. Create a boolean array of size `N + 1` and initially mark every number as prime.
3. Mark `0` and `1` as non-prime.
4. Traverse from `2` while `i × i ≤ N`.
5. If `i` is still marked as prime:

- Mark all multiples of `i` starting from `i × i` as non-prime.

1. After completing the marking process, traverse from `2` to `N`.
2. Print every number that is still marked as prime.

```C
#include <stdio.h>
#include <stdbool.h>

int main() {
    int N;
    scanf("%d", &N);

    bool prime[N + 1];

    for (int i = 0; i <= N; i++)
        prime[i] = true;

    if (N >= 0) prime[0] = false;
    if (N >= 1) prime[1] = false;

    for (int i = 2; i * i <= N; i++) {
        if (prime[i]) {
            for (int j = i * i; j <= N; j += i)
                prime[j] = false;
        }
    }

    for (int i = 2; i <= N; i++) {
        if (prime[i])
            printf("%d ", i);
    }

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int N;
    cin >> N;

    vector<bool> prime(N + 1, true);

    if (N >= 0) prime[0] = false;
    if (N >= 1) prime[1] = false;

    for (int i = 2; i * i <= N; i++) {
        if (prime[i]) {
            for (int j = i * i; j <= N; j += i)
                prime[j] = false;
        }
    }

    for (int i = 2; i <= N; i++) {
        if (prime[i])
            cout << i << " ";
    }

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        boolean[] prime = new boolean[N + 1];
        Arrays.fill(prime, true);

        if (N >= 0) prime[0] = false;
        if (N >= 1) prime[1] = false;

        for (int i = 2; i * i <= N; i++) {
            if (prime[i]) {
                for (int j = i * i; j <= N; j += i)
                    prime[j] = false;
            }
        }

        for (int i = 2; i <= N; i++) {
            if (prime[i])
                System.out.print(i + " ");
        }
    }
}
```
```Python
N = int(input())

prime = [True] * (N + 1)

if N >= 0:
    prime[0] = False
if N >= 1:
    prime[1] = False

i = 2
while i * i <= N:
    if prime[i]:
        j = i * i
        while j <= N:
            prime[j] = False
            j += i
    i += 1

for i in range(2, N + 1):
    if prime[i]:
        print(i, end=" ")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        bool[] prime = new bool[N + 1];

        for (int i = 0; i <= N; i++)
            prime[i] = true;

        if (N >= 0) prime[0] = false;
        if (N >= 1) prime[1] = false;

        for (int i = 2; i * i <= N; i++)
        {
            if (prime[i])
            {
                for (int j = i * i; j <= N; j += i)
                    prime[j] = false;
            }
        }

        for (int i = 2; i <= N; i++)
        {
            if (prime[i])
                Console.Write(i + " ");
        }
    }
}
```

### Output
For Input:
20

Output:
2 3 5 7 11 13 17 19

# Time Complexity
O(N log log N)

# Space Complexity
O(N)

</approaches>




