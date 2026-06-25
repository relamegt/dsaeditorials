# Third Largest Element - Solution

## Problem Statement

Given an array `arr[]` of size `N`, find the **third largest distinct** element in the array.
If the third largest element does not exist, print `-1`.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print a single integer representing the third largest distinct element. If it does not exist, print `-1`.

## Explanation

There are two common approaches to solve this problem.

- **Sorting:** Sort the array in ascending order. Traverse from the end while counting distinct elements. The third distinct element encountered is the answer.
- **Single Traversal (Recommended):** Traverse the array once while maintaining the largest, second largest, and third largest distinct elements. Update these values whenever a larger distinct element is found.

For example, when the array is: `12 13 1 10 34 1`
The distinct elements in descending order are: `34 13 12 10 1`
The third largest distinct element is: `12`
Output: 12

<approaches>
## Approach 1: Sorting

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Sort the array in ascending order.
4. Traverse the array from the last element towards the first.
5. Count distinct elements encountered.
6. When the third distinct element is found, print it.
7. If fewer than three distinct elements exist, print `-1`.

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

    int count = 1;
    int answer = -1;

    for (int i = N - 2; i >= 0; i--)
    {
        if (arr[i] != arr[i + 1])
        {
            count++;

            if (count == 3)
            {
                answer = arr[i];
                break;
            }
        }
    }

    printf("%d", answer);

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

    int count = 1;
    int answer = -1;

    for (int i = N - 2; i >= 0; i--)
    {
        if (arr[i] != arr[i + 1])
        {
            count++;

            if (count == 3)
            {
                answer = arr[i];
                break;
            }
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

        int[] arr = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        Arrays.sort(arr);

        int count = 1;
        int answer = -1;

        for (int i = N - 2; i >= 0; i--)
        {
            if (arr[i] != arr[i + 1])
            {
                count++;

                if (count == 3)
                {
                    answer = arr[i];
                    break;
                }
            }
        }

        System.out.print(answer);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

arr.sort()

count = 1
answer = -1

for i in range(N - 2, -1, -1):
    if arr[i] != arr[i + 1]:
        count += 1

        if count == 3:
            answer = arr[i]
            break

print(answer)
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

        int count = 1;
        int answer = -1;

        for (int i = N - 2; i >= 0; i--)
        {
            if (arr[i] != arr[i + 1])
            {
                count++;

                if (count == 3)
                {
                    answer = arr[i];
                    break;
                }
            }
        }

        Console.Write(answer);
    }
}
```

### Output
For Input:
6
12 13 1 10 34 1

Output:
12

# Time Complexity
O(N log N)

# Space Complexity
O(1)

## Approach 2: Single Traversal (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize:

- `first = minimum possible integer`
- `second = minimum possible integer`
- `third = minimum possible integer`

1. Traverse every element in the array.
2. For each element:

- If it is greater than `first`:
- Shift `first` to `second`.
- Shift `second` to `third`.
- Update `first`.
- Else if it is distinct from `first` and greater than `second`:
- Shift `second` to `third`.
- Update `second`.
- Else if it is distinct from both `first` and `second` and greater than `third`:
- Update `third`.

1. If `third` was never updated, print `-1`.
2. Otherwise, print `third`.

```C
#include <stdio.h>
#include <limits.h>

int main()
{
    int N;
    scanf("%d", &N);

    int first = INT_MIN;
    int second = INT_MIN;
    int third = INT_MIN;

    for (int i = 0; i < N; i++)
    {
        int x;
        scanf("%d", &x);

        if (x > first)
        {
            third = second;
            second = first;
            first = x;
        }
        else if (x != first && x > second)
        {
            third = second;
            second = x;
        }
        else if (x != first && x != second && x > third)
        {
            third = x;
        }
    }

    if (third == INT_MIN)
        printf("-1");
    else
        printf("%d", third);

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

    int first = INT_MIN;
    int second = INT_MIN;
    int third = INT_MIN;

    for (int i = 0; i < N; i++)
    {
        int x;
        cin >> x;

        if (x > first)
        {
            third = second;
            second = first;
            first = x;
        }
        else if (x != first && x > second)
        {
            third = second;
            second = x;
        }
        else if (x != first && x != second && x > third)
        {
            third = x;
        }
    }

    if (third == INT_MIN)
        cout << -1;
    else
        cout << third;

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

        int first = Integer.MIN_VALUE;
        int second = Integer.MIN_VALUE;
        int third = Integer.MIN_VALUE;

        for (int i = 0; i < N; i++)
        {
            int x = sc.nextInt();

            if (x > first)
            {
                third = second;
                second = first;
                first = x;
            }
            else if (x != first && x > second)
            {
                third = second;
                second = x;
            }
            else if (x != first && x != second && x > third)
            {
                third = x;
            }
        }

        if (third == Integer.MIN_VALUE)
            System.out.print(-1);
        else
            System.out.print(third);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

first = float("-inf")
second = float("-inf")
third = float("-inf")

for x in arr:
    if x > first:
        third = second
        second = first
        first = x
    elif x != first and x > second:
        third = second
        second = x
    elif x != first and x != second and x > third:
        third = x

if third == float("-inf"):
    print(-1)
else:
    print(third)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int first = int.MinValue;
        int second = int.MinValue;
        int third = int.MinValue;

        foreach (int x in arr)
        {
            if (x > first)
            {
                third = second;
                second = first;
                first = x;
            }
            else if (x != first && x > second)
            {
                third = second;
                second = x;
            }
            else if (x != first && x != second && x > third)
            {
                third = x;
            }
        }

        if (third == int.MinValue)
            Console.Write(-1);
        else
            Console.Write(third);
    }
}
```

### Output
For Input:
6
12 13 1 10 34 1

Output:
12

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




