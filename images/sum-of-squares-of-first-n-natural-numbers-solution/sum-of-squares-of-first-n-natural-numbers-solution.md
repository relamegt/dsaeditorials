# Sum of Squares of First N Natural Numbers - Solution

## Problem Statement

Given an integer `N`, find the sum of squares of the first `N` natural numbers.

In other words, compute:

`1² + 2² + 3² + ... + N²`

Print the resulting sum as a single integer.

### Input Format

A single integer `N`.

### Output Format

Print a single integer representing the sum of squares of the first `N` natural numbers.

## Explanation

The sum of squares of the first `N` natural numbers can be found in two ways:

- **Using a Loop:** Calculate the square of each number from `1` to `N` and add them together.
- **Using the Mathematical Formula:** Directly compute the sum using `N × (N + 1) × (2 × N + 1) / 6`, which is much more efficient for large values of `N`.

For example, when `N = 3`:

Output:
14

<approaches>
## Approach 1: Using a Loop

### Algorithm

1. Read the integer `N`.
2. Initialize `sum = 0`.
3. Iterate from `1` to `N`.
4. Add `i × i` to `sum`.
5. Print `sum`.

```C
#include <stdio.h>

int main() {
    long long N, sum = 0;
    scanf("%lld", &N);

    for (long long i = 1; i <= N; i++) {
        sum += i * i;
    }

    printf("%lld", sum);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long N, sum = 0;
    cin >> N;

    for (long long i = 1; i <= N; i++) {
        sum += i * i;
    }

    cout << sum;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();
        long sum = 0;

        for (long i = 1; i <= N; i++) {
            sum += i * i;
        }

        System.out.print(sum);
    }
}
```
```Python
N = int(input())

sum = 0

for i in range(1, N + 1):
    sum += i * i

print(sum)
```
```C#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());
        long sum = 0;

        for (long i = 1; i <= N; i++)
        {
            sum += i * i;
        }

        Console.Write(sum);
    }
}
```

### Output
For Input:
3
Output:
14

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Using Mathematical Formula (Recommended)

### Algorithm

1. Read the integer `N`.
2. Calculate `sum = N × (N + 1) × (2 × N + 1) / 6`.
3. Print `sum`.

```C
#include <stdio.h>

int main() {
    long long N;
    scanf("%lld", &N);

    long long sum = N * (N + 1) * (2 * N + 1) / 6;

    printf("%lld", sum);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long N;
    cin >> N;

    long long sum = N * (N + 1) * (2 * N + 1) / 6;

    cout << sum;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();

        long sum = N * (N + 1) * (2 * N + 1) / 6;

        System.out.print(sum);
    }
}
```
```Python
N = int(input())

sum = N * (N + 1) * (2 * N + 1) // 6

print(sum)
```
```C#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());

        long sum = N * (N + 1) * (2 * N + 1) / 6;

        Console.Write(sum);
    }
}
```

### Output
For Input:
3
Output:
14

# Time Complexity
O(1)

# Space Complexity
O(1)

</approaches>

