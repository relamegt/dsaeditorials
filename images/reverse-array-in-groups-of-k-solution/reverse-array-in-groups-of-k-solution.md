# Reverse Array in Groups of K - Solution

## Problem Statement

Given an array `arr[]` of size `N` and an integer `K`, reverse every group of `K` consecutive elements.

If the number of remaining elements in the last group is less than `K`, reverse only those remaining elements.

### Input Format

First line: Two integers `N` and `K`.

Second line: `N` space-separated integers.

### Output Format

Print the modified array as `N` space-separated integers on a single line.

## Explanation

There are two common approaches to solve this problem.

- **Using an Extra Array:** Copy every group of `K` elements into another array in reverse order and finally print the new array.
- **In-place Two Pointer Reversal (Recommended):** Process the array one group at a time. For each group, use two pointers to reverse the elements within that group without using extra space.

For example, when: `N = 8, K = 3`
Array: `1 2 3 4 5 6 7 8`

Groups become:

- `[1 2 3] → [3 2 1]`
- `[4 5 6] → [6 5 4]`
- `[7 8] → [8 7]`

Final array: `3 2 1 6 5 4 8 7`
Output: 3 2 1 6 5 4 8 7

<approaches>
## Approach 1: Using an Extra Array

### Algorithm

1. Read the integers `N` and `K`.
2. Read the array.
3. Create another array of size `N`.
4. Traverse the original array group by group.
5. For each group:

- Determine its ending index.
- Copy the elements of the group into the new array in reverse order.

1. Print the new array.

```C
#include <stdio.h>

int main()
{
    int N, K;
    scanf("%d %d", &N, &K);

    int arr[N], ans[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    int index = 0;

    for (int start = 0; start < N; start += K)
    {
        int end = start + K - 1;

        if (end >= N)
            end = N - 1;

        for (int i = end; i >= start; i--)
            ans[index++] = arr[i];
    }

    for (int i = 0; i < N; i++)
        printf("%d ", ans[i]);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main()
{
    int N, K;
    cin >> N >> K;

    int arr[N], ans[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    int index = 0;

    for (int start = 0; start < N; start += K)
    {
        int end = min(start + K - 1, N - 1);

        for (int i = end; i >= start; i--)
            ans[index++] = arr[i];
    }

    for (int i = 0; i < N; i++)
        cout << ans[i] << " ";

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
        int K = sc.nextInt();

        int[] arr = new int[N];
        int[] ans = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        int index = 0;

        for (int start = 0; start < N; start += K)
        {
            int end = Math.min(start + K - 1, N - 1);

            for (int i = end; i >= start; i--)
                ans[index++] = arr[i];
        }

        for (int x : ans)
            System.out.print(x + " ");
    }
}
```
```Python
N, K = map(int, input().split())

arr = list(map(int, input().split()))

ans = []

for start in range(0, N, K):
    end = min(start + K, N)

    for i in range(end - 1, start - 1, -1):
        ans.append(arr[i])

for x in ans:
    print(x, end=" ")
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] first = Console.ReadLine().Split();

        int N = int.Parse(first[0]);
        int K = int.Parse(first[1]);

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);
        int[] ans = new int[N];

        int index = 0;

        for (int start = 0; start < N; start += K)
        {
            int end = Math.Min(start + K - 1, N - 1);

            for (int i = end; i >= start; i--)
                ans[index++] = arr[i];
        }

        foreach (int x in ans)
            Console.Write(x + " ");
    }
}
```

### Output
For Input:
8 3
1 2 3 4 5 6 7 8

Output:
3 2 1 6 5 4 8 7

# Time Complexity
O(N)

# Space Complexity
O(N)

## Approach 2: In-place Two Pointer Reversal (Recommended)

### Algorithm

1. Read the integers `N` and `K`.
2. Read the array.
3. Traverse the array group by group.
4. For each group:

- Set `left` to the first index of the group.
- Set `right` to the last index of the group (or `N - 1` for the last incomplete group).
- While `left < right`:
- Swap the elements.
- Move both pointers towards the center.

1. Print the modified array.

```C
#include <stdio.h>

int main()
{
    int N, K;
    scanf("%d %d", &N, &K);

    int arr[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    for (int start = 0; start < N; start += K)
    {
        int left = start;
        int right = start + K - 1;

        if (right >= N)
            right = N - 1;

        while (left < right)
        {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;

            left++;
            right--;
        }
    }

    for (int i = 0; i < N; i++)
        printf("%d ", arr[i]);

    return 0;
}
```
```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int main()
{
    int N, K;
    cin >> N >> K;

    int arr[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    for (int start = 0; start < N; start += K)
    {
        int left = start;
        int right = min(start + K - 1, N - 1);

        while (left < right)
        {
            swap(arr[left], arr[right]);
            left++;
            right--;
        }
    }

    for (int i = 0; i < N; i++)
        cout << arr[i] << " ";

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
        int K = sc.nextInt();

        int[] arr = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        for (int start = 0; start < N; start += K)
        {
            int left = start;
            int right = Math.min(start + K - 1, N - 1);

            while (left < right)
            {
                int temp = arr[left];
                arr[left] = arr[right];
                arr[right] = temp;

                left++;
                right--;
            }
        }

        for (int x : arr)
            System.out.print(x + " ");
    }
}
```
```Python
N, K = map(int, input().split())

arr = list(map(int, input().split()))

for start in range(0, N, K):

    left = start
    right = min(start + K - 1, N - 1)

    while left < right:
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1

for x in arr:
    print(x, end=" ")
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] first = Console.ReadLine().Split();

        int N = int.Parse(first[0]);
        int K = int.Parse(first[1]);

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        for (int start = 0; start < N; start += K)
        {
            int left = start;
            int right = Math.Min(start + K - 1, N - 1);

            while (left < right)
            {
                int temp = arr[left];
                arr[left] = arr[right];
                arr[right] = temp;

                left++;
                right--;
            }
        }

        foreach (int x in arr)
            Console.Write(x + " ");
    }
}
```

### Output
For Input:
8 3
1 2 3 4 5 6 7 8

Output:
3 2 1 6 5 4 8 7

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




