# Maximum Sum in the Configuration- Solution

## Problem Statement

Given an array `arr[]` of `N` integers, you can rotate the array any number of times. After each rotation, compute:

`S = Σ (i × arr[i])` where `i` is the 0-indexed position.

Find the maximum possible value of `S` over all rotations.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print a single integer representing the maximum value of `Σ i × arr[i]` over all rotations.

## Explanation

There are two common approaches to solve this problem.

- **Try All Rotations:** Generate every possible rotation, compute `Σ i × arr[i]` for each rotation, and keep the maximum value.
- **Rotation Formula (Recommended):** First compute the array sum and the value for the original array. Then use the recurrence relation to calculate the value for the next rotation in O(1), making the overall solution O(N).

For example, when the array is: `1 2 3 4`
Original value: `0×1 + 1×2 + 2×3 + 3×4 = 20`
The maximum among all rotations is: `20`

Output: 20

<approaches>
## Approach 1: Try All Rotations

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize `maximumValue` to a very small value.
4. Consider every possible right rotation.
5. For each rotation:

- Compute `Σ i × arr[(i - rotation + N) % N]`.
- Update `maximumValue` if the current value is greater.

1. Print `maximumValue`.

```C
#include <stdio.h>
#include <limits.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];

    for (int i = 0; i < N; i++)
        scanf("%lld", &arr[i]);

    long long maximumValue = LLONG_MIN;

    for (int r = 0; r < N; r++)
    {
        long long current = 0;

        for (int i = 0; i < N; i++)
            current += (long long)i * arr[(i - r + N) % N];

        if (current > maximumValue)
            maximumValue = current;
    }

    printf("%lld", maximumValue);

    return 0;
}
```
```cpp
#include <iostream>
#include <climits>
using namespace std;

int main()
{
    int N;
    cin >> N;

    long long arr[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    long long maximumValue = LLONG_MIN;

    for (int r = 0; r < N; r++)
    {
        long long current = 0;

        for (int i = 0; i < N; i++)
            current += 1LL * i * arr[(i - r + N) % N];

        maximumValue = max(maximumValue, current);
    }

    cout << maximumValue;

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        long[] arr = new long[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextLong();

        long maximumValue = Long.MIN_VALUE;

        for (int r = 0; r < N; r++)
        {
            long current = 0;

            for (int i = 0; i < N; i++)
                current += (long)i * arr[(i - r + N) % N];

            maximumValue = Math.max(maximumValue, current);
        }

        System.out.print(maximumValue);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

maximumValue = float("-inf")

for r in range(N):
    current = 0

    for i in range(N):
        current += i * arr[(i - r) % N]

    maximumValue = max(maximumValue, current)

print(maximumValue)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long maximumValue = long.MinValue;

        for (int r = 0; r < N; r++)
        {
            long current = 0;

            for (int i = 0; i < N; i++)
                current += (long)i * arr[(i - r + N) % N];

            maximumValue = Math.Max(maximumValue, current);
        }

        Console.Write(maximumValue);
    }
}
```

### Output
For Input:
4
1 2 3 4

Output:
20

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Rotation Formula (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Compute:

- `arraySum = Σ arr[i]`
- `currentValue = Σ i × arr[i]`

1. Initialize `maximumValue = currentValue`.
2. For every right rotation:

- Compute the next value using:

   `nextValue = currentValue + arraySum - N × lastElement`

   where `lastElement` is the element that moves from the end to the front.

- Update `maximumValue`.
- Set `currentValue = nextValue`.

1. Print `maximumValue`.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];

    long long arraySum = 0;
    long long currentValue = 0;

    for (int i = 0; i < N; i++)
    {
        scanf("%lld", &arr[i]);
        arraySum += arr[i];
        currentValue += (long long)i * arr[i];
    }

    long long maximumValue = currentValue;

    for (int i = N - 1; i >= 1; i--)
    {
        currentValue = currentValue + arraySum - (long long)N * arr[i];

        if (currentValue > maximumValue)
            maximumValue = currentValue;
    }

    printf("%lld", maximumValue);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main()
{
    int N;
    cin >> N;

    long long arr[N];

    long long arraySum = 0;
    long long currentValue = 0;

    for (int i = 0; i < N; i++)
    {
        cin >> arr[i];
        arraySum += arr[i];
        currentValue += 1LL * i * arr[i];
    }

    long long maximumValue = currentValue;

    for (int i = N - 1; i >= 1; i--)
    {
        currentValue = currentValue + arraySum - 1LL * N * arr[i];
        maximumValue = max(maximumValue, currentValue);
    }

    cout << maximumValue;

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        long[] arr = new long[N];

        long arraySum = 0;
        long currentValue = 0;

        for (int i = 0; i < N; i++)
        {
            arr[i] = sc.nextLong();
            arraySum += arr[i];
            currentValue += (long)i * arr[i];
        }

        long maximumValue = currentValue;

        for (int i = N - 1; i >= 1; i--)
        {
            currentValue = currentValue + arraySum - (long)N * arr[i];
            maximumValue = Math.max(maximumValue, currentValue);
        }

        System.out.print(maximumValue);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

arraySum = sum(arr)

currentValue = 0

for i in range(N):
    currentValue += i * arr[i]

maximumValue = currentValue

for i in range(N - 1, 0, -1):
    currentValue = currentValue + arraySum - N * arr[i]
    maximumValue = max(maximumValue, currentValue)

print(maximumValue)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long arraySum = 0;
        long currentValue = 0;

        for (int i = 0; i < N; i++)
        {
            arraySum += arr[i];
            currentValue += (long)i * arr[i];
        }

        long maximumValue = currentValue;

        for (int i = N - 1; i >= 1; i--)
        {
            currentValue = currentValue + arraySum - (long)N * arr[i];
            maximumValue = Math.Max(maximumValue, currentValue);
        }

        Console.Write(maximumValue);
    }
}
```

### Output
For Input:
4
1 2 3 4

Output:
20

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




