# Aggressive Cows - Solution

## Problem Statement

You are given `N` stall positions along a straight line and an integer `C` representing the number of cows. Place the cows in the stalls such that the minimum distance between any two placed cows is as large as possible.

Find and print this largest possible minimum distance.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing stall positions.

Third line: Integer `C`

## Output Format

Print a single integer representing the largest possible minimum distance.

## Explanation

There are two approaches to solve this problem.

- **Approach 1:** Linear Search
- **Approach 2:** Binary Search (Optimal)

For example,

Input

5

1 2 4 8 9

3

Output

3

<approaches>
## Approach 1: Linear Search

### Algorithm

1. Read the stall positions and sort them.
2. Find the maximum possible minimum distance (`last stall - first stall`).
3. Try every distance from `1` to the maximum distance.
4. For each distance, greedily place cows in the stalls.
5. If all `C` cows can be placed, update the answer.
6. Print the largest valid distance.

```C
#include <stdio.h>
#include <stdlib.h>

int cmp(const void *a,const void *b)
{
    return (*(int *)a-*(int *)b);
}

int main()
{
    int n;
    scanf("%d",&n);

    int stalls[n];

    for(int i=0;i<n;i++)
        scanf("%d",&stalls[i]);

    int c;
    scanf("%d",&c);

    qsort(stalls,n,sizeof(int),cmp);

    int ans=0;
    int maxDist=stalls[n-1]-stalls[0];

    for(int dist=1;dist<=maxDist;dist++)
    {
        int cows=1;
        int last=stalls[0];

        for(int i=1;i<n;i++)
        {
            if(stalls[i]-last>=dist)
            {
                cows++;
                last=stalls[i];
            }
        }

        if(cows>=c)
            ans=dist;
    }

    printf("%d",ans);

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

    vector<int> stalls(n);

    for(int i=0;i<n;i++)
        cin>>stalls[i];

    int c;
    cin>>c;

    sort(stalls.begin(),stalls.end());

    int ans=0;
    int maxDist=stalls.back()-stalls.front();

    for(int dist=1;dist<=maxDist;dist++)
    {
        int cows=1;
        int last=stalls[0];

        for(int i=1;i<n;i++)
        {
            if(stalls[i]-last>=dist)
            {
                cows++;
                last=stalls[i];
            }
        }

        if(cows>=c)
            ans=dist;
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

        int[] stalls=new int[n];

        for(int i=0;i<n;i++)
            stalls[i]=sc.nextInt();

        int c=sc.nextInt();

        Arrays.sort(stalls);

        int ans=0;
        int maxDist=stalls[n-1]-stalls[0];

        for(int dist=1;dist<=maxDist;dist++)
        {
            int cows=1;
            int last=stalls[0];

            for(int i=1;i<n;i++)
            {
                if(stalls[i]-last>=dist)
                {
                    cows++;
                    last=stalls[i];
                }
            }

            if(cows>=c)
                ans=dist;
        }

        System.out.print(ans);
    }
}
```
```Python
n=int(input())

stalls=list(map(int,input().split()))

c=int(input())

stalls.sort()

ans=0

maxDist=stalls[-1]-stalls[0]

for dist in range(1,maxDist+1):

    cows=1
    last=stalls[0]

    for i in range(1,n):

        if stalls[i]-last>=dist:
            cows+=1
            last=stalls[i]

    if cows>=c:
        ans=dist

print(ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        int[] stalls=Array.ConvertAll(Console.ReadLine().Split(),int.Parse);

        int c=int.Parse(Console.ReadLine());

        Array.Sort(stalls);

        int ans=0;
        int maxDist=stalls[n-1]-stalls[0];

        for(int dist=1;dist<=maxDist;dist++)
        {
            int cows=1;
            int last=stalls[0];

            for(int i=1;i<n;i++)
            {
                if(stalls[i]-last>=dist)
                {
                    cows++;
                    last=stalls[i];
                }
            }

            if(cows>=c)
                ans=dist;
        }

        Console.Write(ans);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const stalls=[];

for(let i=0;i<n;i++)
    stalls.push(input[idx++]);

const c=input[idx];

stalls.sort((a,b)=>a-b);

let ans=0;

const maxDist=stalls[n-1]-stalls[0];

for(let dist=1;dist<=maxDist;dist++)
{
    let cows=1;
    let last=stalls[0];

    for(let i=1;i<n;i++)
    {
        if(stalls[i]-last>=dist)
        {
            cows++;
            last=stalls[i];
        }
    }

    if(cows>=c)
        ans=dist;
}

console.log(ans);
```

### Output
Input

5

1 2 4 8 9

