# Largest and Second Largest Element - Solution

## Problem Statement

Given an array `arr[]` of size `N`, find the largest and the second largest **distinct** elements in the array.
If no second largest element exists (all elements are the same, or `N = 1`), print `-1` in its place.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print two space-separated integers representing the largest element and the second largest distinct element.
If the second largest element does not exist, print the largest element followed by `-1`.

## Explanation

There are two common approaches to solve this problem.

- **Sorting:** Sort the array in ascending order. The last element is the largest. Traverse backward to find the first element different from the largest.
- **Single Traversal (Recommended):** Traverse the array once while maintaining the largest and second largest distinct elements. Update them whenever a larger or second larger value is found.

For example, when the array is:  `3 1 4 1 5`

- Largest = `5`
- Second Largest = `4`

Output: 5 4

<approaches>
## Approach 1: Sorting

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Sort the array in ascending order.
4. The last element is the largest.
5. Traverse backwards from the second last element.
6. Find the first element different from the largest.
7. If found, it is the second largest.
8. Otherwise, print `-1` as the second largest.

```C
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a, const void *b)
{
    return (*(int *)a - *(int *)b);
}

int main()
{
    int N;
    scanf("%d", &N);

    int arr[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    qsort(arr, N, sizeof(int), compare);

    int largest = arr[N - 1];
    int secondLargest = -1;

    for (int i = N - 2; i >= 0; i--)
    {
        if (arr[i] != largest)
        {
            secondLargest = arr[i];
            break;
        }
    }

    printf("%d %d", largest, secondLargest);

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

    int arr[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    sort(arr, arr + N);

    int largest = arr[N - 1];
    int secondLargest = -1;

    for (int i = N - 2; i >= 0; i--)
    {
        if (arr[i] != largest)
        {
            secondLargest = arr[i];
            break;
        }
    }

    cout << largest << " " << secondLargest;

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

        Arrays.sort(arr);

        int largest = arr[N - 1];
        int secondLargest = -1;

        for (int i = N - 2; i >= 0; i--)
        {
            if (arr[i] != largest)
            {
                secondLargest = arr[i];
                break;
            }
        }

        System.out.print(largest + " " + secondLargest);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

arr.sort()

largest = arr[-1]
secondLargest = -1

for i in range(N - 2, -1, -1):
    if arr[i] != largest:
        secondLargest = arr[i]
        break

print(largest, secondLargest)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        Array.Sort(arr);

        int largest = arr[N - 1];
        int secondLargest = -1;

        for (int i = N - 2; i >= 0; i--)
        {
            if (arr[i] != largest)
            {
                secondLargest = arr[i];
                break;
            }
        }

        Console.Write(largest + " " + secondLargest);
    }
}
```

### Output
For Input:
5
3 1 4 1 5

Output:
5 4

# Time Complexity
O(N log N)

# Space Complexity
O(1)

## Approach 2: Single Traversal (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize:

- `largest = minimum possible integer`
- `secondLargest = minimum possible integer`

1. Traverse every element in the array.
2. For each element:

- If it is greater than `largest`:
- Assign `largest` to `secondLargest`.
- Update `largest`.
- Else if it is different from `largest` and greater than `secondLargest`:
- Update `secondLargest`.

1. If `secondLargest` was never updated, print `largest` and `-1`.
2. Otherwise, print `largest` and `secondLargest`.

```C
#include <stdio.h>
#include <limits.h>

int main()
{
    int N;
    scanf("%d", &N);

    int largest = INT_MIN;
    int secondLargest = INT_MIN;

    for (int i = 0; i < N; i++)
    {
        int x;
        scanf("%d", &x);

        if (x > largest)
        {
            secondLargest = largest;
            largest = x;
        }
        else if (x != largest && x > secondLargest)
        {
            secondLargest = x;
        }
    }

    if (secondLargest == INT_MIN)
        secondLargest = -1;

    printf("%d %d", largest, secondLargest);

    return 0;
}
```
```cpp
#include <iostream>
#include <climits>
using namespace std;

int main()
{
    int N;
    cin >> N;

    int largest = INT_MIN;
    int secondLargest = INT_MIN;

    for (int i = 0; i < N; i++)
    {
        int x;
        cin >> x;

        if (x > largest)
        {
            secondLargest = largest;
            largest = x;
        }
        else if (x != largest && x > secondLargest)
        {
            secondLargest = x;
        }
    }

    if (secondLargest == INT_MIN)
        secondLargest = -1;

    cout << largest << " " << secondLargest;

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

        int largest = Integer.MIN_VALUE;
        int secondLargest = Integer.MIN_VALUE;

        for (int i = 0; i < N; i++)
        {
            int x = sc.nextInt();

            if (x > largest)
            {
                secondLargest = largest;
                largest = x;
            }
            else if (x != largest && x > secondLargest)
            {
                secondLargest = x;
            }
        }

        if (secondLargest == Integer.MIN_VALUE)
            secondLargest = -1;

        System.out.print(largest + " " + secondLargest);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

largest = float("-inf")
secondLargest = float("-inf")

for x in arr:
    if x > largest:
        secondLargest = largest
        largest = x
    elif x != largest and x > secondLargest:
        secondLargest = x

if secondLargest == float("-inf"):
    secondLargest = -1

print(largest, secondLargest)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int largest = int.MinValue;
        int secondLargest = int.MinValue;

        foreach (int x in arr)
        {
            if (x > largest)
            {
                secondLargest = largest;
                largest = x;
            }
            else if (x != largest && x > secondLargest)
            {
                secondLargest = x;
            }
        }

        if (secondLargest == int.MinValue)
            secondLargest = -1;

        Console.Write(largest + " " + secondLargest);
    }
}
```

### Output
For Input:
5
3 1 4 1 5

Output:
5 4

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




