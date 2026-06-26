# Find Peak Element - Solution

## Problem Statement

Given an array of integers `arr` of size `N`, find a peak element and print its index.

An element `arr[i]` is a peak if it is strictly greater than its adjacent elements. For boundary elements, only one adjacent element needs to be checked.

If the array contains multiple peak elements, print the index of any one peak.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers.

## Output Format

Print a single integer representing the index of any peak element.

## Explanation

Since adjacent elements are always different, there is always at least one peak. Using Binary Search, we can determine which half of the array must contain a peak by comparing the middle element with its next element.

For example,

Input

4

1 2 3 1

Output

2

## Algorithm

1. Read the array.
2. Initialize `low = 0` and `high = N - 1`.
3. While `low < high`:

- Find the middle index.
- If `arr[mid] < arr[mid + 1]`, a peak lies on the right, so set `low = mid + 1`.
- Otherwise, a peak lies on the left (including `mid`), so set `high = mid`.

1. When the loop ends, `low` (or `high`) is the index of a peak.
2. Print the index.

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

        if(arr[mid]<arr[mid+1])
            low=mid+1;
        else
            high=mid;
    }

    printf("%d",low);

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

        if(arr[mid]<arr[mid+1])
            low=mid+1;
        else
            high=mid;
    }

    cout<<low;

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

            if(arr[mid]<arr[mid+1])
                low=mid+1;
            else
                high=mid;
        }

        System.out.print(low);
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

    if arr[mid]<arr[mid+1]:
        low=mid+1
    else:
        high=mid

print(low)
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

            if(arr[mid]<arr[mid+1])
                low=mid+1;
            else
                high=mid;
        }

        Console.Write(low);
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

    if(arr[mid]<arr[mid+1])
        low=mid+1;
    else
        high=mid;
}

console.log(low);
```

### Output
Input

4

1 2 3 1

Output

2

# Time Complexity
O(log N)

# Space Complexity
O(1)




