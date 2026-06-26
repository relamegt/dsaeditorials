# Minimize the Heights  - Solution

## Problem Statement

Given an array `arr[]` and a positive integer `K` denoting the heights of towers, modify the height of every tower exactly once by either increasing or decreasing it by `K`.

Find the minimum possible difference between the tallest and the shortest tower after all modifications.

## Input Format

First line: Integer `K`

Second line: Integer `N`

Third line: `N` space-separated integers representing tower heights.

## Output Format

Print a single integer representing the minimum possible difference.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Try every possible combination of adding or subtracting `K` for every tower.
- **Sorting + Greedy (Optimal):** Sort the array and intelligently decide where to switch from increasing to decreasing.

For example,

Input

2

4

1 5 8 10

Output

5

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read `K`, `N`, and the array.
2. Generate every possible combination where each tower is either increased or decreased by `K`.
3. For every combination:

- Compute the minimum and maximum tower heights.
- Update the minimum difference.

1. Print the smallest difference found.

> **Note:** This approach is only feasible for very small values of `N` because it explores all `2^N` possibilities.

```C
#include <stdio.h>
#include <limits.h>

int N,K;
long long arr[25];
long long ans=LLONG_MAX;

void solve(int index)
{
    if(index==N)
    {
        long long mn=arr[0],mx=arr[0];

        for(int i=1;i<N;i++)
        {
            if(arr[i]<mn)
                mn=arr[i];

            if(arr[i]>mx)
                mx=arr[i];
        }

        if(mx-mn<ans)
            ans=mx-mn;

        return;
    }

    arr[index]+=K;
    solve(index+1);
    arr[index]-=K;

    arr[index]-=K;
    solve(index+1);
    arr[index]+=K;
}

int main()
{
    scanf("%d",&K);
    scanf("%d",&N);

    for(int i=0;i<N;i++)
        scanf("%lld",&arr[i]);

    solve(0);

    printf("%lld",ans);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

int N,K;
vector<long long> arr;
long long ans=LLONG_MAX;

void solve(int index)
{
    if(index==N)
    {
        long long mn=arr[0],mx=arr[0];

        for(int i=1;i<N;i++)
        {
            mn=min(mn,arr[i]);
            mx=max(mx,arr[i]);
        }

        ans=min(ans,mx-mn);

        return;
    }

    arr[index]+=K;
    solve(index+1);
    arr[index]-=K;

    arr[index]-=K;
    solve(index+1);
    arr[index]+=K;
}

int main()
{
    cin>>K;
    cin>>N;

    arr.resize(N);

    for(int i=0;i<N;i++)
        cin>>arr[i];

    solve(0);

    cout<<ans;

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    static int N,K;
    static long[] arr;
    static long ans=Long.MAX_VALUE;

    static void solve(int index)
    {
        if(index==N)
        {
            long mn=arr[0];
            long mx=arr[0];

            for(int i=1;i<N;i++)
            {
                mn=Math.min(mn,arr[i]);
                mx=Math.max(mx,arr[i]);
            }

            ans=Math.min(ans,mx-mn);

            return;
        }

        arr[index]+=K;
        solve(index+1);
        arr[index]-=K;

        arr[index]-=K;
        solve(index+1);
        arr[index]+=K;
    }

    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);

        K=sc.nextInt();
        N=sc.nextInt();

        arr=new long[N];

        for(int i=0;i<N;i++)
            arr[i]=sc.nextLong();

        solve(0);

        System.out.print(ans);
    }
}
```
```Python
import sys

sys.setrecursionlimit(1000000)

K=int(input())

N=int(input())

arr=list(map(int,input().split()))

ans=float('inf')

def solve(index):

    global ans

    if index==N:

        ans=min(ans,max(arr)-min(arr))
        return

    arr[index]+=K
    solve(index+1)
    arr[index]-=K

    arr[index]-=K
    solve(index+1)
    arr[index]+=K

solve(0)

print(ans)
```
```C#
using System;

class Program
{
    static int N, K;
    static long[] arr;
    static long ans = long.MaxValue;

    static void Solve(int index)
    {
        if(index == N)
        {
            long mn = arr[0];
            long mx = arr[0];

            for(int i = 1; i < N; i++)
            {
                mn = Math.Min(mn, arr[i]);
                mx = Math.Max(mx, arr[i]);
            }

            ans = Math.Min(ans, mx - mn);
            return;
        }

        arr[index] += K;
        Solve(index + 1);
        arr[index] -= K;

        arr[index] -= K;
        Solve(index + 1);
        arr[index] += K;
    }

    static void Main()
    {
        K = int.Parse(Console.ReadLine());

        N = int.Parse(Console.ReadLine());

        arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        Solve(0);

        Console.Write(ans);
    }
}
```
```JavaScript
const fs = require("fs");

const input = fs.readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const K = input[idx++];
const N = input[idx++];

const arr = [];

for(let i = 0; i < N; i++)
    arr.push(input[idx++]);

let ans = Number.MAX_SAFE_INTEGER;

function solve(index)
{
    if(index === N)
    {
        let mn = arr[0];
        let mx = arr[0];

        for(let i = 1; i < N; i++)
        {
            mn = Math.min(mn, arr[i]);
            mx = Math.max(mx, arr[i]);
        }

        ans = Math.min(ans, mx - mn);
        return;
    }

    arr[index] += K;
    solve(index + 1);
    arr[index] -= K;

    arr[index] -= K;
    solve(index + 1);
    arr[index] += K;
}

solve(0);

console.log(ans);
```

