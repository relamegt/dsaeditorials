# Single Element in a Sorted Array - Solution

## Problem Statement

Given a sorted array where every element appears exactly twice except for one element which appears exactly once, find and print the single element.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers in non-decreasing order.

## Output Format

Print a single integer representing the element that appears only once.

## Explanation

There are two common approaches to solve this problem.

- **Linear Scan:** Check elements in pairs until the unique element is found.
- **Binary Search (Optimal):** Use the pairing property of the sorted array to eliminate half of the search space in each step.

For example,

Input

9

1 1 2 3 3 4 4 8 8

Output

2

<approaches>
## Approach 1: Linear Scan

### Algorithm

1. Read the array.
2. Traverse the array in steps of two.
3. If the current element is different from the next element, it is the answer.
4. If all pairs are valid, the last element is the answer.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    for(int i=0;i<n-1;i+=2)
    {
        if(arr[i]!=arr[i+1])
        {
            printf("%lld",arr[i]);
            return 0;
        }
    }

    printf("%lld",arr[n-1]);

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

    for(int i=0;i<n-1;i+=2)
    {
        if(arr[i]!=arr[i+1])
        {
            cout<<arr[i];
            return 0;
        }
    }

    cout<<arr[n-1];

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

        for(int i=0;i<n-1;i+=2)
        {
            if(arr[i]!=arr[i+1])
            {
                System.out.print(arr[i]);
                return;
            }
        }

        System.out.print(arr[n-1]);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

for i in range(0,n-1,2):

    if arr[i]!=arr[i+1]:
        print(arr[i])
        exit()

print(arr[-1])
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] arr=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        for(int i=0;i<n-1;i+=2)
        {
            if(arr[i]!=arr[i+1])
            {
                Console.Write(arr[i]);
                return;
            }
        }

        Console.Write(arr[n-1]);
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

for(let i=0;i<n-1;i+=2)
{
    if(arr[i]!==arr[i+1])
    {
        console.log(arr[i]);
        return;
    }
}

console.log(arr[n-1]);
```

### Output
Input

9

1 1 2 3 3 4 4 8 8

Output

2

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Binary Search (Optimal)

### Algorithm

1. Read the array.
2. Initialize `low = 0` and `high = N - 1`.
3. While `low < high`:

- Find the middle index.
- If `mid` is odd, decrement it by 1 so that it points to the first element of a pair.
- If `arr[mid] == arr[mid + 1]`, the single element lies on the right, so set `low = mid + 2`.
- Otherwise, the single element lies on the left (including `mid`), so set `high = mid`.

1. Print `arr[low]`.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    int low=0;
    int high=n-1;

    while(low<high)
    {
        int mid=low+(high-low)/2;

        if(mid%2==1)
            mid--;

        if(arr[mid]==arr[mid+1])
            low=mid+2;
        else
            high=mid;
    }

    printf("%lld",arr[low]);

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

    int low=0;
    int high=n-1;

    while(low<high)
    {
        int mid=low+(high-low)/2;

        if(mid%2==1)
            mid--;

        if(arr[mid]==arr[mid+1])
            low=mid+2;
        else
            high=mid;
    }

    cout<<arr[low];

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

        int low=0;
        int high=n-1;

        while(low<high)
        {
            int mid=low+(high-low)/2;

            if(mid%2==1)
                mid--;

            if(arr[mid]==arr[mid+1])
                low=mid+2;
            else
                high=mid;
        }

        System.out.print(arr[low]);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

low=0
high=n-1

while low<high:

    mid=low+(high-low)//2

    if mid%2==1:
        mid-=1

    if arr[mid]==arr[mid+1]:
        low=mid+2
    else:
        high=mid

print(arr[low])
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] arr=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        int low=0;
        int high=n-1;

        while(low<high)
        {
            int mid=low+(high-low)/2;

            if(mid%2==1)
                mid--;

            if(arr[mid]==arr[mid+1])
                low=mid+2;
            else
                high=mid;
        }

        Console.Write(arr[low]);
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

let low=0;
let high=n-1;

while(low<high)
{
    let mid=low+Math.floor((high-low)/2);

    if(mid%2===1)
        mid--;

    if(arr[mid]===arr[mid+1])
        low=mid+2;
    else
        high=mid;
}

console.log(arr[low]);
```

### Output
Input

9

1 1 2 3 3 4 4 8 8

Output

2

# Time Complexity
O(log N)

# Space Complexity
O(1)

</approaches>




