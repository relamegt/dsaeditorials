# Sort the given Matrix - Solution

## Problem Statement

Given a square matrix `Mat` of size `N × N`, sort all of its elements in non-decreasing order and place them back into the matrix row by row.

After sorting, the matrix must be filled from left to right and top to bottom using the sorted sequence.

## Input Format

First line: Integer `N`.

Next `N` lines: `N` space-separated integers representing the matrix.

## Output Format

Print the sorted matrix.

Output exactly `N` lines, each containing `N` space-separated integers.

## Explanation

There is only one optimal approach to solve this problem.

For example,

Input

4

10 20 30 40

15 25 35 45

27 29 37 48

32 33 39 50

Output

10 15 20 25

27 29 30 32

33 35 37 39

40 45 48 50

## Algorithm

1. Read all matrix elements.
2. Store them in a one-dimensional array.
3. Sort the array in non-decreasing order.
4. Fill the matrix row by row using the sorted array.
5. Print the resulting matrix.

```C
#include <stdio.h>
#include <stdlib.h>

int cmp(const void *a,const void *b)
{
    long long x=*(long long*)a;
    long long y=*(long long*)b;

    if(x<y) return -1;
    if(x>y) return 1;
    return 0;
}

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n*n];

    for(int i=0;i<n*n;i++)
        scanf("%lld",&arr[i]);

    qsort(arr,n*n,sizeof(long long),cmp);

    int idx=0;

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
            printf("%lld ",arr[idx++]);
        printf("\n");
    }

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    int n;
    cin>>n;

    vector<long long> arr(n*n);

    for(int i=0;i<n*n;i++)
        cin>>arr[i];

    sort(arr.begin(),arr.end());

    int idx=0;

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
            cout<<arr[idx++]<<" ";
        cout<<"\n";
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

        long[] arr=new long[n*n];

        for(int i=0;i<n*n;i++)
            arr[i]=sc.nextLong();

        Arrays.sort(arr);

        int idx=0;

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
                System.out.print(arr[idx++]+" ");
            System.out.println();
        }
    }
}
```
```Python
n=int(input())

arr=[]

for _ in range(n):
    arr.extend(map(int,input().split()))

arr.sort()

idx=0

for i in range(n):
    for j in range(n):
        print(arr[idx],end=" ")
        idx+=1
    print()
```
```C#
using System;
using System.Linq;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] arr=new long[n*n];

        int idx=0;

        for(int i=0;i<n;i++)
        {
            long[] row=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

            foreach(long x in row)
                arr[idx++]=x;
        }

        Array.Sort(arr);

        idx=0;

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
                Console.Write(arr[idx++]+" ");
            Console.WriteLine();
        }
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const arr=[];

for(let i=0;i<n*n;i++)
    arr.push(input[idx++]);

arr.sort((a,b)=>a-b);

idx=0;

for(let i=0;i<n;i++)
{
    let row=[];

    for(let j=0;j<n;j++)
        row.push(arr[idx++]);

    console.log(row.join(" "));
}
```

### Output
Input

4

10 20 30 40

15 25 35 45

27 29 37 48

32 33 39 50

Output

10 15 20 25

27 29 30 32

33 35 37 39

40 45 48 50

# Time Complexity
O(N² log(N²))

# Space Complexity
O(N²)




