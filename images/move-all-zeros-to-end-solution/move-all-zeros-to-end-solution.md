# Move All Zeros to End - Solution

## Problem Statement

Given an array `arr[]` of size `N`, move all `0`s to the end of the array while maintaining the relative order of all non-zero elements.

The operation must be performed **in-place** without using extra space for another array.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print the modified array as `N` space-separated integers on a single line.

## Explanation

There are two common approaches to solve this problem.

- **Using an Extra Array:** Store all non-zero elements in a new array, then append all zeros at the end.
- **Two Pointer In-place Method (Recommended):** Traverse the array while maintaining the position where the next non-zero element should be placed. Swap non-zero elements into their correct positions and leave all zeros at the end.

For example, when the array is: `0 1 0 3 12 0 0 5`
The non-zero elements are: `1 3 12 5`
After moving all zeros to the end, the array becomes: `1 3 12 5 0 0 0 0`

Output: 1 3 12 5 0 0 0 0

<approaches>
## Approach 1: Using an Extra Array

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Create another array.
4. Traverse the original array and copy every non-zero element into the new array.
5. Count the number of non-zero elements copied.
6. Fill the remaining positions of the new array with `0`.
7. Print the new array.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    int arr[N], ans[N];
    int index = 0;

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    for (int i = 0; i < N; i++)
    {
        if (arr[i] != 0)
            ans[index++] = arr[i];
    }

    while (index < N)
        ans[index++] = 0;

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
    int index = 0;

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    for (int i = 0; i < N; i++)
    {
        if (arr[i] != 0)
            ans[index++] = arr[i];
    }

    while (index < N)
        ans[index++] = 0;

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

        int index = 0;

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        for (int i = 0; i < N; i++)
        {
            if (arr[i] != 0)
                ans[index++] = arr[i];
        }

        while (index < N)
            ans[index++] = 0;

        for (int x : ans)
            System.out.print(x + " ");
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

ans = []

for x in arr:
    if x != 0:
        ans.append(x)

while len(ans) < N:
    ans.append(0)

for x in ans:
    print(x, end=" ")
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

        foreach (int x in arr)
        {
            if (x != 0)
                ans[index++] = x;
        }

        while (index < N)
            ans[index++] = 0;

        foreach (int x in ans)
            Console.Write(x + " ");
    }
}
```

### Output
For Input:
8
0 1 0 3 12 0 0 5

Output:
1 3 12 5 0 0 0 0

# Time Complexity
O(N)

# Space Complexity
O(N)

## Approach 2: Two Pointer In-place Method (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize `index = 0`.
4. Traverse the array from left to right.
5. Whenever a non-zero element is found:

- Swap it with the element at position `index`.
- Increment `index`.

1. After traversal, all non-zero elements occupy the beginning of the array in their original order, and all zeros automatically move to the end.
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

    int index = 0;

    for (int i = 0; i < N; i++)
    {
        if (arr[i] != 0)
        {
            int temp = arr[index];
            arr[index] = arr[i];
            arr[i] = temp;
            index++;
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

    int index = 0;

    for (int i = 0; i < N; i++)
    {
        if (arr[i] != 0)
        {
            swap(arr[index], arr[i]);
            index++;
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

        int index = 0;

        for (int i = 0; i < N; i++)
        {
            if (arr[i] != 0)
            {
                int temp = arr[index];
                arr[index] = arr[i];
                arr[i] = temp;
                index++;
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

index = 0

for i in range(N):
    if arr[i] != 0:
        arr[index], arr[i] = arr[i], arr[index]
        index += 1

for x in arr:
    print(x, end=" ")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int index = 0;

        for (int i = 0; i < N; i++)
        {
            if (arr[i] != 0)
            {
                int temp = arr[index];
                arr[index] = arr[i];
                arr[i] = temp;
                index++;
            }
        }

        foreach (int x in arr)
            Console.Write(x + " ");
    }
}
```

### Output
For Input:
8
0 1 0 3 12 0 0 5

Output:
1 3 12 5 0 0 0 0

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




