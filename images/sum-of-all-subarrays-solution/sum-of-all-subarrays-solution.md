# Sum of All Subarrays - Solution

## Problem Statement

Given an array `arr[]` of `N` integers, find the sum of all possible subarrays of the array.

A subarray is a contiguous part of the array.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers representing `arr[]`.

### Output Format

Print a single integer representing the sum of all possible subarrays.

## Explanation

There are two common approaches to solve this problem.

- **Generate All Subarrays:** Generate every possible subarray, calculate its sum, and add it to the final answer.
- **Contribution Technique (Recommended):** Each element contributes to several subarrays. If an element is at index `i`, it appears in exactly `(i + 1) × (N - i)` subarrays. Multiply the element by its contribution count and add it to the answer.

For example, when the array is: `1 2 3`

Contributions:

- `1` appears in `3` subarrays → `1 × 3 = 3`
- `2` appears in `4` subarrays → `2 × 4 = 8`
- `3` appears in `3` subarrays → `3 × 3 = 9`

Total: `3 + 8 + 9 = 20`

Output:  20

<approaches>
## Approach 1: Generate All Subarrays

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize `totalSum = 0`.
4. Traverse every possible starting index.
5. For each starting index, keep extending the subarray.
6. Maintain the current subarray sum while extending.
7. Add every subarray sum to `totalSum`.
8. Print `totalSum`.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    int arr[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    long long totalSum = 0;

    for (int i = 0; i < N; i++)
    {
        long long currentSum = 0;

        for (int j = i; j < N; j++)
        {
            currentSum += arr[j];
            totalSum += currentSum;
        }
    }

    printf("%lld", totalSum);

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

    int arr[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    long long totalSum = 0;

    for (int i = 0; i < N; i++)
    {
        long long currentSum = 0;

        for (int j = i; j < N; j++)
        {
            currentSum += arr[j];
            totalSum += currentSum;
        }
    }

    cout << totalSum;

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

        int[] arr = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        long totalSum = 0;

        for (int i = 0; i < N; i++)
        {
            long currentSum = 0;

            for (int j = i; j < N; j++)
            {
                currentSum += arr[j];
                totalSum += currentSum;
            }
        }

        System.out.print(totalSum);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

totalSum = 0

for i in range(N):
    currentSum = 0

    for j in range(i, N):
        currentSum += arr[j]
        totalSum += currentSum

print(totalSum)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        long totalSum = 0;

        for (int i = 0; i < N; i++)
        {
            long currentSum = 0;

            for (int j = i; j < N; j++)
            {
                currentSum += arr[j];
                totalSum += currentSum;
            }
        }

        Console.Write(totalSum);
    }
}
```

### Output
For Input:
3
1 2 3

Output:
20

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Contribution Technique (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize `totalSum = 0`.
4. Traverse every element in the array.
5. For each element at index `i`:

- Count the number of choices for the starting index as `(i + 1)`.
- Count the number of choices for the ending index as `(N - i)`.
- Therefore, the element appears in `(i + 1) × (N - i)` subarrays.
- Multiply the element with this count and add it to `totalSum`.

1. Print `totalSum`.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long totalSum = 0;

    for (int i = 0; i < N; i++)
    {
        long long x;
        scanf("%lld", &x);

        totalSum += x * (i + 1LL) * (N - i);
    }

    printf("%lld", totalSum);

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

    long long totalSum = 0;

    for (int i = 0; i < N; i++)
    {
        long long x;
        cin >> x;

        totalSum += x * (i + 1LL) * (N - i);
    }

    cout << totalSum;

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

        long totalSum = 0;

        for (int i = 0; i < N; i++)
        {
            long x = sc.nextLong();

            totalSum += x * (i + 1L) * (N - i);
        }

        System.out.print(totalSum);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

totalSum = 0

for i in range(N):
    totalSum += arr[i] * (i + 1) * (N - i)

print(totalSum)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long totalSum = 0;

        for (int i = 0; i < N; i++)
        {
            totalSum += arr[i] * (i + 1L) * (N - i);
        }

        Console.Write(totalSum);
    }
}
```

### Output
For Input:
3
1 2 3

Output:
20

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




