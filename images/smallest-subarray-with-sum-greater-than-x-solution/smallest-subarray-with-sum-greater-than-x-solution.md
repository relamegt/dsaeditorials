# Smallest subarray with Sum Greater than X - Solution

## Problem Statement

Given an array `arr[]` of integers and an integer `x`, find the minimum length of a contiguous subarray whose sum is **strictly greater** than `x`.

If no such subarray exists, print `0`.

## Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

Third line: Integer `x`.

## Output Format

Print a single integer representing the minimum length of a contiguous subarray whose sum is greater than `x`. If no such subarray exists, print `0`.

## Explanation

There are two approaches to solve this problem.

- **Sliding Window (Recommended):** Since all array elements are non-negative, use two pointers to maintain a valid window.
- **Brute Force:** Check every possible subarray.

For example,

Input

6

1 4 45 6 0 19

51

Output

3

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array and value `x`.
2. Initialize the answer as infinity.
3. For every starting index:

- Keep adding elements one by one.
- As soon as the sum becomes greater than `x`, update the minimum length.

1. After checking all subarrays:

- Print `0` if no valid subarray exists.
- Otherwise print the minimum length.

```C
#include <stdio.h>
#include <limits.h>

int main()
{
    int N;
    scanf("%d",&N);

    long long arr[N];

    for(int i=0;i<N;i++)
        scanf("%lld",&arr[i]);

    long long x;
    scanf("%lld",&x);

    int ans=INT_MAX;

    for(int i=0;i<N;i++)
    {
        long long sum=0;

        for(int j=i;j<N;j++)
        {
            sum+=arr[j];

            if(sum>x)
            {
                if(j-i+1<ans)
                    ans=j-i+1;
                break;
            }
        }
    }

    if(ans==INT_MAX)
        printf("0");
    else
        printf("%d",ans);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

int main()
{
    int N;
    cin>>N;

    vector<long long> arr(N);

    for(int i=0;i<N;i++)
        cin>>arr[i];

    long long x;
    cin>>x;

    int ans=INT_MAX;

    for(int i=0;i<N;i++)
    {
        long long sum=0;

        for(int j=i;j<N;j++)
        {
            sum+=arr[j];

            if(sum>x)
            {
                ans=min(ans,j-i+1);
                break;
            }
        }
    }

    if(ans==INT_MAX)
        cout<<0;
    else
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

        int N=sc.nextInt();

        long[] arr=new long[N];

        for(int i=0;i<N;i++)
            arr[i]=sc.nextLong();

        long x=sc.nextLong();

        int ans=Integer.MAX_VALUE;

        for(int i=0;i<N;i++)
        {
            long sum=0;

            for(int j=i;j<N;j++)
            {
                sum+=arr[j];

                if(sum>x)
                {
                    ans=Math.min(ans,j-i+1);
                    break;
                }
            }
        }

        if(ans==Integer.MAX_VALUE)
            System.out.print(0);
        else
            System.out.print(ans);
    }
}
```
```Python
from math import inf

N = int(input())

arr = list(map(int, input().split()))

x = int(input())

ans = inf

for i in range(N):

    current = 0

    for j in range(i, N):

        current += arr[j]

        if current > x:
            ans = min(ans, j - i + 1)
            break

if ans == inf:
    print(0)
else:
    print(ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long x = long.Parse(Console.ReadLine());

        int ans = int.MaxValue;

        for (int i = 0; i < N; i++)
        {
            long sum = 0;

            for (int j = i; j < N; j++)
            {
                sum += arr[j];

                if (sum > x)
                {
                    ans = Math.Min(ans, j - i + 1);
                    break;
                }
            }
        }

        if (ans == int.MaxValue)
            Console.Write(0);
        else
            Console.Write(ans);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(BigInt);

let idx = 0;

const N = Number(input[idx++]);

const arr = [];

for (let i = 0; i < N; i++)
    arr.push(input[idx++]);

const x = input[idx++];

let ans = Number.MAX_SAFE_INTEGER;

for (let i = 0; i < N; i++)
{
    let sum = 0n;

    for (let j = i; j < N; j++)
    {
        sum += arr[j];

        if (sum > x)
        {
            ans = Math.min(ans, j - i + 1);
            break;
        }
    }
}

if (ans === Number.MAX_SAFE_INTEGER)
    console.log(0);
else
    console.log(ans);
```

