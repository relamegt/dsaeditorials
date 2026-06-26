# Upper Bound - Solution

## Problem Statement

Given a sorted array of integers `arr` of size `N` in non-decreasing order and an integer `X`, find the upper bound of `X`.

The upper bound of `X` is the smallest index `i` such that `arr[i] > X`. If no such index exists, print `N`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers in non-decreasing order

Third line: Integer `X`

## Output Format

Print a single integer representing the upper bound index of `X`.

## Explanation

There are two common approaches to solve this problem.

- **Linear Search:** Traverse the array and find the first element greater than `X`.
- **Binary Search (Optimal):** Use binary search to efficiently locate the upper bound.

For example,

Input

7

1 2 2 2 4 6 8

2

Output

4

<approaches>
## Approach 1: Linear Search

### Algorithm

1. Read the sorted array and `X`.
2. Traverse the array from left to right.
3. Find the first index where `arr[i] > X`.
4. If found, print the index.
5. Otherwise, print `N`.

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

    for(int i=0;i<n;i++)
    {
        if(arr[i]>x)
        {
            printf("%d",i);
            return 0;
        }
    }

    printf("%d",n);

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

    for(int i=0;i<n;i++)
    {
        if(arr[i]>x)
        {
            cout<<i;
            return 0;
        }
    }

    cout<<n;

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

        for(int i=0;i<n;i++)
        {
            if(arr[i]>x)
            {
                System.out.print(i);
                return;
            }
        }

        System.out.print(n);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

x=int(input())

for i in range(n):

    if arr[i]>x:
        print(i)
        exit()

print(n)
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

        for(int i = 0; i < n; i++)
        {
            if(arr[i] > x)
            {
                Console.Write(i);
                return;
            }
        }

        Console.Write(n);
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

for(let i = 0; i < n; i++)
{
    if(arr[i] > x)
    {
        console.log(i);
        return;
    }
}

console.log(n);
```

### Output
Input

7

1 2 2 2 4 6 8

2

Output

4

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Binary Search (Optimal)

### Algorithm

1. Read the sorted array and `X`.
2. Initialize `low = 0`, `high = N - 1`, and `answer = N`.
3. While `low <= high`:

- Compute `mid`.
- If `arr[mid] > X`, store `mid` as the current answer and search the left half.
- Otherwise, search the right half.

1. Print `answer`.

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
    int answer=n;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]>x)
        {
            answer=mid;
            high=mid-1;
        }
        else
        {
            low=mid+1;
        }
    }

    printf("%d",answer);

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
    int answer=n;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]>x)
        {
            answer=mid;
            high=mid-1;
        }
        else
        {
            low=mid+1;
        }
    }

    cout<<answer;

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
        int answer=n;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            if(arr[mid]>x)
            {
                answer=mid;
                high=mid-1;
            }
            else
            {
                low=mid+1;
            }
        }

        System.out.print(answer);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

x=int(input())

low=0
high=n-1
answer=n

while low<=high:

    mid=low+(high-low)//2

    if arr[mid]>x:
        answer=mid
        high=mid-1
    else:
        low=mid+1

print(answer)
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
        int answer = n;

        while(low <= high)
        {
            int mid = low + (high - low) / 2;

            if(arr[mid] > x)
            {
                answer = mid;
                high = mid - 1;
            }
            else
            {
                low = mid + 1;
            }
        }

        Console.Write(answer);
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
let answer = n;

while(low <= high)
{
    const mid = low + Math.floor((high - low) / 2);

    if(arr[mid] > x)
    {
        answer = mid;
        high = mid - 1;
    }
    else
    {
        low = mid + 1;
    }
}

console.log(answer);
```

### Output
Input

7

1 2 2 2 4 6 8

2

Output

4

# Time Complexity
O(log N)

# Space Complexity
O(1)

</approaches>




