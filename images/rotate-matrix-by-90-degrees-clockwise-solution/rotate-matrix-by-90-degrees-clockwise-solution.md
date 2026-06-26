# Rotate Matrix by 90 Degrees Clockwise - Solution

## Problem Statement

Given a square matrix of size `N × N` representing an image, rotate the image by 90 degrees clockwise.

The rotation must modify the matrix itself.

## Input Format

First line: Integer `N`.

Next `N` lines: `N` space-separated integers representing the matrix.

## Output Format

Print the rotated matrix.

Output exactly `N` lines, each containing `N` space-separated integers.

## Explanation

There are two approaches to solve this problem.

- Approach 1: Using Extra Matrix
- Approach 2: In-place Rotation (Optimal)

For example,

Input

3

1 2 3

4 5 6

7 8 9

Output

7 4 1

8 5 2

9 6 3

<approaches>
## Approach 1: Using Extra Matrix

### Algorithm

1. Read the matrix.
2. Create another matrix of the same size.
3. For every element `(i, j)`, place it at position `(j, N-1-i)` in the new matrix.
4. Print the new matrix.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long a[n][n],b[n][n];

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            scanf("%lld",&a[i][j]);

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            b[j][n-1-i]=a[i][j];

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
            printf("%lld ",b[i][j]);
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
    vector<vector<long long>> b(n,vector<long long>(n));

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            cin>>a[i][j];

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            b[j][n-1-i]=a[i][j];

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
            cout<<b[i][j]<<" ";
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
        long[][] b=new long[n][n];

        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                a[i][j]=sc.nextLong();

        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                b[j][n-1-i]=a[i][j];

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
                System.out.print(b[i][j]+" ");
            System.out.println();
        }
    }
}
```
```Python
n=int(input())

a=[list(map(int,input().split())) for _ in range(n)]

b=[[0]*n for _ in range(n)]

for i in range(n):
    for j in range(n):
        b[j][n-1-i]=a[i][j]

for row in b:
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
        long[][] b=new long[n][];

        for(int i=0;i<n;i++)
        {
            a[i]=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);
            b[i]=new long[n];
        }

        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                b[j][n-1-i]=a[i][j];

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
                Console.Write(b[i][j]+" ");
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
const b=Array.from({length:n},()=>Array(n));

for(let i=0;i<n;i++)
    for(let j=0;j<n;j++)
        a[i][j]=input[idx++];

for(let i=0;i<n;i++)
    for(let j=0;j<n;j++)
        b[j][n-1-i]=a[i][j];

for(let i=0;i<n;i++)
    console.log(b[i].join(" "));
```

### Output
Input

3

1 2 3

4 5 6

7 8 9

Output

7 4 1

8 5 2

9 6 3

# Time Complexity
O(N²)

# Space Complexity
O(N²)

## Approach 2: In-place Rotation (Optimal)

### Algorithm

1. Read the matrix.
2. Transpose the matrix by swapping `matrix[i][j]` with `matrix[j][i]` for all `j > i`.
3. Reverse every row of the transposed matrix.
4. Print the rotated matrix.

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
        int left=0,right=n-1;

        while(left<right)
        {
            long long temp=a[i][left];
            a[i][left]=a[i][right];
            a[i][right]=temp;
            left++;
            right--;
        }
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
        for(int j=i+1;j<n;j++)
            swap(a[i][j],a[j][i]);

    for(int i=0;i<n;i++)
    {
        int left=0,right=n-1;

        while(left<right)
        {
            swap(a[i][left],a[i][right]);
            left++;
            right--;
        }
    }

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
            for(int j=i+1;j<n;j++)
            {
                long temp=a[i][j];
                a[i][j]=a[j][i];
                a[j][i]=temp;
            }
        }

        for(int i=0;i<n;i++)
        {
            int left=0,right=n-1;

            while(left<right)
            {
                long temp=a[i][left];
                a[i][left]=a[i][right];
                a[i][right]=temp;
                left++;
                right--;
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
n=int(input())

a=[list(map(int,input().split())) for _ in range(n)]

for i in range(n):
    for j in range(i+1,n):
        a[i][j],a[j][i]=a[j][i],a[i][j]

for i in range(n):
    a[i].reverse()

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
            int left=0,right=n-1;

            while(left<right)
            {
                long temp=a[i][left];
                a[i][left]=a[i][right];
                a[i][right]=temp;
                left++;
                right--;
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
    a[i].reverse();

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

7 4 1

8 5 2

9 6 3

# Time Complexity
O(N²)

# Space Complexity
O(N²) (for storing the matrix, O(1) extra space)

</approaches>




