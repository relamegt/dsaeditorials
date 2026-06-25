# Check for Power of  2 - Solution

## Problem Statement

Given a positive integer `N`, determine whether it is a power of `2`.

A number is a power of `2` if it can be expressed as `2^k` for some non-negative integer `k` (i.e., `1, 2, 4, 8, 16, ...`).

### Input Format

A single integer `N`.

### Output Format

Print `Yes` if `N` is a power of `2`, otherwise print `No`.

## Explanation

There are two common ways to determine whether a number is a power of `2`.

- **Repeated Division:** Continuously divide the number by `2`. If it eventually becomes `1` without ever producing a remainder, then it is a power of `2`.
- **Bit Manipulation (Recommended):** A power of `2` has exactly one bit set in its binary representation. Therefore, for any positive power of `2`, the expression `N & (N - 1)` evaluates to `0`.

For example, when `N = 16`:

- `16 → 8 → 4 → 2 → 1`

Since the number becomes `1` after repeatedly dividing by `2`, it is a power of `2`.

Output:
Yes

<approaches>
## Approach 1: Using Repeated Division

### Algorithm

1. Read the integer `N`.
2. Repeat while `N` is greater than `1`:

- If `N` is not divisible by `2`, print `No` and stop.
- Otherwise, divide `N` by `2`.

1. If `N` becomes `1`, print `Yes`.

```C
#include <stdio.h>

int main() {
    long long N;
    scanf("%lld", &N);

    while (N > 1) {
        if (N % 2 != 0) {
            printf("No");
            return 0;
        }
        N /= 2;
    }

    printf("Yes");

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long N;
    cin >> N;

    while (N > 1) {
        if (N % 2 != 0) {
            cout << "No";
            return 0;
        }
        N /= 2;
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

        long N = sc.nextLong();

        while (N > 1) {
            if (N % 2 != 0) {
                System.out.print("No");
                return;
            }
            N /= 2;
        }

        System.out.print("Yes");
    }
}
```
```Python
N = int(input())

while N > 1:
    if N % 2 != 0:
        print("No")
        break
    N //= 2
else:
    print("Yes")
```
```C#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());

        while (N > 1)
        {
            if (N % 2 != 0)
            {
                Console.Write("No");
                return;
            }

            N /= 2;
        }

        Console.Write("Yes");
    }
}
```

### Output
For Input:
16
Output:
Yes

# Time Complexity
O(log₂N)

# Space Complexity
O(1)

## Approach 2: Using Bit Manipulation (Recommended)

### Algorithm

1. Read the integer `N`.
2. A power of `2` has exactly one set bit in its binary representation.
3. Compute `N & (N - 1)`.
4. If the result is `0`, print `Yes`; otherwise, print `No`.

```C
#include <stdio.h>

int main() {
    long long N;
    scanf("%lld", &N);

    if ((N & (N - 1)) == 0)
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
    long long N;
    cin >> N;

    if ((N & (N - 1)) == 0)
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

        long N = sc.nextLong();

        if ((N & (N - 1)) == 0)
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```
```Python
N = int(input())

if (N & (N - 1)) == 0:
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
        long N = long.Parse(Console.ReadLine());

        if ((N & (N - 1)) == 0)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}
```

### Output
For Input:
16
Output:
Yes

# Time Complexity
O(1)

# Space Complexity
O(1)

</approaches>

