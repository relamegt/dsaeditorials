# Mean of Range in Array - Solution

## Problem Statement

Given an array `arr[]` of `N` integers and `Q` queries, answer the floor value of the mean of elements in the subarray from index `l` to index `r` (0-based, inclusive).

The mean of range `[l, r]` is:

`floor((arr[l] + arr[l+1] + ... + arr[r]) / (r - l + 1))`

## Input Format

First line: Two integers `N` and `Q`

Second line: `N` space-separated integers

Next `Q` lines: Two integers `l` and `r`

## Output Format

For each query, print the floor value of the mean on a new line.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Compute the sum for every query by traversing the requested range.
- **Prefix Sum (Optimal):** Precompute prefix sums so each query can be answered in constant time.

For example,

Input

5 3

1 2 3 4 5

0 2

1 3

0 4

Output

2

3

3

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. For each query:

- Traverse from index `l` to `r`.
- Compute the sum.
- Divide the sum by the number of elements using integer division.

1. Print the result for every query.

```C
#include <stdio.h>

int main()
{
    int N, Q;
    scanf("%d %d", &N, &Q);

    long long arr[N];

    for(int i = 0; i < N; i++)
        scanf("%lld", &arr[i]);

    while(Q--)
    {
        int l, r;
        scanf("%d %d", &l, &r);

        long long sum = 0;

        for(int i = l; i <= r; i++)
            sum += arr[i];

        printf("%lld
", sum / (r - l + 1));
    }

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int N, Q;
    cin >> N >> Q;

    vector<long long> arr(N);

    for(int i = 0; i < N; i++)
        cin >> arr[i];

    while(Q--)
    {
        int l, r;
        cin >> l >> r;

        long long sum = 0;

        for(int i = l; i <= r; i++)
            sum += arr[i];

        cout << sum / (r - l + 1) << "
";
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
        int Q = sc.nextInt();

        long[] arr = new long[N];

        for(int i = 0; i < N; i++)
            arr[i] = sc.nextLong();

        while(Q-- > 0)
        {
            int l = sc.nextInt();
            int r = sc.nextInt();

            long sum = 0;

            for(int i = l; i <= r; i++)
                sum += arr[i];

            System.out.println(sum / (r - l + 1));
        }
    }
}
```
```Python
N, Q = map(int, input().split())

arr = list(map(int, input().split()))

for _ in range(Q):

    l, r = map(int, input().split())

    total = 0

    for i in range(l, r + 1):
        total += arr[i]

    print(total // (r - l + 1))
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] first = Console.ReadLine().Split();

        int N = int.Parse(first[0]);
        int Q = int.Parse(first[1]);

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        while(Q-- > 0)
        {
            string[] query = Console.ReadLine().Split();

            int l = int.Parse(query[0]);
            int r = int.Parse(query[1]);

            long sum = 0;

            for(int i = l; i <= r; i++)
                sum += arr[i];

            Console.WriteLine(sum / (r - l + 1));
        }
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(BigInt);

let idx = 0;

const N = Number(input[idx++]);
const Q = Number(input[idx++]);

const arr = [];

for(let i = 0; i < N; i++)
    arr.push(input[idx++]);

for(let q = 0; q < Q; q++)
{
    const l = Number(input[idx++]);
    const r = Number(input[idx++]);

    let sum = 0n;

    for(let i = l; i <= r; i++)
        sum += arr[i];

    console.log((sum / BigInt(r - l + 1)).toString());
}
```

### Output
Input

5 3

1 2 3 4 5

0 2

1 3

0 4

Output

2
3
3

# Time Complexity
O(N × Q)

# Space Complexity
O(1)

## Approach 2: Prefix Sum (Optimal)

### Algorithm

1. Read the array.
2. Build a prefix sum array where `prefix[i]` stores the sum of the first `i` elements.
3. For each query:

- Compute the subarray sum using:

     `sum = prefix[r + 1] - prefix[l]`

- Compute the floor mean using integer division.

1. Print the answer for every query.

```C
#include <stdio.h>

int main()
{
    int N, Q;
    scanf("%d %d", &N, &Q);

    long long arr[N];
    long long prefix[N + 1];

    prefix[0] = 0;

    for(int i = 0; i < N; i++)
    {
        scanf("%lld", &arr[i]);
        prefix[i + 1] = prefix[i] + arr[i];
    }

    while(Q--)
    {
        int l, r;
        scanf("%d %d", &l, &r);

        long long sum = prefix[r + 1] - prefix[l];

        printf("%lld
", sum / (r - l + 1));
    }

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int N, Q;
    cin >> N >> Q;

    vector<long long> arr(N);
    vector<long long> prefix(N + 1, 0);

    for(int i = 0; i < N; i++)
    {
        cin >> arr[i];
        prefix[i + 1] = prefix[i] + arr[i];
    }

    while(Q--)
    {
        int l, r;
        cin >> l >> r;

        long long sum = prefix[r + 1] - prefix[l];

        cout << sum / (r - l + 1) << "
";
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
        int Q = sc.nextInt();

        long[] prefix = new long[N + 1];

        for(int i = 0; i < N; i++)
            prefix[i + 1] = prefix[i] + sc.nextLong();

        while(Q-- > 0)
        {
            int l = sc.nextInt();
            int r = sc.nextInt();

            long sum = prefix[r + 1] - prefix[l];

            System.out.println(sum / (r - l + 1));
        }
    }
}
```
```Python
N, Q = map(int, input().split())

arr = list(map(int, input().split()))

prefix = [0] * (N + 1)

for i in range(N):
    prefix[i + 1] = prefix[i] + arr[i]

for _ in range(Q):

    l, r = map(int, input().split())

    total = prefix[r + 1] - prefix[l]

    print(total // (r - l + 1))
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] first = Console.ReadLine().Split();

        int N = int.Parse(first[0]);
        int Q = int.Parse(first[1]);

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long[] prefix = new long[N + 1];

        for(int i = 0; i < N; i++)
            prefix[i + 1] = prefix[i] + arr[i];

        while(Q-- > 0)
        {
            string[] query = Console.ReadLine().Split();

            int l = int.Parse(query[0]);
            int r = int.Parse(query[1]);

            long sum = prefix[r + 1] - prefix[l];

            Console.WriteLine(sum / (r - l + 1));
        }
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(BigInt);

let idx = 0;

const N = Number(input[idx++]);
const Q = Number(input[idx++]);

const arr = [];
const prefix = new Array(N + 1).fill(0n);

for(let i = 0; i < N; i++)
{
    arr.push(input[idx]);
    prefix[i + 1] = prefix[i] + input[idx];
    idx++;
}

for(let q = 0; q < Q; q++)
{
    const l = Number(input[idx++]);
    const r = Number(input[idx++]);

    const sum = prefix[r + 1] - prefix[l];

    console.log((sum / BigInt(r - l + 1)).toString());
}
```

### Output
Input

5 3

1 2 3 4 5

0 2

1 3

0 4

Output

2
3
3

# Time Complexity
Prefix Sum Construction: O(N)
Each Query: O(1)
Overall: O(N + Q)

# Space Complexity
O(N)

</approaches>




