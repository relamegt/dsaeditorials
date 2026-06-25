# Smallest Sum Contiguous Subarray - Solution

## Problem Statement

Given an integer array `arr[]` of size `N`, find the minimum (smallest) sum of any contiguous subarray.

A subarray must contain at least one element.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print a single integer representing the minimum subarray sum.

## Explanation

There are two common approaches to solve this problem.

- **Generate All Subarrays:** Generate every possible contiguous subarray, compute its sum, and keep track of the minimum sum.
- **Modified Kadane's Algorithm (Recommended):** Traverse the array once while maintaining the minimum sum ending at the current position. If extending the current subarray gives a larger sum than starting fresh from the current element, begin a new subarray.

For example, when the array is: `3 -4 2 -3 -1`
The minimum sum subarray is: `-4 2 -3 -1`

Its sum is: `-6`

Output: -6

<approaches>
## Approach 1: Generate All Subarrays

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize `minimumSum` as the first element.
4. Traverse every possible starting index.
5. For each starting index:

- Initialize `currentSum = 0`.
- Extend the subarray one element at a time.
- Add the current element to `currentSum`.
- Update `minimumSum` if `currentSum` is smaller.

1. Print `minimumSum`.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];

    for (int i = 0; i < N; i++)
        scanf("%lld", &arr[i]);

    long long minimumSum = arr[0];

    for (int i = 0; i < N; i++)
    {
        long long currentSum = 0;

        for (int j = i; j < N; j++)
        {
            currentSum += arr[j];

            if (currentSum < minimumSum)
                minimumSum = currentSum;
        }
    }

    printf("%lld", minimumSum);

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

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    long long minimumSum = arr[0];

    for (int i = 0; i < N; i++)
    {
        long long currentSum = 0;

        for (int j = i; j < N; j++)
        {
            currentSum += arr[j];

            minimumSum = min(minimumSum, currentSum);
        }
    }

    cout << minimumSum;

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

        long minimumSum = arr[0];

        for (int i = 0; i < N; i++)
        {
            long currentSum = 0;

            for (int j = i; j < N; j++)
            {
                currentSum += arr[j];

                minimumSum = Math.min(minimumSum, currentSum);
            }
        }

        System.out.print(minimumSum);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

minimumSum = arr[0]

for i in range(N):
    currentSum = 0

    for j in range(i, N):
        currentSum += arr[j]
        minimumSum = min(minimumSum, currentSum)

print(minimumSum)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long minimumSum = arr[0];

        for (int i = 0; i < N; i++)
        {
            long currentSum = 0;

            for (int j = i; j < N; j++)
            {
                currentSum += arr[j];
                minimumSum = Math.Min(minimumSum, currentSum);
            }
        }

        Console.Write(minimumSum);
    }
}
```

### Output
For Input:
5
3 -4 2 -3 -1

Output:
-6

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Modified Kadane's Algorithm (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize:

- `currentSum` as the first element.
- `minimumSum` as the first element.

1. Traverse the array from the second element onwards.
2. For every element:

- Decide whether to:
- Extend the previous subarray by adding the current element, or
- Start a new subarray from the current element.
- Update `currentSum` as the minimum of these two choices.
- Update `minimumSum` if `currentSum` is smaller.

1. Print `minimumSum`.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];

    for (int i = 0; i < N; i++)
        scanf("%lld", &arr[i]);

    long long currentSum = arr[0];
    long long minimumSum = arr[0];

    for (int i = 1; i < N; i++)
    {
        if (currentSum + arr[i] < arr[i])
            currentSum = currentSum + arr[i];
        else
            currentSum = arr[i];

        if (currentSum < minimumSum)
            minimumSum = currentSum;
    }

    printf("%lld", minimumSum);

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

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    long long currentSum = arr[0];
    long long minimumSum = arr[0];

    for (int i = 1; i < N; i++)
    {
        currentSum = min(arr[i], currentSum + arr[i]);
        minimumSum = min(minimumSum, currentSum);
    }

    cout << minimumSum;

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

        long currentSum = arr[0];
        long minimumSum = arr[0];

        for (int i = 1; i < N; i++)
        {
            currentSum = Math.min(arr[i], currentSum + arr[i]);
            minimumSum = Math.min(minimumSum, currentSum);
        }

        System.out.print(minimumSum);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

currentSum = arr[0]
minimumSum = arr[0]

for i in range(1, N):
    currentSum = min(arr[i], currentSum + arr[i])
    minimumSum = min(minimumSum, currentSum)

print(minimumSum)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long currentSum = arr[0];
        long minimumSum = arr[0];

        for (int i = 1; i < N; i++)
        {
            currentSum = Math.Min(arr[i], currentSum + arr[i]);
            minimumSum = Math.Min(minimumSum, currentSum);
        }

        Console.Write(minimumSum);
    }
}
```

### Output
For Input:
5
3 -4 2 -3 -1

Output:
-6

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




