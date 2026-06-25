# K-th Smallest Element of Two Sorted Arrays - Solution

## Problem Statement

Given two sorted arrays `arr1[]` and `arr2[]` of sizes `N` and `M`, and an integer `K`, find the K-th smallest element in the sorted order of all elements from both arrays combined.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers of `arr1`.

Third line: Integer `M`.

Fourth line: `M` space-separated integers of `arr2`.

Fifth line: Integer `K`.

### Output Format

Print a single integer representing the K-th smallest element.

## Explanation

There are two common approaches to solve this problem.

- **Merge Process:** Simulate the merge step of Merge Sort until the K-th element is reached.
- **Binary Search Partition (Recommended):** Use binary search on the smaller array to partition both arrays such that exactly `K` elements lie on the left side.

For example,

Input:

`arr1 = [2,3,6,7]`

`arr2 = [1,4,8,10]`

`K = 5`

Merged order:

`1 2 3 4 6 7 8 10`

The 5th smallest element is:

`6`

<approaches>
## Approach 1: Merge Process

### Algorithm

1. Read `N` and `arr1`.
2. Read `M` and `arr2`.
3. Read `K`.
4. Initialize two pointers:

- `i = 0`
- `j = 0`

1. Merge the arrays just like Merge Sort.
2. Count every extracted element.
3. When the count becomes `K`, print that element.
4. Stop the program.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr1[N];

    for(int i = 0; i < N; i++)
        scanf("%lld", &arr1[i]);

    int M;
    scanf("%d", &M);

    long long arr2[M];

    for(int i = 0; i < M; i++)
        scanf("%lld", &arr2[i]);

    int K;
    scanf("%d", &K);

    int i = 0, j = 0, count = 0;

    while(i < N && j < M)
    {
        long long value;

        if(arr1[i] <= arr2[j])
            value = arr1[i++];
        else
            value = arr2[j++];

        count++;

        if(count == K)
        {
            printf("%lld", value);
            return 0;
        }
    }

    while(i < N)
    {
        count++;

        if(count == K)
        {
            printf("%lld", arr1[i]);
            return 0;
        }

        i++;
    }

    while(j < M)
    {
        count++;

        if(count == K)
        {
            printf("%lld", arr2[j]);
            return 0;
        }

        j++;
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

    long long arr1[N];

    for(int i = 0; i < N; i++)
        cin >> arr1[i];

    int M;
    cin >> M;

    long long arr2[M];

    for(int i = 0; i < M; i++)
        cin >> arr2[i];

    int K;
    cin >> K;

    int i = 0, j = 0, count = 0;

    while(i < N && j < M)
    {
        long long value;

        if(arr1[i] <= arr2[j])
            value = arr1[i++];
        else
            value = arr2[j++];

        count++;

        if(count == K)
        {
            cout << value;
            return 0;
        }
    }

    while(i < N)
    {
        count++;

        if(count == K)
        {
            cout << arr1[i];
            return 0;
        }

        i++;
    }

    while(j < M)
    {
        count++;

        if(count == K)
        {
            cout << arr2[j];
            return 0;
        }

        j++;
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
        long[] arr1 = new long[N];

        for(int i = 0; i < N; i++)
            arr1[i] = sc.nextLong();

        int M = sc.nextInt();
        long[] arr2 = new long[M];

        for(int i = 0; i < M; i++)
            arr2[i] = sc.nextLong();

        int K = sc.nextInt();

        int i = 0, j = 0, count = 0;

        while(i < N && j < M)
        {
            long value;

            if(arr1[i] <= arr2[j])
                value = arr1[i++];
            else
                value = arr2[j++];

            count++;

            if(count == K)
            {
                System.out.print(value);
                return;
            }
        }

        while(i < N)
        {
            count++;

            if(count == K)
            {
                System.out.print(arr1[i]);
                return;
            }

            i++;
        }

        while(j < M)
        {
            count++;

            if(count == K)
            {
                System.out.print(arr2[j]);
                return;
            }

            j++;
        }
    }
}
```
```Python
N = int(input())

arr1 = list(map(int, input().split()))

M = int(input())

arr2 = list(map(int, input().split()))

K = int(input())

i = j = 0
count = 0

while i < N and j < M:
    if arr1[i] <= arr2[j]:
        value = arr1[i]
        i += 1
    else:
        value = arr2[j]
        j += 1

    count += 1

    if count == K:
        print(value)
        exit()

while i < N:
    count += 1

    if count == K:
        print(arr1[i])
        exit()

    i += 1

