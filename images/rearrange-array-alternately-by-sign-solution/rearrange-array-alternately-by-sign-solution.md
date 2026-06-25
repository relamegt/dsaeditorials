# Rearrange Array Alternately by Sign - Solution

## Problem Statement

Given an array `arr[]` of size `N` containing both positive and negative integers (excluding zero), rearrange the array such that positive and negative numbers are placed alternately.

The rearranged array should start with a positive number.

If there are extra positive or negative numbers, place them at the end while maintaining their relative order.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print the rearranged array as `N` space-separated integers.

## Explanation

To maintain the relative order of positive and negative numbers, first separate them into two different lists.

Now, build the answer array by alternately taking one positive number followed by one negative number.

Continue this process until either list is exhausted.

If any positive numbers remain, append them to the end.

If any negative numbers remain, append them to the end.

This guarantees:

- The array starts with a positive number.
- Relative order of positive numbers is preserved.
- Relative order of negative numbers is preserved.
- Extra elements appear at the end.

For example,

Input: `-1 2 -3 4`
Positive numbers: `2 4`
Negative numbers: `-1 -3`
Rearranged array: `2 -1 4 -3`

## Algorithm

1. Read the integer `N`.
2. Read the array.
3. Traverse the array.
4. Store all positive numbers in one list.
5. Store all negative numbers in another list.
6. Initialize two pointers for positive and negative lists.
7. Alternately place:

- One positive number.
- One negative number.

1. If positive numbers remain, append them.
2. If negative numbers remain, append them.

10. Print the rearranged array.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];
    long long positive[N], negative[N], result[N];

    int p = 0, n = 0;

    for (int i = 0; i < N; i++)
    {
        scanf("%lld", &arr[i]);

        if (arr[i] > 0)
            positive[p++] = arr[i];
        else
            negative[n++] = arr[i];
    }

    int i = 0, j = 0, k = 0;

    while (i < p && j < n)
    {
        result[k++] = positive[i++];
        result[k++] = negative[j++];
    }

    while (i < p)
        result[k++] = positive[i++];

    while (j < n)
        result[k++] = negative[j++];

    for (int x = 0; x < N; x++)
        printf("%lld ", result[x]);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int N;
    cin >> N;

    vector<long long> positive, negative;

    for (int i = 0; i < N; i++)
    {
        long long x;
        cin >> x;

        if (x > 0)
            positive.push_back(x);
        else
            negative.push_back(x);
    }

    vector<long long> result;

    int i = 0, j = 0;

    while (i < positive.size() && j < negative.size())
    {
        result.push_back(positive[i++]);
        result.push_back(negative[j++]);
    }

    while (i < positive.size())
        result.push_back(positive[i++]);

    while (j < negative.size())
        result.push_back(negative[j++]);

    for (long long x : result)
        cout << x << " ";

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

        ArrayList<Long> positive = new ArrayList<>();
        ArrayList<Long> negative = new ArrayList<>();
        ArrayList<Long> result = new ArrayList<>();

        for (int i = 0; i < N; i++)
        {
            long x = sc.nextLong();

            if (x > 0)
                positive.add(x);
            else
                negative.add(x);
        }

        int i = 0, j = 0;

        while (i < positive.size() && j < negative.size())
        {
            result.add(positive.get(i++));
            result.add(negative.get(j++));
        }

        while (i < positive.size())
            result.add(positive.get(i++));

        while (j < negative.size())
            result.add(negative.get(j++));

        for (long x : result)
            System.out.print(x + " ");
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

positive = []
negative = []

for x in arr:
    if x > 0:
        positive.append(x)
    else:
        negative.append(x)

result = []

i = 0
j = 0

while i < len(positive) and j < len(negative):
    result.append(positive[i])
    result.append(negative[j])
    i += 1
    j += 1

while i < len(positive):
    result.append(positive[i])
    i += 1

while j < len(negative):
    result.append(negative[j])
    j += 1

print(*result)
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        List<long> positive = new List<long>();
        List<long> negative = new List<long>();
        List<long> result = new List<long>();

        foreach (long x in arr)
        {
            if (x > 0)
                positive.Add(x);
            else
                negative.Add(x);
        }

        int i = 0, j = 0;

        while (i < positive.Count && j < negative.Count)
        {
            result.Add(positive[i++]);
            result.Add(negative[j++]);
        }

        while (i < positive.Count)
            result.Add(positive[i++]);

        while (j < negative.Count)
            result.Add(negative[j++]);

        Console.Write(string.Join(" ", result));
    }
}
```

### Output
For Input:
6
1 -2 3 -4 5 -6

Output:
1  -2  3  -4  5  -6

# Time Complexity
O(N)

# Space Complexity
O(N)

### Note

This is the **stable** rearrangement approach:

- The **relative order of positive numbers** is preserved.
- The **relative order of negative numbers** is preserved.
- The array **always starts with a positive number**.
- If one type of number has extra elements, they are appended at the end in their original order.




