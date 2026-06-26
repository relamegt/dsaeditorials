# Minimum Number of Days to Make M Bouquets - Solution

## Problem Statement

You are given an array `bloomDay` of size `N`, where `bloomDay[i]` is the day on which the `i`th flower blooms. You are also given two integers `M` and `K`.

You need to make exactly `M` bouquets. To make one bouquet, you must use `K` adjacent flowers that have all bloomed by the same day. Each flower can be used in at most one bouquet.

Find and print the minimum number of days needed to make `M` bouquets. If it is not possible, print `-1`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing `bloomDay`

Third line: Integer `M`

Fourth line: Integer `K`

## Output Format

Print a single integer representing the minimum number of days, or `-1` if it is not possible.

## Explanation

There are two approaches to solve this problem.

- **Approach 1:** Linear Search
- **Approach 2:** Binary Search (Optimal)

For example,

Input

5

1 10 3 10 2

3

1

Output

3

<approaches>
## Approach 1: Linear Search

### Algorithm

1. If `M × K > N`, print `-1`.
2. Find the maximum bloom day.
3. Try every day from `1` to the maximum bloom day.
4. For each day, count how many bouquets can be formed using adjacent bloomed flowers.
5. The first day on which at least `M` bouquets can be made is the answer.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long bloom[n];
    long long maxi=0;

    for(int i=0;i<n;i++)
    {
        scanf("%lld",&bloom[i]);

        if(bloom[i]>maxi)
            maxi=bloom[i];
    }

    long long m,k;
    scanf("%lld%lld",&m,&k);

    if(m*k>n)
    {
        printf("-1");
        return 0;
    }

    for(long long day=1;day<=maxi;day++)
    {
        long long bouquets=0;
        long long flowers=0;

        for(int i=0;i<n;i++)
        {
            if(bloom[i]<=day)
            {
                flowers++;

                if(flowers==k)
                {
                    bouquets++;
                    flowers=0;
                }
            }
            else
            {
                flowers=0;
            }
        }

        if(bouquets>=m)
        {
            printf("%lld",day);
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

    vector<long long> bloom(n);

    long long maxi=0;

    for(int i=0;i<n;i++)
    {
        cin>>bloom[i];
        maxi=max(maxi,bloom[i]);
    }

    long long m,k;
    cin>>m>>k;

    if(m*k>n)
    {
        cout<<-1;
        return 0;
    }

    for(long long day=1;day<=maxi;day++)
    {
        long long bouquets=0;
        long long flowers=0;

        for(long long x:bloom)
        {
            if(x<=day)
            {
                flowers++;

                if(flowers==k)
                {
                    bouquets++;
                    flowers=0;
                }
            }
            else
            {
                flowers=0;
            }
        }

        if(bouquets>=m)
        {
            cout<<day;
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

        long[] bloom=new long[n];

        long maxi=0;

        for(int i=0;i<n;i++)
        {
            bloom[i]=sc.nextLong();
            maxi=Math.max(maxi,bloom[i]);
        }

        long m=sc.nextLong();
        long k=sc.nextLong();

        if(m*k>n)
        {
            System.out.print(-1);
            return;
        }

        for(long day=1;day<=maxi;day++)
        {
            long bouquets=0;
            long flowers=0;

            for(long x:bloom)
            {
                if(x<=day)
                {
                    flowers++;

                    if(flowers==k)
                    {
                        bouquets++;
                        flowers=0;
                    }
                }
                else
                {
                    flowers=0;
                }
            }

            if(bouquets>=m)
            {
                System.out.print(day);
                return;
            }
        }
    }
}
```
```Python
n=int(input())

bloom=list(map(int,input().split()))

m=int(input())
k=int(input())

if m*k>n:
    print(-1)
    exit()

maxi=max(bloom)

for day in range(1,maxi+1):

    bouquets=0
    flowers=0

    for x in bloom:

        if x<=day:
            flowers+=1

            if flowers==k:
                bouquets+=1
                flowers=0
        else:
            flowers=0

    if bouquets>=m:
        print(day)
        exit()
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] bloom=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        long m=long.Parse(Console.ReadLine());
        long k=long.Parse(Console.ReadLine());

        if(m*k>n)
        {
            Console.Write(-1);
            return;
        }

        long maxi=0;

        foreach(long x in bloom)
            if(x>maxi)
                maxi=x;

        for(long day=1;day<=maxi;day++)
        {
            long bouquets=0;
            long flowers=0;

            foreach(long x in bloom)
            {
                if(x<=day)
                {
                    flowers++;

                    if(flowers==k)
                    {
                        bouquets++;
                        flowers=0;
                    }
                }
                else
                {
                    flowers=0;
                }
            }

            if(bouquets>=m)
            {
                Console.Write(day);
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

const bloom=[];

let maxi=0;

for(let i=0;i<n;i++)
{
    bloom.push(input[idx]);
    maxi=Math.max(maxi,input[idx]);
    idx++;
}

const m=input[idx++];
const k=input[idx];

if(m*k>n)
{
    console.log(-1);
    return;
}

for(let day=1;day<=maxi;day++)
{
    let bouquets=0;
    let flowers=0;

    for(const x of bloom)
    {
        if(x<=day)
        {
            flowers++;

            if(flowers===k)
            {
                bouquets++;
                flowers=0;
            }
        }
        else
        {
            flowers=0;
        }
    }

    if(bouquets>=m)
    {
        console.log(day);
        return;
    }
}
```

### Output
Input

5

1 10 3 10 2

3

1

Output

3

# Time Complexity
O(N × MaxBloomDay)

# Space Complexity
O(1)

## Approach 2: Binary Search (Optimal)

### Algorithm

1. If `M × K > N`, print `-1`.
2. Find the minimum and maximum bloom day.
3. Initialize `low = minimum bloom day` and `high = maximum bloom day`.
4. While `low <= high`:

- Find the middle day.
- Count how many bouquets can be formed by that day.
- If at least `M` bouquets can be made, store the answer and search for a smaller day.
- Otherwise, search for a larger day.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long bloom[n];
    long long mini=1000000000000000000LL;
    long long maxi=0;

    for(int i=0;i<n;i++)
    {
        scanf("%lld",&bloom[i]);

        if(bloom[i]<mini)
            mini=bloom[i];

        if(bloom[i]>maxi)
            maxi=bloom[i];
    }

    long long m,k;
    scanf("%lld%lld",&m,&k);

    if(m*k>n)
    {
        printf("-1");
        return 0;
    }

    long long low=mini;
    long long high=maxi;
    long long ans=maxi;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;

        long long bouquets=0;
        long long flowers=0;

        for(int i=0;i<n;i++)
        {
            if(bloom[i]<=mid)
            {
                flowers++;

                if(flowers==k)
                {
                    bouquets++;
                    flowers=0;
                }
            }
            else
            {
                flowers=0;
            }
        }

        if(bouquets>=m)
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

    vector<long long> bloom(n);

    long long mini=1000000000000000000LL;
    long long maxi=0;

    for(int i=0;i<n;i++)
    {
        cin>>bloom[i];
        mini=min(mini,bloom[i]);
        maxi=max(maxi,bloom[i]);
    }

    long long m,k;
    cin>>m>>k;

    if(m*k>n)
    {
        cout<<-1;
        return 0;
    }

    long long low=mini;
    long long high=maxi;
    long long ans=maxi;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;

        long long bouquets=0;
        long long flowers=0;

        for(long long x:bloom)
        {
            if(x<=mid)
            {
                flowers++;

                if(flowers==k)
                {
                    bouquets++;
                    flowers=0;
                }
            }
            else
            {
                flowers=0;
            }
        }

        if(bouquets>=m)
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

        long[] bloom=new long[n];

        long mini=Long.MAX_VALUE;
        long maxi=0;

        for(int i=0;i<n;i++)
        {
            bloom[i]=sc.nextLong();
            mini=Math.min(mini,bloom[i]);
            maxi=Math.max(maxi,bloom[i]);
        }

        long m=sc.nextLong();
        long k=sc.nextLong();

        if(m*k>n)
        {
            System.out.print(-1);
            return;
        }

        long low=mini;
        long high=maxi;
        long ans=maxi;

        while(low<=high)
        {
            long mid=low+(high-low)/2;

            long bouquets=0;
            long flowers=0;

            for(long x:bloom)
            {
                if(x<=mid)
                {
                    flowers++;

                    if(flowers==k)
                    {
                        bouquets++;
                        flowers=0;
                    }
                }
                else
                {
                    flowers=0;
                }
            }

            if(bouquets>=m)
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

bloom=list(map(int,input().split()))

m=int(input())
k=int(input())

if m*k>n:
    print(-1)
    exit()

low=min(bloom)
high=max(bloom)

ans=high

while low<=high:

    mid=low+(high-low)//2

    bouquets=0
    flowers=0

    for x in bloom:

        if x<=mid:
            flowers+=1

            if flowers==k:
                bouquets+=1
                flowers=0
        else:
            flowers=0

    if bouquets>=m:
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

        long[] bloom=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        long m=long.Parse(Console.ReadLine());
        long k=long.Parse(Console.ReadLine());

        if(m*k>n)
        {
            Console.Write(-1);
            return;
        }

        long mini=long.MaxValue;
        long maxi=0;

        foreach(long x in bloom)
        {
            if(x<mini)
                mini=x;

            if(x>maxi)
                maxi=x;
        }

        long low=mini;
        long high=maxi;
        long ans=maxi;

        while(low<=high)
        {
            long mid=low+(high-low)/2;

            long bouquets=0;
            long flowers=0;

            foreach(long x in bloom)
            {
                if(x<=mid)
                {
                    flowers++;

                    if(flowers==k)
                    {
                        bouquets++;
                        flowers=0;
                    }
                }
                else
                {
                    flowers=0;
                }
            }

            if(bouquets>=m)
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

const bloom=[];

let mini=Number.MAX_SAFE_INTEGER;
let maxi=0;

for(let i=0;i<n;i++)
{
    bloom.push(input[idx]);
    mini=Math.min(mini,input[idx]);
    maxi=Math.max(maxi,input[idx]);
    idx++;
}

const m=input[idx++];
const k=input[idx];

if(m*k>n)
{
    console.log(-1);
    return;
}

let low=mini;
let high=maxi;
let ans=maxi;

while(low<=high)
{
    const mid=low+Math.floor((high-low)/2);

    let bouquets=0;
    let flowers=0;

    for(const x of bloom)
    {
        if(x<=mid)
        {
            flowers++;

            if(flowers===k)
            {
                bouquets++;
                flowers=0;
            }
        }
        else
        {
            flowers=0;
        }
    }

    if(bouquets>=m)
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

5

1 10 3 10 2

3

1

Output

3

# Time Complexity
O(N × log(MaxBloomDay))

# Space Complexity
O(1)

</approaches>




