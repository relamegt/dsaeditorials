# Search in Rotated Sorted Array - Solution

## Problem Statement

Given a sorted array of distinct integers that has been rotated at an unknown pivot, and an integer `X`, find the index of `X`. If `X` is not present, print `-1`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated distinct integers

Third line: Integer `X`

## Output Format

Print a single integer representing the index of `X`, or `-1` if it is not present.

## Explanation

Even though the array is rotated, one half of the array is always sorted. Using Binary Search, we can determine which half is sorted and decide where to continue searching.

For example,

Input

7

4 5 6 7 0 1 2

0

Output

4

## Algorithm

1. Read the array and the value `X`.
2. Initialize `low = 0` and `high = N - 1`.
3. While `low <= high`:

- Find the middle index.
- If `arr[mid] == X`, print `mid`.
- If the left half is sorted:
- Check whether `X` lies in the left half.
- Otherwise, search the right half.
- Otherwise, the right half is sorted:
- Check whether `X` lies in the right half.
- Otherwise, search the left half.

1. If the loop ends, print `-1`.

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

        if(arr[low]<=arr[mid])
        {
            if(x>=arr[low] && x<arr[mid])
                high=mid-1;
            else
                low=mid+1;
        }
        else
        {
            if(x>arr[mid] && x<=arr[high])
                low=mid+1;
            else
                high=mid-1;
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

        if(arr[low]<=arr[mid])
        {
            if(x>=arr[low] && x<arr[mid])
                high=mid-1;
            else
                low=mid+1;
        }
        else
        {
            if(x>arr[mid] && x<=arr[high])
                low=mid+1;
            else
                high=mid-1;
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

            if(arr[low]<=arr[mid])
            {
                if(x>=arr[low] && x<arr[mid])
                    high=mid-1;
                else
                    low=mid+1;
            }
            else
            {
                if(x>arr[mid] && x<=arr[high])
                    low=mid+1;
                else
                    high=mid-1;
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

low=0
high=n-1

while low<=high:

    mid=low+(high-low)//2

    if arr[mid]==x:
        print(mid)
        exit()

    if arr[low]<=arr[mid]:

        if arr[low]<=x<arr[mid]:
            high=mid-1
        else:
            low=mid+1
    else:

        if arr[mid]<x<=arr[high]:
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

            if(arr[low]<=arr[mid])
            {
                if(x>=arr[low] && x<arr[mid])
                    high=mid-1;
                else
                    low=mid+1;
            }
            else
            {
                if(x>arr[mid] && x<=arr[high])
                    low=mid+1;
                else
                    high=mid-1;
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

    if(arr[low]<=arr[mid])
    {
        if(x>=arr[low] && x<arr[mid])
            high=mid-1;
        else
            low=mid+1;
    }
    else
    {
        if(x>arr[mid] && x<=arr[high])
            low=mid+1;
        else
            high=mid-1;
    }
}

console.log(-1);
```

### Output
Input

7

4 5 6 7 0 1 2

0

Output

4

# Time Complexity
O(log N)

# Space Complexity
O(1)




