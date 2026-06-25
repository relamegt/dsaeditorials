# Reverse an Array - Solution

## Problem Statement

Given an array `arr[]` of size `N`, reverse the array in-place and print the result.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print the reversed array as `N` space-separated integers on a single line.

## Explanation

There are two common approaches to reverse an array.

- **Using an Extra Array:** Copy the elements from the original array into another array in reverse order, then print the new array.
- **Using Two Pointers (Recommended):** Place one pointer at the beginning and another at the end of the array. Swap the elements at these positions and move the pointers toward each other until they meet.

For example, when the array is: `1 2 3 4 5`

- Swap `1` and `5`
- Swap `2` and `4`
- `3` remains unchanged

The reversed array becomes: `5 4 3 2 1`

Output: 5 4 3 2 1

<approaches>
## Approach 1: Using an Extra Array

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Create another array of size `N`.
4. Traverse the original array from the last element to the first.
5. Copy each element into the new array.
6. Print the new array.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    int arr[N], rev[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    int index = 0;

    for (int i = N - 1; i >= 0; i--)
        rev[index++] = arr[i];

    for (int i = 0; i < N; i++)
        printf("%d ", rev[i]);

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

    int arr[N], rev[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    int index = 0;

    for (int i = N - 1; i >= 0; i--)
        rev[index++] = arr[i];

    for (int i = 0; i < N; i++)
        cout << rev[i] << " ";

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
        int[] rev = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        int index = 0;

        for (int i = N - 1; i >= 0; i--)
            rev[index++] = arr[i];

        for (int i = 0; i < N; i++)
            System.out.print(rev[i] + " ");
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

rev = []

for i in range(N - 1, -1, -1):
    rev.append(arr[i])

for x in rev:
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
        int[] rev = new int[N];

        int index = 0;

        for (int i = N - 1; i >= 0; i--)
            rev[index++] = arr[i];

        for (int i = 0; i < N; i++)
            Console.Write(rev[i] + " ");
    }
}
```

### Output
For Input:
5
1 2 3 4 5

Output:
5 4 3 2 1

# Time Complexity
O(N)

# Space Complexity
O(N)

## Approach 2: Using Two Pointers (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize two pointers:

- `left = 0`
- `right = N - 1`

1. While `left < right`:

- Swap `arr[left]` and `arr[right]`.
- Increment `left`.
- Decrement `right`.

1. Print the modified array.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    int arr[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    int left = 0;
    int right = N - 1;

    while (left < right)
    {
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;

        left++;
        right--;
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

    int left = 0;
    int right = N - 1;

    while (left < right)
    {
        swap(arr[left], arr[right]);

        left++;
        right--;
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

        int left = 0;
        int right = N - 1;

        while (left < right)
        {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;

            left++;
            right--;
        }

        for (int x : arr)
            System.out.print(x + " ");
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

left = 0
right = N - 1

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
        int N = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int left = 0;
        int right = N - 1;

        while (left < right)
        {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;

            left++;
            right--;
        }

        foreach (int x in arr)
            Console.Write(x + " ");
    }
}
```

### Output
For Input:
5
1 2 3 4 5

Output:
5 4 3 2 1

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




