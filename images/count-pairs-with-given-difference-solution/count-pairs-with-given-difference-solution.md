# Count Pairs with Given Difference - Solution

## Problem Statement

Given an array `arr[]` of `N` integers and a non-negative integer `K`, count the number of unordered pairs `(i, j)` such that `i < j` and:

`|arr[i] - arr[j]| = K`

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

Third line: Integer `K`.

### Output Format

Print a single integer representing the number of valid pairs.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Check every possible pair and count those whose absolute difference is `K`.
- **Hash Map (Recommended):** Store the frequency of every element. For `K = 0`, count pairs among equal elements. For `K > 0`, check whether `value + K` exists and add the corresponding frequency.

For example,

Input: `1 5 3 4`

`K = 2`

Valid pairs are:

- `(1,3)`
- `(3,5)`

Output: 2

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Read the value of `K`.
4. Initialize `count = 0`.
5. Traverse every possible pair `(i, j)` where `i < j`.
6. Compute `|arr[i] - arr[j]|`.
7. If the difference equals `K`, increment `count`.
8. Print `count`.

```C
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];

    for (int i = 0; i < N; i++)
        scanf("%lld", &arr[i]);

    long long K;
    scanf("%lld", &K);

    long long count = 0;

    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {
            if (llabs(arr[i] - arr[j]) == K)
                count++;
        }
    }

    printf("%lld", count);

    return 0;
}
```
```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    int N;
    cin >> N;

    long long arr[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    long long K;
    cin >> K;

    long long count = 0;

    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {
            if (abs(arr[i] - arr[j]) == K)
                count++;
        }
    }

    cout << count;

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

        long[] arr = new long[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextLong();

        long K = sc.nextLong();

        long count = 0;

        for (int i = 0; i < N; i++)
        {
            for (int j = i + 1; j < N; j++)
            {
                if (Math.abs(arr[i] - arr[j]) == K)
                    count++;
            }
        }

        System.out.print(count);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

K = int(input())

count = 0

for i in range(N):
    for j in range(i + 1, N):
        if abs(arr[i] - arr[j]) == K:
            count += 1

print(count)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long K = long.Parse(Console.ReadLine());

        long count = 0;

        for (int i = 0; i < N; i++)
        {
            for (int j = i + 1; j < N; j++)
            {
                if (Math.Abs(arr[i] - arr[j]) == K)
                    count++;
            }
        }

        Console.Write(count);
    }
}
```

### Output
For Input:
4
1 5 3 4
2

Output:
2

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Hash Map (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Read the value of `K`.
4. Store the frequency of every element in a hash map.
5. Initialize `count = 0`.
6. If `K == 0`:

- For every frequency `f`:
- Add `f × (f - 1) / 2` to the answer.

1. Otherwise:

- For every distinct element `x`:
- If `x + K` exists in the map, add the frequency of `x` multiplied by the frequency of `x + K`.

1. Print the final count.

```C
#include <stdio.h>
#include <stdlib.h>

#define SIZE 200003

typedef struct Node
{
    long long key;
    long long freq;
    struct Node *next;
} Node;

Node *table[SIZE];

int hash(long long x)
{
    if (x < 0)
        x = -x;
    return x % SIZE;
}

void insert(long long key)
{
    int h = hash(key);

    Node *cur = table[h];

    while (cur)
    {
        if (cur->key == key)
        {
            cur->freq++;
            return;
        }
        cur = cur->next;
    }

    Node *node = (Node *)malloc(sizeof(Node));
    node->key = key;
    node->freq = 1;
    node->next = table[h];
    table[h] = node;
}

Node *find(long long key)
{
    Node *cur = table[hash(key)];

    while (cur)
    {
        if (cur->key == key)
            return cur;
        cur = cur->next;
    }

    return NULL;
}

int main()
{
    int N;
    scanf("%d", &N);

    long long *arr = (long long *)malloc(sizeof(long long) * N);

    for (int i = 0; i < N; i++)
    {
        scanf("%lld", &arr[i]);
        insert(arr[i]);
    }

    long long K;
    scanf("%lld", &K);

    long long ans = 0;

    if (K == 0)
    {
        for (int i = 0; i < SIZE; i++)
        {
            Node *cur = table[i];
            while (cur)
            {
                ans += cur->freq * (cur->freq - 1) / 2;
                cur = cur->next;
            }
        }
    }
    else
    {
        for (int i = 0; i < SIZE; i++)
        {
            Node *cur = table[i];
            while (cur)
            {
                Node *next = find(cur->key + K);
                if (next)
                    ans += cur->freq * next->freq;
                cur = cur->next;
            }
        }
    }

    printf("%lld", ans);

    return 0;
}
```
```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

int main()
{
    int N;
    cin >> N;

    unordered_map<long long, long long> freq;

    for (int i = 0; i < N; i++)
    {
        long long x;
        cin >> x;
        freq[x]++;
    }

    long long K;
    cin >> K;

    long long ans = 0;

    if (K == 0)
    {
        for (auto x : freq)
            ans += x.second * (x.second - 1) / 2;
    }
    else
    {
        for (auto x : freq)
        {
            if (freq.count(x.first + K))
                ans += x.second * freq[x.first + K];
        }
    }

    cout << ans;

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

        HashMap<Long, Long> map = new HashMap<>();

        for (int i = 0; i < N; i++)
        {
            long x = sc.nextLong();
            map.put(x, map.getOrDefault(x, 0L) + 1);
        }

        long K = sc.nextLong();

        long ans = 0;

        if (K == 0)
        {
            for (long f : map.values())
                ans += f * (f - 1) / 2;
        }
        else
        {
            for (long key : map.keySet())
            {
                if (map.containsKey(key + K))
                    ans += map.get(key) * map.get(key + K);
            }
        }

        System.out.print(ans);
    }
}
```
```Python
from collections import Counter

N = int(input())

arr = list(map(int, input().split()))

K = int(input())

freq = Counter(arr)

count = 0

if K == 0:
    for f in freq.values():
        count += f * (f - 1) // 2
else:
    for x in freq:
        if x + K in freq:
            count += freq[x] * freq[x + K]

print(count)
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long K = long.Parse(Console.ReadLine());

        Dictionary<long, long> freq = new Dictionary<long, long>();

        foreach (long x in arr)
        {
            if (!freq.ContainsKey(x))
                freq[x] = 0;

            freq[x]++;
        }

        long ans = 0;

        if (K == 0)
        {
            foreach (var item in freq)
                ans += item.Value * (item.Value - 1) / 2;
        }
        else
        {
            foreach (var item in freq)
            {
                if (freq.ContainsKey(item.Key + K))
                    ans += item.Value * freq[item.Key + K];
            }
        }

        Console.Write(ans);
    }
}
```

### Output
For Input:
4
1 5 3 4
2

Output:
2

# Time Complexity
O(N)

# Space Complexity
O(N)

</approaches>




