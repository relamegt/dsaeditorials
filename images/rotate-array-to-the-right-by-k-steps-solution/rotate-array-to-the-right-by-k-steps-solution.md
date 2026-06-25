# Rotate Array to the Right by K Steps - Solution

## Problem Statement

Given an array `arr[]` of size `N` and an integer `K`, rotate the array to the right by `K` steps.

A right rotation by one step moves the last element to the front.

### Input Format

First line: Two integers `N` and `K`.

Second line: `N` space-separated integers.

### Output Format

Print the rotated array as `N` space-separated integers on a single line.

## Explanation

There are two common approaches to solve this problem.

- **Using an Extra Array:** Store the rotated elements in another array using their new positions, then print the new array.
- **Reversal Algorithm (Recommended):** Reverse the entire array, then reverse the first `K` elements, and finally reverse the remaining `N-K` elements. This performs the rotation in-place.

For example, when: `N = 7, K = 3`
Original array: `1 2 3 4 5 6 7`
After rotation: `5 6 7 1 2 3 4`

Output:  6 7 1 2 3 4

<approaches>
## Approach 1: Using an Extra Array

### Algorithm

1. Read the integers `N` and `K`.
2. Compute `K = K % N`.
3. Read the array.
4. Create another array of size `N`.
5. For every index `i`:

- Compute the new position as `(i + K) % N`.
- Place the current element into that position.

1. Print the new array.

```C
#include <stdio.h>

int main()
{
    int N, K;
    scanf("%d %d", &N, &K);

    K %= N;

    int arr[N], ans[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    for (int i = 0; i < N; i++)
        ans[(i + K) % N] = arr[i];

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

    K %= N;

    int arr[N], ans[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    for (int i = 0; i < N; i++)
        ans[(i + K) % N] = arr[i];

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

        K %= N;

        int[] arr = new int[N];
        int[] ans = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        for (int i = 0; i < N; i++)
            ans[(i + K) % N] = arr[i];

        for (int x : ans)
            System.out.print(x + " ");
    }
}
```
```Python
N, K = map(int, input().split())

K %= N

arr = list(map(int, input().split()))

ans = [0] * N

for i in range(N):
    ans[(i + K) % N] = arr[i]

print(*ans)
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

        K %= N;

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);
        int[] ans = new int[N];

        for (int i = 0; i < N; i++)
            ans[(i + K) % N] = arr[i];

        foreach (int x in ans)
            Console.Write(x + " ");
    }
}
```

### Output
For Input:
7 3
1 2 3 4 5 6 7

Output:
5 6 7 1 2 3 4

# Time Complexity
O(N)

# Space Complexity
O(N)

## Approach 2: Reversal Algorithm (Recommended)

### Algorithm

1. Read the integers `N` and `K`.
2. Compute `K = K % N`.
3. Read the array.
4. Reverse the entire array.
5. Reverse the first `K` elements.
6. Reverse the remaining `N-K` elements.
7. Print the rotated array.

```C
#include <stdio.h>

void reverse(int arr[], int left, int right)
{
    while (left < right)
    {
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;

        left++;
        right--;
    }
}

int main()
{
    int N, K;
    scanf("%d %d", &N, &K);

    K %= N;

    int arr[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    reverse(arr, 0, N - 1);
    reverse(arr, 0, K - 1);
    reverse(arr, K, N - 1);

    for (int i = 0; i < N; i++)
        printf("%d ", arr[i]);

    return 0;
}
```
```cpp
#include <iostream>
#include <algorithm>
using namespace std;

void reverseArray(int arr[], int left, int right)
{
    while (left < right)
    {
        swap(arr[left], arr[right]);
        left++;
        right--;
    }
}

int main()
{
    int N, K;
    cin >> N >> K;

    K %= N;

    int arr[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    reverseArray(arr, 0, N - 1);
    reverseArray(arr, 0, K - 1);
    reverseArray(arr, K, N - 1);

    for (int i = 0; i < N; i++)
        cout << arr[i] << " ";

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    static void reverse(int[] arr, int left, int right)
    {
        while (left < right)
        {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;

            left++;
            right--;
        }
    }

    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();
        int K = sc.nextInt();

        K %= N;

        int[] arr = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        reverse(arr, 0, N - 1);
        reverse(arr, 0, K - 1);
        reverse(arr, K, N - 1);

        for (int x : arr)
            System.out.print(x + " ");
    }
}
```
```Python
def reverse(arr, left, right):
    while left < right:
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1

N, K = map(int, input().split())

K %= N

arr = list(map(int, input().split()))

reverse(arr, 0, N - 1)
reverse(arr, 0, K - 1)
reverse(arr, K, N - 1)

print(*arr)
```
```C#
using System;

class Program
{
    static void Reverse(int[] arr, int left, int right)
    {
        while (left < right)
        {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;

            left++;
            right--;
        }
    }

    static void Main()
    {
        string[] first = Console.ReadLine().Split();

        int N = int.Parse(first[0]);
        int K = int.Parse(first[1]);

        K %= N;

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        Reverse(arr, 0, N - 1);
        Reverse(arr, 0, K - 1);
        Reverse(arr, K, N - 1);

        foreach (int x in arr)
            Console.Write(x + " ");
    }
}
```

### Output
For Input:
7 3
1 2 3 4 5 6 7

Output:
5 6 7 1 2 3 4

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




