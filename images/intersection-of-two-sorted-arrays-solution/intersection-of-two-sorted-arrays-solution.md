# Intersection of Two Sorted Arrays - Solution

## Problem Statement

Given two sorted arrays `arr1[]` and `arr2[]` of sizes `N` and `M`, find their intersection. The intersection should contain all distinct elements that are present in both arrays, in sorted order, without duplicates.

### Input Format

First line: integer `N`.

Second line: `N` space-separated integers of `arr1` (sorted).

Third line: integer `M`.

Fourth line: `M` space-separated integers of `arr2` (sorted).

### Output Format

Print the distinct common elements in sorted order. If there is no intersection, print nothing.

## Explanation

There are two common approaches to solve this problem.

- **Two Pointers (Recommended):** Traverse both sorted arrays simultaneously and print common distinct elements.
- **Hash Set:** Store one array in a hash set and check the second array.

For example,

Input

5

1 2 3 4 5

5

1 2 3 4 5

Output

1 2 3 4 5

<approaches>
## Approach 1: Two Pointers (Recommended)

### Algorithm

1. Read both sorted arrays.
2. Initialize two pointers `i = 0` and `j = 0`.
3. Compare `arr1[i]` and `arr2[j]`.
4. If `arr1[i] < arr2[j]`, increment `i`.
5. If `arr1[i] > arr2[j]`, increment `j`.
6. If both are equal:

- Print the element if it has not already been printed.
- Increment both pointers.

1. Continue until either array is exhausted.

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

    int i = 0;
    int j = 0;

    int first = 1;
    long long last = 0;

    while(i < N && j < M)
    {
        if(arr1[i] < arr2[j])
        {
            i++;
        }
        else if(arr1[i] > arr2[j])
        {
            j++;
        }
        else
        {
            if(first || arr1[i] != last)
            {
                printf("%lld ", arr1[i]);
                last = arr1[i];
                first = 0;
            }

            i++;
            j++;
        }
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

    int i = 0;
    int j = 0;

    bool first = true;
    long long last = 0;

    while(i < N && j < M)
    {
        if(arr1[i] < arr2[j])
        {
            i++;
        }
        else if(arr1[i] > arr2[j])
        {
            j++;
        }
        else
        {
            if(first || arr1[i] != last)
            {
                cout << arr1[i] << " ";
                last = arr1[i];
                first = false;
            }

            i++;
            j++;
        }
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

        int i = 0;
        int j = 0;

        boolean first = true;
        long last = 0;

        while(i < N && j < M)
        {
            if(arr1[i] < arr2[j])
            {
                i++;
            }
            else if(arr1[i] > arr2[j])
            {
                j++;
            }
            else
            {
                if(first || arr1[i] != last)
                {
                    System.out.print(arr1[i] + " ");
                    last = arr1[i];
                    first = false;
                }

                i++;
                j++;
            }
        }
    }
}
```
```Python
N = int(input())

arr1 = list(map(int, input().split()))

M = int(input())

arr2 = list(map(int, input().split()))

i = 0
j = 0

first = True
last = 0

while i < N and j < M:

    if arr1[i] < arr2[j]:
        i += 1

    elif arr1[i] > arr2[j]:
        j += 1

    else:
        if first or arr1[i] != last:
            print(arr1[i], end=" ")
            last = arr1[i]
            first = False

        i += 1
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

        int i = 0;
        int j = 0;

        bool first = true;
        long last = 0;

        while(i < N && j < M)
        {
            if(arr1[i] < arr2[j])
            {
                i++;
            }
            else if(arr1[i] > arr2[j])
            {
                j++;
            }
            else
            {
                if(first || arr1[i] != last)
                {
                    Console.Write(arr1[i] + " ");
                    last = arr1[i];
                    first = false;
                }

                i++;
                j++;
            }
        }
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const N = input[idx++];
const arr1 = [];

for(let i = 0; i < N; i++)
    arr1.push(input[idx++]);

const M = input[idx++];
const arr2 = [];

for(let i = 0; i < M; i++)
    arr2.push(input[idx++]);

let i = 0;
let j = 0;

let first = true;
let last = 0;

let ans = [];

while(i < N && j < M)
{
    if(arr1[i] < arr2[j])
    {
        i++;
    }
    else if(arr1[i] > arr2[j])
    {
        j++;
    }
    else
    {
        if(first || arr1[i] !== last)
        {
            ans.push(arr1[i]);
            last = arr1[i];
            first = false;
        }

        i++;
        j++;
    }
}

