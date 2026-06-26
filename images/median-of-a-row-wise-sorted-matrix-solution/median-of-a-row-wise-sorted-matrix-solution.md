# Median of a Row-wise Sorted Matrix - Solution

## Problem Statement

Given a row-wise sorted matrix of size `R × C`, find the median of all elements in the matrix.

The matrix is guaranteed to contain an odd number of elements, so the median is the middle element in the sorted order of all matrix values.

## Input Format

First line: Two integers `R` and `C`.

Next `R` lines: `C` space-separated integers representing the matrix.

## Output Format

Print a single integer representing the median of the matrix.

## Explanation

There are two approaches to solve this problem.

- Approach 1: Flatten and Sort
- Approach 2: Binary Search on Answer (Optimal)

For example,

Input

3 3

1 3 5

2 6 9

3 6 9

Output

5

<approaches>
## Approach 1: Flatten and Sort

### Algorithm

1. Read the matrix.
2. Store all matrix elements in a one-dimensional array.
3. Sort the array.
4. Print the middle element.

```C
#include <stdio.h>
#include <stdlib.h>

int cmp(const void *a,const void *b)
{
    long long x=*(long long*)a;
    long long y=*(long long*)b;

    if(x<y) return -1;
    if(x>y) return 1;
    return 0;
}

int main()
{
    int r,c;
    scanf("%d%d",&r,&c);

    long long arr[r*c];

    for(int i=0;i<r*c;i++)
        scanf("%lld",&arr[i]);

    qsort(arr,r*c,sizeof(long long),cmp);

    printf("%lld",arr[(r*c)/2]);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    int r,c;
    cin>>r>>c;

    vector<long long> arr(r*c);

    for(int i=0;i<r*c;i++)
        cin>>arr[i];

    sort(arr.begin(),arr.end());

    cout<<arr[(r*c)/2];

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

        int r=sc.nextInt();
        int c=sc.nextInt();

        long[] arr=new long[r*c];

        for(int i=0;i<r*c;i++)
            arr[i]=sc.nextLong();

        Arrays.sort(arr);

        System.out.print(arr[(r*c)/2]);
    }
}
```
```Python
r,c=map(int,input().split())

arr=[]

for _ in range(r):
    arr.extend(map(int,input().split()))

arr.sort()

print(arr[(r*c)//2])
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] first=Console.ReadLine().Split();

        int r=int.Parse(first[0]);
        int c=int.Parse(first[1]);

        long[] arr=new long[r*c];

        int idx=0;

        for(int i=0;i<r;i++)
        {
            long[] row=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

            foreach(long x in row)
                arr[idx++]=x;
        }

        Array.Sort(arr);

        Console.Write(arr[(r*c)/2]);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const r=input[idx++];
const c=input[idx++];

const arr=[];

for(let i=0;i<r*c;i++)
    arr.push(input[idx++]);

arr.sort((a,b)=>a-b);

console.log(arr[Math.floor((r*c)/2)]);
```

### Output
Input

3 3

1 3 5

2 6 9

3 6 9

Output

5

# Time Complexity
O((R × C) log(R × C))

# Space Complexity
O(R × C)

## Approach 2: Binary Search on Answer (Optimal)

### Algorithm

1. Read the matrix.
2. Find the minimum element (first element of each row) and the maximum element (last element of each row).
3. Let the required position be `(R × C) / 2 + 1`.
4. Perform binary search on the value range.
5. For every middle value, count how many elements are less than or equal to it by performing binary search in each row.
6. If the count is smaller than the required position, search in the higher half.
7. Otherwise, search in the lower half.
8. Print the final value.

