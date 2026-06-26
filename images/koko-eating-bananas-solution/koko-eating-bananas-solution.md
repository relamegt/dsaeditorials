# Koko Eating Bananas - Solution

## Problem Statement

Koko has `N` piles of bananas. The `i`th pile has `piles[i]` bananas. The guards will return after `H` hours.

Koko can decide her eating speed `K` bananas per hour. In one hour, she chooses one pile and eats up to `K` bananas from that pile. If the pile has fewer than `K` bananas, she eats all bananas in that pile during that hour.

Find and print the minimum integer `K` such that Koko can eat all the bananas within `H` hours.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing the piles

Third line: Integer `H`

## Output Format

Print a single integer representing the minimum eating speed.

## Explanation

There are two approaches to solve this problem.

- **Approach 1:** Linear Search
- **Approach 2:** Binary Search (Optimal)

For example,

Input

4

3 6 7 11

8

Output

4

<approaches>
## Approach 1: Linear Search

### Algorithm

1. Read the array and `H`.
2. Find the maximum pile size.
3. Try every eating speed from `1` to the maximum pile size.
4. For each speed, calculate the total hours required.
5. The first speed requiring at most `H` hours is the answer.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long piles[n];
    long long maxi=0;

    for(int i=0;i<n;i++)
    {
        scanf("%lld",&piles[i]);

        if(piles[i]>maxi)
            maxi=piles[i];
    }

    long long h;
    scanf("%lld",&h);

    for(long long k=1;k<=maxi;k++)
    {
        long long hours=0;

        for(int i=0;i<n;i++)
            hours+=(piles[i]+k-1)/k;

        if(hours<=h)
        {
            printf("%lld",k);
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

    vector<long long> piles(n);

    long long maxi=0;

    for(int i=0;i<n;i++)
    {
        cin>>piles[i];
        maxi=max(maxi,piles[i]);
    }

    long long h;
    cin>>h;

    for(long long k=1;k<=maxi;k++)
    {
        long long hours=0;

        for(long long x:piles)
            hours+=(x+k-1)/k;

        if(hours<=h)
        {
            cout<<k;
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

        long[] piles=new long[n];

        long maxi=0;

        for(int i=0;i<n;i++)
        {
            piles[i]=sc.nextLong();
            maxi=Math.max(maxi,piles[i]);
        }

        long h=sc.nextLong();

        for(long k=1;k<=maxi;k++)
        {
            long hours=0;

            for(long x:piles)
                hours+=(x+k-1)/k;

            if(hours<=h)
            {
                System.out.print(k);
                return;
            }
        }
    }
}
```
```Python
n=int(input())

piles=list(map(int,input().split()))

h=int(input())

maxi=max(piles)

for k in range(1,maxi+1):

    hours=0

    for x in piles:
        hours+=(x+k-1)//k

    if hours<=h:
        print(k)
        break
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] piles=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        long h=long.Parse(Console.ReadLine());

        long maxi=0;

        foreach(long x in piles)
            if(x>maxi)
                maxi=x;

        for(long k=1;k<=maxi;k++)
        {
            long hours=0;

            foreach(long x in piles)
                hours+=(x+k-1)/k;

            if(hours<=h)
            {
                Console.Write(k);
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

const piles=[];

let maxi=0;

for(let i=0;i<n;i++)
{
    piles.push(input[idx]);
    maxi=Math.max(maxi,input[idx]);
    idx++;
}

const h=input[idx];

for(let k=1;k<=maxi;k++)
{
    let hours=0;

    for(const x of piles)
        hours+=Math.floor((x+k-1)/k);

    if(hours<=h)
    {
        console.log(k);
        return;
    }
}
```

### Output
Input

4

3 6 7 11

8

Output

4

# Time Complexity
O(N × MaxPile)

# Space Complexity
O(1)

## Approach 2: Binary Search (Optimal)

### Algorithm

1. Read the array and `H`.
2. Find the maximum pile size.
3. Initialize `low = 1` and `high = maximum pile size`.
4. While `low <= high`:

- Compute the middle eating speed.
- Calculate the total hours required at this speed.
- If the total hours are less than or equal to `H`, store the answer and search for a smaller speed.
- Otherwise, search for a larger speed.

1. Print the minimum valid eating speed.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long piles[n];
    long long maxi=0;

    for(int i=0;i<n;i++)
    {
        scanf("%lld",&piles[i]);

        if(piles[i]>maxi)
            maxi=piles[i];
    }

    long long h;
    scanf("%lld",&h);

    long long low=1;
    long long high=maxi;
    long long ans=maxi;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;
        long long hours=0;

        for(int i=0;i<n;i++)
            hours+=(piles[i]+mid-1)/mid;

        if(hours<=h)
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

    vector<long long> piles(n);

    long long maxi=0;

    for(int i=0;i<n;i++)
    {
        cin>>piles[i];
        maxi=max(maxi,piles[i]);
    }

    long long h;
    cin>>h;

    long long low=1;
    long long high=maxi;
    long long ans=maxi;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;
        long long hours=0;

        for(long long x:piles)
            hours+=(x+mid-1)/mid;

        if(hours<=h)
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

        long[] piles=new long[n];

        long maxi=0;

        for(int i=0;i<n;i++)
        {
            piles[i]=sc.nextLong();
            maxi=Math.max(maxi,piles[i]);
        }

        long h=sc.nextLong();

        long low=1;
        long high=maxi;
        long ans=maxi;

        while(low<=high)
        {
            long mid=low+(high-low)/2;
            long hours=0;

            for(long x:piles)
                hours+=(x+mid-1)/mid;

            if(hours<=h)
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

piles=list(map(int,input().split()))

h=int(input())

low=1
high=max(piles)
ans=high

while low<=high:

    mid=low+(high-low)//2

    hours=0

    for x in piles:
        hours+=(x+mid-1)//mid

    if hours<=h:
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

        long[] piles=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        long h=long.Parse(Console.ReadLine());

        long maxi=0;

        foreach(long x in piles)
            if(x>maxi)
                maxi=x;

        long low=1;
        long high=maxi;
        long ans=maxi;

        while(low<=high)
        {
            long mid=low+(high-low)/2;
            long hours=0;

            foreach(long x in piles)
                hours+=(x+mid-1)/mid;

            if(hours<=h)
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

const piles=[];

let maxi=0;

for(let i=0;i<n;i++)
{
    piles.push(input[idx]);
    maxi=Math.max(maxi,input[idx]);
    idx++;
}

const h=input[idx];

let low=1;
let high=maxi;
let ans=maxi;

while(low<=high)
{
    const mid=low+Math.floor((high-low)/2);

    let hours=0;

    for(const x of piles)
        hours+=Math.floor((x+mid-1)/mid);

    if(hours<=h)
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

3 6 7 11

8

Output

4

# Time Complexity
O(N × log(MaxPile))

# Space Complexity
O(1)

</approaches>




