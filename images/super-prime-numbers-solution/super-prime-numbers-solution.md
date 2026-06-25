# Super Prime Numbers - Solution

## Problem Statement

A **Super Prime** is a prime number whose position in the sequence of all prime numbers is also a prime number.

For example:

- Primes in order: `2 (position 1), 3 (position 2), 5 (position 3), 7 (position 4), 11 (position 5), 13 (position 6), 17 (position 7), ...`

The primes at prime positions are:

- Position `2` → `3`
- Position `3` → `5`
- Position `5` → `11`
- Position `7` → `17`

These are called **Super Primes**.

Given a positive integer `N`, print all super primes less than or equal to `N` in ascending order.

### Input Format

A single integer `N`.

### Output Format

Print all super primes less than or equal to `N` separated by spaces. If none exist, print nothing.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Traverse every number from `2` to `N`. Check whether it is prime. If it is prime, count its position among all prime numbers found so far. Again check whether that position is prime. If both conditions are satisfied, print the number.
- **Using Sieve of Eratosthenes (Recommended):** Generate all prime numbers using the sieve. While traversing the primes, keep track of their positions. Since the sieve also tells whether a position is prime, identifying super primes becomes very efficient.

For example, when `N = 20`:

Prime numbers are:
`2 3 5 7 11 13 17 19`

Their positions are:
`1 2 3 4 5 6 7 8`

Prime positions are:
`2 3 5 7`

Hence the super primes are:
`3 5 11 17`

Output:
3 5 11 17

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the integer `N`.
2. Initialize `position = 0`.
3. Traverse every number from `2` to `N`.
4. Check whether the current number is prime.
5. If it is prime:

- Increment its position.
- Check whether the position is also prime.
- If yes, print the current number.

1. Continue until all numbers are processed.

```C
#include <stdio.h>

int isPrime(int n) {
    if (n < 2)
        return 0;

    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0)
            return 0;
    }

    return 1;
}

int main() {
    int N;
    scanf("%d", &N);

    int position = 0;

    for (int i = 2; i <= N; i++) {
        if (isPrime(i)) {
            position++;

            if (isPrime(position))
                printf("%d ", i);
        }
    }

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

bool isPrime(int n) {
    if (n < 2)
        return false;

    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0)
            return false;
    }

    return true;
}

int main() {
    int N;
    cin >> N;

    int position = 0;

    for (int i = 2; i <= N; i++) {
        if (isPrime(i)) {
            position++;

            if (isPrime(position))
                cout << i << " ";
        }
    }

    return 0;
}
```
```Java
import java.util.*;

public class Main {

    static boolean isPrime(int n) {
        if (n < 2)
            return false;

        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0)
                return false;
        }

        return true;
    }

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        int position = 0;

        for (int i = 2; i <= N; i++) {

            if (isPrime(i)) {

                position++;

                if (isPrime(position))
                    System.out.print(i + " ");
            }
        }
    }
}
```
```Python
def isPrime(n):
    if n < 2:
        return False

    i = 2

    while i * i <= n:
        if n % i == 0:
            return False
        i += 1

    return True


N = int(input())

position = 0

for i in range(2, N + 1):
    if isPrime(i):
        position += 1

        if isPrime(position):
            print(i, end=" ")
```
```C#
using System;

class Program
{
    static bool IsPrime(int n)
    {
        if (n < 2)
            return false;

        for (int i = 2; i * i <= n; i++)
        {
            if (n % i == 0)
                return false;
        }

        return true;
    }

    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int position = 0;

        for (int i = 2; i <= N; i++)
        {
            if (IsPrime(i))
            {
                position++;

                if (IsPrime(position))
                    Console.Write(i + " ");
            }
        }
    }
}
```

### Output
For Input:
20

Output:
3 5 11 17

# Time Complexity
O(N√N)

# Space Complexity
O(1)

## Approach 2: Using Sieve of Eratosthenes and Prime Position Check (Recommended)

