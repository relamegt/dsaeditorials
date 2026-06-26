# K-th Smallest Element in a Sorted Matrix - Solution

## Problem Statement

Given an `N × N` matrix where each row and each column is sorted in non-decreasing order, find the `K`-th smallest element in the matrix.

The `K`-th smallest element is based on the full sorted order of all matrix elements, not on distinct values.

## Input Format

First line: Integer `N`.

Next `N` lines: `N` space-separated integers representing the matrix.

Last line: Integer `K`.

## Output Format

Print a single integer representing the `K`-th smallest element.

## Explanation

There are two approaches to solve this problem.

- Approach 1: Flatten and Sort
- Approach 2: Binary Search on Answer (Optimal)

For example,

Input

3

1 5 9

10 11 13

12 13 15

8

Output

13

<approaches>
## Approach 1: Flatten and Sort

### Algorithm

1. Read the matrix.
2. Store all elements in a one-dimensional array.
3. Sort the array.
4. Print the element at index `K-1`.

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
    int n;
    scanf("%d",&n);

    long long arr[n*n];

    for(int i=0;i<n*n;i++)
        scanf("%lld",&arr[i]);

    int k;
    scanf("%d",&k);

    qsort(arr,n*n,sizeof(long long),cmp);

    printf("%lld",arr[k-1]);

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
    int n;
    cin>>n;

    vector<long long> arr(n*n);

    for(int i=0;i<n*n;i++)
        cin>>arr[i];

    int k;
    cin>>k;

    sort(arr.begin(),arr.end());

    cout<<arr[k-1];

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

        long[] arr=new long[n*n];

        for(int i=0;i<n*n;i++)
            arr[i]=sc.nextLong();

        int k=sc.nextInt();

        Arrays.sort(arr);

        System.out.print(arr[k-1]);
    }
}
```
```Python
n=int(input())

arr=[]

for _ in range(n):
    arr.extend(map(int,input().split()))

k=int(input())

arr.sort()

print(arr[k-1])
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] arr=new long[n*n];

        int idx=0;

        for(int i=0;i<n;i++)
        {
            long[] row=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

            foreach(long x in row)
                arr[idx++]=x;
        }

        int k=int.Parse(Console.ReadLine());

        Array.Sort(arr);

        Console.Write(arr[k-1]);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const arr=[];

for(let i=0;i<n*n;i++)
    arr.push(input[idx++]);

const k=input[idx++];

arr.sort((a,b)=>a-b);

console.log(arr[k-1]);
```

### Output
Input

3

1 5 9

10 11 13

12 13 15

8

Output

13

# Time Complexity
O(N² log(N²))

# Space Complexity
O(N²)

## Approach 2: Binary Search on Answer (Optimal)

### Algorithm

1. Read the matrix and the value `K`.
2. Set the search range from the smallest element (`matrix[0][0]`) to the largest element (`matrix[N-1][N-1]`).
3. For each middle value, count how many elements in the matrix are less than or equal to it using binary search on every row.
4. If the count is less than `K`, search the higher half.
5. Otherwise, search the lower half.
6. The final answer is the smallest value having at least `K` elements less than or equal to it.

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
    int n;
    scanf("%d",&n);

    long long a[n][n];

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            scanf("%lld",&a[i][j]);

    int k;
    scanf("%d",&k);

    long long low=a[0][0],high=a[n-1][n-1];

    while(low<high)
    {
        long long mid=low+(high-low)/2;
        int count=0;

        for(int i=0;i<n;i++)
            count+=upperBound(a[i],n,mid);

        if(count<k)
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
    int n;
    cin>>n;

    vector<vector<long long>> a(n,vector<long long>(n));

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            cin>>a[i][j];

    int k;
    cin>>k;

    long long low=a[0][0],high=a[n-1][n-1];

    while(low<high)
    {
        long long mid=low+(high-low)/2;
        int count=0;

        for(int i=0;i<n;i++)
            count+=upperBound(a[i],mid);

        if(count<k)
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

        int n=sc.nextInt();

        long[][] a=new long[n][n];

        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                a[i][j]=sc.nextLong();

        int k=sc.nextInt();

        long low=a[0][0],high=a[n-1][n-1];

        while(low<high)
        {
            long mid=low+(high-low)/2;
            int count=0;

            for(int i=0;i<n;i++)
                count+=upperBound(a[i],mid);

            if(count<k)
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


n=int(input())

a=[list(map(int,input().split())) for _ in range(n)]

k=int(input())

low=a[0][0]
high=a[-1][-1]

while low<high:

    mid=(low+high)//2

    count=0

    for row in a:
        count+=upper_bound(row,mid)

    if count<k:
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
        int n=int.Parse(Console.ReadLine());

        long[][] a=new long[n][];

        for(int i=0;i<n;i++)
            a[i]=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        int k=int.Parse(Console.ReadLine());

        long low=a[0][0],high=a[n-1][n-1];

        while(low<high)
        {
            long mid=low+(high-low)/2;
            int count=0;

            for(int i=0;i<n;i++)
                count+=UpperBound(a[i],mid);

            if(count<k)
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

const n=input[idx++];

const a=Array.from({length:n},()=>Array(n));

for(let i=0;i<n;i++)
    for(let j=0;j<n;j++)
        a[i][j]=input[idx++];

const k=input[idx++];

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

let low=a[0][0],high=a[n-1][n-1];

while(low<high)
{
    const mid=Math.floor((low+high)/2);

    let count=0;

    for(let i=0;i<n;i++)
        count+=upperBound(a[i],mid);

    if(count<k)
        low=mid+1;
    else
        high=mid;
}

console.log(low);
```

### Output
Input

3

1 5 9

10 11 13

12 13 15

8

Output

13

# Time Complexity
O(N log N × log(MaxValue − MinValue))

# Space Complexity
O(N²) (for storing the matrix)

</approaches>




