# Union of Two Sorted Arrays - Solution

## Problem Statement

Given two sorted arrays `arr1[]` and `arr2[]` of sizes `N` and `M`, find their union. The union should contain all distinct elements present in either array, in sorted order, without duplicates.

### Input Format

First line: integer `N`.

Second line: `N` space-separated integers of `arr1`.

Third line: integer `M`.

Fourth line: `M` space-separated integers of `arr2`.

### Output Format

Print the union of the two arrays in sorted order without duplicates.

## Explanation

There are two common approaches to solve this problem.

- **Merge Two Sorted Arrays (Recommended):** Traverse both arrays simultaneously using two pointers while skipping duplicates.
- **Set Based Approach:** Insert all elements into a sorted set and print the distinct elements.

For example,

Input:

5

1 2 3 4 5

5

1 2 3 4 5

Union: 1 2 3 4 5

<approaches>
## Approach 1: Merge Two Sorted Arrays (Recommended)

### Algorithm

1. Read `N` and the first sorted array.
2. Read `M` and the second sorted array.
3. Initialize two pointers `i` and `j` to `0`.
4. Compare elements of both arrays.
5. Print the smaller element if it has not already been printed.
6. If both elements are equal, print only one and move both pointers.
7. After one array finishes, print the remaining distinct elements from the other array.
8. The printed sequence is the required union.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d",&N);

    long long arr1[N];

    for(int i=0;i<N;i++)
        scanf("%lld",&arr1[i]);

    int M;
    scanf("%d",&M);

    long long arr2[M];

    for(int i=0;i<M;i++)
        scanf("%lld",&arr2[i]);

    int i=0,j=0;
    long long last=0;
    int first=1;

    while(i<N && j<M)
    {
        long long value;

        if(arr1[i]<arr2[j])
            value=arr1[i++];
        else if(arr1[i]>arr2[j])
            value=arr2[j++];
        else
        {
            value=arr1[i];
            i++;
            j++;
        }

        if(first || value!=last)
        {
            printf("%lld ",value);
            last=value;
            first=0;
        }
    }

    while(i<N)
    {
        if(first || arr1[i]!=last)
        {
            printf("%lld ",arr1[i]);
            last=arr1[i];
            first=0;
        }
        i++;
    }

    while(j<M)
    {
        if(first || arr2[j]!=last)
        {
            printf("%lld ",arr2[j]);
            last=arr2[j];
            first=0;
        }
        j++;
    }

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main()
{
    int N;
    cin>>N;

    long long arr1[N];

    for(int i=0;i<N;i++)
        cin>>arr1[i];

    int M;
    cin>>M;

    long long arr2[M];

    for(int i=0;i<M;i++)
        cin>>arr2[i];

    int i=0,j=0;
    long long last=0;
    bool first=true;

    while(i<N && j<M)
    {
        long long value;

        if(arr1[i]<arr2[j])
            value=arr1[i++];
        else if(arr1[i]>arr2[j])
            value=arr2[j++];
        else
        {
            value=arr1[i];
            i++;
            j++;
        }

        if(first || value!=last)
        {
            cout<<value<<" ";
            last=value;
            first=false;
        }
    }

    while(i<N)
    {
        if(first || arr1[i]!=last)
        {
            cout<<arr1[i]<<" ";
            last=arr1[i];
            first=false;
        }
        i++;
    }

    while(j<M)
    {
        if(first || arr2[j]!=last)
        {
            cout<<arr2[j]<<" ";
            last=arr2[j];
            first=false;
        }
        j++;
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

        int N=sc.nextInt();

        long[] arr1=new long[N];

        for(int i=0;i<N;i++)
            arr1[i]=sc.nextLong();

        int M=sc.nextInt();

        long[] arr2=new long[M];

        for(int i=0;i<M;i++)
            arr2[i]=sc.nextLong();

        int i=0,j=0;
        long last=0;
        boolean first=true;

        while(i<N && j<M)
        {
            long value;

            if(arr1[i]<arr2[j])
                value=arr1[i++];
            else if(arr1[i]>arr2[j])
                value=arr2[j++];
            else
            {
                value=arr1[i];
                i++;
                j++;
            }

            if(first || value!=last)
            {
                System.out.print(value+" ");
                last=value;
                first=false;
            }
        }

        while(i<N)
        {
            if(first || arr1[i]!=last)
            {
                System.out.print(arr1[i]+" ");
                last=arr1[i];
                first=false;
            }
            i++;
        }

        while(j<M)
        {
            if(first || arr2[j]!=last)
            {
                System.out.print(arr2[j]+" ");
                last=arr2[j];
                first=false;
            }
            j++;
        }
    }
}
```
```Python
N=int(input())

arr1=list(map(int,input().split()))

M=int(input())

arr2=list(map(int,input().split()))

i=j=0
first=True
last=0

while i<N and j<M:

    if arr1[i]<arr2[j]:
        value=arr1[i]
        i+=1
    elif arr1[i]>arr2[j]:
        value=arr2[j]
        j+=1
    else:
        value=arr1[i]
        i+=1
        j+=1

    if first or value!=last:
        print(value,end=" ")
        last=value
        first=False

