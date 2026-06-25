# Print Unique Elements in a Sorted Array - Solution

## Problem Statement

Given a sorted array `arr[]` of `N` integers, print all the unique elements, where a unique element is an element that appears exactly once in the array.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers sorted in non-decreasing order.

### Output Format

Print all unique elements separated by spaces.

If no unique element exists, print nothing.

## Explanation

There are two common approaches to solve this problem.

- **Count Frequencies:** Traverse every group of equal elements, count their frequency, and print the element if its frequency is `1`.
- **Neighbor Comparison (Recommended):** Since the array is already sorted, compare every element with its previous and next elements. If it differs from both neighbors, it appears exactly once.

For example,

Input: `1 1 2 3 3 4`

- `1` appears twice.
- `2` appears once.
- `3` appears twice.
- `4` appears once.

Output: `2 4`

<approaches>
## Approach 1: Count Frequencies

### Algorithm

1. Read the integer `N`.
2. Read the sorted array.
3. Start from the first element.
4. Count how many consecutive times the current element appears.
5. If its count is `1`, print it.
6. Move to the next distinct element.
7. Repeat until the end of the array.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];

    for (int i = 0; i < N; i++)
        scanf("%lld", &arr[i]);

    int i = 0;

    while (i < N)
    {
        int count = 1;

        while (i + count < N && arr[i] == arr[i + count])
            count++;

        if (count == 1)
            printf("%lld ", arr[i]);

        i += count;
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

    int i = 0;

    while (i < N)
    {
        int count = 1;

        while (i + count < N && arr[i] == arr[i + count])
            count++;

        if (count == 1)
            cout << arr[i] << " ";

        i += count;
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

        int i = 0;

        while (i < N)
        {
            int count = 1;

            while (i + count < N && arr[i] == arr[i + count])
                count++;

            if (count == 1)
                System.out.print(arr[i] + " ");

            i += count;
        }
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

i = 0

while i < N:
    count = 1

    while i + count < N and arr[i] == arr[i + count]:
        count += 1

    if count == 1:
        print(arr[i], end=" ")

    i += count
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        int i = 0;

        while (i < N)
        {
            int count = 1;

            while (i + count < N && arr[i] == arr[i + count])
                count++;

            if (count == 1)
                Console.Write(arr[i] + " ");

            i += count;
        }
    }
}
```

### Output
For Input:
6
1 1 2 3 3 4

Output:
2 4

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Neighbor Comparison (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the sorted array.
3. Traverse each element from left to right.
4. For every element:

- Check whether it is different from its previous element (or it is the first element).
- Check whether it is different from its next element (or it is the last element).

1. If both conditions are true, the element appears exactly once, so print it.
2. Continue until all elements are processed.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];

    for (int i = 0; i < N; i++)
        scanf("%lld", &arr[i]);

    for (int i = 0; i < N; i++)
    {
        int leftDifferent = (i == 0 || arr[i] != arr[i - 1]);
        int rightDifferent = (i == N - 1 || arr[i] != arr[i + 1]);

        if (leftDifferent && rightDifferent)
            printf("%lld ", arr[i]);
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

    for (int i = 0; i < N; i++)
    {
        bool leftDifferent = (i == 0 || arr[i] != arr[i - 1]);
        bool rightDifferent = (i == N - 1 || arr[i] != arr[i + 1]);

        if (leftDifferent && rightDifferent)
            cout << arr[i] << " ";
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

        for (int i = 0; i < N; i++)
        {
            boolean leftDifferent = (i == 0 || arr[i] != arr[i - 1]);
            boolean rightDifferent = (i == N - 1 || arr[i] != arr[i + 1]);

            if (leftDifferent && rightDifferent)
                System.out.print(arr[i] + " ");
        }
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

for i in range(N):
    leftDifferent = (i == 0 or arr[i] != arr[i - 1])
    rightDifferent = (i == N - 1 or arr[i] != arr[i + 1])

    if leftDifferent and rightDifferent:
        print(arr[i], end=" ")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        for (int i = 0; i < N; i++)
        {
            bool leftDifferent = (i == 0 || arr[i] != arr[i - 1]);
            bool rightDifferent = (i == N - 1 || arr[i] != arr[i + 1]);

            if (leftDifferent && rightDifferent)
                Console.Write(arr[i] + " ");
        }
    }
}
```

### Output
For Input:
6
1 1 2 3 3 4

Output:
2 4

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




