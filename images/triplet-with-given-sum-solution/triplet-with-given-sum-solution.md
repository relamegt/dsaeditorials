# Triplet with Given Sum - Solution

## Problem Statement

Given an array `arr[]` of `N` integers and an integer `target`, determine whether there exists a triplet of distinct elements whose sum is equal to `target`.

Print `1` if such a triplet exists; otherwise print `0`.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

Third line: Integer `target`.

### Output Format

Print `1` if a valid triplet exists, otherwise print `0`.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Generate every possible triplet and check whether its sum equals the target.
- **Sorting + Two Pointers (Recommended):** Sort the array. Fix one element, then use two pointers to search for the remaining two elements efficiently.

For example,

Input: `12 3 4 1 6 9`
Target: `24`
After sorting: `1 3 4 6 9 12`
Fix `3`.

Now search for two numbers whose sum is `21`.
`9 + 12 = 21`

Triplet found: `3 + 9 + 12 = 24`

Output: `1`

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Read the target value.
4. Generate every possible triplet `(i, j, k)` where `i < j < k`.
5. Compute the sum of the three elements.
6. If the sum equals the target:

- Print `1`.
- Stop the program.

1. If no triplet is found, print `0`.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];

    for (int i = 0; i < N; i++)
        scanf("%lld", &arr[i]);

    long long target;
    scanf("%lld", &target);

    for (int i = 0; i < N - 2; i++)
    {
        for (int j = i + 1; j < N - 1; j++)
        {
            for (int k = j + 1; k < N; k++)
            {
                if (arr[i] + arr[j] + arr[k] == target)
                {
                    printf("1");
                    return 0;
                }
            }
        }
    }

    printf("0");

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

    long long target;
    cin >> target;

    for (int i = 0; i < N - 2; i++)
    {
        for (int j = i + 1; j < N - 1; j++)
        {
            for (int k = j + 1; k < N; k++)
            {
                if (arr[i] + arr[j] + arr[k] == target)
                {
                    cout << 1;
                    return 0;
                }
            }
        }
    }

    cout << 0;

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

        long target = sc.nextLong();

        for (int i = 0; i < N - 2; i++)
        {
            for (int j = i + 1; j < N - 1; j++)
            {
                for (int k = j + 1; k < N; k++)
                {
                    if (arr[i] + arr[j] + arr[k] == target)
                    {
                        System.out.print(1);
                        return;
                    }
                }
            }
        }

        System.out.print(0);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

target = int(input())

for i in range(N - 2):
    for j in range(i + 1, N - 1):
        for k in range(j + 1, N):
            if arr[i] + arr[j] + arr[k] == target:
                print(1)
                exit()

print(0)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long target = long.Parse(Console.ReadLine());

        for (int i = 0; i < N - 2; i++)
        {
            for (int j = i + 1; j < N - 1; j++)
            {
                for (int k = j + 1; k < N; k++)
                {
                    if (arr[i] + arr[j] + arr[k] == target)
                    {
                        Console.Write(1);
                        return;
                    }
                }
            }
        }

        Console.Write(0);
    }
}
```

### Output
For Input:
6
12 3 4 1 6 9
24

Output:
1

# Time Complexity
O(N³)

# Space Complexity
O(1)

## Approach 2: Sorting + Two Pointers (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Read the target value.
4. Sort the array in ascending order.
5. Traverse each element from index `0` to `N-3`.
6. Fix the current element as the first element of the triplet.
7. Initialize:

- `left = i + 1`
- `right = N - 1`

1. While `left < right`:

- Compute the current sum.
- If the sum equals the target:
- Print `1` and stop.
- If the sum is smaller than the target:
- Move `left` one step to the right.
- Otherwise:
- Move `right` one step to the left.

1. If no triplet is found after checking all elements, print `0`.

```C
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a, const void *b)
{
    long long x = *(long long *)a;
    long long y = *(long long *)b;

    if (x < y) return -1;
    if (x > y) return 1;
    return 0;
}

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];

    for (int i = 0; i < N; i++)
        scanf("%lld", &arr[i]);

    long long target;
    scanf("%lld", &target);

    qsort(arr, N, sizeof(long long), compare);

    for (int i = 0; i < N - 2; i++)
    {
        int left = i + 1;
        int right = N - 1;

        while (left < right)
        {
            long long sum = arr[i] + arr[left] + arr[right];

            if (sum == target)
            {
                printf("1");
                return 0;
            }
            else if (sum < target)
            {
                left++;
            }
            else
            {
                right--;
            }
        }
    }

    printf("0");

    return 0;
}
```
```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int main()
{
    int N;
    cin >> N;

    long long arr[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    long long target;
    cin >> target;

    sort(arr, arr + N);

    for (int i = 0; i < N - 2; i++)
    {
        int left = i + 1;
        int right = N - 1;

        while (left < right)
        {
            long long sum = arr[i] + arr[left] + arr[right];

            if (sum == target)
            {
                cout << 1;
                return 0;
            }
            else if (sum < target)
            {
                left++;
            }
            else
            {
                right--;
            }
        }
    }

    cout << 0;

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

        long target = sc.nextLong();

        Arrays.sort(arr);

        for (int i = 0; i < N - 2; i++)
        {
            int left = i + 1;
            int right = N - 1;

            while (left < right)
            {
                long sum = arr[i] + arr[left] + arr[right];

                if (sum == target)
                {
                    System.out.print(1);
                    return;
                }
                else if (sum < target)
                {
                    left++;
                }
                else
                {
                    right--;
                }
            }
        }

        System.out.print(0);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

target = int(input())

arr.sort()

for i in range(N - 2):
    left = i + 1
    right = N - 1

    while left < right:
        current = arr[i] + arr[left] + arr[right]

        if current == target:
            print(1)
            exit()
        elif current < target:
            left += 1
        else:
            right -= 1

print(0)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long target = long.Parse(Console.ReadLine());

        Array.Sort(arr);

        for (int i = 0; i < N - 2; i++)
        {
            int left = i + 1;
            int right = N - 1;

            while (left < right)
            {
                long sum = arr[i] + arr[left] + arr[right];

                if (sum == target)
                {
                    Console.Write(1);
                    return;
                }
                else if (sum < target)
                {
                    left++;
                }
                else
                {
                    right--;
                }
            }
        }

        Console.Write(0);
    }
}
```

### Output
For Input:
6
12 3 4 1 6 9
24

Output:
1

# Time Complexity
O(N²)

# Space Complexity
O(1)

</approaches>