### Output
Input

6

1 4 45 6 0 19

51

Output

3

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Sliding Window (Recommended)

### Algorithm

1. Read the array and value `x`.
2. Initialize two pointers `start` and `end`.
3. Expand the window by moving `end` and adding elements to the current sum.
4. While the sum is greater than `x`:

- Update the minimum length.
- Remove the leftmost element.
- Move `start` forward.

1. If no valid subarray is found, print `0`.
2. Otherwise print the minimum length.

```C
#include <stdio.h>
#include <limits.h>

int main()
{
    int N;
    scanf("%d",&N);

    long long arr[N];

    for(int i=0;i<N;i++)
        scanf("%lld",&arr[i]);

    long long x;
    scanf("%lld",&x);

    int start=0;
    long long sum=0;
    int ans=INT_MAX;

    for(int end=0;end<N;end++)
    {
        sum+=arr[end];

        while(sum>x)
        {
            if(end-start+1<ans)
                ans=end-start+1;

            sum-=arr[start];
            start++;
        }
    }

    if(ans==INT_MAX)
        printf("0");
    else
        printf("%d",ans);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

int main()
{
    int N;
    cin>>N;

    vector<long long> arr(N);

    for(int i=0;i<N;i++)
        cin>>arr[i];

    long long x;
    cin>>x;

    int start=0;
    long long sum=0;
    int ans=INT_MAX;

    for(int end=0;end<N;end++)
    {
        sum+=arr[end];

        while(sum>x)
        {
            ans=min(ans,end-start+1);
            sum-=arr[start];
            start++;
        }
    }

    if(ans==INT_MAX)
        cout<<0;
    else
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

        int N=sc.nextInt();

        long[] arr=new long[N];

        for(int i=0;i<N;i++)
            arr[i]=sc.nextLong();

        long x=sc.nextLong();

        int start=0;
        long sum=0;
        int ans=Integer.MAX_VALUE;

        for(int end=0;end<N;end++)
        {
            sum+=arr[end];

            while(sum>x)
            {
                ans=Math.min(ans,end-start+1);
                sum-=arr[start];
                start++;
            }
        }

        if(ans==Integer.MAX_VALUE)
            System.out.print(0);
        else
            System.out.print(ans);
    }
}
```
```Python
from math import inf

N=int(input())

arr=list(map(int,input().split()))

x=int(input())

start=0
current=0
ans=inf

for end in range(N):

    current+=arr[end]

    while current>x:
        ans=min(ans,end-start+1)
        current-=arr[start]
        start+=1

if ans==inf:
    print(0)
else:
    print(ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long x = long.Parse(Console.ReadLine());

        int start = 0;
        long sum = 0;
        int ans = int.MaxValue;

        for (int end = 0; end < N; end++)
        {
            sum += arr[end];

            while (sum > x)
            {
                ans = Math.Min(ans, end - start + 1);
                sum -= arr[start];
                start++;
            }
        }

        if (ans == int.MaxValue)
            Console.Write(0);
        else
            Console.Write(ans);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(BigInt);

let idx = 0;

const N = Number(input[idx++]);

const arr = [];

for (let i = 0; i < N; i++)
    arr.push(input[idx++]);

const x = input[idx++];

let start = 0;
let sum = 0n;
let ans = Number.MAX_SAFE_INTEGER;

for (let end = 0; end < N; end++)
{
    sum += arr[end];

    while (sum > x)
    {
        ans = Math.min(ans, end - start + 1);
        sum -= arr[start];
        start++;
    }
}

if (ans === Number.MAX_SAFE_INTEGER)
    console.log(0);
else
    console.log(ans);
```

### Output
Input

6

1 4 45 6 0 19

51

Output

3

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




