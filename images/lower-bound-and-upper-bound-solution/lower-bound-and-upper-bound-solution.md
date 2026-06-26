# Lower Bound and Upper Bound - Solution

## Problem Statement

Given a sorted array of integers `arr` of size `N` in non-decreasing order and an integer `X`, find the lower bound and upper bound of `X`.

- The **lower bound** of `X` is the smallest index `i` such that `arr[i] >= X`. If no such index exists, print `N`.
- The **upper bound** of `X` is the smallest index `i` such that `arr[i] > X`. If no such index exists, print `N`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers in non-decreasing order

Third line: Integer `X`

## Output Format

Print two space-separated integers:

`lower_bound upper_bound`

## Explanation

There are two common approaches to solve this problem.

- **Linear Search:** Scan the array to find the first valid indices.
- **Binary Search (Optimal):** Use two binary searches to compute the lower and upper bounds efficiently.

For example,

Input

7

1 2 2 2 4 6 8

2

Output

1 4

<approaches>
## Approach 1: Linear Search

### Algorithm

1. Read the sorted array and `X`.
2. Traverse the array to find the first index where `arr[i] >= X`.
3. Traverse the array again to find the first index where `arr[i] > X`.
4. If either index is not found, use `N`.
5. Print both indices.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    long long x;
    scanf("%lld",&x);

    int lower=n;
    int upper=n;

    for(int i=0;i<n;i++)
    {
        if(arr[i]>=x)
        {
            lower=i;
            break;
        }
    }

    for(int i=0;i<n;i++)
    {
        if(arr[i]>x)
        {
            upper=i;
            break;
        }
    }

    printf("%d %d",lower,upper);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int n;
    cin>>n;

    vector<long long> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    long long x;
    cin>>x;

    int lower=n;
    int upper=n;

    for(int i=0;i<n;i++)
    {
        if(arr[i]>=x)
        {
            lower=i;
            break;
        }
    }

    for(int i=0;i<n;i++)
    {
        if(arr[i]>x)
        {
            upper=i;
            break;
        }
    }

    cout<<lower<<" "<<upper;

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

        int n=sc.nextInt();

        long[] arr=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        long x=sc.nextLong();

        int lower=n;
        int upper=n;

        for(int i=0;i<n;i++)
        {
            if(arr[i]>=x)
            {
                lower=i;
                break;
            }
        }

        for(int i=0;i<n;i++)
        {
            if(arr[i]>x)
            {
                upper=i;
                break;
            }
        }

        System.out.print(lower+" "+upper);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

x=int(input())

lower=n
upper=n

for i in range(n):

    if arr[i]>=x:
        lower=i
        break

for i in range(n):

    if arr[i]>x:
        upper=i
        break

print(lower,upper)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long x = long.Parse(Console.ReadLine());

        int lower = n;
        int upper = n;

        for(int i = 0; i < n; i++)
        {
            if(arr[i] >= x)
            {
                lower = i;
                break;
            }
        }

        for(int i = 0; i < n; i++)
        {
            if(arr[i] > x)
            {
                upper = i;
                break;
            }
        }

        Console.Write(lower + " " + upper);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const arr = [];

for(let i = 0; i < n; i++)
    arr.push(input[idx++]);

const x = input[idx++];

let lower = n;
let upper = n;

for(let i = 0; i < n; i++)
{
    if(arr[i] >= x)
    {
        lower = i;
        break;
    }
}

for(let i = 0; i < n; i++)
{
    if(arr[i] > x)
    {
        upper = i;
        break;
    }
}

console.log(lower + " " + upper);
```

### Output
Input

7

1 2 2 2 4 6 8

2

Output

1 4

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Binary Search (Optimal)

### Algorithm

1. Read the sorted array and `X`.
2. Perform the first binary search to find the smallest index where `arr[i] >= X` (lower bound).
3. Perform the second binary search to find the smallest index where `arr[i] > X` (upper bound).
4. If no valid index is found, the answer remains `N`.
5. Print the lower bound and upper bound.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    long long x;
    scanf("%lld",&x);

    int low=0;
    int high=n-1;
    int lower=n;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]>=x)
        {
            lower=mid;
            high=mid-1;
        }
        else
            low=mid+1;
    }

    low=0;
    high=n-1;

    int upper=n;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]>x)
        {
            upper=mid;
            high=mid-1;
        }
        else
            low=mid+1;
    }

    printf("%d %d",lower,upper);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int n;
    cin>>n;

    vector<long long> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    long long x;
    cin>>x;

    int low=0;
    int high=n-1;
    int lower=n;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]>=x)
        {
            lower=mid;
            high=mid-1;
        }
        else
            low=mid+1;
    }

    low=0;
    high=n-1;

    int upper=n;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]>x)
        {
            upper=mid;
            high=mid-1;
        }
        else
            low=mid+1;
    }

    cout<<lower<<" "<<upper;

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

        int n=sc.nextInt();

        long[] arr=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        long x=sc.nextLong();

        int low=0;
        int high=n-1;
        int lower=n;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            if(arr[mid]>=x)
            {
                lower=mid;
                high=mid-1;
            }
            else
                low=mid+1;
        }

        low=0;
        high=n-1;

        int upper=n;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            if(arr[mid]>x)
            {
                upper=mid;
                high=mid-1;
            }
            else
                low=mid+1;
        }

        System.out.print(lower+" "+upper);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

x=int(input())

low=0
high=n-1
lower=n

while low<=high:

    mid=low+(high-low)//2

    if arr[mid]>=x:
        lower=mid
        high=mid-1
    else:
        low=mid+1

low=0
high=n-1
upper=n

while low<=high:

    mid=low+(high-low)//2

    if arr[mid]>x:
        upper=mid
        high=mid-1
    else:
        low=mid+1

print(lower,upper)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long x = long.Parse(Console.ReadLine());

        int low = 0;
        int high = n - 1;
        int lower = n;

        while(low <= high)
        {
            int mid = low + (high - low) / 2;

            if(arr[mid] >= x)
            {
                lower = mid;
                high = mid - 1;
            }
            else
            {
                low = mid + 1;
            }
        }

        low = 0;
        high = n - 1;

        int upper = n;

        while(low <= high)
        {
            int mid = low + (high - low) / 2;

            if(arr[mid] > x)
            {
                upper = mid;
                high = mid - 1;
            }
            else
            {
                low = mid + 1;
            }
        }

        Console.Write(lower + " " + upper);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const arr = [];

for(let i = 0; i < n; i++)
    arr.push(input[idx++]);

const x = input[idx++];

let low = 0;
let high = n - 1;
let lower = n;

while(low <= high)
{
    const mid = low + Math.floor((high - low) / 2);

    if(arr[mid] >= x)
    {
        lower = mid;
        high = mid - 1;
    }
    else
    {
        low = mid + 1;
    }
}

low = 0;
high = n - 1;

let upper = n;

while(low <= high)
{
    const mid = low + Math.floor((high - low) / 2);

    if(arr[mid] > x)
    {
        upper = mid;
        high = mid - 1;
    }
    else
    {
        low = mid + 1;
    }
}

console.log(lower + " " + upper);
```

### Output
Input

7

1 2 2 2 4 6 8

2

Output

1 4

# Time Complexity
O(log N)

# Space Complexity
O(1)

</approaches>




