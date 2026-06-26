# Quick Sort - Solution

## Problem Statement

Given an array of integers `arr` of size `N`, sort the array in non-decreasing order using the Quick Sort algorithm.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing the array.

## Output Format

Print the sorted array in a single line as `N` space-separated integers.

## Explanation

Quick Sort is a divide-and-conquer algorithm. It selects a pivot element, partitions the array into elements smaller and larger than the pivot, and recursively sorts the partitions.

For example,

Input

7

5 8 1 3 7 9 2

Output

1 2 3 5 7 8 9

## Algorithm

1. Choose the last element as the pivot.
2. Partition the array so that elements smaller than or equal to the pivot are placed before it and larger elements after it.
3. Place the pivot in its correct sorted position.
4. Recursively apply Quick Sort to the left and right partitions.
5. Print the sorted array.

```C
#include <stdio.h>

void swap(long long *a,long long *b)
{
    long long temp=*a;
    *a=*b;
    *b=temp;
}

int partition(long long arr[],int low,int high)
{
    long long pivot=arr[high];
    int i=low-1;

    for(int j=low;j<high;j++)
    {
        if(arr[j]<=pivot)
        {
            i++;
            swap(&arr[i],&arr[j]);
        }
    }

    swap(&arr[i+1],&arr[high]);

    return i+1;
}

void quickSort(long long arr[],int low,int high)
{
    if(low<high)
    {
        int pi=partition(arr,low,high);

        quickSort(arr,low,pi-1);
        quickSort(arr,pi+1,high);
    }
}

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    quickSort(arr,0,n-1);

    for(int i=0;i<n;i++)
        printf("%lld ",arr[i]);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int partition(vector<long long>& arr,int low,int high)
{
    long long pivot=arr[high];
    int i=low-1;

    for(int j=low;j<high;j++)
    {
        if(arr[j]<=pivot)
        {
            i++;
            swap(arr[i],arr[j]);
        }
    }

    swap(arr[i+1],arr[high]);

    return i+1;
}

void quickSort(vector<long long>& arr,int low,int high)
{
    if(low<high)
    {
        int pi=partition(arr,low,high);

        quickSort(arr,low,pi-1);
        quickSort(arr,pi+1,high);
    }
}

int main()
{
    int n;
    cin>>n;

    vector<long long> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    quickSort(arr,0,n-1);

    for(long long x:arr)
        cout<<x<<" ";

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    static void swap(long[] arr,int i,int j)
    {
        long temp=arr[i];
        arr[i]=arr[j];
        arr[j]=temp;
    }

    static int partition(long[] arr,int low,int high)
    {
        long pivot=arr[high];
        int i=low-1;

        for(int j=low;j<high;j++)
        {
            if(arr[j]<=pivot)
            {
                i++;
                swap(arr,i,j);
            }
        }

        swap(arr,i+1,high);

        return i+1;
    }

    static void quickSort(long[] arr,int low,int high)
    {
        if(low<high)
        {
            int pi=partition(arr,low,high);

            quickSort(arr,low,pi-1);
            quickSort(arr,pi+1,high);
        }
    }

    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);

        int n=sc.nextInt();

        long[] arr=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        quickSort(arr,0,n-1);

        for(long x:arr)
            System.out.print(x+" ");
    }
}
```
```Python
def partition(arr,low,high):

    pivot=arr[high]
    i=low-1

    for j in range(low,high):

        if arr[j]<=pivot:
            i+=1
            arr[i],arr[j]=arr[j],arr[i]

    arr[i+1],arr[high]=arr[high],arr[i+1]

    return i+1

def quickSort(arr,low,high):

    if low<high:

        pi=partition(arr,low,high)

        quickSort(arr,low,pi-1)
        quickSort(arr,pi+1,high)

n=int(input())

arr=list(map(int,input().split()))

quickSort(arr,0,n-1)

print(*arr)
```
```C#
using System;

class Program
{
    static void Swap(long[] arr, int i, int j)
    {
        long temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    static int Partition(long[] arr, int low, int high)
    {
        long pivot = arr[high];
        int i = low - 1;

        for(int j = low; j < high; j++)
        {
            if(arr[j] <= pivot)
            {
                i++;
                Swap(arr, i, j);
            }
        }

        Swap(arr, i + 1, high);

        return i + 1;
    }

    static void QuickSort(long[] arr, int low, int high)
    {
        if(low < high)
        {
            int pi = Partition(arr, low, high);

            QuickSort(arr, low, pi - 1);
            QuickSort(arr, pi + 1, high);
        }
    }

    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        QuickSort(arr, 0, n - 1);

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

function partition(low, high)
{
    const pivot = arr[high];
    let i = low - 1;

    for(let j = low; j < high; j++)
    {
        if(arr[j] <= pivot)
        {
            i++;
            [arr[i], arr[j]] = [arr[j], arr[i]];
        }
    }

    [arr[i + 1], arr[high]] = [arr[high], arr[i + 1]];

    return i + 1;
}

function quickSort(low, high)
{
    if(low < high)
    {
        const pi = partition(low, high);

        quickSort(low, pi - 1);
        quickSort(pi + 1, high);
    }
}

quickSort(0, n - 1);

console.log(arr.join(" "));
```

### Output
Input

7

5 8 1 3 7 9 2

Output

1 2 3 5 7 8 9

# Time Complexity
Best Case: O(N log N)
Average Case: O(N log N)
Worst Case: O(N²)

# Space Complexity
Average Case: O(log N)
Worst Case: O(N)




