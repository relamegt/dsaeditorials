# Binomial Coefficient (nCr) - Solution

## Problem Statement

Given two non-negative integers `N` and `R`, compute the binomial coefficient `nCr`, defined as:

`nCr = N! / (R! × (N - R)!)`

Since the answer can be very large, print the result modulo `10^9 + 7`.

### Input Format

A single line containing two space-separated integers `N` and `R`.

### Output Format

Print a single integer representing `nCr` modulo `10^9 + 7`.

## Explanation

There are two common approaches to compute `nCr`.

- **Using Factorials:** Compute `N!`, `R!`, and `(N-R)!` separately and then apply the formula. This approach is simple but performs unnecessary computations and is not suitable for large values with modulo arithmetic.
- **Using Pascal's Triangle (Recommended):** The binomial coefficient satisfies the relation:

`nCr = (n-1)C(r-1) + (n-1)Cr`

Using dynamic programming, we can compute the required value efficiently while taking modulo after every addition.

For example, when `N = 5` and `R = 2`:

`5C2 = 10`

Output:
10

<approaches>
## Approach 1: Using Factorials

### Algorithm

1. Read the integers `N` and `R`.
2. Compute `N!`.
3. Compute `R!`.
4. Compute `(N-R)!`.
5. Apply the formula:

   `nCr = N! / (R! × (N-R)!)`

1. Print the result.

```C
#include <stdio.h>

int main() {
    long long N, R;
    scanf("%lld %lld", &N, &R);

    long long factN = 1;
    long long factR = 1;
    long long factNR = 1;

    for (long long i = 1; i <= N; i++)
        factN *= i;

    for (long long i = 1; i <= R; i++)
        factR *= i;

    for (long long i = 1; i <= N - R; i++)
        factNR *= i;

    printf("%lld", factN / (factR * factNR));

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long N, R;
    cin >> N >> R;

    long long factN = 1;
    long long factR = 1;
    long long factNR = 1;

    for (long long i = 1; i <= N; i++)
        factN *= i;

    for (long long i = 1; i <= R; i++)
        factR *= i;

    for (long long i = 1; i <= N - R; i++)
        factNR *= i;

    cout << factN / (factR * factNR);

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();
        long R = sc.nextLong();

        long factN = 1;
        long factR = 1;
        long factNR = 1;

        for (long i = 1; i <= N; i++)
            factN *= i;

        for (long i = 1; i <= R; i++)
            factR *= i;

        for (long i = 1; i <= N - R; i++)
            factNR *= i;

        System.out.print(factN / (factR * factNR));
    }
}
```
```Python
N, R = map(int, input().split())

factN = 1
factR = 1
factNR = 1

for i in range(1, N + 1):
    factN *= i

for i in range(1, R + 1):
    factR *= i

for i in range(1, N - R + 1):
    factNR *= i

print(factN // (factR * factNR))
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] input = Console.ReadLine().Split();

        long N = long.Parse(input[0]);
        long R = long.Parse(input[1]);

        long factN = 1;
        long factR = 1;
        long factNR = 1;

        for (long i = 1; i <= N; i++)
            factN *= i;

        for (long i = 1; i <= R; i++)
            factR *= i;

        for (long i = 1; i <= N - R; i++)
            factNR *= i;

        Console.Write(factN / (factR * factNR));
    }
}
```

### Output
For Input:
5 2
Output:
10

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Using Pascal's Triangle (Recommended)

### Algorithm

1. Read the integers `N` and `R`.
2. If `R > N-R`, replace `R` with `N-R` to reduce computations.
3. Create a one-dimensional DP array of size `R + 1`.
4. Initialize `dp[0] = 1`.
5. For each row from `1` to `N`:

- Update the DP array from right to left.
- Use the relation:

     `dp[j] = (dp[j] + dp[j-1]) mod (10^9 + 7)`

1. After completing all rows, `dp[R]` contains `nCr`.
2. Print `dp[R]`.

```C
#include <stdio.h>
#include <stdlib.h>

#define MOD 1000000007

int main() {
    int N, R;
    scanf("%d %d", &N, &R);

    if (R > N - R)
        R = N - R;

    long long *dp = (long long *)calloc(R + 1, sizeof(long long));
    dp[0] = 1;

    for (int i = 1; i <= N; i++) {
        int limit = (i < R) ? i : R;
        for (int j = limit; j > 0; j--) {
            dp[j] = (dp[j] + dp[j - 1]) % MOD;
        }
    }

    printf("%lld", dp[R]);

    free(dp);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

const long long MOD = 1000000007;

int main() {
    int N, R;
    cin >> N >> R;

    if (R > N - R)
        R = N - R;

    vector<long long> dp(R + 1, 0);
    dp[0] = 1;

    for (int i = 1; i <= N; i++) {
        int limit = min(i, R);
        for (int j = limit; j > 0; j--) {
            dp[j] = (dp[j] + dp[j - 1]) % MOD;
        }
    }

    cout << dp[R];

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
        int R = sc.nextInt();

        if (R > N - R)
            R = N - R;

        long[] dp = new long[R + 1];
        dp[0] = 1;

        for (int i = 1; i <= N; i++) {
            int limit = Math.min(i, R);
            for (int j = limit; j > 0; j--) {
                dp[j] = (dp[j] + dp[j - 1]) % MOD;
            }
        }

        System.out.print(dp[R]);
    }
}
```
```Python
MOD = 1000000007

N, R = map(int, input().split())

if R > N - R:
    R = N - R

dp = [0] * (R + 1)
dp[0] = 1

for i in range(1, N + 1):
    limit = min(i, R)
    for j in range(limit, 0, -1):
        dp[j] = (dp[j] + dp[j - 1]) % MOD

print(dp[R])
```
```C#
using System;

class Program
{
    const long MOD = 1000000007;

    static void Main()
    {
        string[] input = Console.ReadLine().Split();

        int N = int.Parse(input[0]);
        int R = int.Parse(input[1]);

        if (R > N - R)
            R = N - R;

        long[] dp = new long[R + 1];
        dp[0] = 1;

        for (int i = 1; i <= N; i++)
        {
            int limit = Math.Min(i, R);

            for (int j = limit; j > 0; j--)
            {
                dp[j] = (dp[j] + dp[j - 1]) % MOD;
            }
        }

        Console.Write(dp[R]);
    }
}
```

### Output
For Input:
5 2
Output:
10

# Time Complexity
O(N × R)

# Space Complexity
O(R)

</approaches>



**Note:** The factorial approach is only suitable for understanding the mathematical formula and small values because factorials overflow quickly and it does not correctly handle modulo division. For the given constraints, a more advanced approach using factorials with modular inverse runs in **O(N)** preprocessing and **O(1)** per query, but among these two approaches, the Pascal's Triangle method is the recommended correct solution.
