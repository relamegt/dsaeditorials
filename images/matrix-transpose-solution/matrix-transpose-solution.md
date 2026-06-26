# Matrix Transpose - Solution

## Problem Statement

Given a square matrix of size `N × N`, print its transpose.

The transpose of a matrix is obtained by converting rows into columns and columns into rows. In the transposed matrix, the value at position `(i, j)` becomes the value at position `(j, i)`.

## Input Format

First line: Integer `N` representing the size of the matrix.

Next `N` lines: `N` space-separated integers representing the matrix.

## Output Format

Print the transpose of the matrix.

Output exactly `N` lines, each containing `N` space-separated integers.

## Explanation

There are two approaches to solve this problem.

- **Approach 1:** Using an Extra Matrix
- **Approach 2:** In-place Transpose (Optimal)

For example,

Input

3

1 2 3

4 5 6

7 8 9

Output

1 4 7

2 5 8

3 6 9

<approaches>
## Approach 1: Using an Extra Matrix

### Algorithm

1. Read the matrix.
2. Create another matrix of the same size.
3. Traverse every element.
4. Store `transpose[j][i] = matrix[i][j]`.
5. Print the transpose matrix.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long a[n][n];
    long long t[n][n];

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            scanf("%lld",&a[i][j]);

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            t[j][i]=a[i][j];

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
            printf("%lld ",t[i][j]);
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

    vector<vector<long long>> a(n,vector<long long>(n));
    vector<vector<long long>> t(n,vector<long long>(n));

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            cin>>a[i][j];

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            t[j][i]=a[i][j];

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
            cout<<t[i][j]<<" ";
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

        long[][] a=new long[n][n];
        long[][] t=new long[n][n];

        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                a[i][j]=sc.nextLong();

        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                t[j][i]=a[i][j];

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
                System.out.print(t[i][j]+" ");
            System.out.println();
        }
    }
}
```
```Python
n=int(input())

a=[list(map(int,input().split())) for _ in range(n)]

t=[[0]*n for _ in range(n)]

for i in range(n):
    for j in range(n):
        t[j][i]=a[i][j]

for row in t:
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
        long[][] t=new long[n][];

        for(int i=0;i<n;i++)
            a[i]=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        for(int i=0;i<n;i++)
            t[i]=new long[n];

        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                t[j][i]=a[i][j];

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
                Console.Write(t[i][j]+" ");
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
const t=Array.from({length:n},()=>Array(n));

for(let i=0;i<n;i++)
    for(let j=0;j<n;j++)
        a[i][j]=input[idx++];

for(let i=0;i<n;i++)
    for(let j=0;j<n;j++)
        t[j][i]=a[i][j];

for(let i=0;i<n;i++)
    console.log(t[i].join(" "));
```

### Output
Input

3

1 2 3

4 5 6

7 8 9

Output

1 4 7

2 5 8

3 6 9

# Time Complexity
O(N²)

# Space Complexity
O(N²)

## Approach 2: In-place Transpose (Optimal)

### Algorithm

1. Read the matrix.
2. Traverse only the upper triangular part of the matrix.
3. For every pair `(i, j)` where `j > i`, swap `matrix[i][j]` with `matrix[j][i]`.
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
        for(int j=i+1;j<n;j++)
        {
            long long temp=a[i][j];
            a[i][j]=a[j][i];
            a[j][i]=temp;
        }
    }

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
            printf("%lld ",a[i][j]);
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

    vector<vector<long long>> a(n,vector<long long>(n));

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            cin>>a[i][j];

    for(int i=0;i<n;i++)
    {
        for(int j=i+1;j<n;j++)
            swap(a[i][j],a[j][i]);
    }

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
            cout<<a[i][j]<<" ";
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

        long[][] a=new long[n][n];

        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                a[i][j]=sc.nextLong();

        for(int i=0;i<n;i++)
        {
            for(int j=i+1;j<n;j++)
            {
                long temp=a[i][j];
                a[i][j]=a[j][i];
                a[j][i]=temp;
            }
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
n = int(input())

a = [list(map(int, input().split())) for _ in range(n)]

for i in range(n):

    for j in range(i + 1, n):
        a[i][j], a[j][i] = a[j][i], a[i][j]

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
            for(int j=i+1;j<n;j++)
            {
                long temp=a[i][j];
                a[i][j]=a[j][i];
                a[j][i]=temp;
            }
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
{
    for(let j=i+1;j<n;j++)
        [a[i][j],a[j][i]]=[a[j][i],a[i][j]];
}

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

1 4 7

2 5 8

3 6 9

# Time Complexity
O(N²)

# Space Complexity
O(1)

</approaches>




