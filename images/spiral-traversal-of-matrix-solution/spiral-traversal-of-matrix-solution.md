# Spiral Traversal of Matrix - Solution

## Problem Statement

Given a matrix of size `N × M`, print all its elements in spiral order.

Spiral order starts at the top-left corner, moves left to right across the top row, then top to bottom along the right column, then right to left across the bottom row, then bottom to top along the left column, and continues inward until all elements are printed.

## Input Format

First line: Two integers `N` and `M`.

Next `N` lines: `M` space-separated integers representing the matrix.

## Output Format

Print all matrix elements in spiral order as space-separated integers.

## Explanation

There is only one optimal approach to solve this problem.

For example,

Input

3 3

1 2 3

4 5 6

7 8 9

Output

1 2 3 6 9 8 7 4 5

## Algorithm

1. Initialize four boundaries: `top`, `bottom`, `left`, and `right`.
2. Traverse the top row from left to right and increment `top`.
3. Traverse the right column from top to bottom and decrement `right`.
4. If rows remain, traverse the bottom row from right to left and decrement `bottom`.
5. If columns remain, traverse the left column from bottom to top and increment `left`.
6. Repeat until all elements are printed.

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

    int top=0,bottom=n-1,left=0,right=m-1;

    while(top<=bottom && left<=right)
    {
        for(int j=left;j<=right;j++)
            printf("%lld ",a[top][j]);
        top++;

        for(int i=top;i<=bottom;i++)
            printf("%lld ",a[i][right]);
        right--;

        if(top<=bottom)
        {
            for(int j=right;j>=left;j--)
                printf("%lld ",a[bottom][j]);
            bottom--;
        }

        if(left<=right)
        {
            for(int i=bottom;i>=top;i--)
                printf("%lld ",a[i][left]);
            left++;
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

    int top=0,bottom=n-1,left=0,right=m-1;

    while(top<=bottom && left<=right)
    {
        for(int j=left;j<=right;j++)
            cout<<a[top][j]<<" ";
        top++;

        for(int i=top;i<=bottom;i++)
            cout<<a[i][right]<<" ";
        right--;

        if(top<=bottom)
        {
            for(int j=right;j>=left;j--)
                cout<<a[bottom][j]<<" ";
            bottom--;
        }

        if(left<=right)
        {
            for(int i=bottom;i>=top;i--)
                cout<<a[i][left]<<" ";
            left++;
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

        int top=0,bottom=n-1,left=0,right=m-1;

        while(top<=bottom && left<=right)
        {
            for(int j=left;j<=right;j++)
                System.out.print(a[top][j]+" ");
            top++;

            for(int i=top;i<=bottom;i++)
                System.out.print(a[i][right]+" ");
            right--;

            if(top<=bottom)
            {
                for(int j=right;j>=left;j--)
                    System.out.print(a[bottom][j]+" ");
                bottom--;
            }

            if(left<=right)
            {
                for(int i=bottom;i>=top;i--)
                    System.out.print(a[i][left]+" ");
                left++;
            }
        }
    }
}
```
```Python
n,m=map(int,input().split())

a=[list(map(int,input().split())) for _ in range(n)]

top,bottom,left,right=0,n-1,0,m-1

while top<=bottom and left<=right:

    for j in range(left,right+1):
        print(a[top][j],end=" ")
    top+=1

    for i in range(top,bottom+1):
        print(a[i][right],end=" ")
    right-=1

    if top<=bottom:
        for j in range(right,left-1,-1):
            print(a[bottom][j],end=" ")
        bottom-=1

    if left<=right:
        for i in range(bottom,top-1,-1):
            print(a[i][left],end=" ")
        left+=1
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

        int top=0,bottom=n-1,left=0,right=m-1;

        while(top<=bottom && left<=right)
        {
            for(int j=left;j<=right;j++)
                Console.Write(a[top][j]+" ");
            top++;

            for(int i=top;i<=bottom;i++)
                Console.Write(a[i][right]+" ");
            right--;

            if(top<=bottom)
            {
                for(int j=right;j>=left;j--)
                    Console.Write(a[bottom][j]+" ");
                bottom--;
            }

            if(left<=right)
            {
                for(int i=bottom;i>=top;i--)
                    Console.Write(a[i][left]+" ");
                left++;
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

let top=0,bottom=n-1,left=0,right=m-1;

const ans=[];

while(top<=bottom && left<=right)
{
    for(let j=left;j<=right;j++)
        ans.push(a[top][j]);
    top++;

    for(let i=top;i<=bottom;i++)
        ans.push(a[i][right]);
    right--;

    if(top<=bottom)
    {
        for(let j=right;j>=left;j--)
            ans.push(a[bottom][j]);
        bottom--;
    }

    if(left<=right)
    {
        for(let i=bottom;i>=top;i--)
            ans.push(a[i][left]);
        left++;
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

1 2 3 6 9 8 7 4 5

# Time Complexity
O(N × M)

# Space Complexity
O(N × M) (for storing the matrix)




