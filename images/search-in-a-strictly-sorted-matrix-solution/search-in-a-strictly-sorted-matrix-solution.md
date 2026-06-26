# Search in a Strictly Sorted Matrix - Solution

## Problem Statement

Given a strictly sorted matrix `mat` of size `N × M` and an integer `X`, determine whether `X` is present in the matrix.

A matrix is strictly sorted if:

- Each row is sorted in strictly increasing order.
- The first element of every row is greater than the last element of the previous row.

## Input Format

First line: Two integers `N` and `M`.

Next `N` lines: `M` space-separated integers representing the matrix.

Last line: Integer `X`.

## Output Format

Print `1` if `X` is present in the matrix.

Otherwise, print `0`.

## Explanation

There are two approaches to solve this problem.

- Approach 1: Linear Search
- Approach 2: Binary Search (Optimal)

For example,

Input

3 4

1 3 5 7

10 11 16 20

23 30 34 60

3

Output

1

<approaches>
## Approach 1: Linear Search

### Algorithm

1. Read the matrix and the target value `X`.
2. Traverse every element of the matrix.
3. If any element equals `X`, print `1`.
4. If the traversal completes without finding `X`, print `0`.

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

    long long x;
    scanf("%lld",&x);

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
        {
            if(a[i][j]==x)
            {
                printf("1");
                return 0;
            }
        }
    }

    printf("0");

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

    long long x;
    cin>>x;

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
        {
            if(a[i][j]==x)
            {
                cout<<1;
                return 0;
            }
        }
    }

    cout<<0;

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

        long x=sc.nextLong();

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(a[i][j]==x)
                {
                    System.out.print(1);
                    return;
                }
            }
        }

        System.out.print(0);
    }
}
```
```Python
n,m=map(int,input().split())

a=[list(map(int,input().split())) for _ in range(n)]

x=int(input())

for i in range(n):
    for j in range(m):
        if a[i][j]==x:
            print(1)
            exit()

print(0)
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

        long x=long.Parse(Console.ReadLine());

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(a[i][j]==x)
                {
                    Console.Write(1);
                    return;
                }
            }
        }

        Console.Write(0);
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

const x=input[idx++];

for(let i=0;i<n;i++)
{
    for(let j=0;j<m;j++)
    {
        if(a[i][j]===x)
        {
            console.log(1);
            return;
        }
    }
}

console.log(0);
```

### Output
Input

3 4

1 3 5 7

10 11 16 20

23 30 34 60

3

Output

1

# Time Complexity
O(N × M)

# Space Complexity
O(N × M)

## Approach 2: Binary Search (Optimal)

### Algorithm

1. Read the matrix and the target value `X`.
2. Treat the matrix as a sorted 1D array of size `N × M`.
3. Apply binary search on the range `0` to `N × M - 1`.
4. Convert the middle index into matrix coordinates:

- `row = mid / M`
- `col = mid % M`

1. If the element equals `X`, print `1`.
2. Otherwise, continue binary search on the appropriate half.
3. If `X` is not found, print `0`.

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

    long long x;
    scanf("%lld",&x);

    int low=0,high=n*m-1;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        int row=mid/m;
        int col=mid%m;

        if(a[row][col]==x)
        {
            printf("1");
            return 0;
        }
        else if(a[row][col]<x)
            low=mid+1;
        else
            high=mid-1;
    }

    printf("0");

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

    long long x;
    cin>>x;

    int low=0,high=n*m-1;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        int row=mid/m;
        int col=mid%m;

        if(a[row][col]==x)
        {
            cout<<1;
            return 0;
        }
        else if(a[row][col]<x)
            low=mid+1;
        else
            high=mid-1;
    }

    cout<<0;

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

        long x=sc.nextLong();

        int low=0,high=n*m-1;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            int row=mid/m;
            int col=mid%m;

            if(a[row][col]==x)
            {
                System.out.print(1);
                return;
            }
            else if(a[row][col]<x)
                low=mid+1;
            else
                high=mid-1;
        }

        System.out.print(0);
    }
}
```
```Python
n,m=map(int,input().split())

a=[list(map(int,input().split())) for _ in range(n)]

x=int(input())

low,high=0,n*m-1

while low<=high:

    mid=(low+high)//2

    row=mid//m
    col=mid%m

    if a[row][col]==x:
        print(1)
        exit()
    elif a[row][col]<x:
        low=mid+1
    else:
        high=mid-1

print(0)
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

        long x=long.Parse(Console.ReadLine());

        int low=0,high=n*m-1;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            int row=mid/m;
            int col=mid%m;

            if(a[row][col]==x)
            {
                Console.Write(1);
                return;
            }
            else if(a[row][col]<x)
                low=mid+1;
            else
                high=mid-1;
        }

        Console.Write(0);
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

const x=input[idx++];

let low=0,high=n*m-1;

while(low<=high)
{
    const mid=Math.floor((low+high)/2);

    const row=Math.floor(mid/m);
    const col=mid%m;

    if(a[row][col]===x)
    {
        console.log(1);
        return;
    }
    else if(a[row][col]<x)
        low=mid+1;
    else
        high=mid-1;
}

console.log(0);
```

### Output
Input

3 4

1 3 5 7

10 11 16 20

23 30 34 60

3

Output

1

# Time Complexity
O(log(N × M))

# Space Complexity
O(N × M) (for storing the matrix)

</approaches>




