# Equilibrium Index - Solution

## Problem Statement

Given an array `arr[]` of size `N`, find the equilibrium index — an index `i` (0-based) such that the sum of all elements before index `i` equals the sum of all elements after index `i`.

If multiple equilibrium indices exist, return the first one. If no such index exists, return `-1`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers

## Output Format

Print a single integer — the 0-based equilibrium index, or `-1` if none exists.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** For every index, calculate the left and right sums separately.
- **Prefix Sum (Optimal):** Compute the total sum once and maintain a running left sum while traversing the array.

For example,

Input

5

1 3 5 2 2

Output

2

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. For every index:

- Calculate the sum of all elements before it.
- Calculate the sum of all elements after it.

1. If both sums are equal, print the index and stop.
2. If no such index exists, print `-1`.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d",&N);

    long long arr[N];

    for(int i=0;i<N;i++)
        scanf("%lld",&arr[i]);

    for(int i=0;i<N;i++)
    {
        long long left=0;
        long long right=0;

        for(int j=0;j<i;j++)
            left+=arr[j];

        for(int j=i+1;j<N;j++)
            right+=arr[j];

        if(left==right)
        {
            printf("%d",i);
            return 0;
        }
    }

    printf("-1");

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
    cin>>N;

    vector<long long> arr(N);

    for(int i=0;i<N;i++)
        cin>>arr[i];

    for(int i=0;i<N;i++)
    {
        long long left=0;
        long long right=0;

        for(int j=0;j<i;j++)
            left+=arr[j];

        for(int j=i+1;j<N;j++)
            right+=arr[j];

        if(left==right)
        {
            cout<<i;
            return 0;
        }
    }

    cout<<-1;

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

        for(int i=0;i<N;i++)
        {
            long left=0;
            long right=0;

            for(int j=0;j<i;j++)
                left+=arr[j];

            for(int j=i+1;j<N;j++)
                right+=arr[j];

            if(left==right)
            {
                System.out.print(i);
                return;
            }
        }

        System.out.print(-1);
    }
}
```
```Python
N=int(input())

arr=list(map(int,input().split()))

for i in range(N):

    left=0
    right=0

    for j in range(i):
        left+=arr[j]

    for j in range(i+1,N):
        right+=arr[j]

    if left==right:
        print(i)
        exit()

print(-1)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        for(int i = 0; i < N; i++)
        {
            long left = 0;
            long right = 0;

            for(int j = 0; j < i; j++)
                left += arr[j];

            for(int j = i + 1; j < N; j++)
                right += arr[j];

            if(left == right)
            {
                Console.Write(i);
                return;
            }
        }

        Console.Write(-1);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(BigInt);

let idx = 0;

const N = Number(input[idx++]);

const arr = [];

for(let i = 0; i < N; i++)
    arr.push(input[idx++]);

for(let i = 0; i < N; i++)
{
    let left = 0n;
    let right = 0n;

    for(let j = 0; j < i; j++)
        left += arr[j];

    for(let j = i + 1; j < N; j++)
        right += arr[j];

    if(left === right)
    {
        console.log(i);
        process.exit(0);
    }
}

console.log(-1);
```

### Output
Input

5

1 3 5 2 2

Output

2

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Prefix Sum (Optimal)

### Algorithm

1. Read the array.
2. Compute the total sum of all elements.
3. Initialize `leftSum = 0`.
4. Traverse the array from left to right.
5. For each index:

- Compute `rightSum = totalSum - leftSum - arr[i]`.
- If `leftSum == rightSum`, print the current index.
- Otherwise, add `arr[i]` to `leftSum`.

1. If no equilibrium index is found, print `-1`.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];
    long long total = 0;

    for(int i = 0; i < N; i++)
    {
        scanf("%lld", &arr[i]);
        total += arr[i];
    }

    long long left = 0;

    for(int i = 0; i < N; i++)
    {
        long long right = total - left - arr[i];

        if(left == right)
        {
            printf("%d", i);
            return 0;
        }

        left += arr[i];
    }

    printf("-1");

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

    vector<long long> arr(N);

    long long total = 0;

    for(int i = 0; i < N; i++)
    {
        cin >> arr[i];
        total += arr[i];
    }

    long long left = 0;

    for(int i = 0; i < N; i++)
    {
        long long right = total - left - arr[i];

        if(left == right)
        {
            cout << i;
            return 0;
        }

        left += arr[i];
    }

    cout << -1;

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

        long total = 0;

        for(int i = 0; i < N; i++)
        {
            arr[i] = sc.nextLong();
            total += arr[i];
        }

        long left = 0;

        for(int i = 0; i < N; i++)
        {
            long right = total - left - arr[i];

            if(left == right)
            {
                System.out.print(i);
                return;
            }

            left += arr[i];
        }

        System.out.print(-1);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

total = sum(arr)

left = 0

for i in range(N):

    right = total - left - arr[i]

    if left == right:
        print(i)
        exit()

    left += arr[i]

print(-1)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long total = 0;

        foreach(long value in arr)
            total += value;

        long left = 0;

        for(int i = 0; i < N; i++)
        {
            long right = total - left - arr[i];

            if(left == right)
            {
                Console.Write(i);
                return;
            }

            left += arr[i];
        }

        Console.Write(-1);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(BigInt);

let idx = 0;

const N = Number(input[idx++]);

const arr = [];

let total = 0n;

for(let i = 0; i < N; i++)
{
    arr.push(input[idx]);
    total += input[idx];
    idx++;
}

let left = 0n;

for(let i = 0; i < N; i++)
{
    const right = total - left - arr[i];

    if(left === right)
    {
        console.log(i);
        process.exit(0);
    }

    left += arr[i];
}

console.log(-1);
```

### Output
Input

5

1 3 5 2 2

Output

2

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




