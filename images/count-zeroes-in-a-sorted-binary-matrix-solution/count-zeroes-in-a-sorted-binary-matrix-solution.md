# Count Zeroes in a Sorted Binary Matrix - Solution

## Problem Statement

Given a binary matrix of size `N × N` where each row and each column is sorted in non-decreasing order, count the total number of zeroes in the matrix.

Each matrix element is either `0` or `1`.

## Input Format

First line: Integer `N`.

Next `N` lines: `N` space-separated integers representing the matrix.

## Output Format

Print a single integer representing the number of zeroes in the matrix.

## Explanation

There are two approaches to solve this problem.

- Approach 1: Traverse Every Element
- Approach 2: Top-Right Traversal (Optimal)

For example,

Input

3

0 0 1

0 1 1

1 1 1

Output

3

<approaches>
## Approach 1: Traverse Every Element

### Algorithm

1. Read the matrix.
2. Initialize a counter to `0`.
3. Traverse every element of the matrix.
4. If the current element is `0`, increment the counter.
5. Print the final count.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int a[n][n];
    int count=0;

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            scanf("%d",&a[i][j]);

            if(a[i][j]==0)
                count++;
        }
    }

    printf("%d",count);

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

    vector<vector<int>> a(n,vector<int>(n));
    int count=0;

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            cin>>a[i][j];

            if(a[i][j]==0)
                count++;
        }
    }

    cout<<count;

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

        int[][] a=new int[n][n];
        int count=0;

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
            {
                a[i][j]=sc.nextInt();

                if(a[i][j]==0)
                    count++;
            }
        }

        System.out.print(count);
    }
}
```
```Python
n=int(input())

count=0

for _ in range(n):
    row=list(map(int,input().split()))

    for x in row:
        if x==0:
            count+=1

print(count)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        int count=0;

        for(int i=0;i<n;i++)
        {
            int[] row=Array.ConvertAll(Console.ReadLine().Split(),int.Parse);

            foreach(int x in row)
            {
                if(x==0)
                    count++;
            }
        }

        Console.Write(count);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

let count=0;

for(let i=0;i<n;i++)
{
    for(let j=0;j<n;j++)
    {
        if(input[idx++]===0)
            count++;
    }
}

console.log(count);
```

## Approach 2: Top-Right Traversal (Optimal)

### Algorithm

1. Read the matrix.
2. Start from the top-right corner of the matrix.
3. If the current element is `0`, then all elements to its left in that row are also `0`. Add `column + 1` to the answer and move to the next row.
4. Otherwise, move one column to the left.
5. Continue until all rows or columns are processed.
6. Print the total count of zeroes.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int a[n][n];

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            scanf("%d",&a[i][j]);

    int row=0,col=n-1;
    long long count=0;

    while(row<n && col>=0)
    {
        if(a[row][col]==0)
        {
            count+=col+1;
            row++;
        }
        else
            col--;
    }

    printf("%lld",count);

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

    vector<vector<int>> a(n,vector<int>(n));

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            cin>>a[i][j];

    int row=0,col=n-1;
    long long count=0;

    while(row<n && col>=0)
    {
        if(a[row][col]==0)
        {
            count+=col+1;
            row++;
        }
        else
            col--;
    }

    cout<<count;

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

        int[][] a=new int[n][n];

        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                a[i][j]=sc.nextInt();

        int row=0,col=n-1;
        long count=0;

        while(row<n && col>=0)
        {
            if(a[row][col]==0)
            {
                count+=col+1;
                row++;
            }
            else
                col--;
        }

        System.out.print(count);
    }
}
```
```Python
n=int(input())

a=[list(map(int,input().split())) for _ in range(n)]

row=0
col=n-1
count=0

while row<n and col>=0:

    if a[row][col]==0:
        count+=col+1
        row+=1
    else:
        col-=1

print(count)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        int[][] a=new int[n][];

        for(int i=0;i<n;i++)
            a[i]=Array.ConvertAll(Console.ReadLine().Split(),int.Parse);

        int row=0,col=n-1;
        long count=0;

        while(row<n && col>=0)
        {
            if(a[row][col]==0)
            {
                count+=col+1;
                row++;
            }
            else
                col--;
        }

        Console.Write(count);
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

let row=0,col=n-1;
let count=0;

while(row<n && col>=0)
{
    if(a[row][col]===0)
    {
        count+=col+1;
        row++;
    }
    else
        col--;
}

console.log(count);
```

</approaches>




