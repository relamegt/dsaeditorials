# Search in an Almost Sorted Array - Solution

## Problem Statement

Given an almost sorted array `arr` of size `N` and an integer `X`, find the index of `X`.

An array is called almost sorted if every element that should be at index `i` in the fully sorted array may be present at index `i`, `i - 1`, or `i + 1`.

If `X` is present, print its index. Otherwise, print `-1`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing the almost sorted array.

Third line: Integer `X`

## Output Format

Print a single integer representing the index of `X`, or `-1` if `X` is not present.

## Explanation

There are two common approaches to solve this problem.

- **Linear Search:** Check every element one by one.
- **Modified Binary Search (Optimal):** Since every element can be misplaced by at most one position, check the middle element and its adjacent elements before deciding which half to search.

For example,

Input

7

10 3 40 20 50 80 70

40

Output

2

<approaches>
## Approach 1: Linear Search

### Algorithm

1. Read the array and the value `X`.
2. Traverse the array from left to right.
3. If `arr[i] == X`, print `i`.
4. If the loop finishes without finding `X`, print `-1`.

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
        int n=int.Parse(Console.ReadLine());

        long[] arr=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        long x=long.Parse(Console.ReadLine());

        for(int i=0;i<n;i++)
        {
            if(arr[i]==x)
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
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const arr=[];

for(let i=0;i<n;i++)
    arr.push(input[idx++]);

const x=input[idx++];

for(let i=0;i<n;i++)
{
    if(arr[i]===x)
    {
        console.log(i);
        return;
    }
}

console.log(-1);
```

### Output
Input

7

10 3 40 20 50 80 70

40

Output

2

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Modified Binary Search (Optimal)

### Algorithm

1. Read the array and the value `X`.
2. Initialize `low = 0` and `high = N - 1`.
3. While `low <= high`:

- Find the middle index.
- If `arr[mid] == X`, print `mid`.
- If `mid > low` and `arr[mid - 1] == X`, print `mid - 1`.
- If `mid < high` and `arr[mid + 1] == X`, print `mid + 1`.
- If `arr[mid] > X`, search the left half by setting `high = mid - 2`.
- Otherwise, search the right half by setting `low = mid + 2`.

1. If the loop finishes, print `-1`.

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

        if(mid>low && arr[mid-1]==x)
        {
            printf("%d",mid-1);
            return 0;
        }

        if(mid<high && arr[mid+1]==x)
        {
            printf("%d",mid+1);
            return 0;
        }

        if(arr[mid]>x)
            high=mid-2;
        else
            low=mid+2;
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

        if(mid>low && arr[mid-1]==x)
        {
            cout<<mid-1;
            return 0;
        }

        if(mid<high && arr[mid+1]==x)
        {
            cout<<mid+1;
            return 0;
        }

        if(arr[mid]>x)
            high=mid-2;
        else
            low=mid+2;
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

            if(mid>low && arr[mid-1]==x)
            {
                System.out.print(mid-1);
                return;
            }

            if(mid<high && arr[mid+1]==x)
            {
                System.out.print(mid+1);
                return;
            }

            if(arr[mid]>x)
                high=mid-2;
            else
                low=mid+2;
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
        break

    if mid>low and arr[mid-1]==x:
        print(mid-1)
        break

    if mid<high and arr[mid+1]==x:
        print(mid+1)
        break

    if arr[mid]>x:
        high=mid-2
    else:
        low=mid+2
else:
    print(-1)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] arr=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        long x=long.Parse(Console.ReadLine());

        int low=0;
        int high=n-1;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            if(arr[mid]==x)
            {
                Console.Write(mid);
                return;
            }

            if(mid>low && arr[mid-1]==x)
            {
                Console.Write(mid-1);
                return;
            }

            if(mid<high && arr[mid+1]==x)
            {
                Console.Write(mid+1);
                return;
            }

            if(arr[mid]>x)
                high=mid-2;
            else
                low=mid+2;
        }

        Console.Write(-1);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const arr=[];

for(let i=0;i<n;i++)
    arr.push(input[idx++]);

const x=input[idx++];

let low=0;
let high=n-1;

while(low<=high)
{
    const mid=low+Math.floor((high-low)/2);

    if(arr[mid]===x)
    {
        console.log(mid);
        return;
    }

    if(mid>low && arr[mid-1]===x)
    {
        console.log(mid-1);
        return;
    }

    if(mid<high && arr[mid+1]===x)
    {
        console.log(mid+1);
        return;
    }

    if(arr[mid]>x)
        high=mid-2;
    else
        low=mid+2;
}

console.log(-1);
```

### Output
Input

7

10 3 40 20 50 80 70

40

Output

2

# Time Complexity
O(log N)

# Space Complexity
O(1)

</approaches>




