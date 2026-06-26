# Counting Sort - Solution

## Problem Statement

Given an array of integers `arr` of size `N` where every element lies in the range `0` to `K` inclusive, sort the array in non-decreasing order using the Counting Sort algorithm.

## Input Format

First line: Two space-separated integers `N` and `K`

Second line: `N` space-separated integers representing the array.

## Output Format

Print the sorted array in a single line as `N` space-separated integers.

## Explanation

Counting Sort counts the frequency of each element and reconstructs the sorted array based on these frequencies. It is efficient when the range of input values is limited.

For example,

Input

7 9

4 2 2 8 3 3 1

Output

1 2 2 3 3 4 8

## Algorithm

1. Read `N`, `K`, and the array.
2. Create a frequency array of size `K + 1` initialized with zeros.
3. Traverse the array and increment the count for each element.
4. Traverse the frequency array from `0` to `K`.
5. Print each value according to its frequency.

```C
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int n,k;
    scanf("%d %d",&n,&k);

    int arr[n];
    int *count=(int*)calloc(k+1,sizeof(int));

    for(int i=0;i<n;i++)
    {
        scanf("%d",&arr[i]);
        count[arr[i]]++;
    }

    for(int i=0;i<=k;i++)
    {
        while(count[i]--)
            printf("%d ",i);
    }

    free(count);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int n,k;
    cin>>n>>k;

    vector<int> count(k+1,0);

    for(int i=0;i<n;i++)
    {
        int x;
        cin>>x;
        count[x]++;
    }

    for(int i=0;i<=k;i++)
    {
        while(count[i]--)
            cout<<i<<" ";
    }

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
        int k=sc.nextInt();

        int[] count=new int[k+1];

        for(int i=0;i<n;i++)
        {
            int x=sc.nextInt();
            count[x]++;
        }

        for(int i=0;i<=k;i++)
        {
            while(count[i]-- > 0)
                System.out.print(i+" ");
        }
    }
}
```
```Python
n,k=map(int,input().split())

arr=list(map(int,input().split()))

count=[0]*(k+1)

for x in arr:
    count[x]+=1

for i in range(k+1):

    while count[i]>0:
        print(i,end=" ")
        count[i]-=1
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] first=Console.ReadLine().Split();

        int n=int.Parse(first[0]);
        int k=int.Parse(first[1]);

        int[] arr=Array.ConvertAll(Console.ReadLine().Split(),int.Parse);

        int[] count=new int[k+1];

        foreach(int x in arr)
            count[x]++;

        for(int i=0;i<=k;i++)
        {
            while(count[i]-- > 0)
                Console.Write(i+" ");
        }
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];
const k=input[idx++];

const count=new Array(k+1).fill(0);

for(let i=0;i<n;i++)
    count[input[idx++]]++;

let ans=[];

for(let i=0;i<=k;i++)
{
    while(count[i]-->0)
        ans.push(i);
}

console.log(ans.join(" "));
```

### Output
Input

7 9

4 2 2 8 3 3 1

Output

1 2 2 3 3 4 8

# Time Complexity
O(N + K)

# Space Complexity
O(K)