### Algorithm

1. Read the integer `N`.
2. Create a boolean array `isPrime` of size `N + 1` and initially mark every number as prime.
3. Apply the **Sieve of Eratosthenes** to find all prime numbers up to `N`.
4. Initialize `position = 0`.
5. Traverse all numbers from `2` to `N`.
6. Whenever a prime number is found:

- Increment its position in the sequence of prime numbers.
- Check whether this position is also prime using the `isPrime` array.
- If the position is prime, print the current prime number.

1. Continue until all numbers are processed.

```C
#include <stdio.h>
#include <stdbool.h>

int main() {
    int N;
    scanf("%d", &N);

    bool isPrime[N + 1];

    for (int i = 0; i <= N; i++)
        isPrime[i] = true;

    if (N >= 0) isPrime[0] = false;
    if (N >= 1) isPrime[1] = false;

    for (int i = 2; i * i <= N; i++) {
        if (isPrime[i]) {
            for (int j = i * i; j <= N; j += i)
                isPrime[j] = false;
        }
    }

    int position = 0;

    for (int i = 2; i <= N; i++) {
        if (isPrime[i]) {
            position++;

            if (isPrime[position])
                printf("%d ", i);
        }
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

    vector<bool> isPrime(N + 1, true);

    if (N >= 0) isPrime[0] = false;
    if (N >= 1) isPrime[1] = false;

    for (int i = 2; i * i <= N; i++) {
        if (isPrime[i]) {
            for (int j = i * i; j <= N; j += i)
                isPrime[j] = false;
        }
    }

    int position = 0;

    for (int i = 2; i <= N; i++) {
        if (isPrime[i]) {
            position++;

            if (isPrime[position])
                cout << i << " ";
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

        int N = sc.nextInt();

        boolean[] isPrime = new boolean[N + 1];
        Arrays.fill(isPrime, true);

        if (N >= 0) isPrime[0] = false;
        if (N >= 1) isPrime[1] = false;

        for (int i = 2; i * i <= N; i++) {
            if (isPrime[i]) {
                for (int j = i * i; j <= N; j += i)
                    isPrime[j] = false;
            }
        }

        int position = 0;

        for (int i = 2; i <= N; i++) {
            if (isPrime[i]) {
                position++;

                if (isPrime[position])
                    System.out.print(i + " ");
            }
        }
    }
}
```
```Python
N = int(input())

isPrime = [True] * (N + 1)

if N >= 0:
    isPrime[0] = False
if N >= 1:
    isPrime[1] = False

i = 2
while i * i <= N:
    if isPrime[i]:
        j = i * i
        while j <= N:
            isPrime[j] = False
            j += i
    i += 1

position = 0

for i in range(2, N + 1):
    if isPrime[i]:
        position += 1

        if isPrime[position]:
            print(i, end=" ")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        bool[] isPrime = new bool[N + 1];

        for (int i = 0; i <= N; i++)
            isPrime[i] = true;

        if (N >= 0) isPrime[0] = false;
        if (N >= 1) isPrime[1] = false;

        for (int i = 2; i * i <= N; i++)
        {
            if (isPrime[i])
            {
                for (int j = i * i; j <= N; j += i)
                    isPrime[j] = false;
            }
        }

        int position = 0;

        for (int i = 2; i <= N; i++)
        {
            if (isPrime[i])
            {
                position++;

                if (isPrime[position])
                    Console.Write(i + " ");
            }
        }
    }
}
```

### Output
For Input:
20

Output:
3 5 11

# Time Complexity
Building the sieve: O(N log log N)
Traversing all numbers: O(N)
Overall: O(N log log N)

# Space Complexity
O(N)

</approaches>



> **Note:** For this problem, the optimal approach is to generate all primes using the **Sieve of Eratosthenes** and then use the same sieve to determine whether the **position** of each prime is also prime. This avoids repeatedly checking primality and efficiently solves the problem within the given constraints.
