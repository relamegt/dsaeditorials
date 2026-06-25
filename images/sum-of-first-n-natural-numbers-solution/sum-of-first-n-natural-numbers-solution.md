# Sum of First N Natural Numbers - Solution

## Problem Statement

Given an integer `N`, find the sum of the first `N` natural numbers.

The first `N` natural numbers are `1, 2, 3, ..., N`.

Print the resulting sum as a single integer.

### Input Format

A single integer `N`.

### Output Format

Print a single integer representing the sum of the first `N` natural numbers.

## Explanation

The sum of the first `N` natural numbers can be found in two ways:

- **Using a Loop:** Add all numbers from `1` to `N` one by one.
- **Using the Mathematical Formula:** Directly compute the sum using `N × (N + 1) / 2`, which is more efficient for large values of `N`.

For example, when `N = 5`:

Output:
15

<approaches>
## Approach 1: Using a Loop

### Algorithm

1. Read the integer `N`.
2. Initialize `sum = 0`.
3. Iterate from `1` to `N`.
4. Add the current number to `sum`.
5. Print `sum`.

```C
#include <stdio.h>

int main() {
    long long N, sum = 0;
    scanf("%lld", &N);

    for (long long i = 1; i <= N; i++) {
        sum += i;
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
        sum += i;
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
            sum += i;
        }

        System.out.print(sum);
    }
}
```
```Python
N = int(input())

sum = 0

for i in range(1, N + 1):
    sum += i

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
            sum += i;
        }

        Console.Write(sum);
    }
}
```

### Output
For Input:
5
Output:
15

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Using Mathematical Formula (Recommended)

### Algorithm

1. Read the integer `N`.
2. Calculate `sum = N × (N + 1) / 2`.
3. Print `sum`.

```C
#include <stdio.h>

int main() {
    long long N;
    scanf("%lld", &N);

    long long sum = N * (N + 1) / 2;

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

    long long sum = N * (N + 1) / 2;

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

        long sum = N * (N + 1) / 2;

        System.out.print(sum);
    }
}
```
```Python
N = int(input())

sum = N * (N + 1) // 2

print(sum)
```
```C#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());

        long sum = N * (N + 1) / 2;

        Console.Write(sum);
    }
}
```

### Output
For Input:
5
Output:
15

# Time Complexity
O(1)

# Space Complexity
O(1)

</approaches>