while j < M:
    count += 1

    if count == K:
        print(arr2[j])
        exit()

    j += 1
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr1 = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        int M = int.Parse(Console.ReadLine());

        long[] arr2 = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        int K = int.Parse(Console.ReadLine());

        int i = 0, j = 0, count = 0;

        while(i < N && j < M)
        {
            long value;

            if(arr1[i] <= arr2[j])
                value = arr1[i++];
            else
                value = arr2[j++];

            count++;

            if(count == K)
            {
                Console.Write(value);
                return;
            }
        }

        while(i < N)
        {
            count++;

            if(count == K)
            {
                Console.Write(arr1[i]);
                return;
            }

            i++;
        }

        while(j < M)
        {
            count++;

            if(count == K)
            {
                Console.Write(arr2[j]);
                return;
            }

            j++;
        }
    }
}
```

### Output
For Input:
4
2 3 6 7
4
1 4 8 10
5

Output:
6

# Time Complexity
O(K)

# Space Complexity
O(1)

## Approach 2: Binary Search Partition (Recommended)

### Algorithm

1. Ensure the first array is the smaller array.
2. Perform binary search on the smaller array.
3. Partition both arrays such that exactly `K` elements lie on the left.
4. Compute:

- `left1`, `right1`
- `left2`, `right2`

1. If:

- `left1 <= right2`
- `left2 <= right1`

     then the answer is `max(left1, left2)`.

1. Otherwise:

- Move binary search left or right accordingly.

1. Print the answer.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>
using namespace std;

int main()
{
    int N;
    cin >> N;

    vector<long long> a(N);

    for(int i = 0; i < N; i++)
        cin >> a[i];

    int M;
    cin >> M;

    vector<long long> b(M);

    for(int i = 0; i < M; i++)
        cin >> b[i];

    int K;
    cin >> K;

    if(N > M)
    {
        swap(a, b);
        swap(N, M);
    }

    int low = max(0, K - M);
    int high = min(K, N);

    while(low <= high)
    {
        int cut1 = (low + high) / 2;
        int cut2 = K - cut1;

        long long left1 = (cut1 == 0) ? LLONG_MIN : a[cut1 - 1];
        long long left2 = (cut2 == 0) ? LLONG_MIN : b[cut2 - 1];
        long long right1 = (cut1 == N) ? LLONG_MAX : a[cut1];
        long long right2 = (cut2 == M) ? LLONG_MAX : b[cut2];

        if(left1 <= right2 && left2 <= right1)
        {
            cout << max(left1, left2);
            return 0;
        }

        if(left1 > right2)
            high = cut1 - 1;
        else
            low = cut1 + 1;
    }

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    static long kth(long[] a, long[] b, int k)
    {
        if(a.length > b.length)
            return kth(b, a, k);

        int n = a.length;
        int m = b.length;

        int low = Math.max(0, k - m);
        int high = Math.min(k, n);

        while(low <= high)
        {
            int cut1 = (low + high) / 2;
            int cut2 = k - cut1;

            long left1 = (cut1 == 0) ? Long.MIN_VALUE : a[cut1 - 1];
            long left2 = (cut2 == 0) ? Long.MIN_VALUE : b[cut2 - 1];
            long right1 = (cut1 == n) ? Long.MAX_VALUE : a[cut1];
            long right2 = (cut2 == m) ? Long.MAX_VALUE : b[cut2];

            if(left1 <= right2 && left2 <= right1)
                return Math.max(left1, left2);

            if(left1 > right2)
                high = cut1 - 1;
            else
                low = cut1 + 1;
        }

        return -1;
    }

    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();
        long[] a = new long[N];

        for(int i = 0; i < N; i++)
            a[i] = sc.nextLong();

        int M = sc.nextInt();
        long[] b = new long[M];

        for(int i = 0; i < M; i++)
            b[i] = sc.nextLong();

        int K = sc.nextInt();

        System.out.print(kth(a, b, K));
    }
}
```
```Python
N = int(input())
a = list(map(int, input().split()))

M = int(input())
b = list(map(int, input().split()))

K = int(input())

if len(a) > len(b):
    a, b = b, a

n = len(a)
m = len(b)

low = max(0, K - m)
high = min(K, n)

while low <= high:
    cut1 = (low + high) // 2
    cut2 = K - cut1

    left1 = float("-inf") if cut1 == 0 else a[cut1 - 1]
    right1 = float("inf") if cut1 == n else a[cut1]

    left2 = float("-inf") if cut2 == 0 else b[cut2 - 1]
    right2 = float("inf") if cut2 == m else b[cut2]

    if left1 <= right2 and left2 <= right1:
        print(max(left1, left2))
        break

    if left1 > right2:
        high = cut1 - 1
    else:
        low = cut1 + 1
```

### Output
For Input:
4
2 3 6 7
4
1 4 8 10
5

Output:
6

# Time Complexity
O(log(min(N, M)))

# Space Complexity
O(1)

</approaches>



> **Note:** The binary search partition approach is the standard optimal solution with **O(log(min(N, M)))** time complexity. Implementing it in C and C# is considerably longer, so in interviews and competitive programming, the above logic is directly translated similarly.
