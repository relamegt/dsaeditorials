# Insertion Sort - Solution

## Problem Statement

Given an array of integers `arr` of size `N`, sort the array in non-decreasing order using the Insertion Sort algorithm.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing the array.

## Output Format

Print the sorted array in a single line as `N` space-separated integers.

## Explanation

Insertion Sort builds the sorted array one element at a time by inserting each element into its correct position among the previously sorted elements.

For example,

Input

6

5 2 4 6 1 3

Output

1 2 3 4 5 6

## Algorithm

1. Read the array.
2. Start from the second element (`i = 1`).
3. Store the current element as `key`.
4. Compare `key` with elements before it and shift larger elements one position to the right.
5. Insert `key` into its correct position.
6. Repeat until all elements are processed.
7. Print the sorted array.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    for(int i=1;i<n;i++)
    {
        long long key=arr[i];
        int j=i-1;

        while(j>=0 && arr[j]>key)
        {
            arr[j+1]=arr[j];
            j--;
        }

        arr[j+1]=key;
    }

    for(int i=0;i<n;i++)
        printf("%lld ",arr[i]);

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

    for(int i=1;i<n;i++)
    {
        long long key=arr[i];
        int j=i-1;

        while(j>=0 && arr[j]>key)
        {
            arr[j+1]=arr[j];
            j--;
        }

        arr[j+1]=key;
    }

    for(long long x:arr)
        cout<<x<<" ";

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

        for(int i=1;i<n;i++)
        {
            long key=arr[i];
            int j=i-1;

            while(j>=0 && arr[j]>key)
            {
                arr[j+1]=arr[j];
                j--;
            }

            arr[j+1]=key;
        }

        for(long x:arr)
            System.out.print(x+" ");
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

for i in range(1,n):

    key=arr[i]
    j=i-1

    while j>=0 and arr[j]>key:
        arr[j+1]=arr[j]
        j-=1

    arr[j+1]=key

print(*arr)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] arr=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        for(int i=1;i<n;i++)
        {
            long key=arr[i];
            int j=i-1;

            while(j>=0 && arr[j]>key)
            {
                arr[j+1]=arr[j];
                j--;
            }

            arr[j+1]=key;
        }

        foreach(long x in arr)
            Console.Write(x+" ");
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

for(let i=1;i<n;i++)
{
    let key=arr[i];
    let j=i-1;

    while(j>=0 && arr[j]>key)
    {
        arr[j+1]=arr[j];
        j--;
    }

    arr[j+1]=key;
}

console.log(arr.join(" "));
```

### Output
Input

6

5 2 4 6 1 3

Output

1 2 3 4 5 6

# Time Complexity
Best Case: O(N)
Average Case: O(N²)
Worst Case: O(N²)

# Space Complexity
O(1)




