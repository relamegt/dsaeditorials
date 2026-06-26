# Painter's Partition Problem - Solution

## Problem Statement

You are given an array `boards` of size `N`, where `boards[i]` represents the length of the `i`th board. You are also given an integer `K` representing the number of painters.

Each painter paints contiguous boards only, and each board must be painted by exactly one painter. Assume one unit length of board takes one unit of time to paint.

Find and print the minimum time required to paint all boards.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing the boards array.

Third line: Integer `K`

## Output Format

Print a single integer representing the minimum time required.

## Explanation

There are two approaches to solve this problem.

- **Approach 1:** Linear Search
- **Approach 2:** Binary Search (Optimal)

For example,

Input

4

10 20 30 40

2

Output

60

<approaches>
## Approach 1: Linear Search

### Algorithm

1. Find the maximum board length and the total sum of board lengths.
2. Try every possible answer from `maximum board length` to `total sum`.
3. For each value, allocate boards greedily while keeping the total length assigned to a painter within the current limit.
4. The first valid value is the answer.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long boards[n];
    long long low=0,high=0;

    for(int i=0;i<n;i++)
    {
        scanf("%lld",&boards[i]);

        if(boards[i]>low)
            low=boards[i];

        high+=boards[i];
    }

    int k;
    scanf("%d",&k);

    for(long long limit=low;limit<=high;limit++)
    {
        int painters=1;
        long long sum=0;

        for(int i=0;i<n;i++)
        {
            if(sum+boards[i]<=limit)
                sum+=boards[i];
            else
            {
                painters++;
                sum=boards[i];
            }
        }

        if(painters<=k)
        {
            printf("%lld",limit);
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

    vector<long long> boards(n);

    long long low=0,high=0;

    for(int i=0;i<n;i++)
    {
        cin>>boards[i];
        low=max(low,boards[i]);
        high+=boards[i];
    }

    int k;
    cin>>k;

    for(long long limit=low;limit<=high;limit++)
    {
        int painters=1;
        long long sum=0;

        for(long long x:boards)
        {
            if(sum+x<=limit)
                sum+=x;
            else
            {
                painters++;
                sum=x;
            }
        }

        if(painters<=k)
        {
            cout<<limit;
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

        long[] boards=new long[n];

        long low=0,high=0;

        for(int i=0;i<n;i++)
        {
            boards[i]=sc.nextLong();
            low=Math.max(low,boards[i]);
            high+=boards[i];
        }

        int k=sc.nextInt();

        for(long limit=low;limit<=high;limit++)
        {
            int painters=1;
            long sum=0;

            for(long x:boards)
            {
                if(sum+x<=limit)
                    sum+=x;
                else
                {
                    painters++;
                    sum=x;
                }
            }

            if(painters<=k)
            {
                System.out.print(limit);
                return;
            }
        }
    }
}
```
```Python
n=int(input())

boards=list(map(int,input().split()))

k=int(input())

low=max(boards)
high=sum(boards)

for limit in range(low,high+1):

    painters=1
    total=0

    for x in boards:

        if total+x<=limit:
            total+=x
        else:
            painters+=1
            total=x

    if painters<=k:
        print(limit)
        break
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] boards=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        int k=int.Parse(Console.ReadLine());

        long low=0;
        long high=0;

        foreach(long x in boards)
        {
            if(x>low)
                low=x;

            high+=x;
        }

        for(long limit=low;limit<=high;limit++)
        {
            int painters=1;
            long sum=0;

            foreach(long x in boards)
            {
                if(sum+x<=limit)
                    sum+=x;
                else
                {
                    painters++;
                    sum=x;
                }
            }

            if(painters<=k)
            {
                Console.Write(limit);
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

const boards=[];

let low=0;
let high=0;

for(let i=0;i<n;i++)
{
    boards.push(input[idx]);
    low=Math.max(low,input[idx]);
    high+=input[idx];
    idx++;
}

const k=input[idx];

for(let limit=low;limit<=high;limit++)
{
    let painters=1;
    let sum=0;

    for(const x of boards)
    {
        if(sum+x<=limit)
            sum+=x;
        else
        {
            painters++;
            sum=x;
        }
    }

    if(painters<=k)
    {
        console.log(limit);
        return;
    }
}
```

### Output
Input

4

10 20 30 40

2

Output

60

# Time Complexity
O(N × TotalBoardLength)

# Space Complexity
O(1)

## Approach 2: Binary Search (Optimal)

### Algorithm

1. Find the maximum board length and the total length of all boards.
2. Initialize `low` as the maximum board length and `high` as the total board length.
3. While `low <= high`:

- Compute `mid`.
- Allocate boards greedily so that no painter paints more than `mid` units.
- If the required painters are less than or equal to `K`, store the answer and search for a smaller value.
- Otherwise, search for a larger value.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long boards[n];
    long long low=0,high=0;

    for(int i=0;i<n;i++)
    {
        scanf("%lld",&boards[i]);

        if(boards[i]>low)
            low=boards[i];

        high+=boards[i];
    }

    int k;
    scanf("%d",&k);

    long long ans=high;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;

        int painters=1;
        long long sum=0;

        for(int i=0;i<n;i++)
        {
            if(sum+boards[i]<=mid)
                sum+=boards[i];
            else
            {
                painters++;
                sum=boards[i];
            }
        }

        if(painters<=k)
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

    vector<long long> boards(n);

    long long low=0,high=0;

    for(int i=0;i<n;i++)
    {
        cin>>boards[i];
        low=max(low,boards[i]);
        high+=boards[i];
    }

    int k;
    cin>>k;

    long long ans=high;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;

        int painters=1;
        long long sum=0;

        for(long long x:boards)
        {
            if(sum+x<=mid)
                sum+=x;
            else
            {
                painters++;
                sum=x;
            }
        }

        if(painters<=k)
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

        long[] boards=new long[n];

        long low=0,high=0;

        for(int i=0;i<n;i++)
        {
            boards[i]=sc.nextLong();
            low=Math.max(low,boards[i]);
            high+=boards[i];
        }

        int k=sc.nextInt();

        long ans=high;

        while(low<=high)
        {
            long mid=low+(high-low)/2;

            int painters=1;
            long sum=0;

            for(long x:boards)
            {
                if(sum+x<=mid)
                    sum+=x;
                else
                {
                    painters++;
                    sum=x;
                }
            }

            if(painters<=k)
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

boards=list(map(int,input().split()))

k=int(input())

low=max(boards)
high=sum(boards)

ans=high

while low<=high:

    mid=low+(high-low)//2

    painters=1
    total=0

    for x in boards:

        if total+x<=mid:
            total+=x
        else:
            painters+=1
            total=x

    if painters<=k:
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

        long[] boards=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        int k=int.Parse(Console.ReadLine());

        long low=0;
        long high=0;

        foreach(long x in boards)
        {
            if(x>low)
                low=x;

            high+=x;
        }

        long ans=high;

        while(low<=high)
        {
            long mid=low+(high-low)/2;

            int painters=1;
            long sum=0;

            foreach(long x in boards)
            {
                if(sum+x<=mid)
                    sum+=x;
                else
                {
                    painters++;
                    sum=x;
                }
            }

            if(painters<=k)
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

const boards=[];

let low=0;
let high=0;

for(let i=0;i<n;i++)
{
    boards.push(input[idx]);
    low=Math.max(low,input[idx]);
    high+=input[idx];
    idx++;
}

const k=input[idx];

let ans=high;

while(low<=high)
{
    const mid=low+Math.floor((high-low)/2);

    let painters=1;
    let sum=0;

    for(const x of boards)
    {
        if(sum+x<=mid)
            sum+=x;
        else
        {
            painters++;
            sum=x;
        }
    }

    if(painters<=k)
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

10 20 30 40

2

Output

60

# Time Complexity
O(N × log(TotalBoardLength))

# Space Complexity
O(1)

</approaches>




