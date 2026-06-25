# Alternates in an Array - Solution

## Problem Statement

Given an array `arr[]` of size `N`, return a new array containing the elements at even indices (0-indexed) of the array in the same order.

In other words, print the elements at positions `0, 2, 4, 6, ...`.

### Input Format

First line: Integer `N` — size of the array.

Second line: `N` space-separated integers.

### Output Format

Print the alternate elements (starting from index `0`) separated by spaces.

## Explanation

To solve this problem, we simply traverse the array by increasing the index by `2` each time.

Since we only visit indices `0, 2, 4, ...`, every printed element is at an even index.

For example, when the array is: `1 2 3 4`

- Index `0` → `1`
- Index `2` → `3`

Therefore, the output is: `1 3`

Output: 1 3

## Algorithm

1. Read the integer `N`.
2. Read the array of size `N`.
3. Traverse the array starting from index `0`.
4. Increase the index by `2` after every iteration.
5. Print the current element.
6. Continue until the index becomes greater than or equal to `N`.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    int arr[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    for (int i = 0; i < N; i += 2)
        printf("%d ", arr[i]);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    int N;
    cin >> N;

    int arr[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    for (int i = 0; i < N; i += 2)
        cout << arr[i] << " ";

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        int[] arr = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        for (int i = 0; i < N; i += 2)
            System.out.print(arr[i] + " ");
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

for i in range(0, N, 2):
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

        for (int i = 0; i < N; i += 2)
            Console.Write(arr[i] + " ");
    }
}
```

### Output
For Input:
4
1 2 3 4

Output:
1 3

# Time Complexity
O(N)

# Space Complexity
O(1)




