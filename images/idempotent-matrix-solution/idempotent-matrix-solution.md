# Idempotent Matrix - Solution

## Problem Statement

Given a square matrix `A` of size `N × N`, determine whether it is an idempotent matrix.

A matrix is idempotent if multiplying it by itself gives the same matrix, that is,

`A × A = A`

## Input Format

First line: Integer `N`.

Next `N` lines: `N` space-separated integers representing the matrix.

## Output Format

Print `1` if the matrix is idempotent.

Otherwise, print `0`.

## Explanation

There is only one optimal approach to solve this problem.

For example,

Input

2

3 -6

1 -2

Output

1

## Algorithm

1. Read the matrix.
2. Compute the matrix product `A × A`.
3. Compare every element of the product with the corresponding element of the original matrix.
4. If any element differs, print `0`.
5. Otherwise, print `1`.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long a[n][n],b[n][n];

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            scanf("%lld",&a[i][j]);

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            b[i][j]=0;

            for(int k=0;k<n;k++)
                b[i][j]+=a[i][k]*a[k][j];
        }
    }

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            if(a[i][j]!=b[i][j])
            {
                printf("0");
                return 0;
            }
        }
    }

    printf("1");

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

    vector<vector<long long>> a(n,vector<long long>(n));
    vector<vector<long long>> b(n,vector<long long>(n,0));

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            cin>>a[i][j];

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            for(int k=0;k<n;k++)
                b[i][j]+=a[i][k]*a[k][j];
        }
    }

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            if(a[i][j]!=b[i][j])
            {
                cout<<0;
                return 0;
            }
        }
    }

    cout<<1;

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

        long[][] a=new long[n][n];
        long[][] b=new long[n][n];

        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                a[i][j]=sc.nextLong();

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
            {
                for(int k=0;k<n;k++)
                    b[i][j]+=a[i][k]*a[k][j];
            }
        }

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
            {
                if(a[i][j]!=b[i][j])
                {
                    System.out.print(0);
                    return;
                }
            }
        }

        System.out.print(1);
    }
}
```
```Python
n=int(input())

a=[list(map(int,input().split())) for _ in range(n)]

b=[[0]*n for _ in range(n)]

for i in range(n):
    for j in range(n):
        for k in range(n):
            b[i][j]+=a[i][k]*a[k][j]

for i in range(n):
    for j in range(n):
        if a[i][j]!=b[i][j]:
            print(0)
            exit()

print(1)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[][] a=new long[n][];
        long[][] b=new long[n][];

        for(int i=0;i<n;i++)
        {
            a[i]=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);
            b[i]=new long[n];
        }

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
            {
                for(int k=0;k<n;k++)
                    b[i][j]+=a[i][k]*a[k][j];
            }
        }

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
            {
                if(a[i][j]!=b[i][j])
                {
                    Console.Write(0);
                    return;
                }
            }
        }

        Console.Write(1);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const a=Array.from({length:n},()=>Array(n));
const b=Array.from({length:n},()=>Array(n).fill(0));

for(let i=0;i<n;i++)
    for(let j=0;j<n;j++)
        a[i][j]=input[idx++];

for(let i=0;i<n;i++)
{
    for(let j=0;j<n;j++)
    {
        for(let k=0;k<n;k++)
            b[i][j]+=a[i][k]*a[k][j];
    }
}

for(let i=0;i<n;i++)
{
    for(let j=0;j<n;j++)
    {
        if(a[i][j]!==b[i][j])
        {
            console.log(0);
            return;
        }
    }
}

console.log(1);
```

### Output
Input

2

3 -6

1 -2

Output

1

# Time Complexity
O(N³)

# Space Complexity
O(N²)