console.log(ans.join(" "));
```

### Output
For Input:
5
1 2 3 4 5
5
1 2 3 4 5

Output:
1 2 3 4 5

# Time Complexity
O(N + M)

# Space Complexity
O(1)

## Approach 2: Hash Set

### Algorithm

1. Read both arrays.
2. Insert every element of the first array into a hash set.
3. Traverse the second array.
4. If the current element exists in the hash set, insert it into another set (or ordered set) to avoid duplicates.
5. Print all elements of the answer set in sorted order.

```C
#include <stdio.h>
#include <stdlib.h>

#define SIZE 200003

typedef struct Node
{
    long long key;
    struct Node *next;
} Node;

Node *table[SIZE];

int hash(long long x)
{
    if(x < 0)
        x = -x;

    return x % SIZE;
}

int exists(long long key)
{
    Node *cur = table[hash(key)];

    while(cur)
    {
        if(cur->key == key)
            return 1;

        cur = cur->next;
    }

    return 0;
}

void insert(long long key)
{
    if(exists(key))
        return;

    int h = hash(key);

    Node *node = (Node *)malloc(sizeof(Node));

    node->key = key;
    node->next = table[h];
    table[h] = node;
}

int compare(const void *a, const void *b)
{
    long long x = *(long long *)a;
    long long y = *(long long *)b;

    if(x < y)
        return -1;

    if(x > y)
        return 1;

    return 0;
}

int main()
{
    int N;
    scanf("%d", &N);

    for(int i = 0; i < N; i++)
    {
        long long x;
        scanf("%lld", &x);
        insert(x);
    }

    int M;
    scanf("%d", &M);

    long long ans[M];
    int cnt = 0;

    for(int i = 0; i < M; i++)
    {
        long long x;
        scanf("%lld", &x);

        if(exists(x))
            ans[cnt++] = x;
    }

    qsort(ans, cnt, sizeof(long long), compare);

    if(cnt > 0)
    {
        printf("%lld", ans[0]);

        for(int i = 1; i < cnt; i++)
        {
            if(ans[i] != ans[i - 1])
                printf(" %lld", ans[i]);
        }
    }

    return 0;
}
```
```cpp
#include <iostream>
#include <unordered_set>
#include <set>
using namespace std;

int main()
{
    int N;
    cin >> N;

    unordered_set<long long> st;

    for(int i = 0; i < N; i++)
    {
        long long x;
        cin >> x;
        st.insert(x);
    }

    int M;
    cin >> M;

    set<long long> ans;

    for(int i = 0; i < M; i++)
    {
        long long x;
        cin >> x;

        if(st.count(x))
            ans.insert(x);
    }

    for(long long x : ans)
        cout << x << " ";

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

        HashSet<Long> set = new HashSet<>();

        for(int i = 0; i < N; i++)
            set.add(sc.nextLong());

        int M = sc.nextInt();

        TreeSet<Long> ans = new TreeSet<>();

        for(int i = 0; i < M; i++)
        {
            long x = sc.nextLong();

            if(set.contains(x))
                ans.add(x);
        }

        for(long x : ans)
            System.out.print(x + " ");
    }
}
```
```Python
N = int(input())

arr1 = list(map(int, input().split()))

M = int(input())

arr2 = list(map(int, input().split()))

elements = set(arr1)

answer = set()

for x in arr2:
    if x in elements:
        answer.add(x)

print(*sorted(answer))
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr1 = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        int M = int.Parse(Console.ReadLine());

        long[] arr2 = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        HashSet<long> set = new HashSet<long>();

        foreach(long x in arr1)
            set.Add(x);

        SortedSet<long> answer = new SortedSet<long>();

        foreach(long x in arr2)
        {
            if(set.Contains(x))
                answer.Add(x);
        }

        foreach(long x in answer)
            Console.Write(x + " ");
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const N = input[idx++];

const elements = new Set();

for(let i = 0; i < N; i++)
    elements.add(input[idx++]);

const M = input[idx++];

const answer = new Set();

for(let i = 0; i < M; i++)
{
    const value = input[idx++];

    if(elements.has(value))
        answer.add(value);
}

console.log([...answer].sort((a, b) => a - b).join(" "));
```

### Output
For Input:
5
1 2 3 4 5
5
1 2 3 4 5

Output:
1 2 3 4 5

# Time Complexity
O(N + M)

# Space Complexity
O(N)

</approaches>



> **Note:** The binary search partition approach is the standard optimal solution with **O(log(min(N, M)))** time complexity. Implementing it in C and C# is considerably longer, so in interviews and competitive programming, the above logic is directly translated similarly.
