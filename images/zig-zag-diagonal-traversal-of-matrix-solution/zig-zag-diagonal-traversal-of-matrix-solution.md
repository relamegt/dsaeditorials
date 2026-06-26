# Zig-Zag Diagonal Traversal of Matrix - Solution

## Problem Statement

Given a matrix of size `N × M`, print all its elements in zig-zag diagonal order.

The traversal starts from the top-left element. Elements are printed diagonal by diagonal, and the direction alternates for every diagonal.

## Input Format

First line: Two integers `N` and `M`.

Next `N` lines: `M` space-separated integers representing the matrix.

## Output Format

Print all matrix elements in zig-zag diagonal order as space-separated integers.

## Explanation

There is only one optimal approach to solve this problem.

For example,

Input

3 3

1 2 3

4 5 6

7 8 9

Output

1 2 4 7 5 3 6 8 9

## Algorithm

1. Traverse all diagonals from `0` to `N + M - 2`.
2. For each diagonal, collect all valid elements.
3. If the diagonal number is even, print the collected elements in reverse order.
4. Otherwise, print them in the same order.
5. Continue until all diagonals are processed.

```C
#include <stdio.h>

int main()
{
    int n,m;
    scanf("%d%d",&n,&m);

    long long a[n][m];

    for(int i=0;i<n;i++)
        for(int j=0;j<m;j++)
            scanf("%lld",&a[i][j]);

    long long temp[1000];

    for(int d=0;d<n+m-1;d++)
    {
        int k=0;

        int row=d<m?0:d-m+1;
        int col=d<m?d:m-1;

        while(row<n && col>=0)
        {
            temp[k++]=a[row][col];
            row++;
            col--;
        }

        if(d%2==0)
        {
            for(int i=k-1;i>=0;i--)
                printf("%lld ",temp[i]);
        }
        else
        {
            for(int i=0;i<k;i++)
                printf("%lld ",temp[i]);
        }
    }

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int n,m;
    cin>>n>>m;

    vector<vector<long long>> a(n,vector<long long>(m));

    for(int i=0;i<n;i++)
        for(int j=0;j<m;j++)
            cin>>a[i][j];

    vector<long long> temp;

    for(int d=0;d<n+m-1;d++)
    {
        temp.clear();

        int row=d<m?0:d-m+1;
        int col=d<m?d:m-1;

        while(row<n && col>=0)
        {
            temp.push_back(a[row][col]);
            row++;
            col--;
        }

        if(d%2==0)
        {
            for(int i=temp.size()-1;i>=0;i--)
                cout<<temp[i]<<" ";
        }
        else
        {
            for(long long x:temp)
                cout<<x<<" ";
        }
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
        int m=sc.nextInt();

        long[][] a=new long[n][m];

        for(int i=0;i<n;i++)
            for(int j=0;j<m;j++)
                a[i][j]=sc.nextLong();

        ArrayList<Long> temp=new ArrayList<>();

        for(int d=0;d<n+m-1;d++)
        {
            temp.clear();

            int row=d<m?0:d-m+1;
            int col=d<m?d:m-1;

            while(row<n && col>=0)
            {
                temp.add(a[row][col]);
                row++;
                col--;
            }

            if(d%2==0)
            {
                for(int i=temp.size()-1;i>=0;i--)
                    System.out.print(temp.get(i)+" ");
            }
            else
            {
                for(long x:temp)
                    System.out.print(x+" ");
            }
        }
    }
}
```
```Python
n,m=map(int,input().split())

a=[list(map(int,input().split())) for _ in range(n)]

for d in range(n+m-1):

    temp=[]

    row=0 if d<m else d-m+1
    col=d if d<m else m-1

    while row<n and col>=0:
        temp.append(a[row][col])
        row+=1
        col-=1

    if d%2==0:
        for x in temp[::-1]:
            print(x,end=" ")
    else:
        for x in temp:
            print(x,end=" ")
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        string[] first=Console.ReadLine().Split();

        int n=int.Parse(first[0]);
        int m=int.Parse(first[1]);

        long[][] a=new long[n][];

        for(int i=0;i<n;i++)
            a[i]=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        List<long> temp=new List<long>();

        for(int d=0;d<n+m-1;d++)
        {
            temp.Clear();

            int row=d<m?0:d-m+1;
            int col=d<m?d:m-1;

            while(row<n && col>=0)
            {
                temp.Add(a[row][col]);
                row++;
                col--;
            }

            if(d%2==0)
            {
                for(int i=temp.Count-1;i>=0;i--)
                    Console.Write(temp[i]+" ");
            }
            else
            {
                foreach(long x in temp)
                    Console.Write(x+" ");
            }
        }
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];
const m=input[idx++];

const a=Array.from({length:n},()=>Array(m));

for(let i=0;i<n;i++)
    for(let j=0;j<m;j++)
        a[i][j]=input[idx++];

const ans=[];

for(let d=0;d<n+m-1;d++)
{
    const temp=[];

    let row=d<m?0:d-m+1;
    let col=d<m?d:m-1;

    while(row<n && col>=0)
    {
        temp.push(a[row][col]);
        row++;
        col--;
    }

    if(d%2===0)
    {
        for(let i=temp.length-1;i>=0;i--)
            ans.push(temp[i]);
    }
    else
    {
        for(const x of temp)
            ans.push(x);
    }
}

console.log(ans.join(" "));
```

### Output
Input

3 3

1 2 3

4 5 6

7 8 9

Output

1 2 4 7 5 3 6 8 9

# Time Complexity
O(N × M)

# Space Complexity
O(min(N, M))




