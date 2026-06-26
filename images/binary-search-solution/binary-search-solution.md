# Binary Search - Solution

## Problem Statement

Given a sorted array of integers `arr` of size `N` in non-decreasing order and an integer `X`, find the index of `X` in the array. If `X` is present multiple times, print the index of any one occurrence. If `X` is not present, print `-1`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers in non-decreasing order

Third line: Integer `X`

## Output Format

Print a single integer representing an index where `X` is present, or `-1` if it is not found.

## Explanation

There are two common approaches to solve this problem.

- **Linear Search:** Traverse the array from left to right until the element is found.
- **Binary Search (Optimal):** Repeatedly divide the search space in half.

For example,

Input

6

1 3 5 7 9 11

7

Output

3

<approaches>
## Approach 1: Linear Search

### Algorithm

1. Read the array and the target element.
2. Traverse the array from left to right.
3. If the current element equals `X`, print its index and stop.
4. If the traversal ends without finding `X`, print `-1`.

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
        if(arr[i]==x)
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
    int n;
    cin>>n;

    vector<long long> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    long long x;
    cin>>x;

    for(int i=0;i<n;i++)
    {
        if(arr[i]==x)
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

        int n=sc.nextInt();

        long[] arr=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        long x=sc.nextLong();

        for(int i=0;i<n;i++)
        {
            if(arr[i]==x)
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
n=int(input())

arr=list(map(int,input().split()))

x=int(input())

for i in range(n):

    if arr[i]==x:
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
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long x = long.Parse(Console.ReadLine());

        for(int i = 0; i < n; i++)
        {
            if(arr[i] == x)
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
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const arr = [];

for(let i = 0; i < n; i++)
    arr.push(input[idx++]);

const x = input[idx++];

for(let i = 0; i < n; i++)
{
    if(arr[i] === x)
    {
        console.log(i);
        return;
    }
}

console.log(-1);
```

### Output
Input

6

1 3 5 7 9 11

7

Output

3

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Binary Search (Optimal)

### Algorithm

1. Read the sorted array and the target element.
2. Initialize two pointers:

- `low = 0`
- `high = n - 1`

1. While `low <= high`:

- Compute `mid = low + (high - low) / 2`.
- If `arr[mid] == X`, print `mid`.
- If `arr[mid] < X`, search the right half.
- Otherwise, search the left half.

1. If the loop ends without finding `X`, print `-1`.

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

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]==x)
        {
            printf("%d",mid);
            return 0;
        }

        if(arr[mid]<x)
            low=mid+1;
        else
            high=mid-1;
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
    int n;
    cin>>n;

    vector<long long> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    long long x;
    cin>>x;

    int low=0;
    int high=n-1;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]==x)
        {
            cout<<mid;
            return 0;
        }

        if(arr[mid]<x)
            low=mid+1;
        else
            high=mid-1;
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

        int n=sc.nextInt();

        long[] arr=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        long x=sc.nextLong();

        int low=0;
        int high=n-1;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            if(arr[mid]==x)
            {
                System.out.print(mid);
                return;
            }

            if(arr[mid]<x)
                low=mid+1;
            else
                high=mid-1;
        }

        System.out.print(-1);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

x=int(input())

low=0
high=n-1

while low<=high:

    mid=low+(high-low)//2

    if arr[mid]==x:
        print(mid)
        exit()

    if arr[mid]<x:
        low=mid+1
    else:
        high=mid-1

print(-1)
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

        while(low <= high)
        {
            int mid = low + (high - low) / 2;

            if(arr[mid] == x)
            {
                Console.Write(mid);
                return;
            }

            if(arr[mid] < x)
                low = mid + 1;
            else
                high = mid - 1;
        }

        Console.Write(-1);
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

while(low <= high)
{
    const mid = low + Math.floor((high - low) / 2);

    if(arr[mid] === x)
    {
        console.log(mid);
        return;
    }

    if(arr[mid] < x)
        low = mid + 1;
    else
        high = mid - 1;
}

console.log(-1);
```

### Output
Input

6

1 3 5 7 9 11

7

Output

3

# Time Complexity
O(log N)

# Space Complexity
O(1)

</approaches>




