# Merge Sort - Solution

## Problem Statement

Given an array of integers `arr` of size `N`, sort the array in non-decreasing order using the Merge Sort algorithm.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing the array.

## Output Format

Print the sorted array in a single line as `N` space-separated integers.

## Explanation

Merge Sort follows the divide-and-conquer approach. It recursively divides the array into two halves, sorts each half, and then merges the sorted halves into a single sorted array.

For example,

Input

5

4 1 3 9 7

Output

1 3 4 7 9

## Algorithm

1. Divide the array into two halves until each subarray contains one element.
2. Recursively sort the left half.
3. Recursively sort the right half.
4. Merge the two sorted halves into a temporary array.
5. Copy the merged elements back to the original array.
6. Print the sorted array.

```C
#include <stdio.h>
#include <stdlib.h>

void merge(long long arr[],int left,int mid,int right)
{
    int n1=mid-left+1;
    int n2=right-mid;

    long long L[n1],R[n2];

    for(int i=0;i<n1;i++)
        L[i]=arr[left+i];

    for(int i=0;i<n2;i++)
        R[i]=arr[mid+1+i];

    int i=0,j=0,k=left;

    while(i<n1 && j<n2)
    {
        if(L[i]<=R[j])
            arr[k++]=L[i++];
        else
            arr[k++]=R[j++];
    }

    while(i<n1)
        arr[k++]=L[i++];

    while(j<n2)
        arr[k++]=R[j++];
}

void mergeSort(long long arr[],int left,int right)
{
    if(left>=right)
        return;

    int mid=left+(right-left)/2;

    mergeSort(arr,left,mid);
    mergeSort(arr,mid+1,right);

    merge(arr,left,mid,right);
}

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    mergeSort(arr,0,n-1);

    for(int i=0;i<n;i++)
        printf("%lld ",arr[i]);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

void merge(vector<long long>& arr,int left,int mid,int right)
{
    vector<long long> temp;

    int i=left;
    int j=mid+1;

    while(i<=mid && j<=right)
    {
        if(arr[i]<=arr[j])
            temp.push_back(arr[i++]);
        else
            temp.push_back(arr[j++]);
    }

    while(i<=mid)
        temp.push_back(arr[i++]);

    while(j<=right)
        temp.push_back(arr[j++]);

    for(int k=left;k<=right;k++)
        arr[k]=temp[k-left];
}

void mergeSort(vector<long long>& arr,int left,int right)
{
    if(left>=right)
        return;

    int mid=left+(right-left)/2;

    mergeSort(arr,left,mid);
    mergeSort(arr,mid+1,right);

    merge(arr,left,mid,right);
}

int main()
{
    int n;
    cin>>n;

    vector<long long> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    mergeSort(arr,0,n-1);

    for(long long x:arr)
        cout<<x<<" ";

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    static void merge(long[] arr,int left,int mid,int right)
    {
        long[] temp=new long[right-left+1];

        int i=left;
        int j=mid+1;
        int k=0;

        while(i<=mid && j<=right)
        {
            if(arr[i]<=arr[j])
                temp[k++]=arr[i++];
            else
                temp[k++]=arr[j++];
        }

        while(i<=mid)
            temp[k++]=arr[i++];

        while(j<=right)
            temp[k++]=arr[j++];

        for(i=left,k=0;i<=right;i++,k++)
            arr[i]=temp[k];
    }

    static void mergeSort(long[] arr,int left,int right)
    {
        if(left>=right)
            return;

        int mid=left+(right-left)/2;

        mergeSort(arr,left,mid);
        mergeSort(arr,mid+1,right);

        merge(arr,left,mid,right);
    }

    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);

        int n=sc.nextInt();

        long[] arr=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        mergeSort(arr,0,n-1);

        for(long x:arr)
            System.out.print(x+" ");
    }
}
```
```Python
def merge(arr,left,mid,right):

    temp=[]

    i=left
    j=mid+1

    while i<=mid and j<=right:

        if arr[i]<=arr[j]:
            temp.append(arr[i])
            i+=1
        else:
            temp.append(arr[j])
            j+=1

    while i<=mid:
        temp.append(arr[i])
        i+=1

    while j<=right:
        temp.append(arr[j])
        j+=1

    arr[left:right+1]=temp

def mergeSort(arr,left,right):

    if left>=right:
        return

    mid=(left+right)//2

    mergeSort(arr,left,mid)
    mergeSort(arr,mid+1,right)

    merge(arr,left,mid,right)

n=int(input())

arr=list(map(int,input().split()))

mergeSort(arr,0,n-1)

print(*arr)
```
```C#
using System;

class Program
{
    static void Merge(long[] arr, int left, int mid, int right)
    {
        long[] temp = new long[right - left + 1];

        int i = left;
        int j = mid + 1;
        int k = 0;

        while(i <= mid && j <= right)
        {
            if(arr[i] <= arr[j])
                temp[k++] = arr[i++];
            else
                temp[k++] = arr[j++];
        }

        while(i <= mid)
            temp[k++] = arr[i++];

        while(j <= right)
            temp[k++] = arr[j++];

        for(i = left, k = 0; i <= right; i++, k++)
            arr[i] = temp[k];
    }

    static void MergeSort(long[] arr, int left, int right)
    {
        if(left >= right)
            return;

        int mid = left + (right - left) / 2;

        MergeSort(arr, left, mid);
        MergeSort(arr, mid + 1, right);

        Merge(arr, left, mid, right);
    }

    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        MergeSort(arr, 0, n - 1);

        foreach(long x in arr)
            Console.Write(x + " ");
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const arr = [];

for(let i = 0; i < n; i++)
    arr.push(input[idx++]);

function merge(left, mid, right)
{
    const temp = [];

    let i = left;
    let j = mid + 1;

    while(i <= mid && j <= right)
    {
        if(arr[i] <= arr[j])
            temp.push(arr[i++]);
        else
            temp.push(arr[j++]);
    }

    while(i <= mid)
        temp.push(arr[i++]);

    while(j <= right)
        temp.push(arr[j++]);

    for(let k = 0; k < temp.length; k++)
        arr[left + k] = temp[k];
}

function mergeSort(left, right)
{
    if(left >= right)
        return;

    const mid = Math.floor((left + right) / 2);

    mergeSort(left, mid);
    mergeSort(mid + 1, right);

    merge(left, mid, right);
}

mergeSort(0, n - 1);

console.log(arr.join(" "));
```

### Output
Input

5

4 1 3 9 7

Output

1 3 4 7 9

# Time Complexity
O(N log N)

# Space Complexity
O(N)




