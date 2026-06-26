# Bubble Sort - Solution

## Problem Statement

Given an array of integers `arr` of size `N`, sort the array in non-decreasing order using the Bubble Sort algorithm.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing the array.

## Output Format

Print the sorted array as `N` space-separated integers.

## Explanation

There are two common approaches to solve this problem.

- **Basic Bubble Sort:** Repeatedly swap adjacent elements if they are in the wrong order.
- **Optimized Bubble Sort:** Stop early if no swaps occur during a pass.

For example,

Input

5

4 1 3 9 7

Output

1 3 4 7 9

<approaches>
## Approach 1: Basic Bubble Sort

### Algorithm

1. Read the array.
2. Perform `N-1` passes over the array.
3. During each pass, compare adjacent elements.
4. Swap them if they are in the wrong order.
5. Print the sorted array.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    for(int i=0;i<n-1;i++)
    {
        for(int j=0;j<n-i-1;j++)
        {
            if(arr[j]>arr[j+1])
            {
                long long temp=arr[j];
                arr[j]=arr[j+1];
                arr[j+1]=temp;
            }
        }
    }

    for(int i=0;i<n;i++)
        printf("%lld ",arr[i]);

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

    for(int i=0;i<n-1;i++)
    {
        for(int j=0;j<n-i-1;j++)
        {
            if(arr[j]>arr[j+1])
                swap(arr[j],arr[j+1]);
        }
    }

    for(long long x:arr)
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

        int n=sc.nextInt();

        long[] arr=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        for(int i=0;i<n-1;i++)
        {
            for(int j=0;j<n-i-1;j++)
            {
                if(arr[j]>arr[j+1])
                {
                    long temp=arr[j];
                    arr[j]=arr[j+1];
                    arr[j+1]=temp;
                }
            }
        }

        for(long x:arr)
            System.out.print(x+" ");
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

for i in range(n-1):

    for j in range(n-i-1):

        if arr[j]>arr[j+1]:
            arr[j],arr[j+1]=arr[j+1],arr[j]

print(*arr)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        for(int i = 0; i < n - 1; i++)
        {
            for(int j = 0; j < n - i - 1; j++)
            {
                if(arr[j] > arr[j + 1])
                {
                    long temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }

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

for(let i = 0; i < n - 1; i++)
{
    for(let j = 0; j < n - i - 1; j++)
    {
        if(arr[j] > arr[j + 1])
        {
            let temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
        }
    }
}

console.log(arr.join(" "));
```

### Output
Input

5

4 1 3 9 7

Output

1 3 4 7 9

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Optimized Bubble Sort

### Algorithm

1. Read the array.
2. Perform Bubble Sort passes.
3. Keep a boolean variable `swapped`.
4. If no swaps occur during a complete pass, stop because the array is already sorted.
5. Print the sorted array.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    for(int i=0;i<n-1;i++)
    {
        int swapped=0;

        for(int j=0;j<n-i-1;j++)
        {
            if(arr[j]>arr[j+1])
            {
                long long temp=arr[j];
                arr[j]=arr[j+1];
                arr[j+1]=temp;
                swapped=1;
            }
        }

        if(!swapped)
            break;
    }

    for(int i=0;i<n;i++)
        printf("%lld ",arr[i]);

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

    for(int i=0;i<n-1;i++)
    {
        bool swapped=false;

        for(int j=0;j<n-i-1;j++)
        {
            if(arr[j]>arr[j+1])
            {
                swap(arr[j],arr[j+1]);
                swapped=true;
            }
        }

        if(!swapped)
            break;
    }

    for(long long x:arr)
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

        int n=sc.nextInt();

        long[] arr=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        for(int i=0;i<n-1;i++)
        {
            boolean swapped=false;

            for(int j=0;j<n-i-1;j++)
            {
                if(arr[j]>arr[j+1])
                {
                    long temp=arr[j];
                    arr[j]=arr[j+1];
                    arr[j+1]=temp;
                    swapped=true;
                }
            }

            if(!swapped)
                break;
        }

        for(long x:arr)
            System.out.print(x+" ");
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

for i in range(n-1):

    swapped=False

    for j in range(n-i-1):

        if arr[j]>arr[j+1]:
            arr[j],arr[j+1]=arr[j+1],arr[j]
            swapped=True

    if not swapped:
        break

print(*arr)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        for(int i = 0; i < n - 1; i++)
        {
            bool swapped = false;

            for(int j = 0; j < n - i - 1; j++)
            {
                if(arr[j] > arr[j + 1])
                {
                    long temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }

            if(!swapped)
                break;
        }

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

for(let i = 0; i < n - 1; i++)
{
    let swapped = false;

    for(let j = 0; j < n - i - 1; j++)
    {
        if(arr[j] > arr[j + 1])
        {
            let temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
            swapped = true;
        }
    }

    if(!swapped)
        break;
}

console.log(arr.join(" "));
```

### Output
Input

5

4 1 3 9 7

Output

1 3 4 7 9

# Time Complexity
Best Case: O(N)
Average Case: O(N²)
Worst Case: O(N²)

# Space Complexity
O(1)

</approaches>




