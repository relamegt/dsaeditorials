# Check if Array is Sorted and Rotated - Solution

## Problem Statement

Given an array of integers `arr` of size `N`, determine whether the array was originally sorted in non-decreasing order and then rotated some number of positions, including zero.

Print `true` if it is possible, otherwise print `false`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers.

## Output Format

Print `true` or `false`.

## Explanation

In a sorted and rotated array, there can be at most one position where an element is greater than its next element. Also, the last element should not be greater than the first element after rotation.

For example,

Input

5

3 4 5 1 2

Output

true

## Algorithm

1. Read the array.
2. Initialize a counter `count = 0`.
3. Traverse the array:

- If `arr[i] > arr[(i + 1) % N]`, increment `count`.

1. If `count <= 1`, print `true`.
2. Otherwise, print `false`.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    int count=0;

    for(int i=0;i<n;i++)
    {
        if(arr[i]>arr[(i+1)%n])
            count++;
    }

    if(count<=1)
        printf("true");
    else
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

    int count=0;

    for(int i=0;i<n;i++)
    {
        if(arr[i]>arr[(i+1)%n])
            count++;
    }

    if(count<=1)
        cout<<"true";
    else
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

        int count=0;

        for(int i=0;i<n;i++)
        {
            if(arr[i]>arr[(i+1)%n])
                count++;
        }

        if(count<=1)
            System.out.print("true");
        else
            System.out.print("false");
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

count=0

for i in range(n):

    if arr[i]>arr[(i+1)%n]:
        count+=1

if count<=1:
    print("true")
else:
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

        int count=0;

        for(int i=0;i<n;i++)
        {
            if(arr[i]>arr[(i+1)%n])
                count++;
        }

        if(count<=1)
            Console.Write("true");
        else
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

let count=0;

for(let i=0;i<n;i++)
{
    if(arr[i]>arr[(i+1)%n])
        count++;
}

if(count<=1)
    console.log("true");
else
    console.log("false");
```

### Output
Input

5

3 4 5 1 2

Output

true

# Time Complexity
O(N)

# Space Complexity
O(1)




