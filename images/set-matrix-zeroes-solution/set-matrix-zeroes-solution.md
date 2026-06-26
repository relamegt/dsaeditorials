# Set Matrix Zeroes - Solution

## Problem Statement

Given a matrix of size `N × M`, if an element is `0`, set its entire row and column to `0`.

The modification must be reflected in the final matrix after considering all zero positions from the original matrix.

## Input Format

First line: Two integers `N` and `M`.

Next `N` lines: `M` space-separated integers representing the matrix.

## Output Format

Print the modified matrix.

Output exactly `N` lines, each containing `M` space-separated integers.

## Explanation

There are two approaches to solve this problem.

- Approach 1: Using Extra Arrays
- Approach 2: Constant Space (Optimal)

For example,

Input

3 3

1 1 1

1 0 1

1 1 1

Output

1 0 1

0 0 0

1 0 1

<approaches>
## Approach 1: Using Extra Arrays

### Algorithm

1. Read the matrix.
2. Create two arrays to mark rows and columns containing a zero.
3. Traverse the matrix and mark the corresponding row and column whenever a zero is found.
4. Traverse the matrix again.
5. If a row or column is marked, set that cell to `0`.
6. Print the modified matrix.

```C
#include <stdio.h>

int main()
{
    int n,m;
    scanf("%d%d",&n,&m);

    long long a[n][m];
    int row[n],col[m];

    for(int i=0;i<n;i++)
        row[i]=0;

    for(int j=0;j<m;j++)
        col[j]=0;

    for(int i=0;i<n;i++)
        for(int j=0;j<m;j++)
            scanf("%lld",&a[i][j]);

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
        {
            if(a[i][j]==0)
            {
                row[i]=1;
                col[j]=1;
            }
        }
    }

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
        {
            if(row[i]||col[j])
                a[i][j]=0;
        }
    }

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
            printf("%lld ",a[i][j]);
        printf("
");
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
    vector<int> row(n,0),col(m,0);

    for(int i=0;i<n;i++)
        for(int j=0;j<m;j++)
            cin>>a[i][j];

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
        {
            if(a[i][j]==0)
            {
                row[i]=1;
                col[j]=1;
            }
        }
    }

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
        {
            if(row[i]||col[j])
                a[i][j]=0;
        }
    }

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
            cout<<a[i][j]<<" ";
        cout<<"
";
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
        boolean[] row=new boolean[n];
        boolean[] col=new boolean[m];

        for(int i=0;i<n;i++)
            for(int j=0;j<m;j++)
                a[i][j]=sc.nextLong();

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(a[i][j]==0)
                {
                    row[i]=true;
                    col[j]=true;
                }
            }
        }

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(row[i]||col[j])
                    a[i][j]=0;
            }
        }

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
                System.out.print(a[i][j]+" ");
            System.out.println();
        }
    }
}
```
```Python
n,m=map(int,input().split())

a=[list(map(int,input().split())) for _ in range(n)]

row=[False]*n
col=[False]*m

for i in range(n):
    for j in range(m):
        if a[i][j]==0:
            row[i]=True
            col[j]=True

for i in range(n):
    for j in range(m):
        if row[i] or col[j]:
            a[i][j]=0

for r in a:
    print(*r)
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
        bool[] row=new bool[n];
        bool[] col=new bool[m];

        for(int i=0;i<n;i++)
            a[i]=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(a[i][j]==0)
                {
                    row[i]=true;
                    col[j]=true;
                }
            }
        }

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(row[i]||col[j])
                    a[i][j]=0;
            }
        }

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
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
const m=input[idx++];

const a=Array.from({length:n},()=>Array(m));

const row=new Array(n).fill(false);
const col=new Array(m).fill(false);

for(let i=0;i<n;i++)
    for(let j=0;j<m;j++)
        a[i][j]=input[idx++];

for(let i=0;i<n;i++)
{
    for(let j=0;j<m;j++)
    {
        if(a[i][j]===0)
        {
            row[i]=true;
            col[j]=true;
        }
    }
}

for(let i=0;i<n;i++)
{
    for(let j=0;j<m;j++)
    {
        if(row[i]||col[j])
            a[i][j]=0;
    }
}

for(let i=0;i<n;i++)
    console.log(a[i].join(" "));
```

### Output
Input

3 3

1 1 1

1 0 1

1 1 1

Output

1 0 1

0 0 0

1 0 1

# Time Complexity
O(N × M)

# Space Complexity
O(N + M)

## Approach 2: Constant Space (Optimal)

### Algorithm