3

Output

3

# Time Complexity
O(N log N + N × MaxDistance)

# Space Complexity
O(1)

## Approach 2: Binary Search (Optimal)

### Algorithm

1. Read the stall positions and sort them.
2. Set `low = 1` and `high = last stall - first stall`.
3. While `low <= high`:

- Find `mid` as the candidate minimum distance.
- Greedily place cows while maintaining at least `mid` distance.
- If all cows can be placed, store the answer and search for a larger distance.
- Otherwise, search for a smaller distance.

```C
#include <stdio.h>
#include <stdlib.h>

int cmp(const void *a,const void *b)
{
    return (*(int *)a-*(int *)b);
}

int main()
{
    int n;
    scanf("%d",&n);

    int stalls[n];

    for(int i=0;i<n;i++)
        scanf("%d",&stalls[i]);

    int c;
    scanf("%d",&c);

    qsort(stalls,n,sizeof(int),cmp);

    int low=1;
    int high=stalls[n-1]-stalls[0];
    int ans=0;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        int cows=1;
        int last=stalls[0];

        for(int i=1;i<n;i++)
        {
            if(stalls[i]-last>=mid)
            {
                cows++;
                last=stalls[i];
            }
        }

        if(cows>=c)
        {
            ans=mid;
            low=mid+1;
        }
        else
        {
            high=mid-1;
        }
    }

    printf("%d",ans);

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

    vector<int> stalls(n);

    for(int i=0;i<n;i++)
        cin>>stalls[i];

    int c;
    cin>>c;

    sort(stalls.begin(),stalls.end());

    int low=1;
    int high=stalls.back()-stalls.front();
    int ans=0;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        int cows=1;
        int last=stalls[0];

        for(int i=1;i<n;i++)
        {
            if(stalls[i]-last>=mid)
            {
                cows++;
                last=stalls[i];
            }
        }

        if(cows>=c)
        {
            ans=mid;
            low=mid+1;
        }
        else
        {
            high=mid-1;
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

        int[] stalls=new int[n];

        for(int i=0;i<n;i++)
            stalls[i]=sc.nextInt();

        int c=sc.nextInt();

        Arrays.sort(stalls);

        int low=1;
        int high=stalls[n-1]-stalls[0];
        int ans=0;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            int cows=1;
            int last=stalls[0];

            for(int i=1;i<n;i++)
            {
                if(stalls[i]-last>=mid)
                {
                    cows++;
                    last=stalls[i];
                }
            }

            if(cows>=c)
            {
                ans=mid;
                low=mid+1;
            }
            else
            {
                high=mid-1;
            }
        }

        System.out.print(ans);
    }
}
```
```Python
n = int(input())

stalls = list(map(int, input().split()))

c = int(input())

stalls.sort()

low = 1
high = stalls[-1] - stalls[0]

ans = 0

while low <= high:

    mid = low + (high - low) // 2

    cows = 1
    last = stalls[0]

    for i in range(1, n):

        if stalls[i] - last >= mid:
            cows += 1
            last = stalls[i]

    if cows >= c:
        ans = mid
        low = mid + 1
    else:
        high = mid - 1

print(ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] stalls = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int c = int.Parse(Console.ReadLine());

        Array.Sort(stalls);

        int low = 1;
        int high = stalls[n - 1] - stalls[0];
        int ans = 0;

        while (low <= high)
        {
            int mid = low + (high - low) / 2;

            int cows = 1;
            int last = stalls[0];

            for (int i = 1; i < n; i++)
            {
                if (stalls[i] - last >= mid)
                {
                    cows++;
                    last = stalls[i];
                }
            }

            if (cows >= c)
            {
                ans = mid;
                low = mid + 1;
            }
            else
            {
                high = mid - 1;
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

const stalls = [];

for (let i = 0; i < n; i++)
    stalls.push(input[idx++]);

const c = input[idx];

stalls.sort((a, b) => a - b);

let low = 1;
let high = stalls[n - 1] - stalls[0];
let ans = 0;

while (low <= high)
{
    const mid = low + Math.floor((high - low) / 2);

    let cows = 1;
    let last = stalls[0];

    for (let i = 1; i < n; i++)
    {
        if (stalls[i] - last >= mid)
        {
            cows++;
            last = stalls[i];
        }
    }

    if (cows >= c)
    {
        ans = mid;
        low = mid + 1;
    }
    else
    {
        high = mid - 1;
    }
}

console.log(ans);
```

### Output
Input

5

1 2 4 8 9

3

Output

3

# Time Complexity
O(N log N + N log(MaxDistance))

# Space Complexity
O(1)

</approaches>




