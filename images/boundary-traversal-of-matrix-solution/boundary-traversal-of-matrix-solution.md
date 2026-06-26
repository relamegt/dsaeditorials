# Boundary Traversal of Matrix - Solution

## Problem Statement

Given a matrix of size `N × M`, print all boundary elements of the matrix in clockwise order starting from the top-left element.

The boundary consists of:

- The top row
- The rightmost column
- The bottom row in reverse order
- The leftmost column in reverse order

Each boundary element must be printed exactly once.

## Input Format

First line: Two integers `N` and `M`.

Next `N` lines: `M` space-separated integers representing the matrix.

## Output Format

Print the boundary elements in clockwise order as space-separated integers.

## Explanation

There is one optimal approach to solve this problem.

For example,

Input

3 3

1 2 3

4 5 6

7 8 9

Output

1 2 3 6 9 8 7 4

## Algorithm

1. Read the matrix.
2. Print the first row.
3. Print the last column excluding the first row.
4. If there is more than one row, print the last row in reverse order excluding the last column.
5. If there is more than one column, print the first column in reverse order excluding the first and last rows.
6. Every boundary element is printed exactly once.

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
        printf("%lld ",a[0][j]);

    for(int i=1;i<n;i++)
        printf("%lld ",a[i][m-1]);

    if(n>1)
    {
        for(int j=m-2;j>=0;j--)
            printf("%lld ",a[n-1][j]);
    }

    if(m>1)
    {
        for(int i=n-2;i>=1;i--)
            printf("%lld ",a[i][0]);
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
        cout<<a[0][j]<<" ";

    for(int i=1;i<n;i++)
        cout<<a[i][m-1]<<" ";

    if(n>1)
    {
        for(int j=m-2;j>=0;j--)
            cout<<a[n-1][j]<<" ";
    }

    if(m>1)
    {
        for(int i=n-2;i>=1;i--)
            cout<<a[i][0]<<" ";
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
            System.out.print(a[0][j]+" ");

        for(int i=1;i<n;i++)
            System.out.print(a[i][m-1]+" ");

        if(n>1)
        {
            for(int j=m-2;j>=0;j--)
                System.out.print(a[n-1][j]+" ");
        }

        if(m>1)
        {
            for(int i=n-2;i>=1;i--)
                System.out.print(a[i][0]+" ");
        }
    }
}
```
```Python
n,m=map(int,input().split())

a=[list(map(int,input().split())) for _ in range(n)]

for j in range(m):
    print(a[0][j],end=" ")

for i in range(1,n):
    print(a[i][m-1],end=" ")

if n>1:
    for j in range(m-2,-1,-1):
        print(a[n-1][j],end=" ")

if m>1:
    for i in range(n-2,0,-1):
        print(a[i][0],end=" ")
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
            Console.Write(a[0][j]+" ");

        for(int i=1;i<n;i++)
            Console.Write(a[i][m-1]+" ");

        if(n>1)
        {
            for(int j=m-2;j>=0;j--)
                Console.Write(a[n-1][j]+" ");
        }

        if(m>1)
        {
            for(int i=n-2;i>=1;i--)
                Console.Write(a[i][0]+" ");
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
    ans.push(a[0][j]);

for(let i=1;i<n;i++)
    ans.push(a[i][m-1]);

if(n>1)
{
    for(let j=m-2;j>=0;j--)
        ans.push(a[n-1][j]);
}

if(m>1)
{
    for(let i=n-2;i>=1;i--)
        ans.push(a[i][0]);
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

1 2 3 6 9 8 7 4

# Time Complexity
O(N × M)

# Space Complexity
O(N × M) for the input matrix (O(1) extra space, excluding the matrix itself).