1. Read the matrix.
2. Check whether the first row or first column originally contains any zero.
3. Use the first row and first column as markers.
4. For every zero found (excluding the first row and first column), mark its row and column by setting the corresponding first row and first column cells to zero.
5. Traverse the remaining matrix and set elements to zero based on the markers.
6. Finally, update the first row and first column if they originally contained a zero.
7. Print the modified matrix.

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

    int firstRow=0,firstCol=0;

    for(int j=0;j<m;j++)
        if(a[0][j]==0)
            firstRow=1;

    for(int i=0;i<n;i++)
        if(a[i][0]==0)
            firstCol=1;

    for(int i=1;i<n;i++)
    {
        for(int j=1;j<m;j++)
        {
            if(a[i][j]==0)
            {
                a[i][0]=0;
                a[0][j]=0;
            }
        }
    }

    for(int i=1;i<n;i++)
    {
        for(int j=1;j<m;j++)
        {
            if(a[i][0]==0||a[0][j]==0)
                a[i][j]=0;
        }
    }

    if(firstRow)
    {
        for(int j=0;j<m;j++)
            a[0][j]=0;
    }

    if(firstCol)
    {
        for(int i=0;i<n;i++)
            a[i][0]=0;
    }

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
            printf("%lld ",a[i][j]);
        printf("
");
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

    bool firstRow=false,firstCol=false;

    for(int j=0;j<m;j++)
        if(a[0][j]==0)
            firstRow=true;

    for(int i=0;i<n;i++)
        if(a[i][0]==0)
            firstCol=true;

    for(int i=1;i<n;i++)
    {
        for(int j=1;j<m;j++)
        {
            if(a[i][j]==0)
            {
                a[i][0]=0;
                a[0][j]=0;
            }
        }
    }

    for(int i=1;i<n;i++)
    {
        for(int j=1;j<m;j++)
        {
            if(a[i][0]==0||a[0][j]==0)
                a[i][j]=0;
        }
    }

    if(firstRow)
        for(int j=0;j<m;j++)
            a[0][j]=0;

    if(firstCol)
        for(int i=0;i<n;i++)
            a[i][0]=0;

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
            cout<<a[i][j]<<" ";
        cout<<"
";
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

        boolean firstRow=false,firstCol=false;

        for(int j=0;j<m;j++)
            if(a[0][j]==0)
                firstRow=true;

        for(int i=0;i<n;i++)
            if(a[i][0]==0)
                firstCol=true;

        for(int i=1;i<n;i++)
        {
            for(int j=1;j<m;j++)
            {
                if(a[i][j]==0)
                {
                    a[i][0]=0;
                    a[0][j]=0;
                }
            }
        }

        for(int i=1;i<n;i++)
        {
            for(int j=1;j<m;j++)
            {
                if(a[i][0]==0||a[0][j]==0)
                    a[i][j]=0;
            }
        }

        if(firstRow)
            for(int j=0;j<m;j++)
                a[0][j]=0;

        if(firstCol)
            for(int i=0;i<n;i++)
                a[i][0]=0;

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
                System.out.print(a[i][j]+" ");
            System.out.println();
        }
    }
}
```
```Python
n,m=map(int,input().split())

a=[list(map(int,input().split())) for _ in range(n)]

firstRow=any(a[0][j]==0 for j in range(m))
firstCol=any(a[i][0]==0 for i in range(n))

for i in range(1,n):
    for j in range(1,m):
        if a[i][j]==0:
            a[i][0]=0
            a[0][j]=0

for i in range(1,n):
    for j in range(1,m):
        if a[i][0]==0 or a[0][j]==0:
            a[i][j]=0

if firstRow:
    for j in range(m):
        a[0][j]=0

if firstCol:
    for i in range(n):
        a[i][0]=0

for row in a:
    print(*row)
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

        bool firstRow=false,firstCol=false;

        for(int j=0;j<m;j++)
            if(a[0][j]==0)
                firstRow=true;

        for(int i=0;i<n;i++)
            if(a[i][0]==0)
                firstCol=true;

        for(int i=1;i<n;i++)
        {
            for(int j=1;j<m;j++)
            {
                if(a[i][j]==0)
                {
                    a[i][0]=0;
                    a[0][j]=0;
                }
            }
        }

        for(int i=1;i<n;i++)
        {
            for(int j=1;j<m;j++)
            {
                if(a[i][0]==0||a[0][j]==0)
                    a[i][j]=0;
            }
        }

        if(firstRow)
            for(int j=0;j<m;j++)
                a[0][j]=0;

        if(firstCol)
            for(int i=0;i<n;i++)
                a[i][0]=0;

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
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
const m=input[idx++];

const a=Array.from({length:n},()=>Array(m));

for(let i=0;i<n;i++)
    for(let j=0;j<m;j++)
        a[i][j]=input[idx++];

let firstRow=false,firstCol=false;

for(let j=0;j<m;j++)
    if(a[0][j]===0)
        firstRow=true;

for(let i=0;i<n;i++)
    if(a[i][0]===0)
        firstCol=true;

for(let i=1;i<n;i++)
{
    for(let j=1;j<m;j++)
    {
        if(a[i][j]===0)
        {
            a[i][0]=0;
            a[0][j]=0;
        }
    }
}

for(let i=1;i<n;i++)
{
    for(let j=1;j<m;j++)
    {
        if(a[i][0]===0||a[0][j]===0)
            a[i][j]=0;
    }
}

if(firstRow)
    for(let j=0;j<m;j++)
        a[0][j]=0;

if(firstCol)
    for(let i=0;i<n;i++)
        a[i][0]=0;

for(let i=0;i<n;i++)
    console.log(a[i].join(" "));
```

### Output
Input

3 3

1 1 1

1 0 1

1 1 1

Output

1 0 1

0 0 0

1 0 1

# Time Complexity
O(N × M)

# Space Complexity
O(N × M) (for storing the matrix, O(1) extra space)

</approaches>




