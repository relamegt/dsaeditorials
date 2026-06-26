# Max Consecutive Ones after flipping 0's - Solution

## Problem Statement

Given a binary array `nums` and an integer `k`, return the maximum number of consecutive `1`s in the array if you can flip at most `k` `0`s to `1`s.

## Input Format

First line: Integer `n`

Second line: `n` space-separated integers (`0`s and `1`s)

Third line: Integer `k`

## Output Format

Print a single integer representing the maximum number of consecutive `1`s after flipping at most `k` zeros.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Consider every possible starting index and extend the subarray while counting flipped zeros.
- **Sliding Window (Optimal):** Maintain a window containing at most `k` zeros and maximize its length.

For example,

Input

6

1 1 1 0 0 1

2

Output

6

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array and value `k`.
2. For every starting index:

- Initialize `zeroCount = 0`.
- Extend the subarray to the right.
- Increment `zeroCount` whenever a `0` is encountered.
- Stop when `zeroCount` becomes greater than `k`.
- Update the maximum window length.

1. Print the maximum length.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    int k;
    scanf("%d",&k);

    int ans=0;

    for(int i=0;i<n;i++)
    {
        int zeros=0;

        for(int j=i;j<n;j++)
        {
            if(arr[j]==0)
                zeros++;

            if(zeros>k)
                break;

            if(j-i+1>ans)
                ans=j-i+1;
        }
    }

    printf("%d",ans);

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

    vector<int> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    int k;
    cin>>k;

    int ans=0;

    for(int i=0;i<n;i++)
    {
        int zeros=0;

        for(int j=i;j<n;j++)
        {
            if(arr[j]==0)
                zeros++;

            if(zeros>k)
                break;

            ans=max(ans,j-i+1);
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

        int[] arr=new int[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextInt();

        int k=sc.nextInt();

        int ans=0;

        for(int i=0;i<n;i++)
        {
            int zeros=0;

            for(int j=i;j<n;j++)
            {
                if(arr[j]==0)
                    zeros++;

                if(zeros>k)
                    break;

                ans=Math.max(ans,j-i+1);
            }
        }

        System.out.print(ans);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

k=int(input())

ans=0

for i in range(n):

    zeros=0

    for j in range(i,n):

        if arr[j]==0:
            zeros+=1

        if zeros>k:
            break

        ans=max(ans,j-i+1)

print(ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int k = int.Parse(Console.ReadLine());

        int ans = 0;

        for(int i = 0; i < n; i++)
        {
            int zeros = 0;

            for(int j = i; j < n; j++)
            {
                if(arr[j] == 0)
                    zeros++;

                if(zeros > k)
                    break;

                ans = Math.Max(ans, j - i + 1);
            }
        }

        Console.Write(ans);
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

const k = input[idx++];

let ans = 0;

for(let i = 0; i < n; i++)
{
    let zeros = 0;

    for(let j = i; j < n; j++)
    {
        if(arr[j] === 0)
            zeros++;

        if(zeros > k)
            break;

        ans = Math.max(ans, j - i + 1);
    }
}

console.log(ans);
```

### Output
Input

6

1 1 1 0 0 1

2

Output

6

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Sliding Window (Optimal)

### Algorithm

1. Read the array and value `k`.
2. Initialize two pointers `left` and `right`.
3. Expand the window by moving `right`.
4. Count the number of zeros in the current window.
5. If the number of zeros exceeds `k`, move `left` until the window again contains at most `k` zeros.
6. Update the maximum window length after each expansion.
7. Print the maximum length.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    int k;
    scanf("%d",&k);

    int left=0;
    int zeros=0;
    int ans=0;

    for(int right=0;right<n;right++)
    {
        if(arr[right]==0)
            zeros++;

        while(zeros>k)
        {
            if(arr[left]==0)
                zeros--;

            left++;
        }

        if(right-left+1>ans)
            ans=right-left+1;
    }

    printf("%d",ans);

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

    vector<int> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    int k;
    cin>>k;

    int left=0;
    int zeros=0;
    int ans=0;

    for(int right=0;right<n;right++)
    {
        if(arr[right]==0)
            zeros++;

        while(zeros>k)
        {
            if(arr[left]==0)
                zeros--;

            left++;
        }

        ans=max(ans,right-left+1);
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

        int[] arr=new int[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextInt();

        int k=sc.nextInt();

        int left=0;
        int zeros=0;
        int ans=0;

        for(int right=0;right<n;right++)
        {
            if(arr[right]==0)
                zeros++;

            while(zeros>k)
            {
                if(arr[left]==0)
                    zeros--;

                left++;
            }

            ans=Math.max(ans,right-left+1);
        }

        System.out.print(ans);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

k=int(input())

left=0
zeros=0
ans=0

for right in range(n):

    if arr[right]==0:
        zeros+=1

    while zeros>k:

        if arr[left]==0:
            zeros-=1

        left+=1

    ans=max(ans,right-left+1)

print(ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int k = int.Parse(Console.ReadLine());

        int left = 0;
        int zeros = 0;
        int ans = 0;

        for(int right = 0; right < n; right++)
        {
            if(arr[right] == 0)
                zeros++;

            while(zeros > k)
            {
                if(arr[left] == 0)
                    zeros--;

                left++;
            }

            ans = Math.Max(ans, right - left + 1);
        }

        Console.Write(ans);
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

const k = input[idx++];

let left = 0;
let zeros = 0;
let ans = 0;

for(let right = 0; right < n; right++)
{
    if(arr[right] === 0)
        zeros++;

    while(zeros > k)
    {
        if(arr[left] === 0)
            zeros--;

        left++;
    }

    ans = Math.max(ans, right - left + 1);
}

console.log(ans);
```

### Output
Input

6

1 1 1 0 0 1

2

Output

6

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




