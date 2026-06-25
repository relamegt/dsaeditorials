# LCM of Two Numbers- Solution

## Problem Statement

Given two positive integers `A` and `B`, find their Least Common Multiple (LCM).

The LCM of two integers is the smallest positive integer that is divisible by both `A` and `B`.

### Input Format

A single line containing two space-separated integers `A` and `B`.

### Output Format

Print a single integer representing the LCM of `A` and `B`.

## Explanation

There are two common approaches to find the LCM of two numbers.

- **Brute Force:** Start from the larger of the two numbers and keep checking the next multiples until a number divisible by both `A` and `B` is found.
- **Using GCD (Recommended):** First find the Greatest Common Divisor (GCD) using the Euclidean Algorithm. Then use the relation:

`LCM = (A × B) / GCD`

This approach is much faster for large numbers.

For example, when `A = 4` and `B = 6`:

- `GCD(4, 6) = 2`
- `LCM = (4 × 6) / 2 = 12`

Output:
12

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the integers `A` and `B`.
2. Find the larger of the two numbers and store it in `lcm`.
3. Repeat the following steps:

- Check whether `lcm` is divisible by both `A` and `B`.
- If it is divisible by both, print `lcm` and stop.
- Otherwise, increase `lcm` by `1` and continue checking.

```C
#include <stdio.h>

int main() {
    long long A, B;
    scanf("%lld %lld", &A, &B);

    long long lcm = (A > B) ? A : B;

    while (1) {
        if (lcm % A == 0 && lcm % B == 0) {
            printf("%lld", lcm);
            break;
        }
        lcm++;
    }

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long A, B;
    cin >> A >> B;

    long long lcm = max(A, B);

    while (true) {
        if (lcm % A == 0 && lcm % B == 0) {
            cout << lcm;
            break;
        }
        lcm++;
    }

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

        long lcm = Math.max(A, B);

        while (true) {
            if (lcm % A == 0 && lcm % B == 0) {
                System.out.print(lcm);
                break;
            }
            lcm++;
        }
    }
}
```
```Python
A, B = map(int, input().split())

lcm = max(A, B)

while True:
    if lcm % A == 0 and lcm % B == 0:
        print(lcm)
        break
    lcm += 1
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

        long lcm = Math.Max(A, B);

        while (true)
        {
            if (lcm % A == 0 && lcm % B == 0)
            {
                Console.Write(lcm);
                break;
            }

            lcm++;
        }
    }
}
```

### Output
For Input:
4 6
Output:
12

# Time Complexity
O(A × B) (Worst Case)

# Space Complexity
O(1)

## Approach 2: Using GCD (Recommended)

### Algorithm

1. Read the integers `A` and `B`.
2. Store the original values of `A` and `B`.
3. Find the GCD using the Euclidean Algorithm:

- Repeat while `B` is not `0`:
- Find the remainder using `A % B`.
- Assign `B` to `A`.
- Assign the remainder to `B`.

1. After the loop, `A` contains the GCD.
2. Compute the LCM using the formula `(originalA × originalB) / GCD`.
3. Print the LCM.

```C
#include <stdio.h>

int main() {
    long long A, B;
    scanf("%lld %lld", &A, &B);

    long long x = A, y = B;

    while (y != 0) {
        long long temp = x % y;
        x = y;
        y = temp;
    }

    long long lcm = (A / x) * B;

    printf("%lld", lcm);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long A, B;
    cin >> A >> B;

    long long x = A, y = B;

    while (y != 0) {
        long long temp = x % y;
        x = y;
        y = temp;
    }

    long long lcm = (A / x) * B;

    cout << lcm;

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

        long x = A;
        long y = B;

        while (y != 0) {
            long temp = x % y;
            x = y;
            y = temp;
        }

        long lcm = (A / x) * B;

        System.out.print(lcm);
    }
}
```
```Python
A, B = map(int, input().split())

x = A
y = B

while y != 0:
    temp = x % y
    x = y
    y = temp

lcm = (A // x) * B

print(lcm)
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

        long x = A;
        long y = B;

        while (y != 0)
        {
            long temp = x % y;
            x = y;
            y = temp;
        }

        long lcm = (A / x) * B;

        Console.Write(lcm);
    }
}
```

### Output
For Input:
4 6
Output:
12

# Time Complexity
O(log(min(A, B)))

# Space Complexity
O(1)

</approaches>

