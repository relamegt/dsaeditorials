# Selection Sort - Solution

## Problem Statement

Given an array of integers `arr` of size `N`, sort the array in non-decreasing order using the Selection Sort algorithm.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing the array.

## Output Format

Print the sorted array in a single line as `N` space-separated integers.

## Explanation

Selection Sort repeatedly finds the smallest element from the unsorted part of the array and places it at its correct position in the sorted part.

For example,

Input

5

7 4 1 5 3

Output

1 3 4 5 7

## Algorithm

1. Read the array.
2. For each position `i` from `0` to `N-2`:

- Assume the current position contains the minimum element.
- Traverse the remaining unsorted portion to find the actual minimum element.
- Swap the minimum element with the element at position `i`.

1. Print the sorted array.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    for(int i=0;i<n-1;i++)
    {
        int minIndex=i;

        for(int j=i+1;j<n;j++)
        {
            if(arr[j]<arr[minIndex])
                minIndex=j;
        }

        long long temp=arr[i];
        arr[i]=arr[minIndex];
        arr[minIndex]=temp;
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

    for(int i=0;i<n-1;i++)
    {
        int minIndex=i;

        for(int j=i+1;j<n;j++)
        {
            if(arr[j]<arr[minIndex])
                minIndex=j;
        }

        swap(arr[i],arr[minIndex]);
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

        for(int i=0;i<n-1;i++)
        {
            int minIndex=i;

            for(int j=i+1;j<n;j++)
            {
                if(arr[j]<arr[minIndex])
                    minIndex=j;
            }

            long temp=arr[i];
            arr[i]=arr[minIndex];
            arr[minIndex]=temp;
        }

        for(long x:arr)
            System.out.print(x+" ");
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

for i in range(n-1):

    minIndex=i

    for j in range(i+1,n):

        if arr[j]<arr[minIndex]:
            minIndex=j

    arr[i],arr[minIndex]=arr[minIndex],arr[i]

print(*arr)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        for(int i = 0; i < n - 1; i++)
        {
            int minIndex = i;

            for(int j = i + 1; j < n; j++)
            {
                if(arr[j] < arr[minIndex])
                    minIndex = j;
            }

            long temp = arr[i];
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }

        foreach(long x in arr)
            Console.Write(x + " ");
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

for(let i = 0; i < n - 1; i++)
{
    let minIndex = i;

    for(let j = i + 1; j < n; j++)
    {
        if(arr[j] < arr[minIndex])
            minIndex = j;
    }

    let temp = arr[i];
    arr[i] = arr[minIndex];
    arr[minIndex] = temp;
}

console.log(arr.join(" "));
```

### Output
Input

5

7 4 1 5 3

Output

1 3 4 5 7

# Time Complexity
O(N²)

# Space Complexity
O(1)




