# Find Minimum in Rotated Sorted Array - Solution

## Problem Statement

Given a sorted array of distinct integers that has been rotated between `0` and `N - 1` times, find the minimum element in the array.

## Input Format

First line: Integer `N`

Second line: `N` space-separated distinct integers.

## Output Format

Print a single integer representing the minimum element.

## Explanation

The array consists of two sorted parts. Using Binary Search, we can determine which half contains the minimum element and reduce the search space in each step.

For example,

Input

5

3 4 5 1 2

Output

1

## Algorithm

1. Read the array.
2. Initialize `low = 0` and `high = N - 1`.
3. While `low < high`:

- Find the middle index.
- If `arr[mid] > arr[high]`, the minimum lies in the right half, so set `low = mid + 1`.
- Otherwise, the minimum lies in the left half (including `mid`), so set `high = mid`.

1. Print `arr[low]`.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    int low=0;
    int high=n-1;

    while(low<high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]>arr[high])
            low=mid+1;
        else
            high=mid;
    }

    printf("%lld",arr[low]);

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

    int low=0;
    int high=n-1;

    while(low<high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]>arr[high])
            low=mid+1;
        else
            high=mid;
    }

    cout<<arr[low];

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

        int low=0;
        int high=n-1;

        while(low<high)
        {
            int mid=low+(high-low)/2;

            if(arr[mid]>arr[high])
                low=mid+1;
            else
                high=mid;
        }

        System.out.print(arr[low]);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

low=0
high=n-1

while low<high:

    mid=low+(high-low)//2

    if arr[mid]>arr[high]:
        low=mid+1
    else:
        high=mid

print(arr[low])
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] arr=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        int low=0;
        int high=n-1;

        while(low<high)
        {
            int mid=low+(high-low)/2;

            if(arr[mid]>arr[high])
                low=mid+1;
            else
                high=mid;
        }

        Console.Write(arr[low]);
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

let low=0;
let high=n-1;

while(low<high)
{
    const mid=low+Math.floor((high-low)/2);

    if(arr[mid]>arr[high])
        low=mid+1;
    else
        high=mid;
}

console.log(arr[low]);
```

### Output
Input

5

3 4 5 1 2

Output

1

# Time Complexity
O(log N)

# Space Complexity
O(1)