```C
#include <stdio.h>

int upperBound(long long row[],int n,long long x)
{
    int low=0,high=n;

    while(low<high)
    {
        int mid=low+(high-low)/2;

        if(row[mid]<=x)
            low=mid+1;
        else
            high=mid;
    }

    return low;
}

int main()
{
    int r,c;
    scanf("%d%d",&r,&c);

    long long a[r][c];

    for(int i=0;i<r;i++)
        for(int j=0;j<c;j++)
            scanf("%lld",&a[i][j]);

    long long low=a[0][0],high=a[0][c-1];

    for(int i=1;i<r;i++)
    {
        if(a[i][0]<low)
            low=a[i][0];

        if(a[i][c-1]>high)
            high=a[i][c-1];
    }

    int need=(r*c)/2+1;

    while(low<high)
    {
        long long mid=low+(high-low)/2;
        int count=0;

        for(int i=0;i<r;i++)
            count+=upperBound(a[i],c,mid);

        if(count<need)
            low=mid+1;
        else
            high=mid;
    }

    printf("%lld",low);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int upperBound(vector<long long> &row,long long x)
{
    int low=0,high=row.size();

    while(low<high)
    {
        int mid=low+(high-low)/2;

        if(row[mid]<=x)
            low=mid+1;
        else
            high=mid;
    }

    return low;
}

int main()
{
    int r,c;
    cin>>r>>c;

    vector<vector<long long>> a(r,vector<long long>(c));

    for(int i=0;i<r;i++)
        for(int j=0;j<c;j++)
            cin>>a[i][j];

    long long low=a[0][0],high=a[0][c-1];

    for(int i=1;i<r;i++)
    {
        low=min(low,a[i][0]);
        high=max(high,a[i][c-1]);
    }

    int need=(r*c)/2+1;

    while(low<high)
    {
        long long mid=low+(high-low)/2;
        int count=0;

        for(int i=0;i<r;i++)
            count+=upperBound(a[i],mid);

        if(count<need)
            low=mid+1;
        else
            high=mid;
    }

    cout<<low;

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    static int upperBound(long[] row,long x)
    {
        int low=0,high=row.length;

        while(low<high)
        {
            int mid=low+(high-low)/2;

            if(row[mid]<=x)
                low=mid+1;
            else
                high=mid;
        }

        return low;
    }

    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);

        int r=sc.nextInt();
        int c=sc.nextInt();

        long[][] a=new long[r][c];

        for(int i=0;i<r;i++)
            for(int j=0;j<c;j++)
                a[i][j]=sc.nextLong();

        long low=a[0][0],high=a[0][c-1];

        for(int i=1;i<r;i++)
        {
            low=Math.min(low,a[i][0]);
            high=Math.max(high,a[i][c-1]);
        }

        int need=(r*c)/2+1;

        while(low<high)
        {
            long mid=low+(high-low)/2;
            int count=0;

            for(int i=0;i<r;i++)
                count+=upperBound(a[i],mid);

            if(count<need)
                low=mid+1;
            else
                high=mid;
        }

        System.out.print(low);
    }
}
```
```Python
def upper_bound(row,x):

    low,high=0,len(row)

    while low<high:

        mid=(low+high)//2

        if row[mid]<=x:
            low=mid+1
        else:
            high=mid

    return low


r,c=map(int,input().split())

a=[list(map(int,input().split())) for _ in range(r)]

low=min(row[0] for row in a)
high=max(row[-1] for row in a)

need=(r*c)//2+1

while low<high:

    mid=(low+high)//2

    count=0

    for row in a:
        count+=upper_bound(row,mid)

    if count<need:
        low=mid+1
    else:
        high=mid

print(low)
```
```C#
using System;

class Program
{
    static int UpperBound(long[] row,long x)
    {
        int low=0,high=row.Length;

        while(low<high)
        {
            int mid=low+(high-low)/2;

            if(row[mid]<=x)
                low=mid+1;
            else
                high=mid;
        }

        return low;
    }

    static void Main()
    {
        string[] first=Console.ReadLine().Split();

        int r=int.Parse(first[0]);
        int c=int.Parse(first[1]);

        long[][] a=new long[r][];

        for(int i=0;i<r;i++)
            a[i]=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        long low=a[0][0],high=a[0][c-1];

        for(int i=1;i<r;i++)
        {
            low=Math.Min(low,a[i][0]);
            high=Math.Max(high,a[i][c-1]);
        }

        int need=(r*c)/2+1;

        while(low<high)
        {
            long mid=low+(high-low)/2;
            int count=0;

            for(int i=0;i<r;i++)
                count+=UpperBound(a[i],mid);

            if(count<need)
                low=mid+1;
            else
                high=mid;
        }

        Console.Write(low);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const r=input[idx++];
const c=input[idx++];

const a=Array.from({length:r},()=>Array(c));

for(let i=0;i<r;i++)
    for(let j=0;j<c;j++)
        a[i][j]=input[idx++];

function upperBound(row,x)
{
    let low=0,high=row.length;

    while(low<high)
    {
        const mid=Math.floor((low+high)/2);

        if(row[mid]<=x)
            low=mid+1;
        else
            high=mid;
    }

    return low;
}

let low=a[0][0],high=a[0][c-1];

for(let i=1;i<r;i++)
{
    low=Math.min(low,a[i][0]);
    high=Math.max(high,a[i][c-1]);
}

const need=Math.floor((r*c)/2)+1;

while(low<high)
{
    const mid=Math.floor((low+high)/2);

    let count=0;

    for(let i=0;i<r;i++)
        count+=upperBound(a[i],mid);

    if(count<need)
        low=mid+1;
    else
        high=mid;
}

console.log(low);
```

### Output
Input

3 3

1 3 5

2 6 9

3 6 9

Output

5

# Time Complexity
O(R × log C × log(MaxValue − MinValue))

# Space Complexity
O(R × C) (for storing the matrix)

</approaches>




