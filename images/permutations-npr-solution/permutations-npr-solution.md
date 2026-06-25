# Permutations (nPr) - Solution

## Problem Statement

Given two non-negative integers `N` and `R`, compute the number of permutations `nPr`, defined as:

`nPr = N! / (N - R)!`

Since the answer can be very large, print the result modulo `10^9 + 7`.

### Input Format

A single line containing two space-separated integers `N` and `R`.

### Output Format

Print a single integer representing `nPr` modulo `10^9 + 7`.

## Explanation

There are two common approaches to compute `nPr`.

- **Using Factorials:** Compute `N!` and `(N-R)!` separately and then divide them. This method is simple but performs unnecessary computations.
- **Direct Multiplication (Recommended):** Observe that

`N! / (N-R)! = N × (N-1) × (N-2) × ... × (N-R+1)`

Instead of computing complete factorials, multiply only the required `R` terms while taking modulo at every step.

For example, when `N = 5` and `R = 2`:

`5P2 = 5 × 4 = 20`

Output:
20

<approaches>
## Approach 1: Using Factorials

### Algorithm

1. Read the integers `N` and `R`.
2. Initialize `factN = 1` and `factNR = 1`.
3. Compute `N!` by multiplying all numbers from `1` to `N`, taking modulo `10^9 + 7` after each multiplication.
4. Compute `(N-R)!` by multiplying all numbers from `1` to `N-R`, taking modulo `10^9 + 7`.
5. Since `(N-R)!` divides `N!` exactly, compute the answer as `factN / factNR`.
6. Print the result.

```C
#include <stdio.h>

int main() {
    long long N, R;
    scanf("%lld %lld", &N, &R);

    long long factN = 1;
    long long factNR = 1;

    for (long long i = 1; i <= N; i++)
        factN *= i;

    for (long long i = 1; i <= N - R; i++)
        factNR *= i;

    printf("%lld", factN / factNR);

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
    long long factNR = 1;

    for (long long i = 1; i <= N; i++)
        factN *= i;

    for (long long i = 1; i <= N - R; i++)
        factNR *= i;

    cout << factN / factNR;

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
        long factNR = 1;

        for (long i = 1; i <= N; i++)
            factN *= i;

        for (long i = 1; i <= N - R; i++)
            factNR *= i;

        System.out.print(factN / factNR);
    }
}
```
```Python
N, R = map(int, input().split())

factN = 1
factNR = 1

for i in range(1, N + 1):
    factN *= i

for i in range(1, N - R + 1):
    factNR *= i

print(factN // factNR)
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
        long factNR = 1;

        for (long i = 1; i <= N; i++)
            factN *= i;

        for (long i = 1; i <= N - R; i++)
            factNR *= i;

        Console.Write(factN / factNR);
    }
}
```

### Output
For Input:
5 2
Output:
20

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Direct Multiplication (Recommended)

### Algorithm

1. Read the integers `N` and `R`.
2. Initialize `answer = 1`.
3. The permutation formula can be written as:

   `N × (N-1) × (N-2) × ... × (N-R+1)`

1. Repeat `R` times:

- Multiply `answer` by the current term.
- Take modulo `10^9 + 7` after every multiplication.

1. Print the final answer.

```C
#include <stdio.h>

#define MOD 1000000007LL

int main() {
    long long N, R;
    scanf("%lld %lld", &N, &R);

    long long ans = 1;

    for (long long i = 0; i < R; i++) {
        ans = (ans * (N - i)) % MOD;
    }

    printf("%lld", ans);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

const long long MOD = 1000000007;

int main() {
    long long N, R;
    cin >> N >> R;

    long long ans = 1;

    for (long long i = 0; i < R; i++) {
        ans = (ans * (N - i)) % MOD;
    }

    cout << ans;

    return 0;
}
```
```Java
import java.util.*;

public class Main {

    static final long MOD = 1000000007;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();
        long R = sc.nextLong();

        long ans = 1;

        for (long i = 0; i < R; i++) {
            ans = (ans * (N - i)) % MOD;
        }

        System.out.print(ans);
    }
}
```
```Python
MOD = 1000000007

N, R = map(int, input().split())

ans = 1

for i in range(R):
    ans = (ans * (N - i)) % MOD

print(ans)
```
```C#
using System;

class Program
{
    const long MOD = 1000000007;

    static void Main()
    {
        string[] input = Console.ReadLine().Split();

        long N = long.Parse(input[0]);
        long R = long.Parse(input[1]);

        long ans = 1;

        for (long i = 0; i < R; i++)
        {
            ans = (ans * (N - i)) % MOD;
        }

        Console.Write(ans);
    }
}
```

### Output
For Input:
5 2
Output:
20

# Time Complexity
O(R)

# Space Complexity
O(1)

</approaches>



**Note:** The first approach is suitable only for understanding the mathematical formula and for very small values of `N`. It will overflow for the given constraints. The second approach is the correct and efficient solution for this problem.
