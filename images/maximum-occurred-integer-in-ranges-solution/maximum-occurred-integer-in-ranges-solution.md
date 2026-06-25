# Maximum Occurred Integer in Ranges - Solution

## Problem Statement

Given `N` ranges `[L[i], R[i]]` (inclusive), find the integer that appears the maximum number of times across all ranges.

If multiple integers have the same maximum frequency, return the **smallest** one.

An integer `x` is said to occur in range `[L, R]` if:

`L <= x <= R`

### Input Format

First line: Integer `N`.

Next `N` lines: Two space-separated integers `L[i]` and `R[i]`.

### Output Format

Print a single integer representing the maximum occurred integer.

## Explanation

Instead of marking every integer inside every range, we use a **Difference Array (Prefix Sum)** technique.

For every range `[L, R]`:

- Increment `diff[L]` by `1`.
- Decrement `diff[R + 1]` by `1` (if it is within bounds).

After processing all ranges, compute the prefix sum of the difference array.

The prefix sum at index `i` gives the number of ranges containing `i`.

While computing the prefix sum, keep track of:

- Maximum frequency found so far.
- Smallest index having that maximum frequency.

For example,

Ranges:

`[1,4]`

`[4,6]`

`[3,7]`

Difference array updates:

- +1 at 1, -1 at 5
- +1 at 4, -1 at 7
- +1 at 3, -1 at 8

After taking prefix sums:

```Code
1 -> 1
2 -> 1
3 -> 2
4 -> 3
5 -> 2
6 -> 2
7 -> 1
```

The maximum frequency is `3`, occurring at integer `4`.

Output: 4

## Algorithm

1. Read the integer `N`.
2. Find the maximum value among all `R[i]`.
3. Create a difference array of size `maxR + 2` initialized to `0`.
4. For every range:

- Increment `diff[L]`.
- Decrement `diff[R + 1]`.

1. Compute the prefix sum of the difference array.
2. While computing the prefix sum:

- Maintain the current frequency.
- If it is greater than the maximum frequency found so far, update:
- Maximum frequency.
- Answer.

1. Print the answer.

```C
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int N;
    scanf("%d", &N);

    int *L = (int *)malloc(N * sizeof(int));
    int *R = (int *)malloc(N * sizeof(int));

    int maxR = 0;

    for (int i = 0; i < N; i++)
    {
        scanf("%d %d", &L[i], &R[i]);

        if (R[i] > maxR)
            maxR = R[i];
    }

    int *diff = (int *)calloc(maxR + 2, sizeof(int));

    for (int i = 0; i < N; i++)
    {
        diff[L[i]]++;

        if (R[i] + 1 <= maxR + 1)
            diff[R[i] + 1]--;
    }

    int current = 0;
    int maximum = 0;
    int answer = 0;

    for (int i = 0; i <= maxR; i++)
    {
        current += diff[i];

        if (current > maximum)
        {
            maximum = current;
            answer = i;
        }
    }

    printf("%d", answer);

    free(L);
    free(R);
    free(diff);

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

    vector<pair<int, int>> ranges(N);

    int maxR = 0;

    for (int i = 0; i < N; i++)
    {
        cin >> ranges[i].first >> ranges[i].second;
        maxR = max(maxR, ranges[i].second);
    }

    vector<int> diff(maxR + 2, 0);

    for (auto range : ranges)
    {
        diff[range.first]++;

        if (range.second + 1 <= maxR + 1)
            diff[range.second + 1]--;
    }

    int current = 0;
    int maximum = 0;
    int answer = 0;

    for (int i = 0; i <= maxR; i++)
    {
        current += diff[i];

        if (current > maximum)
        {
            maximum = current;
            answer = i;
        }
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

        int[] L = new int[N];
        int[] R = new int[N];

        int maxR = 0;

        for (int i = 0; i < N; i++)
        {
            L[i] = sc.nextInt();
            R[i] = sc.nextInt();

            maxR = Math.max(maxR, R[i]);
        }

        int[] diff = new int[maxR + 2];

        for (int i = 0; i < N; i++)
        {
            diff[L[i]]++;

            if (R[i] + 1 <= maxR + 1)
                diff[R[i] + 1]--;
        }

        int current = 0;
        int maximum = 0;
        int answer = 0;

        for (int i = 0; i <= maxR; i++)
        {
            current += diff[i];

            if (current > maximum)
            {
                maximum = current;
                answer = i;
            }
        }

        System.out.print(answer);
    }
}
```
```Python
N = int(input())

L = []
R = []

maxR = 0

for _ in range(N):
    l, r = map(int, input().split())
    L.append(l)
    R.append(r)
    maxR = max(maxR, r)

diff = [0] * (maxR + 2)

for i in range(N):
    diff[L[i]] += 1

    if R[i] + 1 <= maxR + 1:
        diff[R[i] + 1] -= 1

current = 0
maximum = 0
answer = 0

for i in range(maxR + 1):
    current += diff[i]

    if current > maximum:
        maximum = current
        answer = i

print(answer)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] L = new int[N];
        int[] R = new int[N];

        int maxR = 0;

        for (int i = 0; i < N; i++)
        {
            string[] input = Console.ReadLine().Split();

            L[i] = int.Parse(input[0]);
            R[i] = int.Parse(input[1]);

            maxR = Math.Max(maxR, R[i]);
        }

        int[] diff = new int[maxR + 2];

        for (int i = 0; i < N; i++)
        {
            diff[L[i]]++;

            if (R[i] + 1 <= maxR + 1)
                diff[R[i] + 1]--;
        }

        int current = 0;
        int maximum = 0;
        int answer = 0;

        for (int i = 0; i <= maxR; i++)
        {
            current += diff[i];

            if (current > maximum)
            {
                maximum = current;
                answer = i;
            }
        }

        Console.Write(answer);
    }
}
```

### Output
For Input:
3
1 4
4 6
3 7

Output:
4

# Time Complexity
O(N + M)Where M is the maximum value among all `R[i]`.

# Space Complexity
O(M)




