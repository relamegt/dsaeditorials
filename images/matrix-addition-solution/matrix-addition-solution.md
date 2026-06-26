# Matrix Addition - Solution

## Problem Statement

Given two square matrices `A` and `B` of size `N × N`, compute their sum.

The resulting matrix `C` is defined as:

`C[i][j] = A[i][j] + B[i][j]`

## Input Format

First line: Integer `N`

Next `N` lines: `N` space-separated integers representing matrix `A`

Next `N` lines: `N` space-separated integers representing matrix `B`

## Output Format

Print the resulting matrix.

Output exactly `N` lines, each containing `N` space-separated integers.

## Explanation

There is only one approach to solve this problem.

For example,

Input

2

1 2

3 4

5 6

7 8

Output

6 8

10 12

## Algorithm

1. Read the size `N`.
2. Read matrix `A`.
3. Read matrix `B`.
4. Traverse every cell `(i, j)`.
5. Compute `A[i][j] + B[i][j]`.
6. Print the resulting matrix.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long A[n][n];
    long long B[n][n];

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            scanf("%lld",&A[i][j]);

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            scanf("%lld",&B[i][j]);

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
            printf("%lld ",A[i][j]+B[i][j]);

        printf(" ");
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
    int n;
    cin>>n;

    vector<vector<long long>> A(n,vector<long long>(n));
    vector<vector<long long>> B(n,vector<long long>(n));

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            cin>>A[i][j];

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            cin>>B[i][j];

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
            cout<<A[i][j]+B[i][j]<<" ";

        cout<<" ";
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

        long[][] A=new long[n][n];
        long[][] B=new long[n][n];

        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                A[i][j]=sc.nextLong();

        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                B[i][j]=sc.nextLong();

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
                System.out.print((A[i][j]+B[i][j])+" ");

            System.out.println();
        }
    }
}
```
```Python
n = int(input())

A = [list(map(int, input().split())) for _ in range(n)]
B = [list(map(int, input().split())) for _ in range(n)]

for i in range(n):

    for j in range(n):
        print(A[i][j] + B[i][j], end=" ")

    print()
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[][] A=new long[n][];
        long[][] B=new long[n][];

        for(int i=0;i<n;i++)
            A[i]=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        for(int i=0;i<n;i++)
            B[i]=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
                Console.Write((A[i][j]+B[i][j])+" ");

            Console.WriteLine();
        }
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const A=Array.from({length:n},()=>Array(n));
const B=Array.from({length:n},()=>Array(n));

for(let i=0;i<n;i++)
    for(let j=0;j<n;j++)
        A[i][j]=input[idx++];

for(let i=0;i<n;i++)
    for(let j=0;j<n;j++)
        B[i][j]=input[idx++];

for(let i=0;i<n;i++)
{
    let row=[];

    for(let j=0;j<n;j++)
        row.push(A[i][j]+B[i][j]);

    console.log(row.join(" "));
}
```

### Output
Input

2

1 2

3 4

5 6

7 8

Output

6 8

10 12

# Time Complexity
O(N²)

# Space Complexity
O(N²)