### Output
Input

2

4

1 5 8 10

Output

5

# Time Complexity
O(2ᴺ × N)

# Space Complexity
O(N)

## Approach 2: Sorting + Greedy (Optimal)

### Algorithm

1. Sort the array.
2. Initialize the answer as the original difference between the maximum and minimum heights.
3. Assume all towers before index `i` are increased by `K` and all towers from index `i` onward are decreased by `K`.
4. For every partition:

- Skip if decreasing makes a height negative.
- Compute:
- `small = min(arr[0] + K, arr[i] - K)`
- `large = max(arr[N-1] - K, arr[i-1] + K)`
- Update the minimum difference.

1. Print the minimum difference.

```C
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a,const void *b)
{
    return (*(int*)a)-(*(int*)b);
}

int main()
{
    int K,N;
    scanf("%d",&K);
    scanf("%d",&N);

    int arr[N];

    for(int i=0;i<N;i++)
        scanf("%d",&arr[i]);

    qsort(arr,N,sizeof(int),compare);

    int ans=arr[N-1]-arr[0];

    for(int i=1;i<N;i++)
    {
        if(arr[i]<K)
            continue;

        int small=arr[0]+K;

        if(arr[i]-K<small)
            small=arr[i]-K;

        int large=arr[N-1]-K;

        if(arr[i-1]+K>large)
            large=arr[i-1]+K;

        if(large-small<ans)
            ans=large-small;
    }

    printf("%d",ans);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    int K,N;
    cin>>K;
    cin>>N;

    vector<int> arr(N);

    for(int i=0;i<N;i++)
        cin>>arr[i];

    sort(arr.begin(),arr.end());

    int ans=arr[N-1]-arr[0];

    for(int i=1;i<N;i++)
    {
        if(arr[i]<K)
            continue;

        int small=min(arr[0]+K,arr[i]-K);
        int large=max(arr[N-1]-K,arr[i-1]+K);

        ans=min(ans,large-small);
    }

    cout<<ans;

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);

        int K=sc.nextInt();
        int N=sc.nextInt();

        int[] arr=new int[N];

        for(int i=0;i<N;i++)
            arr[i]=sc.nextInt();

        Arrays.sort(arr);

        int ans=arr[N-1]-arr[0];

        for(int i=1;i<N;i++)
        {
            if(arr[i]<K)
                continue;

            int small=Math.min(arr[0]+K,arr[i]-K);
            int large=Math.max(arr[N-1]-K,arr[i-1]+K);

            ans=Math.min(ans,large-small);
        }

        System.out.print(ans);
    }
}
```
```Python
K=int(input())

N=int(input())

arr=list(map(int,input().split()))

arr.sort()

ans=arr[-1]-arr[0]

for i in range(1,N):

    if arr[i]<K:
        continue

    small=min(arr[0]+K,arr[i]-K)
    large=max(arr[-1]-K,arr[i-1]+K)

    ans=min(ans,large-small)

print(ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int K = int.Parse(Console.ReadLine());

        int N = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        Array.Sort(arr);

        int ans = arr[N - 1] - arr[0];

        for(int i = 1; i < N; i++)
        {
            if(arr[i] < K)
                continue;

            int small = Math.Min(arr[0] + K, arr[i] - K);
            int large = Math.Max(arr[N - 1] - K, arr[i - 1] + K);

            ans = Math.Min(ans, large - small);
        }

        Console.Write(ans);
    }
}
```
```JavaScript
const fs = require("fs");

const input = fs.readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const K = input[idx++];
const N = input[idx++];

const arr = [];

for(let i = 0; i < N; i++)
    arr.push(input[idx++]);

arr.sort((a, b) => a - b);

let ans = arr[N - 1] - arr[0];

for(let i = 1; i < N; i++)
{
    if(arr[i] < K)
        continue;

    const small = Math.min(arr[0] + K, arr[i] - K);
    const large = Math.max(arr[N - 1] - K, arr[i - 1] + K);

    ans = Math.min(ans, large - small);
}

console.log(ans);
```

### Output
Input

2

4

1 5 8 10

Output

5

# Time Complexity
O(N log N)

# Space Complexity
O(1)

</approaches>




