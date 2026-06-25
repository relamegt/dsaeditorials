# Prime Number - Solution

## Problem Statement

Given an integer `N`, determine whether it is a prime number.

A prime number is a natural number greater than `1` that has no positive divisors other than `1` and itself.

### Input Format

A single integer `N`.

### Output Format

Print `Yes` if `N` is prime, otherwise print `No`.

## Explanation

There are two common approaches to determine whether a number is prime:

- **Check all numbers from 2 to N - 1:** If any number divides `N` exactly, then `N` is not prime.
- **Check only up to √N (Recommended):** If `N` has a divisor greater than its square root, then it must also have a corresponding divisor smaller than the square root. Therefore, checking up to √N is sufficient and much more efficient.

For example, when `N = 7`:

- 7 is not divisible by 2.
- 7 is not divisible by any number up to √7.

Hence, the answer is: `Yes`

<approaches>
## Approach 1: Check Divisibility from 2 to N - 1

### Algorithm

1. Read the integer `N`.
2. If `N` is less than or equal to `1`, print `No`.
3. Check every integer from `2` to `N - 1`.
4. If any number divides `N` exactly (`N % i == 0`), then `N` is not prime. Print `No` and stop.
5. If no divisor is found after checking all numbers, print `Yes`.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    if (N <= 1) {
        printf("No");
        return 0;
    }

    for (int i = 2; i < N; i++) {
        if (N % i == 0) {
            printf("No");
            return 0;
        }
    }

    printf("Yes");

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    int N;
    cin >> N;

    if (N <= 1) {
        cout << "No";
        return 0;
    }

    for (int i = 2; i < N; i++) {
        if (N % i == 0) {
            cout << "No";
            return 0;
        }
    }

    cout << "Yes";

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        if (N <= 1) {
            System.out.print("No");
            return;
        }

        for (int i = 2; i < N; i++) {
            if (N % i == 0) {
                System.out.print("No");
                return;
            }
        }

        System.out.print("Yes");
    }
}
```
```Python
N = int(input())

if N <= 1:
    print("No")
else:
    for i in range(2, N):
        if N % i == 0:
            print("No")
            break
    else:
        print("Yes")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        if (N <= 1)
        {
            Console.Write("No");
            return;
        }

        for (int i = 2; i < N; i++)
        {
            if (N % i == 0)
            {
                Console.Write("No");
                return;
            }
        }

        Console.Write("Yes");
    }
}
```

### Output
For Input:
7
Output:
Yes

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Check Divisibility up to √N (Recommended)

### Algorithm

1. Read the integer `N`.
2. If `N` is less than or equal to `1`, print `No`.
3. Check every integer from `2` while `i × i <= N`.
4. If any number divides `N` exactly (`N % i == 0`), then `N` is not prime. Print `No` and stop.
5. If no divisor is found up to the square root of `N`, print `Yes`.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    if (N <= 1) {
        printf("No");
        return 0;
    }

    for (int i = 2; i * i <= N; i++) {
        if (N % i == 0) {
            printf("No");
            return 0;
        }
    }

    printf("Yes");

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    int N;
    cin >> N;

    if (N <= 1) {
        cout << "No";
        return 0;
    }

    for (int i = 2; i * i <= N; i++) {
        if (N % i == 0) {
            cout << "No";
            return 0;
        }
    }

    cout << "Yes";

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        if (N <= 1) {
            System.out.print("No");
            return;
        }

        for (int i = 2; i * i <= N; i++) {
            if (N % i == 0) {
                System.out.print("No");
                return;
            }
        }

        System.out.print("Yes");
    }
}
```
```Python
N = int(input())

if N <= 1:
    print("No")
else:
    for i in range(2, int(N ** 0.5) + 1):
        if N % i == 0:
            print("No")
            break
    else:
        print("Yes")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        if (N <= 1)
        {
            Console.Write("No");
            return;
        }

        for (int i = 2; i * i <= N; i++)
        {
            if (N % i == 0)
            {
                Console.Write("No");
                return;
            }
        }

        Console.Write("Yes");
    }
}
```

### Output
For Input:
7
Output:
Yes

# Time Complexity
O(√N)

# Space Complexity
O(1)

</approaches>

