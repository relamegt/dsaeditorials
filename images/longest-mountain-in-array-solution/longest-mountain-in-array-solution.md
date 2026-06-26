# Longest Mountain in Array - Solution

## Problem Statement

You may recall that an array `arr` is a mountain array if and only if:

- `arr.length >= 3`
- There exists an index `i` (`0 < i < arr.length - 1`) such that:
- `arr[0] < arr[1] < ... < arr[i]`
- `arr[i] > arr[i+1] > ... > arr[arr.length-1]`

Given an integer array `arr`, return the length of the longest mountain subarray. If there is no mountain subarray, return `0`.

## Input Format

First line: Integer `n`

Second line: `n` space-separated integers

## Output Format

Print a single integer representing the length of the longest mountain subarray.

## Explanation

There are three common approaches to solve this problem.

- **Brute Force:** Check every possible subarray to determine whether it forms a mountain.
- **Expand Around Peak:** Treat every possible peak and expand to both sides.
- **Single Traversal (Optimal):** Traverse once while counting increasing and decreasing slopes.

For example,

Input

8

2 1 4 7 3 2 5 1

Output

5

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. Consider every possible subarray of length at least `3`.
3. Check whether it first strictly increases and then strictly decreases.
4. If it is a valid mountain, update the maximum length.
5. Print the maximum length.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    int ans=0;

    for(int start=0;start<n;start++)
    {
        for(int end=start+2;end<n;end++)
        {
            int i=start;

            while(i<end && arr[i]<arr[i+1])
                i++;

            if(i==start || i==end)
                continue;

            int peak=i;

            while(i<end && arr[i]>arr[i+1])
                i++;

            if(i==end && end-start+1>ans)
                ans=end-start+1;
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

    int ans=0;

    for(int start=0;start<n;start++)
    {
        for(int end=start+2;end<n;end++)
        {
            int i=start;

            while(i<end && arr[i]<arr[i+1])
                i++;

            if(i==start || i==end)
                continue;

            while(i<end && arr[i]>arr[i+1])
                i++;

            if(i==end)
                ans=max(ans,end-start+1);
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

        int ans=0;

        for(int start=0;start<n;start++)
        {
            for(int end=start+2;end<n;end++)
            {
                int i=start;

                while(i<end && arr[i]<arr[i+1])
                    i++;

                if(i==start || i==end)
                    continue;

                while(i<end && arr[i]>arr[i+1])
                    i++;

                if(i==end)
                    ans=Math.max(ans,end-start+1);
            }
        }

        System.out.print(ans);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

ans=0

for start in range(n):

    for end in range(start+2,n):

        i=start

        while i<end and arr[i]<arr[i+1]:
            i+=1

        if i==start or i==end:
            continue

        while i<end and arr[i]>arr[i+1]:
            i+=1

        if i==end:
            ans=max(ans,end-start+1)

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

        int ans = 0;

        for(int start = 0; start < n; start++)
        {
            for(int end = start + 2; end < n; end++)
            {
                int i = start;

                while(i < end && arr[i] < arr[i + 1])
                    i++;

                if(i == start || i == end)
                    continue;

                while(i < end && arr[i] > arr[i + 1])
                    i++;

                if(i == end)
                    ans = Math.Max(ans, end - start + 1);
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

let ans = 0;

for(let start = 0; start < n; start++)
{
    for(let end = start + 2; end < n; end++)
    {
        let i = start;

        while(i < end && arr[i] < arr[i + 1])
            i++;

        if(i === start || i === end)
            continue;

        while(i < end && arr[i] > arr[i + 1])
            i++;

        if(i === end)
            ans = Math.max(ans, end - start + 1);
    }
}

console.log(ans);
```

### Output
Input

8

2 1 4 7 3 2 5 1

Output

5

# Time Complexity
O(N³)

# Space Complexity
O(1)

## Approach 2: Expand Around Peak

### Algorithm

1. Traverse every index as a possible peak.
2. A valid peak satisfies:

- `arr[i] > arr[i-1]`
- `arr[i] > arr[i+1]`

1. Expand to the left while elements are strictly increasing.
2. Expand to the right while elements are strictly decreasing.
3. Update the maximum mountain length.
4. Print the maximum length.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    int ans=0;

    for(int i=1;i<n-1;i++)
    {
        if(arr[i]>arr[i-1] && arr[i]>arr[i+1])
        {
            int left=i;
            int right=i;

            while(left>0 && arr[left]>arr[left-1])
                left--;

            while(right<n-1 && arr[right]>arr[right+1])
                right++;

            if(right-left+1>ans)
                ans=right-left+1;
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

    int ans=0;

    for(int i=1;i<n-1;i++)
    {
        if(arr[i]>arr[i-1] && arr[i]>arr[i+1])
        {
            int left=i;
            int right=i;

            while(left>0 && arr[left]>arr[left-1])
                left--;

            while(right<n-1 && arr[right]>arr[right+1])
                right++;

            ans=max(ans,right-left+1);
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

        int ans=0;

        for(int i=1;i<n-1;i++)
        {
            if(arr[i]>arr[i-1] && arr[i]>arr[i+1])
            {
                int left=i;
                int right=i;

                while(left>0 && arr[left]>arr[left-1])
                    left--;

                while(right<n-1 && arr[right]>arr[right+1])
                    right++;

                ans=Math.max(ans,right-left+1);
            }
        }

        System.out.print(ans);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

ans=0

for i in range(1,n-1):

    if arr[i]>arr[i-1] and arr[i]>arr[i+1]:

        left=i
        right=i

        while left>0 and arr[left]>arr[left-1]:
            left-=1

        while right<n-1 and arr[right]>arr[right+1]:
            right+=1

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

        int ans = 0;

        for(int i = 1; i < n - 1; i++)
        {
            if(arr[i] > arr[i - 1] && arr[i] > arr[i + 1])
            {
                int left = i;
                int right = i;

                while(left > 0 && arr[left] > arr[left - 1])
                    left--;

                while(right < n - 1 && arr[right] > arr[right + 1])
                    right++;

                ans = Math.Max(ans, right - left + 1);
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

let ans = 0;

for(let i = 1; i < n - 1; i++)
{
    if(arr[i] > arr[i - 1] && arr[i] > arr[i + 1])
    {
        let left = i;
        let right = i;

        while(left > 0 && arr[left] > arr[left - 1])
            left--;

        while(right < n - 1 && arr[right] > arr[right + 1])
            right++;

        ans = Math.max(ans, right - left + 1);
    }
}

console.log(ans);
```

### Output
Input

8

2 1 4 7 3 2 5 1

Output

5

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 3: Single Traversal (Optimal)

### Algorithm

1. Read the array.
2. Traverse the array using an index.
3. Skip flat regions where adjacent elements are equal.
4. Count the length of the increasing slope.
5. Count the length of the decreasing slope.
6. If both slopes exist, update the maximum mountain length as:

- `up + down + 1`

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

    int ans=0;
    int i=1;

    while(i<n)
    {
        int up=0;
        int down=0;

        while(i<n && arr[i]==arr[i-1])
            i++;

        while(i<n && arr[i]>arr[i-1])
        {
            up++;
            i++;
        }

        while(i<n && arr[i]<arr[i-1])
        {
            down++;
            i++;
        }

        if(up>0 && down>0 && up+down+1>ans)
            ans=up+down+1;
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

    int ans=0;
    int i=1;

    while(i<n)
    {
        int up=0;
        int down=0;

        while(i<n && arr[i]==arr[i-1])
            i++;

        while(i<n && arr[i]>arr[i-1])
        {
            up++;
            i++;
        }

        while(i<n && arr[i]<arr[i-1])
        {
            down++;
            i++;
        }

        if(up>0 && down>0)
            ans=max(ans,up+down+1);
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

        int ans=0;
        int i=1;

        while(i<n)
        {
            int up=0;
            int down=0;

            while(i<n && arr[i]==arr[i-1])
                i++;

            while(i<n && arr[i]>arr[i-1])
            {
                up++;
                i++;
            }

            while(i<n && arr[i]<arr[i-1])
            {
                down++;
                i++;
            }

            if(up>0 && down>0)
                ans=Math.max(ans,up+down+1);
        }

        System.out.print(ans);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

ans=0
i=1

while i<n:

    up=0
    down=0

    while i<n and arr[i]==arr[i-1]:
        i+=1

    while i<n and arr[i]>arr[i-1]:
        up+=1
        i+=1

    while i<n and arr[i]<arr[i-1]:
        down+=1
        i+=1

    if up>0 and down>0:
        ans=max(ans,up+down+1)

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

        int ans = 0;
        int i = 1;

        while(i < n)
        {
            int up = 0;
            int down = 0;

            while(i < n && arr[i] == arr[i - 1])
                i++;

            while(i < n && arr[i] > arr[i - 1])
            {
                up++;
                i++;
            }

            while(i < n && arr[i] < arr[i - 1])
            {
                down++;
                i++;
            }

            if(up > 0 && down > 0)
                ans = Math.Max(ans, up + down + 1);
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

let ans = 0;
let i = 1;

while(i < n)
{
    let up = 0;
    let down = 0;

    while(i < n && arr[i] === arr[i - 1])
        i++;

    while(i < n && arr[i] > arr[i - 1])
    {
        up++;
        i++;
    }

    while(i < n && arr[i] < arr[i - 1])
    {
        down++;
        i++;
    }

    if(up > 0 && down > 0)
        ans = Math.max(ans, up + down + 1);
}

console.log(ans);
```

### Output
Input

8

2 1 4 7 3 2 5 1

Output

5

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




