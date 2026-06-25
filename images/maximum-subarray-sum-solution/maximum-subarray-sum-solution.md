# Maximum Subarray Sum - Solution

## Problem Statement

Given an integer array `arr[]` of size `N`, find the maximum sum of any contiguous subarray.

A subarray must contain at least one element.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print a single integer representing the maximum subarray sum.

## Explanation

There are two common approaches to solve this problem.

- **Generate All Subarrays:** Generate every possible subarray, calculate its sum, and keep track of the maximum sum obtained.
- **Kadane's Algorithm (Recommended):** Traverse the array once while maintaining the maximum sum ending at the current position. If the current sum becomes worse than starting a new subarray, begin a new subarray from the current element.

For example, when the array is: `-2 1 -3 4 -1 2 1 -5 4`
The maximum sum subarray is: `4 -1 2 1`
Its sum is: `6`

Output: 6

<approaches>
## Approach 1: Generate All Subarrays

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize `maximumSum` as the first element.
4. Traverse every possible starting index.
5. For each starting index:

- Initialize `currentSum = 0`.
- Extend the subarray one element at a time.
- Add the current element to `currentSum`.
- Update `maximumSum` if `currentSum` is greater.

1. Print `maximumSum`.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];

    for (int i = 0; i < N; i++)
        scanf("%lld", &arr[i]);

    long long maximumSum = arr[0];

    for (int i = 0; i < N; i++)
    {
        long long currentSum = 0;

        for (int j = i; j < N; j++)
        {
            currentSum += arr[j];

            if (currentSum > maximumSum)
                maximumSum = currentSum;
        }
    }

    printf("%lld", maximumSum);

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

    long long maximumSum = arr[0];

    for (int i = 0; i < N; i++)
    {
        long long currentSum = 0;

        for (int j = i; j < N; j++)
        {
            currentSum += arr[j];

            if (currentSum > maximumSum)
                maximumSum = currentSum;
        }
    }

    cout << maximumSum;

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

        long maximumSum = arr[0];

        for (int i = 0; i < N; i++)
        {
            long currentSum = 0;

            for (int j = i; j < N; j++)
            {
                currentSum += arr[j];

                if (currentSum > maximumSum)
                    maximumSum = currentSum;
            }
        }

        System.out.print(maximumSum);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

maximumSum = arr[0]

for i in range(N):
    currentSum = 0

    for j in range(i, N):
        currentSum += arr[j]

        if currentSum > maximumSum:
            maximumSum = currentSum

print(maximumSum)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long maximumSum = arr[0];

        for (int i = 0; i < N; i++)
        {
            long currentSum = 0;

            for (int j = i; j < N; j++)
            {
                currentSum += arr[j];

                if (currentSum > maximumSum)
                    maximumSum = currentSum;
            }
        }

        Console.Write(maximumSum);
    }
}
```

### Output
For Input:
9
-2 1 -3 4 -1 2 1 -5 4

Output:
6

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Kadane's Algorithm (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize:

- `currentSum` as the first element.
- `maximumSum` as the first element.

1. Traverse the array from the second element onwards.
2. For every element:

- Decide whether to:
- Extend the previous subarray by adding the current element, or
- Start a new subarray from the current element.
- Update `currentSum` as the maximum of these two choices.
- Update `maximumSum` if `currentSum` is greater.

1. Print `maximumSum`.

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
    long long maximumSum = arr[0];

    for (int i = 1; i < N; i++)
    {
        if (currentSum + arr[i] > arr[i])
            currentSum = currentSum + arr[i];
        else
            currentSum = arr[i];

        if (currentSum > maximumSum)
            maximumSum = currentSum;
    }

    printf("%lld", maximumSum);

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
    long long maximumSum = arr[0];

    for (int i = 1; i < N; i++)
    {
        currentSum = max(arr[i], currentSum + arr[i]);
        maximumSum = max(maximumSum, currentSum);
    }

    cout << maximumSum;

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
        long maximumSum = arr[0];

        for (int i = 1; i < N; i++)
        {
            currentSum = Math.max(arr[i], currentSum + arr[i]);
            maximumSum = Math.max(maximumSum, currentSum);
        }

        System.out.print(maximumSum);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

currentSum = arr[0]
maximumSum = arr[0]

for i in range(1, N):
    currentSum = max(arr[i], currentSum + arr[i])
    maximumSum = max(maximumSum, currentSum)

print(maximumSum)
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
        long maximumSum = arr[0];

        for (int i = 1; i < N; i++)
        {
            currentSum = Math.Max(arr[i], currentSum + arr[i]);
            maximumSum = Math.Max(maximumSum, currentSum);
        }

        Console.Write(maximumSum);
    }
}
```

### Output
For Input:
9
-2 1 -3 4 -1 2 1 -5 4

Output:
6

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




