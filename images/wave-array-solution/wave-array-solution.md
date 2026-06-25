# Wave Array - Solution

## Problem Statement

Given a sorted array `arr[]` of distinct integers in ascending order, rearrange the elements into a wave-like array.

A wave array satisfies:

`arr[0] >= arr[1] <= arr[2] >= arr[3] <= arr[4] >= ...`

If multiple answers are possible, print any valid wave arrangement.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers in ascending order.

### Output Format

Print `N` space-separated integers forming a valid wave array.

## Explanation

There are two common approaches to solve this problem.

- **Using an Extra Array:** Create a new array and place every adjacent pair in reversed order.
- **Adjacent Swapping (Recommended):** Since the array is already sorted, simply swap every pair of adjacent elements `(0,1), (2,3), (4,5)...`. This automatically satisfies the wave property and is done in-place.

For example, when the array is: `1 2 3 4 5 6`

Swap adjacent pairs:

- `(1, 2)` → `(2, 1)`
- `(3, 4)` → `(4, 3)`
- `(5, 6)` → `(6, 5)`

Result: `2 1 4 3 6 5`

Output: 2 1 4 3 6 5

<approaches>
## Approach 1: Using an Extra Array

### Algorithm

1. Read the integer `N`.
2. Read the sorted array.
3. Create another array of size `N`.
4. Traverse the array two elements at a time.
5. If two elements exist:

- Place the second element first.
- Place the first element next.

1. If only one element remains, copy it directly.
2. Print the new array.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    int arr[N], ans[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    int index = 0;

    for (int i = 0; i < N; i += 2)
    {
        if (i + 1 < N)
        {
            ans[index++] = arr[i + 1];
            ans[index++] = arr[i];
        }
        else
        {
            ans[index++] = arr[i];
        }
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
    int N;
    cin >> N;

    int arr[N], ans[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    int index = 0;

    for (int i = 0; i < N; i += 2)
    {
        if (i + 1 < N)
        {
            ans[index++] = arr[i + 1];
            ans[index++] = arr[i];
        }
        else
        {
            ans[index++] = arr[i];
        }
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

        int[] arr = new int[N];
        int[] ans = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        int index = 0;

        for (int i = 0; i < N; i += 2)
        {
            if (i + 1 < N)
            {
                ans[index++] = arr[i + 1];
                ans[index++] = arr[i];
            }
            else
            {
                ans[index++] = arr[i];
            }
        }

        for (int x : ans)
            System.out.print(x + " ");
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

ans = []

for i in range(0, N, 2):
    if i + 1 < N:
        ans.append(arr[i + 1])
        ans.append(arr[i])
    else:
        ans.append(arr[i])

print(*ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);
        int[] ans = new int[N];

        int index = 0;

        for (int i = 0; i < N; i += 2)
        {
            if (i + 1 < N)
            {
                ans[index++] = arr[i + 1];
                ans[index++] = arr[i];
            }
            else
            {
                ans[index++] = arr[i];
            }
        }

        foreach (int x in ans)
            Console.Write(x + " ");
    }
}
```

### Output
For Input:
6
1 2 3 4 5 6

Output:
2 1 4 3 6 5

# Time Complexity
O(N)

# Space Complexity
O(N)

## Approach 2: Adjacent Swapping (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the sorted array.
3. Traverse the array with a step of `2`.
4. For every pair of adjacent elements:

- Swap `arr[i]` and `arr[i+1]`.

1. Continue until all adjacent pairs are processed.
2. Print the modified array.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    int arr[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    for (int i = 0; i + 1 < N; i += 2)
    {
        int temp = arr[i];
        arr[i] = arr[i + 1];
        arr[i + 1] = temp;
    }

    for (int i = 0; i < N; i++)
        printf("%d ", arr[i]);

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

    for (int i = 0; i + 1 < N; i += 2)
        swap(arr[i], arr[i + 1]);

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

        int[] arr = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        for (int i = 0; i + 1 < N; i += 2)
        {
            int temp = arr[i];
            arr[i] = arr[i + 1];
            arr[i + 1] = temp;
        }

        for (int x : arr)
            System.out.print(x + " ");
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

for i in range(0, N - 1, 2):
    arr[i], arr[i + 1] = arr[i + 1], arr[i]

print(*arr)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        for (int i = 0; i + 1 < N; i += 2)
        {
            int temp = arr[i];
            arr[i] = arr[i + 1];
            arr[i + 1] = temp;
        }

        foreach (int x in arr)
            Console.Write(x + " ");
    }
}
```

### Output
For Input:
6
1 2 3 4 5 6

Output:
2 1 4 3 6 5

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




