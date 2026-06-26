# First and Last Occurrence of an Element - Solution

## Problem Statement

Given a sorted array of integers `arr` of size `N` in non-decreasing order and an integer `X`, find the first and last occurrence of `X` in the array.

If `X` is not present, print `-1 -1`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers in non-decreasing order

Third line: Integer `X`

## Output Format

Print two space-separated integers: `first_index last_index`.

## Explanation

Since the array is sorted, Binary Search can efficiently find both the first and last occurrence of `X` in `O(log N)` time.

For example,

Input

6

1 2 2 2 3 4

2

Output

1 3

## Algorithm

1. Read the array and the value `X`.
2. Perform a binary search to find the first occurrence:

- If `arr[mid] == X`, store the index and continue searching on the left.

1. Perform another binary search to find the last occurrence:

- If `arr[mid] == X`, store the index and continue searching on the right.

1. Print the first and last occurrence.

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
    int first=-1;
    int last=-1;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]==x)
        {
            first=mid;
            high=mid-1;
        }
        else if(arr[mid]<x)
            low=mid+1;
        else
            high=mid-1;
    }

    low=0;
    high=n-1;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]==x)
        {
            last=mid;
            low=mid+1;
        }
        else if(arr[mid]<x)
            low=mid+1;
        else
            high=mid-1;
    }

    printf("%d %d",first,last);

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
    int first=-1;
    int last=-1;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]==x)
        {
            first=mid;
            high=mid-1;
        }
        else if(arr[mid]<x)
            low=mid+1;
        else
            high=mid-1;
    }

    low=0;
    high=n-1;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]==x)
        {
            last=mid;
            low=mid+1;
        }
        else if(arr[mid]<x)
            low=mid+1;
        else
            high=mid-1;
    }

    cout<<first<<" "<<last;

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
        int first=-1;
        int last=-1;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            if(arr[mid]==x)
            {
                first=mid;
                high=mid-1;
            }
            else if(arr[mid]<x)
                low=mid+1;
            else
                high=mid-1;
        }

        low=0;
        high=n-1;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            if(arr[mid]==x)
            {
                last=mid;
                low=mid+1;
            }
            else if(arr[mid]<x)
                low=mid+1;
            else
                high=mid-1;
        }

        System.out.print(first+" "+last);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

x=int(input())

low=0
high=n-1

first=-1
last=-1

while low<=high:

    mid=low+(high-low)//2

    if arr[mid]==x:
        first=mid
        high=mid-1
    elif arr[mid]<x:
        low=mid+1
    else:
        high=mid-1

low=0
high=n-1

while low<=high:

    mid=low+(high-low)//2

    if arr[mid]==x:
        last=mid
        low=mid+1
    elif arr[mid]<x:
        low=mid+1
    else:
        high=mid-1

print(first,last)
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
        int first=-1;
        int last=-1;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            if(arr[mid]==x)
            {
                first=mid;
                high=mid-1;
            }
            else if(arr[mid]<x)
                low=mid+1;
            else
                high=mid-1;
        }

        low=0;
        high=n-1;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            if(arr[mid]==x)
            {
                last=mid;
                low=mid+1;
            }
            else if(arr[mid]<x)
                low=mid+1;
            else
                high=mid-1;
        }

        Console.Write(first+" "+last);
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

let first=-1;
let last=-1;

while(low<=high)
{
    const mid=low+Math.floor((high-low)/2);

    if(arr[mid]===x)
    {
        first=mid;
        high=mid-1;
    }
    else if(arr[mid]<x)
        low=mid+1;
    else
        high=mid-1;
}

low=0;
high=n-1;

while(low<=high)
{
    const mid=low+Math.floor((high-low)/2);

    if(arr[mid]===x)
    {
        last=mid;
        low=mid+1;
    }
    else if(arr[mid]<x)
        low=mid+1;
    else
        high=mid-1;
}

console.log(first+" "+last);
```

### Output
Input

6

1 2 2 2 3 4

2

Output

1 3

# Time Complexity
O(log N)

# Space Complexity
O(1)




