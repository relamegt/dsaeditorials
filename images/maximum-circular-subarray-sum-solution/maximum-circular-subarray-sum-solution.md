# Maximum Circular Subarray Sum - Solution

## Problem Statement

Given a circular integer array `arr[]` of size `N`, find the maximum sum of any contiguous subarray considering the array is circular (i.e., the end wraps around to the beginning).

A subarray must contain at least one element.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print a single integer representing the maximum circular subarray sum.

## Explanation

There are two common approaches to solve this problem.

- **Generate All Circular Subarrays:** Consider every index as a starting point, extend the subarray up to `N` elements while wrapping around using modulo, and keep track of the maximum sum.
- **Kadane's Algorithm + Minimum Subarray (Recommended):** Compute the maximum normal subarray using Kadane's Algorithm. Also compute the minimum subarray. The maximum circular sum is either the normal maximum subarray or `totalSum - minimumSubarray`. If all elements are negative, the normal maximum is the answer.

For example, when the array is: `8 -8 9 -9 10`

- Total sum = `10`
- Maximum normal subarray = `10`
- Minimum subarray = `-17`
- Maximum circular subarray = `10 - (-17) = 27`

Output: 27

<approaches>
## Approach 1: Generate All Circular Subarrays

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize `maximumSum` as the first element.
4. Consider every index as the starting position.
5. Extend the subarray one element at a time up to `N` elements.
6. Use `(start + length) % N` to wrap around the array.
7. Maintain the current sum while extending the subarray.
8. Update the maximum sum whenever a larger sum is found.
9. Print the maximum sum.

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

    for (int start = 0; start < N; start++)
    {
        long long currentSum = 0;

        for (int len = 0; len < N; len++)
        {
            currentSum += arr[(start + len) % N];

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

    for (int start = 0; start < N; start++)
    {
        long long currentSum = 0;

        for (int len = 0; len < N; len++)
        {
            currentSum += arr[(start + len) % N];
            maximumSum = max(maximumSum, currentSum);
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

        for (int start = 0; start < N; start++)
        {
            long currentSum = 0;

            for (int len = 0; len < N; len++)
            {
                currentSum += arr[(start + len) % N];

                maximumSum = Math.max(maximumSum, currentSum);
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

for start in range(N):
    currentSum = 0

    for length in range(N):
        currentSum += arr[(start + length) % N]
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

        long maximumSum = arr[0];

        for (int start = 0; start < N; start++)
        {
            long currentSum = 0;

            for (int len = 0; len < N; len++)
            {
                currentSum += arr[(start + len) % N];

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
5
8 -8 9 -9 10

Output:
27

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Kadane's Algorithm + Minimum Subarray (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Find the total sum of all elements.
4. Apply Kadane's Algorithm to find the maximum subarray sum.
5. Apply a modified Kadane's Algorithm to find the minimum subarray sum.
6. If the maximum subarray sum is negative, print it because all elements are negative.
7. Otherwise:

- Compute the circular sum as `totalSum - minimumSubarray`.
- The answer is the maximum of the normal maximum subarray and the circular subarray sum.

1. Print the answer.

```C
#include <stdio.h>

long long max(long long a, long long b)
{
    return a > b ? a : b;
}

long long min(long long a, long long b)
{
    return a < b ? a : b;
}

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];

    for (int i = 0; i < N; i++)
        scanf("%lld", &arr[i]);

    long long totalSum = arr[0];

    long long maxEnding = arr[0];
    long long maxSoFar = arr[0];

    long long minEnding = arr[0];
    long long minSoFar = arr[0];

    for (int i = 1; i < N; i++)
    {
        totalSum += arr[i];

        maxEnding = max(arr[i], maxEnding + arr[i]);
        maxSoFar = max(maxSoFar, maxEnding);

        minEnding = min(arr[i], minEnding + arr[i]);
        minSoFar = min(minSoFar, minEnding);
    }

    if (maxSoFar < 0)
        printf("%lld", maxSoFar);
    else
        printf("%lld", max(maxSoFar, totalSum - minSoFar));

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

    long long totalSum = arr[0];

    long long maxEnding = arr[0];
    long long maxSoFar = arr[0];

    long long minEnding = arr[0];
    long long minSoFar = arr[0];

    for (int i = 1; i < N; i++)
    {
        totalSum += arr[i];

        maxEnding = max(arr[i], maxEnding + arr[i]);
        maxSoFar = max(maxSoFar, maxEnding);

        minEnding = min(arr[i], minEnding + arr[i]);
        minSoFar = min(minSoFar, minEnding);
    }

    if (maxSoFar < 0)
        cout << maxSoFar;
    else
        cout << max(maxSoFar, totalSum - minSoFar);

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

        long totalSum = arr[0];

        long maxEnding = arr[0];
        long maxSoFar = arr[0];

        long minEnding = arr[0];
        long minSoFar = arr[0];

        for (int i = 1; i < N; i++)
        {
            totalSum += arr[i];

            maxEnding = Math.max(arr[i], maxEnding + arr[i]);
            maxSoFar = Math.max(maxSoFar, maxEnding);

            minEnding = Math.min(arr[i], minEnding + arr[i]);
            minSoFar = Math.min(minSoFar, minEnding);
        }

        if (maxSoFar < 0)
            System.out.print(maxSoFar);
        else
            System.out.print(Math.max(maxSoFar, totalSum - minSoFar));
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

totalSum = arr[0]

maxEnding = arr[0]
maxSoFar = arr[0]

minEnding = arr[0]
minSoFar = arr[0]

for i in range(1, N):
    totalSum += arr[i]

    maxEnding = max(arr[i], maxEnding + arr[i])
    maxSoFar = max(maxSoFar, maxEnding)

    minEnding = min(arr[i], minEnding + arr[i])
    minSoFar = min(minSoFar, minEnding)

if maxSoFar < 0:
    print(maxSoFar)
else:
    print(max(maxSoFar, totalSum - minSoFar))
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long totalSum = arr[0];

        long maxEnding = arr[0];
        long maxSoFar = arr[0];

        long minEnding = arr[0];
        long minSoFar = arr[0];

        for (int i = 1; i < N; i++)
        {
            totalSum += arr[i];

            maxEnding = Math.Max(arr[i], maxEnding + arr[i]);
            maxSoFar = Math.Max(maxSoFar, maxEnding);

            minEnding = Math.Min(arr[i], minEnding + arr[i]);
            minSoFar = Math.Min(minSoFar, minEnding);
        }

        if (maxSoFar < 0)
            Console.Write(maxSoFar);
        else
            Console.Write(Math.Max(maxSoFar, totalSum - minSoFar));
    }
}
```

### Output
For Input:
5
8 -8 9 -9 10

Output:
27

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




