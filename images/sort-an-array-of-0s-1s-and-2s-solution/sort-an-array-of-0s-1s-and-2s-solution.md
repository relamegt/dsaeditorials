# Sort an Array of 0s, 1s, and 2s - Solution

## Problem Statement

Given an array `arr[]` of `N` integers containing only `0`s, `1`s, and `2`s, sort the array in non-decreasing order.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print the sorted array as `N` space-separated integers.

## Explanation

There are two common approaches to solve this problem.

- **Counting Sort:** Count the number of `0`s, `1`s, and `2`s, then overwrite the array accordingly.
- **Dutch National Flag Algorithm (Recommended):** Use three pointers to sort the array in a single traversal without counting.

For example,

Input: `0 2 1 2 0`

Sorted array: `0 0 1 2 2`

<approaches>
## Approach 1: Counting Sort

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize three counters:

- `count0 = 0`
- `count1 = 0`
- `count2 = 0`

1. Traverse the array once.
2. For every element:

- If it is `0`, increment `count0`.
- If it is `1`, increment `count1`.
- Otherwise increment `count2`.

1. Overwrite the array:

- Fill `count0` positions with `0`.
- Fill `count1` positions with `1`.
- Fill `count2` positions with `2`.

1. Print the modified array.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    int arr[N];
    int count0 = 0, count1 = 0, count2 = 0;

    for (int i = 0; i < N; i++)
    {
        scanf("%d", &arr[i]);

        if (arr[i] == 0)
            count0++;
        else if (arr[i] == 1)
            count1++;
        else
            count2++;
    }

    int index = 0;

    while (count0--)
        arr[index++] = 0;

    while (count1--)
        arr[index++] = 1;

    while (count2--)
        arr[index++] = 2;

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
    int count0 = 0, count1 = 0, count2 = 0;

    for (int i = 0; i < N; i++)
    {
        cin >> arr[i];

        if (arr[i] == 0)
            count0++;
        else if (arr[i] == 1)
            count1++;
        else
            count2++;
    }

    int index = 0;

    while (count0--)
        arr[index++] = 0;

    while (count1--)
        arr[index++] = 1;

    while (count2--)
        arr[index++] = 2;

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

        int count0 = 0, count1 = 0, count2 = 0;

        for (int i = 0; i < N; i++)
        {
            arr[i] = sc.nextInt();

            if (arr[i] == 0)
                count0++;
            else if (arr[i] == 1)
                count1++;
            else
                count2++;
        }

        int index = 0;

        while (count0-- > 0)
            arr[index++] = 0;

        while (count1-- > 0)
            arr[index++] = 1;

        while (count2-- > 0)
            arr[index++] = 2;

        for (int x : arr)
            System.out.print(x + " ");
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

count0 = arr.count(0)
count1 = arr.count(1)
count2 = arr.count(2)

index = 0

for _ in range(count0):
    arr[index] = 0
    index += 1

for _ in range(count1):
    arr[index] = 1
    index += 1

for _ in range(count2):
    arr[index] = 2
    index += 1

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

        int count0 = 0, count1 = 0, count2 = 0;

        foreach (int x in arr)
        {
            if (x == 0)
                count0++;
            else if (x == 1)
                count1++;
            else
                count2++;
        }

        int index = 0;

        while (count0-- > 0)
            arr[index++] = 0;

        while (count1-- > 0)
            arr[index++] = 1;

        while (count2-- > 0)
            arr[index++] = 2;

        Console.Write(string.Join(" ", arr));
    }
}
```

### Output
For Input:
5
0 2 1 2 0

Output:
0 0 1 2 2

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Dutch National Flag Algorithm (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize three pointers:

- `low = 0`
- `mid = 0`
- `high = N - 1`

1. Repeat while `mid <= high`:

- If `arr[mid] == 0`:
- Swap `arr[low]` and `arr[mid]`.
- Increment both `low` and `mid`.
- Else if `arr[mid] == 1`:
- Increment `mid`.
- Else (`arr[mid] == 2`):
- Swap `arr[mid]` and `arr[high]`.
- Decrement `high`.
- Do **not** increment `mid` because the swapped element needs to be checked.

1. Print the sorted array.

```C
#include <stdio.h>

void swap(int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main()
{
    int N;
    scanf("%d", &N);

    int arr[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    int low = 0, mid = 0, high = N - 1;

    while (mid <= high)
    {
        if (arr[mid] == 0)
        {
            swap(&arr[low], &arr[mid]);
            low++;
            mid++;
        }
        else if (arr[mid] == 1)
        {
            mid++;
        }
        else
        {
            swap(&arr[mid], &arr[high]);
            high--;
        }
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

    int low = 0, mid = 0, high = N - 1;

    while (mid <= high)
    {
        if (arr[mid] == 0)
        {
            swap(arr[low], arr[mid]);
            low++;
            mid++;
        }
        else if (arr[mid] == 1)
        {
            mid++;
        }
        else
        {
            swap(arr[mid], arr[high]);
            high--;
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

        int[] arr = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        int low = 0, mid = 0, high = N - 1;

        while (mid <= high)
        {
            if (arr[mid] == 0)
            {
                int temp = arr[low];
                arr[low] = arr[mid];
                arr[mid] = temp;
                low++;
                mid++;
            }
            else if (arr[mid] == 1)
            {
                mid++;
            }
            else
            {
                int temp = arr[mid];
                arr[mid] = arr[high];
                arr[high] = temp;
                high--;
            }
        }

        for (int x : arr)
            System.out.print(x + " ");
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

low = 0
mid = 0
high = N - 1

while mid <= high:
    if arr[mid] == 0:
        arr[low], arr[mid] = arr[mid], arr[low]
        low += 1
        mid += 1
    elif arr[mid] == 1:
        mid += 1
    else:
        arr[mid], arr[high] = arr[high], arr[mid]
        high -= 1

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

        int low = 0, mid = 0, high = N - 1;

        while (mid <= high)
        {
            if (arr[mid] == 0)
            {
                int temp = arr[low];
                arr[low] = arr[mid];
                arr[mid] = temp;
                low++;
                mid++;
            }
            else if (arr[mid] == 1)
            {
                mid++;
            }
            else
            {
                int temp = arr[mid];
                arr[mid] = arr[high];
                arr[high] = temp;
                high--;
            }
        }

        Console.Write(string.Join(" ", arr));
    }
}
```

### Output
For Input:
5
0 2 1 2 0

Output:
0 0 1 2 2

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




