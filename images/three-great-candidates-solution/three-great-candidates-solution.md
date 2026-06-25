# Three Great Candidates- Solution

## Problem Statement

Given an array `arr[]` of `N` integers representing the abilities of candidates, find the maximum product that can be obtained by multiplying any three distinct elements.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print a single integer representing the maximum product of any three distinct elements.

## Explanation

The maximum product can be obtained in two ways:

- By multiplying the **three largest numbers**.
- By multiplying the **two smallest (most negative) numbers** with the **largest positive number**.

This is because multiplying two negative numbers gives a positive number.

For example,

Input: `-10 -10 5 2 1`

Possible products:

- `5 × 2 × 1 = 10`
- `(-10) × (-10) × 5 = 500`

The maximum product is `500`.

## Algorithm

1. Read the integer `N`.
2. Read the array.
3. Sort the array in ascending order.
4. Compute:

- `product1 = largest × second largest × third largest`
- `product2 = smallest × second smallest × largest`

1. Print the larger of the two products.

```C
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a, const void *b)
{
    long long x = *(long long *)a;
    long long y = *(long long *)b;

    if (x < y)
        return -1;
    if (x > y)
        return 1;
    return 0;
}

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];

    for (int i = 0; i < N; i++)
        scanf("%lld", &arr[i]);

    qsort(arr, N, sizeof(long long), compare);

    long long product1 = arr[N - 1] * arr[N - 2] * arr[N - 3];
    long long product2 = arr[0] * arr[1] * arr[N - 1];

    if (product1 > product2)
        printf("%lld", product1);
    else
        printf("%lld", product2);

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

    sort(arr, arr + N);

    long long product1 = arr[N - 1] * arr[N - 2] * arr[N - 3];
    long long product2 = arr[0] * arr[1] * arr[N - 1];

    cout << max(product1, product2);

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

        Arrays.sort(arr);

        long product1 = arr[N - 1] * arr[N - 2] * arr[N - 3];
        long product2 = arr[0] * arr[1] * arr[N - 1];

        System.out.print(Math.max(product1, product2));
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

arr.sort()

product1 = arr[-1] * arr[-2] * arr[-3]
product2 = arr[0] * arr[1] * arr[-1]

print(max(product1, product2))
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        Array.Sort(arr);

        long product1 = arr[N - 1] * arr[N - 2] * arr[N - 3];
        long product2 = arr[0] * arr[1] * arr[N - 1];

        Console.Write(Math.Max(product1, product2));
    }
}
```

### Output
For Input:
5
1 2 3 4 5

Output:
60

# Time Complexity
O(N log N)

# Space Complexity
O(1) (Ignoring the space used by the sorting algorithm implementation.)




