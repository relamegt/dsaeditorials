# Count Inversions - Solution

## Problem Statement

Given an array of integers `arr` of size `N`, count the number of inversions in the array.

An inversion is a pair of indices `(i, j)` such that `i < j` and `arr[i] > arr[j]`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing the array.

## Output Format

Print a single integer representing the inversion count.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Check every possible pair of indices.
- **Merge Sort (Optimal):** Count inversions while merging two sorted halves.

For example,

Input

5

2 4 1 3 5

Output

3

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. Initialize the inversion count as `0`.
3. For every pair `(i, j)` where `i < j`:

- If `arr[i] > arr[j]`, increment the inversion count.

1. Print the inversion count.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    long long count=0;

    for(int i=0;i<n;i++)
    {
        for(int j=i+1;j<n;j++)
        {
            if(arr[i]>arr[j])
                count++;
        }
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

    vector<long long> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    long long count=0;

    for(int i=0;i<n;i++)
    {
        for(int j=i+1;j<n;j++)
        {
            if(arr[i]>arr[j])
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

        long[] arr=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        long count=0;

        for(int i=0;i<n;i++)
        {
            for(int j=i+1;j<n;j++)
            {
                if(arr[i]>arr[j])
                    count++;
            }
        }

        System.out.print(count);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

count=0

for i in range(n):

    for j in range(i+1,n):

        if arr[i]>arr[j]:
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

        long[] arr=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        long count=0;

        for(int i=0;i<n;i++)
        {
            for(int j=i+1;j<n;j++)
            {
                if(arr[i]>arr[j])
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

const arr=[];

for(let i=0;i<n;i++)
    arr.push(input[idx++]);

let count=0;

for(let i=0;i<n;i++)
{
    for(let j=i+1;j<n;j++)
    {
        if(arr[i]>arr[j])
            count++;
    }
}

console.log(count);
```

### Output
Input

5

2 4 1 3 5

Output

3

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Merge Sort (Optimal)

### Algorithm

1. Divide the array recursively into two halves.
2. Count inversions in the left half.
3. Count inversions in the right half.
4. During merging:

- If the left element is smaller, copy it.
- Otherwise, all remaining elements in the left half form inversions with the current right element.

1. Return the total inversion count.
2. Print the final count.

```C
#include <stdio.h>

long long merge(long long arr[],int left,int mid,int right)
{
    int n1=mid-left+1;
    int n2=right-mid;

    long long L[n1],R[n2];

    for(int i=0;i<n1;i++)
        L[i]=arr[left+i];

    for(int i=0;i<n2;i++)
        R[i]=arr[mid+1+i];

    int i=0,j=0,k=left;
    long long inv=0;

    while(i<n1 && j<n2)
    {
        if(L[i]<=R[j])
            arr[k++]=L[i++];
        else
        {
            arr[k++]=R[j++];
            inv+=n1-i;
        }
    }

    while(i<n1)
        arr[k++]=L[i++];

    while(j<n2)
        arr[k++]=R[j++];

    return inv;
}

long long mergeSort(long long arr[],int left,int right)
{
    if(left>=right)
        return 0;

    int mid=left+(right-left)/2;

    long long inv=0;

    inv+=mergeSort(arr,left,mid);
    inv+=mergeSort(arr,mid+1,right);
    inv+=merge(arr,left,mid,right);

    return inv;
}

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    printf("%lld",mergeSort(arr,0,n-1));

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

long long merge(vector<long long>& arr,int left,int mid,int right)
{
    vector<long long> temp;

    int i=left;
    int j=mid+1;

    long long inv=0;

    while(i<=mid && j<=right)
    {
        if(arr[i]<=arr[j])
            temp.push_back(arr[i++]);
        else
        {
            temp.push_back(arr[j++]);
            inv+=mid-i+1;
        }
    }

    while(i<=mid)
        temp.push_back(arr[i++]);

    while(j<=right)
        temp.push_back(arr[j++]);

    for(int k=left;k<=right;k++)
        arr[k]=temp[k-left];

    return inv;
}

long long mergeSort(vector<long long>& arr,int left,int right)
{
    if(left>=right)
        return 0;

    int mid=left+(right-left)/2;

    long long inv=0;

    inv+=mergeSort(arr,left,mid);
    inv+=mergeSort(arr,mid+1,right);
    inv+=merge(arr,left,mid,right);

    return inv;
}

int main()
{
    int n;
    cin>>n;

    vector<long long> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    cout<<mergeSort(arr,0,n-1);

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    static long merge(long[] arr,int left,int mid,int right)
    {
        long[] temp=new long[right-left+1];

        int i=left;
        int j=mid+1;
        int k=0;

        long inv=0;

        while(i<=mid && j<=right)
        {
            if(arr[i]<=arr[j])
                temp[k++]=arr[i++];
            else
            {
                temp[k++]=arr[j++];
                inv+=mid-i+1;
            }
        }

        while(i<=mid)
            temp[k++]=arr[i++];

        while(j<=right)
            temp[k++]=arr[j++];

        for(i=left,k=0;i<=right;i++,k++)
            arr[i]=temp[k];

        return inv;
    }

    static long mergeSort(long[] arr,int left,int right)
    {
        if(left>=right)
            return 0;

        int mid=left+(right-left)/2;

        long inv=0;

        inv+=mergeSort(arr,left,mid);
        inv+=mergeSort(arr,mid+1,right);
        inv+=merge(arr,left,mid,right);

        return inv;
    }

    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);

        int n=sc.nextInt();

        long[] arr=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        System.out.print(mergeSort(arr,0,n-1));
    }
}
```
```Python
def merge(arr,left,mid,right):

    temp=[]

    i=left
    j=mid+1

    inv=0

    while i<=mid and j<=right:

        if arr[i]<=arr[j]:
            temp.append(arr[i])
            i+=1
        else:
            temp.append(arr[j])
            inv+=mid-i+1
            j+=1

    while i<=mid:
        temp.append(arr[i])
        i+=1

    while j<=right:
        temp.append(arr[j])
        j+=1

    arr[left:right+1]=temp

    return inv

def mergeSort(arr,left,right):

    if left>=right:
        return 0

    mid=(left+right)//2

    inv=0

    inv+=mergeSort(arr,left,mid)
    inv+=mergeSort(arr,mid+1,right)
    inv+=merge(arr,left,mid,right)

    return inv

n=int(input())

arr=list(map(int,input().split()))

print(mergeSort(arr,0,n-1))
```
```C#
using System;

class Program
{
    static long Merge(long[] arr,int left,int mid,int right)
    {
        long[] temp=new long[right-left+1];

        int i=left;
        int j=mid+1;
        int k=0;

        long inv=0;

        while(i<=mid && j<=right)
        {
            if(arr[i]<=arr[j])
                temp[k++]=arr[i++];
            else
            {
                temp[k++]=arr[j++];
                inv+=mid-i+1;
            }
        }

        while(i<=mid)
            temp[k++]=arr[i++];

        while(j<=right)
            temp[k++]=arr[j++];

        for(i=left,k=0;i<=right;i++,k++)
            arr[i]=temp[k];

        return inv;
    }

    static long MergeSort(long[] arr,int left,int right)
    {
        if(left>=right)
            return 0;

        int mid=left+(right-left)/2;

        long inv=0;

        inv+=MergeSort(arr,left,mid);
        inv+=MergeSort(arr,mid+1,right);
        inv+=Merge(arr,left,mid,right);

        return inv;
    }

    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] arr=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        Console.Write(MergeSort(arr,0,n-1));
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const arr=[];

for(let i=0;i<n;i++)
    arr.push(input[idx++]);

function merge(left,mid,right)
{
    const temp=[];

    let i=left;
    let j=mid+1;

    let inv=0;

    while(i<=mid && j<=right)
    {
        if(arr[i]<=arr[j])
            temp.push(arr[i++]);
        else
        {
            temp.push(arr[j++]);
            inv+=mid-i+1;
        }
    }

    while(i<=mid)
        temp.push(arr[i++]);

    while(j<=right)
        temp.push(arr[j++]);

    for(let k=0;k<temp.length;k++)
        arr[left+k]=temp[k];

    return inv;
}

function mergeSort(left,right)
{
    if(left>=right)
        return 0;

    const mid=Math.floor((left+right)/2);

    let inv=0;

    inv+=mergeSort(left,mid);
    inv+=mergeSort(mid+1,right);
    inv+=merge(left,mid,right);

    return inv;
}

console.log(mergeSort(0,n-1));
```

### Output
Input

5

2 4 1 3 5

Output

3

# Time Complexity
O(N log N)

# Space Complexity
O(N)

</approaches>




