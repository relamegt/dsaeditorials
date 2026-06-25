# Perfect Number - Solution

## Problem Statement

Given a positive integer `N`, determine whether it is a perfect number.

A perfect number is a positive integer that is equal to the sum of all its proper divisors (divisors excluding itself).

For example:

`6 = 1 + 2 + 3`

### Input Format

A single integer `N`.

### Output Format

Print `Yes` if `N` is a perfect number, otherwise print `No`.

## Explanation

There are two common approaches to determine whether a number is perfect.

- **Brute Force:** Find all proper divisors by checking every number from `1` to `N - 1` and add the divisors.
- **Optimized Approach (Recommended):** Divisors always occur in pairs. Instead of checking every number, check only up to `√N`. Whenever a divisor is found, add both the divisor and its corresponding pair.

For example, when `N = 6`:

- Proper divisors are `1`, `2`, and `3`.
- Their sum is `1 + 2 + 3 = 6`.

Since the sum of proper divisors equals the number itself, the answer is:

Output:
Yes

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the integer `N`.
2. If `N` is `1`, print `No` because `1` has no proper divisors.
3. Initialize `sum = 0`.
4. Check every integer from `1` to `N - 1`.
5. If the current number divides `N` exactly, add it to `sum`.
6. After checking all numbers, compare `sum` with `N`.
7. If both are equal, print `Yes`; otherwise, print `No`.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    if (N == 1) {
        printf("No");
        return 0;
    }

    int sum = 0;

    for (int i = 1; i < N; i++) {
        if (N % i == 0)
            sum += i;
    }

    if (sum == N)
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
    int N;
    cin >> N;

    if (N == 1) {
        cout << "No";
        return 0;
    }

    int sum = 0;

    for (int i = 1; i < N; i++) {
        if (N % i == 0)
            sum += i;
    }

    if (sum == N)
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

        int N = sc.nextInt();

        if (N == 1) {
            System.out.print("No");
            return;
        }

        int sum = 0;

        for (int i = 1; i < N; i++) {
            if (N % i == 0)
                sum += i;
        }

        System.out.print(sum == N ? "Yes" : "No");
    }
}
```
```Python
N = int(input())

if N == 1:
    print("No")
else:
    sum = 0

    for i in range(1, N):
        if N % i == 0:
            sum += i

    if sum == N:
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
        int N = int.Parse(Console.ReadLine());

        if (N == 1)
        {
            Console.Write("No");
            return;
        }

        int sum = 0;

        for (int i = 1; i < N; i++)
        {
            if (N % i == 0)
                sum += i;
        }

        if (sum == N)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}
```

### Output
For Input:
6
Output:
Yes

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Using Divisor Pairs (Recommended)

### Algorithm

1. Read the integer `N`.
2. If `N` is `1`, print `No`.
3. Initialize `sum = 1` because `1` is a proper divisor of every number greater than `1`.
4. Check every integer `i` from `2` while `i × i <= N`.
5. If `i` divides `N` exactly:

- Add `i` to `sum`.
- Find the paired divisor `N / i`.
- If the paired divisor is different from `i`, add it to `sum`.

1. After checking all possible divisors, compare `sum` with `N`.
2. If they are equal, print `Yes`; otherwise, print `No`.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    if (N == 1) {
        printf("No");
        return 0;
    }

    int sum = 1;

    for (int i = 2; i * i <= N; i++) {
        if (N % i == 0) {
            sum += i;

            if (i != N / i)
                sum += N / i;
        }
    }

    if (sum == N)
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
    int N;
    cin >> N;

    if (N == 1) {
        cout << "No";
        return 0;
    }

    int sum = 1;

    for (int i = 2; i * i <= N; i++) {
        if (N % i == 0) {
            sum += i;

            if (i != N / i)
                sum += N / i;
        }
    }

    if (sum == N)
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

        int N = sc.nextInt();

        if (N == 1) {
            System.out.print("No");
            return;
        }

        int sum = 1;

        for (int i = 2; i * i <= N; i++) {
            if (N % i == 0) {
                sum += i;

                if (i != N / i)
                    sum += N / i;
            }
        }

        System.out.print(sum == N ? "Yes" : "No");
    }
}
```
```Python
N = int(input())

if N == 1:
    print("No")
else:
    sum = 1

    i = 2
    while i * i <= N:
        if N % i == 0:
            sum += i

            if i != N // i:
                sum += N // i

        i += 1

    if sum == N:
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
        int N = int.Parse(Console.ReadLine());

        if (N == 1)
        {
            Console.Write("No");
            return;
        }

        int sum = 1;

        for (int i = 2; i * i <= N; i++)
        {
            if (N % i == 0)
            {
                sum += i;

                if (i != N / i)
                    sum += N / i;
            }
        }

        if (sum == N)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}
```

### Output
For Input:
6
Output:
Yes

# Time Complexity
O(√N)

# Space Complexity
O(1)

</approaches>

