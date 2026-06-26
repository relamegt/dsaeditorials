# Search Insert Position - Solution

## Problem Statement

Given a sorted array of distinct integers `arr` of size `N` and an integer `X`, return the index if `X` is found. Otherwise, return the index where it would be inserted so that the array remains sorted.

## Input Format

First line: Integer `N`

Second line: `N` space-separated distinct integers in strictly increasing order

Third line: Integer `X`

## Output Format

Print a single integer representing the required index.

## Explanation

Since the array is sorted, Binary Search can efficiently find either the position of `X` or the position where it should be inserted while maintaining sorted order.

For example,

Input

4

1 3 5 6

2

Output

1

## Algorithm

1. Read the array and the value `X`.
2. Initialize `low = 0`, `high = N - 1`, and `answer = N`.
3. Perform Binary Search:

- If `arr[mid] == X`, print `mid`.
- If `arr[mid] > X`, update `answer = mid` and search the left half.
- Otherwise, search the right half.

1. If `X` is not found, print `answer`.

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

        if(arr[mid]==x)
        {
            printf("%d",mid);
            return 0;
        }

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

        if(arr[mid]==x)
        {
            cout<<mid;
            return 0;
        }

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

            if(arr[mid]==x)
            {
                System.out.print(mid);
                return;
            }

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

    if arr[mid]==x:
        print(mid)
        exit()

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
        int n=int.Parse(Console.ReadLine());

        long[] arr=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        long x=long.Parse(Console.ReadLine());

        int low=0;
        int high=n-1;
        int answer=n;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            if(arr[mid]==x)
            {
                Console.Write(mid);
                return;
            }

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

        Console.Write(answer);
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
let answer=n;

while(low<=high)
{
    const mid=low+Math.floor((high-low)/2);

    if(arr[mid]===x)
    {
        console.log(mid);
        return;
    }

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

console.log(answer);
```

### Output
Input

4

1 3 5 6

2

Output

1

# Time Complexity
O(log N)

# Space Complexity
O(1)




