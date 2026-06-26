# Swap Diagonals - Solution

## Problem Statement

Given a square matrix of size `N × N`, swap its major diagonal with its minor diagonal.

The major diagonal contains the elements at positions `(i, i)`.

The minor diagonal contains the elements at positions `(i, N - 1 - i)`.

After swapping, print the modified matrix.

## Input Format

First line: Integer `N`.

Next `N` lines: `N` space-separated integers representing the matrix.

## Output Format

Print the matrix after swapping the major and minor diagonals.

Output exactly `N` lines, each containing `N` space-separated integers.

## Explanation

There is only one optimal approach to solve this problem.

For example,

Input

3

1 2 3

4 5 6

7 8 9

Output

3 2 1

4 5 6

9 8 7

## Algorithm

1. Read the matrix.
2. Traverse each row.
3. Swap the major diagonal element `matrix[i][i]` with the minor diagonal element `matrix[i][N-1-i]`.
4. Print the modified matrix.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long a[n][n];

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            scanf("%lld",&a[i][j]);

    for(int i=0;i<n;i++)
    {
        long long temp=a[i][i];
        a[i][i]=a[i][n-1-i];
        a[i][n-1-i]=temp;
    }

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
            printf("%lld ",a[i][j]);
        printf("\n");
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

    vector<vector<long long>> a(n,vector<long long>(n));

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            cin>>a[i][j];

    for(int i=0;i<n;i++)
        swap(a[i][i],a[i][n-1-i]);

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
            cout<<a[i][j]<<" ";
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

        long[][] a=new long[n][n];

        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                a[i][j]=sc.nextLong();

        for(int i=0;i<n;i++)
        {
            long temp=a[i][i];
            a[i][i]=a[i][n-1-i];
            a[i][n-1-i]=temp;
        }

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
                System.out.print(a[i][j]+" ");
            System.out.println();
        }
    }
}
```
```Python
n=int(input())

a=[list(map(int,input().split())) for _ in range(n)]

for i in range(n):
    a[i][i],a[i][n-1-i]=a[i][n-1-i],a[i][i]

for row in a:
    print(*row)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[][] a=new long[n][];

        for(int i=0;i<n;i++)
            a[i]=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        for(int i=0;i<n;i++)
        {
            long temp=a[i][i];
            a[i][i]=a[i][n-1-i];
            a[i][n-1-i]=temp;
        }

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
                Console.Write(a[i][j]+" ");
            Console.WriteLine();
        }
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const a=Array.from({length:n},()=>Array(n));

for(let i=0;i<n;i++)
    for(let j=0;j<n;j++)
        a[i][j]=input[idx++];

for(let i=0;i<n;i++)
    [a[i][i],a[i][n-1-i]]=[a[i][n-1-i],a[i][i]];

for(let i=0;i<n;i++)
    console.log(a[i].join(" "));
```

### Output
Input

3

1 2 3

4 5 6

7 8 9

Output

3 2 1

4 5 6

9 8 7

# Time Complexity
O(N²)

# Space Complexity
O(N²) (for storing the matrix)




