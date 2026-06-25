# Two Sum in a Sorted Array - Solution

## Problem Statement

Given a sorted array `arr[]` of `N` integers and an integer `target`, find two distinct indices such that the elements at those indices add up to `target`.

Return the indices using **1-based indexing**.

It is guaranteed that exactly one valid answer exists.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers sorted in non-decreasing order.

Third line: Integer `target`.

### Output Format

Print two space-separated integers representing the required **1-based indices**.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Check every possible pair of elements and see whether their sum equals the target.
- **Two Pointers (Recommended):** Since the array is already sorted, use one pointer at the beginning and another at the end. Depending on the current sum, move one of the pointers until the required pair is found.

For example,

Input: `2 7 11 15`

Target: `9`

- `2 + 15 = 17` (Too large, move the right pointer.)
- `2 + 11 = 13` (Too large, move the right pointer.)
- `2 + 7 = 9` (Target found.)

Indices are: `1 2`

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the integer `N`.
2. Read the sorted array.
3. Read the target value.
4. Traverse every element as the first element of the pair.
5. For each element, check every element after it.
6. If the sum equals the target:

- Print the 1-based indices.
- Stop the program.

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

    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {
            if (arr[i] + arr[j] == target)
            {
                printf("%d %d", i + 1, j + 1);
                return 0;
            }
        }
    }

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

    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {
            if (arr[i] + arr[j] == target)
            {
                cout << i + 1 << " " << j + 1;
                return 0;
            }
        }
    }

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

        for (int i = 0; i < N; i++)
        {
            for (int j = i + 1; j < N; j++)
            {
                if (arr[i] + arr[j] == target)
                {
                    System.out.print((i + 1) + " " + (j + 1));
                    return;
                }
            }
        }
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

target = int(input())

for i in range(N):
    for j in range(i + 1, N):
        if arr[i] + arr[j] == target:
            print(i + 1, j + 1)
            exit()
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

        for (int i = 0; i < N; i++)
        {
            for (int j = i + 1; j < N; j++)
            {
                if (arr[i] + arr[j] == target)
                {
                    Console.Write((i + 1) + " " + (j + 1));
                    return;
                }
            }
        }
    }
}
```

### Output
For Input:
4
2 7 11 15
9

Output:
1 2

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Two Pointers (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the sorted array.
3. Read the target value.
4. Initialize two pointers:

- `left = 0`
- `right = N - 1`

1. Repeat while `left < right`:

- Compute `sum = arr[left] + arr[right]`.
- If `sum == target`:
- Print `left + 1` and `right + 1`.
- Stop.
- If `sum < target`:
- Increment `left` to increase the sum.
- Otherwise:
- Decrement `right` to decrease the sum.

1. The required pair is guaranteed to exist.

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

    int left = 0;
    int right = N - 1;

    while (left < right)
    {
        long long sum = arr[left] + arr[right];

        if (sum == target)
        {
            printf("%d %d", left + 1, right + 1);
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

    int left = 0;
    int right = N - 1;

    while (left < right)
    {
        long long sum = arr[left] + arr[right];

        if (sum == target)
        {
            cout << left + 1 << " " << right + 1;
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

        int left = 0;
        int right = N - 1;

        while (left < right)
        {
            long sum = arr[left] + arr[right];

            if (sum == target)
            {
                System.out.print((left + 1) + " " + (right + 1));
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
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

target = int(input())

left = 0
right = N - 1

while left < right:
    current = arr[left] + arr[right]

    if current == target:
        print(left + 1, right + 1)
        break
    elif current < target:
        left += 1
    else:
        right -= 1
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

        int left = 0;
        int right = arr.Length - 1;

        while (left < right)
        {
            long sum = arr[left] + arr[right];

            if (sum == target)
            {
                Console.Write((left + 1) + " " + (right + 1));
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
}
```

### Output
For Input:
4
2 7 11 15
9

Output:
1 2

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




