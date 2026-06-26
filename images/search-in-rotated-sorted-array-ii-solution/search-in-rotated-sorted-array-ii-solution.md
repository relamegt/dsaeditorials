# Search in Rotated Sorted Array II - Solution

## Problem Statement

Given a sorted array that has been rotated at an unknown pivot and may contain duplicate elements, determine whether a target `X` exists in the array.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers

Third line: Integer `X`

## Output Format

Print `true` if `X` is present in the array, otherwise print `false`.

## Explanation

The array may contain duplicate elements, making it impossible to always determine the sorted half directly. When the left, middle, and right elements are equal, shrink the search space by moving both ends inward.

For example,

Input

7

2 5 6 0 0 1 2

0

Output

true

## Algorithm

1. Read the array and the value `X`.
2. Initialize `low = 0` and `high = N - 1`.
3. While `low <= high`:

- Find the middle index.
- If `arr[mid] == X`, print `true`.
- If `arr[low] == arr[mid] == arr[high]`, increment `low` and decrement `high`.
- Otherwise, determine which half is sorted.
- Continue searching in the appropriate half.

1. If the loop ends, print `false`.

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
            printf("true");
            return 0;
        }

        if(arr[low]==arr[mid] && arr[mid]==arr[high])
        {
            low++;
            high--;
        }
        else if(arr[low]<=arr[mid])
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

    printf("false");

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
            cout<<"true";
            return 0;
        }

        if(arr[low]==arr[mid] && arr[mid]==arr[high])
        {
            low++;
            high--;
        }
        else if(arr[low]<=arr[mid])
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

    cout<<"false";

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
                System.out.print("true");
                return;
            }

            if(arr[low]==arr[mid] && arr[mid]==arr[high])
            {
                low++;
                high--;
            }
            else if(arr[low]<=arr[mid])
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

        System.out.print("false");
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
        print("true")
        exit()

    if arr[low]==arr[mid]==arr[high]:
        low+=1
        high-=1

    elif arr[low]<=arr[mid]:

        if arr[low]<=x<arr[mid]:
            high=mid-1
        else:
            low=mid+1

    else:

        if arr[mid]<x<=arr[high]:
            low=mid+1
        else:
            high=mid-1

print("false")
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
                Console.Write("true");
                return;
            }

            if(arr[low]==arr[mid] && arr[mid]==arr[high])
            {
                low++;
                high--;
            }
            else if(arr[low]<=arr[mid])
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

        Console.Write("false");
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
        console.log("true");
        return;
    }

    if(arr[low]===arr[mid] && arr[mid]===arr[high])
    {
        low++;
        high--;
    }
    else if(arr[low]<=arr[mid])
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

console.log("false");
```

### Output
Input

7

2 5 6 0 0 1 2

0

Output

true

# Time Complexity
Average Case: O(log N)
Worst Case: O(N)

# Space Complexity
O(1)




