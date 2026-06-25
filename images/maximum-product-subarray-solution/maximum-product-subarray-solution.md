# Maximum Product Subarray - Solution

## Problem Statement

Given an array `arr[]` of `N` integers that may contain positive numbers, negative numbers, and zeros, find the maximum product that can be obtained from any contiguous subarray.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print a single integer representing the maximum product of any contiguous subarray.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Generate every possible contiguous subarray, compute its product, and keep track of the maximum product.
- **Dynamic Programming (Recommended):** While traversing the array, maintain both the maximum and minimum product ending at the current index. A negative number can turn the smallest product into the largest one after multiplication.

For example,

Input: `2 3 -2 4`

Possible subarray products:

- `[2] = 2`
- `[2,3] = 6`
- `[3,-2] = -6`
- `[-2,4] = -8`
- `[4] = 4`

The maximum product is: `6`

Output: 6

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize `maximumProduct` with the first element.
4. For every starting index:

- Initialize `product = 1`.

1. Extend the subarray one element at a time.
2. Multiply the current element with `product`.
3. Update the maximum product whenever a larger product is found.
4. Print the maximum product.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];

    for (int i = 0; i < N; i++)
        scanf("%lld", &arr[i]);

    long long maximumProduct = arr[0];

    for (int i = 0; i < N; i++)
    {
        long long product = 1;

        for (int j = i; j < N; j++)
        {
            product *= arr[j];

            if (product > maximumProduct)
                maximumProduct = product;
        }
    }

    printf("%lld", maximumProduct);

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

    long long maximumProduct = arr[0];

    for (int i = 0; i < N; i++)
    {
        long long product = 1;

        for (int j = i; j < N; j++)
        {
            product *= arr[j];
            maximumProduct = max(maximumProduct, product);
        }
    }

    cout << maximumProduct;

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

        long maximumProduct = arr[0];

        for (int i = 0; i < N; i++)
        {
            long product = 1;

            for (int j = i; j < N; j++)
            {
                product *= arr[j];
                maximumProduct = Math.max(maximumProduct, product);
            }
        }

        System.out.print(maximumProduct);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

maximumProduct = arr[0]

for i in range(N):
    product = 1

    for j in range(i, N):
        product *= arr[j]
        maximumProduct = max(maximumProduct, product)

print(maximumProduct)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long maximumProduct = arr[0];

        for (int i = 0; i < N; i++)
        {
            long product = 1;

            for (int j = i; j < N; j++)
            {
                product *= arr[j];
                maximumProduct = Math.Max(maximumProduct, product);
            }
        }

        Console.Write(maximumProduct);
    }
}
```

### Output
For Input:
4
2 3 -2 4

Output:
6

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Dynamic Programming (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize:

- `maximumEndingHere = arr[0]`
- `minimumEndingHere = arr[0]`
- `answer = arr[0]`

1. Traverse the array from the second element.
2. If the current element is negative, swap `maximumEndingHere` and `minimumEndingHere`.
3. Update:

- `maximumEndingHere = max(current, maximumEndingHere × current)`
- `minimumEndingHere = min(current, minimumEndingHere × current)`

1. Update the answer using the maximum ending here.
2. Print the answer.

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

    long long maximumEndingHere = arr[0];
    long long minimumEndingHere = arr[0];
    long long answer = arr[0];

    for (int i = 1; i < N; i++)
    {
        if (arr[i] < 0)
        {
            long long temp = maximumEndingHere;
            maximumEndingHere = minimumEndingHere;
            minimumEndingHere = temp;
        }

        maximumEndingHere = max(arr[i], maximumEndingHere * arr[i]);
        minimumEndingHere = min(arr[i], minimumEndingHere * arr[i]);

        answer = max(answer, maximumEndingHere);
    }

    printf("%lld", answer);

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

    long long maximumEndingHere = arr[0];
    long long minimumEndingHere = arr[0];
    long long answer = arr[0];

    for (int i = 1; i < N; i++)
    {
        if (arr[i] < 0)
            swap(maximumEndingHere, minimumEndingHere);

        maximumEndingHere = max(arr[i], maximumEndingHere * arr[i]);
        minimumEndingHere = min(arr[i], minimumEndingHere * arr[i]);

        answer = max(answer, maximumEndingHere);
    }

    cout << answer;

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

        long maximumEndingHere = arr[0];
        long minimumEndingHere = arr[0];
        long answer = arr[0];

        for (int i = 1; i < N; i++)
        {
            if (arr[i] < 0)
            {
                long temp = maximumEndingHere;
                maximumEndingHere = minimumEndingHere;
                minimumEndingHere = temp;
            }

            maximumEndingHere = Math.max(arr[i], maximumEndingHere * arr[i]);
            minimumEndingHere = Math.min(arr[i], minimumEndingHere * arr[i]);

            answer = Math.max(answer, maximumEndingHere);
        }

        System.out.print(answer);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

maximumEndingHere = arr[0]
minimumEndingHere = arr[0]
answer = arr[0]

for i in range(1, N):
    if arr[i] < 0:
        maximumEndingHere, minimumEndingHere = minimumEndingHere, maximumEndingHere

    maximumEndingHere = max(arr[i], maximumEndingHere * arr[i])
    minimumEndingHere = min(arr[i], minimumEndingHere * arr[i])

    answer = max(answer, maximumEndingHere)

print(answer)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long maximumEndingHere = arr[0];
        long minimumEndingHere = arr[0];
        long answer = arr[0];

        for (int i = 1; i < N; i++)
        {
            if (arr[i] < 0)
            {
                long temp = maximumEndingHere;
                maximumEndingHere = minimumEndingHere;
                minimumEndingHere = temp;
            }

            maximumEndingHere = Math.Max(arr[i], maximumEndingHere * arr[i]);
            minimumEndingHere = Math.Min(arr[i], minimumEndingHere * arr[i]);

            answer = Math.Max(answer, maximumEndingHere);
        }

        Console.Write(answer);
    }
}
```

### Output
For Input:
4
2 3 -2 4

Output:
6

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




