# Print Matrix in Wave Form - Solution

## Problem Statement

Given a matrix of size `N × M`, print its elements in vertical wave form.

In wave form traversal:

- Print the first column from top to bottom.
- Print the second column from bottom to top.
- Print the third column from top to bottom.
- Continue alternating in this pattern.

## Input Format

First line: Two integers `N` and `M`.

Next `N` lines: `M` space-separated integers representing the matrix.

## Output Format

Print all matrix elements in wave form as space-separated integers.

## Explanation

There is only one optimal approach to solve this problem.

For example,

Input

4 4

1 2 3 4

5 6 7 8

9 10 11 12

13 14 15 16

Output

1 5 9 13 14 10 6 2 3 7 11 15 16 12 8 4

## Algorithm

1. Read the matrix.
2. Traverse each column from left to right.
3. If the column index is even, print the column from top to bottom.
4. Otherwise, print the column from bottom to top.
5. Continue until all columns are processed.

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

    for(int j=0;j<m;j++)
    {
        if(j%2==0)
        {
            for(int i=0;i<n;i++)
                printf("%lld ",a[i][j]);
        }
        else
        {
            for(int i=n-1;i>=0;i--)
                printf("%lld ",a[i][j]);
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

    for(int j=0;j<m;j++)
    {
        if(j%2==0)
        {
            for(int i=0;i<n;i++)
                cout<<a[i][j]<<" ";
        }
        else
        {
            for(int i=n-1;i>=0;i--)
                cout<<a[i][j]<<" ";
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

        for(int j=0;j<m;j++)
        {
            if(j%2==0)
            {
                for(int i=0;i<n;i++)
                    System.out.print(a[i][j]+" ");
            }
            else
            {
                for(int i=n-1;i>=0;i--)
                    System.out.print(a[i][j]+" ");
            }
        }
    }
}
```
```Python
n,m=map(int,input().split())

a=[list(map(int,input().split())) for _ in range(n)]

for j in range(m):

    if j%2==0:
        for i in range(n):
            print(a[i][j],end=" ")
    else:
        for i in range(n-1,-1,-1):
            print(a[i][j],end=" ")
```
```C#
using System;

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

        for(int j=0;j<m;j++)
        {
            if(j%2==0)
            {
                for(int i=0;i<n;i++)
                    Console.Write(a[i][j]+" ");
            }
            else
            {
                for(int i=n-1;i>=0;i--)
                    Console.Write(a[i][j]+" ");
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

let ans=[];

for(let j=0;j<m;j++)
{
    if(j%2===0)
    {
        for(let i=0;i<n;i++)
            ans.push(a[i][j]);
    }
    else
    {
        for(let i=n-1;i>=0;i--)
            ans.push(a[i][j]);
    }
}

console.log(ans.join(" "));
```

### Output
Input

4 4

1 2 3 4

5 6 7 8

9 10 11 12

13 14 15 16

Output

1 5 9 13 14 10 6 2 3 7 11 15 16 12 8 4

# Time Complexity
O(N × M)

# Space Complexity
O(N × M)




