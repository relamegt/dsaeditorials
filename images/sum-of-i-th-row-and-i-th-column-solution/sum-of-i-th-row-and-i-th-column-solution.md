# Sum of i-th Row and i-th column - Solution

## Problem Statement

Given a matrix `A` of dimensions `N × M`, determine whether the sum of the `i`-th row is equal to the sum of the `i`-th column for every valid index `i`.

Check only for valid indices `i` such that both the `i`-th row and the `i`-th column exist. In other words, check for `i` from `1` to `min(N, M)`.

## Input Format

First line: Two integers `N` and `M` representing the number of rows and columns.

Next `N` lines: `M` space-separated integers representing the matrix.

## Output Format

Print `1` if for every valid `i`, the sum of the `i`-th row is equal to the sum of the `i`-th column.

Otherwise, print `0`.

## Explanation

There is only one approach to solve this problem.

For example,

Input

3 3

1 2 3

2 1 3

3 3 0

Output

1

## Algorithm

1. Read the matrix.
2. Compute the sum of every row.
3. Compute the sum of every column.
4. Compare the `i`-th row sum and `i`-th column sum for every `i` from `0` to `min(N, M) - 1`.
5. If any pair differs, print `0`.
6. Otherwise, print `1`.

```C
#include <stdio.h>

int main()
{
    int n,m;
    scanf("%d%d",&n,&m);

    long long arr[n][m];

    for(int i=0;i<n;i++)
        for(int j=0;j<m;j++)
            scanf("%lld",&arr[i][j]);

    int limit=n<m?n:m;

    for(int i=0;i<limit;i++)
    {
        long long rowSum=0;
        long long colSum=0;

        for(int j=0;j<m;j++)
            rowSum+=arr[i][j];

        for(int j=0;j<n;j++)
            colSum+=arr[j][i];

        if(rowSum!=colSum)
        {
            printf("0");
            return 0;
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
    int n,m;
    cin>>n>>m;

    vector<vector<long long>> arr(n,vector<long long>(m));

    for(int i=0;i<n;i++)
        for(int j=0;j<m;j++)
            cin>>arr[i][j];

    int limit=min(n,m);

    for(int i=0;i<limit;i++)
    {
        long long rowSum=0;
        long long colSum=0;

        for(int j=0;j<m;j++)
            rowSum+=arr[i][j];

        for(int j=0;j<n;j++)
            colSum+=arr[j][i];

        if(rowSum!=colSum)
        {
            cout<<"0";
            return 0;
        }
    }

    cout<<"1";

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

        long[][] arr=new long[n][m];

        for(int i=0;i<n;i++)
            for(int j=0;j<m;j++)
                arr[i][j]=sc.nextLong();

        int limit=Math.min(n,m);

        for(int i=0;i<limit;i++)
        {
            long rowSum=0;
            long colSum=0;

            for(int j=0;j<m;j++)
                rowSum+=arr[i][j];

            for(int j=0;j<n;j++)
                colSum+=arr[j][i];

            if(rowSum!=colSum)
            {
                System.out.print(0);
                return;
            }
        }

        System.out.print(1);
    }
}
```
```Python
n,m=map(int,input().split())

arr=[list(map(int,input().split())) for _ in range(n)]

limit=min(n,m)

for i in range(limit):

    rowSum=sum(arr[i])
    colSum=0

    for j in range(n):
        colSum+=arr[j][i]

    if rowSum!=colSum:
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
        string[] first=Console.ReadLine().Split();

        int n=int.Parse(first[0]);
        int m=int.Parse(first[1]);

        long[][] arr=new long[n][];

        for(int i=0;i<n;i++)
            arr[i]=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        int limit=Math.Min(n,m);

        for(int i=0;i<limit;i++)
        {
            long rowSum=0;
            long colSum=0;

            for(int j=0;j<m;j++)
                rowSum+=arr[i][j];

            for(int j=0;j<n;j++)
                colSum+=arr[j][i];

            if(rowSum!=colSum)
            {
                Console.Write(0);
                return;
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
const m=input[idx++];

const arr=Array.from({length:n},()=>Array(m));

for(let i=0;i<n;i++)
    for(let j=0;j<m;j++)
        arr[i][j]=input[idx++];

const limit=Math.min(n,m);

for(let i=0;i<limit;i++)
{
    let rowSum=0;
    let colSum=0;

    for(let j=0;j<m;j++)
        rowSum+=arr[i][j];

    for(let j=0;j<n;j++)
        colSum+=arr[j][i];

    if(rowSum!==colSum)
    {
        console.log(0);
        return;
    }
}

console.log(1);
```

### Output
Input

3 3

1 2 3

2 1 3

3 3 0

Output

1

# Time Complexity
O(N × M)

# Space Complexity
O(N × M)




