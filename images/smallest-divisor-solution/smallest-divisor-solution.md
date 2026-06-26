# Smallest Divisor - Solution

## Problem Statement

Given an array of positive integers `nums` of size `N` and an integer `threshold`, choose a positive integer divisor and divide every array element by it. The division result for each element is rounded up to the nearest integer, and all these rounded values are added.

Find and print the smallest divisor such that the total sum is less than or equal to `threshold`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated positive integers

Third line: Integer `threshold`

## Output Format

Print a single integer representing the smallest divisor.

## Explanation

There are two approaches to solve this problem.

- **Approach 1:** Linear Search
- **Approach 2:** Binary Search (Optimal)

For example,

Input

4

1 2 5 9

6

Output

5

<approaches>
## Approach 1: Linear Search

### Algorithm

1. Read the array and the threshold.
2. Find the maximum element in the array.
3. Try every divisor from `1` to the maximum element.
4. Compute the sum of `ceil(nums[i] / divisor)` for all elements.
5. The first divisor whose sum is less than or equal to the threshold is the answer.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];
    long long maxi=0;

    for(int i=0;i<n;i++)
    {
        scanf("%lld",&arr[i]);
        if(arr[i]>maxi)
            maxi=arr[i];
    }

    long long threshold;
    scanf("%lld",&threshold);

    for(long long d=1;d<=maxi;d++)
    {
        long long sum=0;

        for(int i=0;i<n;i++)
            sum+=(arr[i]+d-1)/d;

        if(sum<=threshold)
        {
            printf("%lld",d);
            return 0;
        }
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

    vector<long long> arr(n);

    long long maxi=0;

    for(int i=0;i<n;i++)
    {
        cin>>arr[i];
        maxi=max(maxi,arr[i]);
    }

    long long threshold;
    cin>>threshold;

    for(long long d=1;d<=maxi;d++)
    {
        long long sum=0;

        for(long long x:arr)
            sum+=(x+d-1)/d;

        if(sum<=threshold)
        {
            cout<<d;
            return 0;
        }
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

        long[] arr=new long[n];

        long maxi=0;

        for(int i=0;i<n;i++)
        {
            arr[i]=sc.nextLong();
            maxi=Math.max(maxi,arr[i]);
        }

        long threshold=sc.nextLong();

        for(long d=1;d<=maxi;d++)
        {
            long sum=0;

            for(long x:arr)
                sum+=(x+d-1)/d;

            if(sum<=threshold)
            {
                System.out.print(d);
                return;
            }
        }
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

threshold=int(input())

maxi=max(arr)

for d in range(1,maxi+1):

    total=0

    for x in arr:
        total+=(x+d-1)//d

    if total<=threshold:
        print(d)
        break
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] arr=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        long threshold=long.Parse(Console.ReadLine());

        long maxi=0;

        foreach(long x in arr)
            if(x>maxi)
                maxi=x;

        for(long d=1;d<=maxi;d++)
        {
            long sum=0;

            foreach(long x in arr)
                sum+=(x+d-1)/d;

            if(sum<=threshold)
            {
                Console.Write(d);
                return;
            }
        }
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const arr=[];

let maxi=0;

for(let i=0;i<n;i++)
{
    arr.push(input[idx]);
    maxi=Math.max(maxi,input[idx]);
    idx++;
}

const threshold=input[idx];

for(let d=1;d<=maxi;d++)
{
    let sum=0;

    for(const x of arr)
        sum+=Math.floor((x+d-1)/d);

    if(sum<=threshold)
    {
        console.log(d);
        return;
    }
}
```

### Output
Input

4

1 2 5 9

6

Output

5

# Time Complexity
O(N × MaxElement)

# Space Complexity
O(1)

## Approach 2: Binary Search (Optimal)

### Algorithm

1. Read the array and the threshold.
2. Find the maximum element in the array.
3. Set `low = 1` and `high = maximum element`.
4. While `low <= high`:

- Find the middle divisor.
- Compute the sum of `ceil(nums[i] / mid)` for all elements.
- If the sum is less than or equal to the threshold, store the divisor and search for a smaller one.
- Otherwise, search for a larger divisor.

1. Print the stored answer.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];
    long long maxi=0;

    for(int i=0;i<n;i++)
    {
        scanf("%lld",&arr[i]);

        if(arr[i]>maxi)
            maxi=arr[i];
    }

    long long threshold;
    scanf("%lld",&threshold);

    long long low=1;
    long long high=maxi;
    long long ans=maxi;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;
        long long sum=0;

        for(int i=0;i<n;i++)
            sum+=(arr[i]+mid-1)/mid;

        if(sum<=threshold)
        {
            ans=mid;
            high=mid-1;
        }
        else
        {
            low=mid+1;
        }
    }

    printf("%lld",ans);

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

    long long maxi=0;

    for(int i=0;i<n;i++)
    {
        cin>>arr[i];
        maxi=max(maxi,arr[i]);
    }

    long long threshold;
    cin>>threshold;

    long long low=1;
    long long high=maxi;
    long long ans=maxi;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;
        long long sum=0;

        for(long long x:arr)
            sum+=(x+mid-1)/mid;

        if(sum<=threshold)
        {
            ans=mid;
            high=mid-1;
        }
        else
        {
            low=mid+1;
        }
    }

    cout<<ans;

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

        long maxi=0;

        for(int i=0;i<n;i++)
        {
            arr[i]=sc.nextLong();
            maxi=Math.max(maxi,arr[i]);
        }

        long threshold=sc.nextLong();

        long low=1;
        long high=maxi;
        long ans=maxi;

        while(low<=high)
        {
            long mid=low+(high-low)/2;
            long sum=0;

            for(long x:arr)
                sum+=(x+mid-1)/mid;

            if(sum<=threshold)
            {
                ans=mid;
                high=mid-1;
            }
            else
            {
                low=mid+1;
            }
        }

        System.out.print(ans);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

threshold=int(input())

low=1
high=max(arr)
ans=high

while low<=high:

    mid=low+(high-low)//2

    total=0

    for x in arr:
        total+=(x+mid-1)//mid

    if total<=threshold:
        ans=mid
        high=mid-1
    else:
        low=mid+1

print(ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] arr=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        long threshold=long.Parse(Console.ReadLine());

        long maxi=0;

        foreach(long x in arr)
            if(x>maxi)
                maxi=x;

        long low=1;
        long high=maxi;
        long ans=maxi;

        while(low<=high)
        {
            long mid=low+(high-low)/2;
            long sum=0;

            foreach(long x in arr)
                sum+=(x+mid-1)/mid;

            if(sum<=threshold)
            {
                ans=mid;
                high=mid-1;
            }
            else
            {
                low=mid+1;
            }
        }

        Console.Write(ans);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const arr=[];

let maxi=0;

for(let i=0;i<n;i++)
{
    arr.push(input[idx]);
    maxi=Math.max(maxi,input[idx]);
    idx++;
}

const threshold=input[idx];

let low=1;
let high=maxi;
let ans=maxi;

while(low<=high)
{
    const mid=low+Math.floor((high-low)/2);

    let sum=0;

    for(const x of arr)
        sum+=Math.floor((x+mid-1)/mid);

    if(sum<=threshold)
    {
        ans=mid;
        high=mid-1;
    }
    else
    {
        low=mid+1;
    }
}

console.log(ans);
```

### Output
Input

4

1 2 5 9

6

Output

5

# Time Complexity
O(N × log(MaxElement))

# Space Complexity
O(1)

</approaches>




