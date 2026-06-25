# Leaders in an Array - Solution

## Problem Statement

Given an array `arr[]` of `N` integers, print all the leaders in the array.

An element is a leader if it is **strictly greater** than all elements to its right. The rightmost element is always a leader.

Print the leaders in the order they appear in the array.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print all leaders separated by spaces on a single line.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** For every element, check all the elements to its right. If none of them is greater than or equal to the current element, then it is a leader.
- **Traverse from Right (Recommended):** Start from the last element, which is always a leader. Keep track of the maximum element seen so far while moving from right to left. Whenever the current element is greater than this maximum, it is also a leader.

For example, when the array is: `16 17 4 3 5 2`

- `2` is a leader.
- `5 > 2`, so `5` is a leader.
- `17 > 5`, so `17` is a leader.

Printing them in their original order gives: `17 5 2`

Output: 17 5 2

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Traverse every element from left to right.
4. For each element, check every element to its right.
5. If a greater than or equal element exists, it is not a leader.
6. Otherwise, print the element.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    int arr[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    for (int i = 0; i < N; i++)
    {
        int leader = 1;

        for (int j = i + 1; j < N; j++)
        {
            if (arr[j] >= arr[i])
            {
                leader = 0;
                break;
            }
        }

        if (leader)
            printf("%d ", arr[i]);
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

    int arr[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    for (int i = 0; i < N; i++)
    {
        bool leader = true;

        for (int j = i + 1; j < N; j++)
        {
            if (arr[j] >= arr[i])
            {
                leader = false;
                break;
            }
        }

        if (leader)
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

        int[] arr = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        for (int i = 0; i < N; i++)
        {
            boolean leader = true;

            for (int j = i + 1; j < N; j++)
            {
                if (arr[j] >= arr[i])
                {
                    leader = false;
                    break;
                }
            }

            if (leader)
                System.out.print(arr[i] + " ");
        }
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

for i in range(N):
    leader = True

    for j in range(i + 1, N):
        if arr[j] >= arr[i]:
            leader = False
            break

    if leader:
        print(arr[i], end=" ")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        for (int i = 0; i < N; i++)
        {
            bool leader = true;

            for (int j = i + 1; j < N; j++)
            {
                if (arr[j] >= arr[i])
                {
                    leader = false;
                    break;
                }
            }

            if (leader)
                Console.Write(arr[i] + " ");
        }
    }
}
```

### Output
For Input:
6
16 17 4 3 5 2

Output:
17 5 2

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Traverse from Right (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Initialize `maxRight` as the last element.
4. Store the last element as the first leader.
5. Traverse the array from right to left.
6. If the current element is greater than `maxRight`:

- It is a leader.
- Store it.
- Update `maxRight`.

1. Since leaders are collected from right to left, print them in reverse order.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    int arr[N], leaders[N];
    int count = 0;

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    int maxRight = arr[N - 1];
    leaders[count++] = maxRight;

    for (int i = N - 2; i >= 0; i--)
    {
        if (arr[i] > maxRight)
        {
            maxRight = arr[i];
            leaders[count++] = arr[i];
        }
    }

    for (int i = count - 1; i >= 0; i--)
        printf("%d ", leaders[i]);

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

    vector<int> arr(N);
    vector<int> leaders;

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    int maxRight = arr[N - 1];
    leaders.push_back(maxRight);

    for (int i = N - 2; i >= 0; i--)
    {
        if (arr[i] > maxRight)
        {
            maxRight = arr[i];
            leaders.push_back(arr[i]);
        }
    }

    for (int i = leaders.size() - 1; i >= 0; i--)
        cout << leaders[i] << " ";

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

        ArrayList<Integer> leaders = new ArrayList<>();

        int maxRight = arr[N - 1];
        leaders.add(maxRight);

        for (int i = N - 2; i >= 0; i--)
        {
            if (arr[i] > maxRight)
            {
                maxRight = arr[i];
                leaders.add(arr[i]);
            }
        }

        for (int i = leaders.size() - 1; i >= 0; i--)
            System.out.print(leaders.get(i) + " ");
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

leaders = []

maxRight = arr[-1]
leaders.append(maxRight)

for i in range(N - 2, -1, -1):
    if arr[i] > maxRight:
        maxRight = arr[i]
        leaders.append(arr[i])

for x in reversed(leaders):
    print(x, end=" ")
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        List<int> leaders = new List<int>();

        int maxRight = arr[N - 1];
        leaders.Add(maxRight);

        for (int i = N - 2; i >= 0; i--)
        {
            if (arr[i] > maxRight)
            {
                maxRight = arr[i];
                leaders.Add(arr[i]);
            }
        }

        for (int i = leaders.Count - 1; i >= 0; i--)
            Console.Write(leaders[i] + " ");
    }
}
```

### Output
For Input:
6
16 17 4 3 5 2

Output:
17 5 2

# Time Complexity
O(N)

# Space Complexity
O(N)

</approaches>