while i<N:
    if first or arr1[i]!=last:
        print(arr1[i],end=" ")
        last=arr1[i]
        first=False
    i+=1

while j<M:
    if first or arr2[j]!=last:
        print(arr2[j],end=" ")
        last=arr2[j]
        first=False
    j+=1
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N=int.Parse(Console.ReadLine());

        long[] arr1=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        int M=int.Parse(Console.ReadLine());

        long[] arr2=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        int i=0,j=0;
        bool first=true;
        long last=0;

        while(i < N)
        {
            if(first || arr1[i] != last)
            {
                Console.Write(arr1[i] + " ");
                last = arr1[i];
                first = false;
            }
            i++;
        }

        while(j < M)
        {
            if(first || arr2[j] != last)
            {
                Console.Write(arr2[j] + " ");
                last = arr2[j];
                first = false;
            }
            j++;
        }
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const N = input[idx++];
const arr1 = [];

for(let i = 0; i < N; i++)
    arr1.push(input[idx++]);

const M = input[idx++];
const arr2 = [];

for(let i = 0; i < M; i++)
    arr2.push(input[idx++]);

let i = 0;
let j = 0;
let first = true;
let last = 0;
let ans = [];

while(i < N && j < M)
{
    let value;

    if(arr1[i] < arr2[j])
        value = arr1[i++];
    else if(arr1[i] > arr2[j])
        value = arr2[j++];
    else
    {
        value = arr1[i];
        i++;
        j++;
    }

    if(first || value !== last)
    {
        ans.push(value);
        last = value;
        first = false;
    }
}

while(i < N)
{
    if(first || arr1[i] !== last)
    {
        ans.push(arr1[i]);
        last = arr1[i];
        first = false;
    }
    i++;
}

while(j < M)
{
    if(first || arr2[j] !== last)
    {
        ans.push(arr2[j]);
        last = arr2[j];
        first = false;
    }
    j++;
}

console.log(ans.join(" "));
```

### Output
For Input:
5
1 2 3 4 5
5
1 2 3 4 5

Output:
1 2 3 4 5

# Time Complexity
O(N + M)

# Space Complexity
O(1)

## Approach 2: Using Set

### Algorithm

1. Read both arrays.
2. Insert all elements of both arrays into a set.
3. Since a set stores only distinct values, duplicates are automatically removed.
4. Traverse the set in sorted order.
5. Print every element.

```C
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a,const void *b)
{
    long long x=*(long long*)a;
    long long y=*(long long*)b;

    if(x<y) return -1;
    if(x>y) return 1;
    return 0;
}

int main()
{
    int N;
    scanf("%d",&N);

    int M;

    scanf("%*[
]");

    long long *arr;

    arr=(long long*)malloc(sizeof(long long)*(2*N+200000));

    for(int i=0;i<N;i++)
        scanf("%lld",&arr[i]);

    scanf("%d",&M);

    for(int i=0;i<M;i++)
        scanf("%lld",&arr[N+i]);

    int total=N+M;

    qsort(arr,total,sizeof(long long),compare);

    printf("%lld ",arr[0]);

    for(int i=1;i<total;i++)
    {
        if(arr[i]!=arr[i-1])
            printf("%lld ",arr[i]);
    }

    free(arr);

    return 0;
}
```
```cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
    int N;
    cin>>N;

    set<long long> s;

    for(int i=0;i<N;i++)
    {
        long long x;
        cin>>x;
        s.insert(x);
    }

    int M;
    cin>>M;

    for(int i=0;i<M;i++)
    {
        long long x;
        cin>>x;
        s.insert(x);
    }

    for(auto x:s)
        cout<<x<<" ";

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

        int N=sc.nextInt();

        TreeSet<Long> set=new TreeSet<>();

        for(int i=0;i<N;i++)
            set.add(sc.nextLong());

        int M=sc.nextInt();

        for(int i=0;i<M;i++)
            set.add(sc.nextLong());

        for(long x:set)
            System.out.print(x+" ");
    }
}
```
```Python
N=int(input())

arr1=list(map(int,input().split()))

M=int(input())

arr2=list(map(int,input().split()))

print(*sorted(set(arr1+arr2)))
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int N=int.Parse(Console.ReadLine());

        long[] arr1=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        int M=int.Parse(Console.ReadLine());

        long[] arr2=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        SortedSet<long> set=new SortedSet<long>();

        foreach(long x in arr1)
            set.Add(x);

        foreach(long x in arr2)
            set.Add(x);

        foreach(long x in set)
            Console.Write(x+" ");
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const N = input[idx++];

const set = new Set();

for(let i=0;i<N;i++)
    set.add(input[idx++]);

const M = input[idx++];

for(let i=0;i<M;i++)
    set.add(input[idx++]);

const ans = Array.from(set).sort((a,b)=>a-b);

console.log(ans.join(" "));
```

### Output
For Input:
5
1 2 3 4 5
5
1 2 3 4 5

Output:
1 2 3 4 5

# Time Complexity
O((N + M) log(N + M))

# Space Complexity
O(N + M)

</approaches>



>
