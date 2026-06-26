# Split Array Largest Sum - Solution

## Problem Statement

Given an array `nums` of size `N` and an integer `K`, split the array into `K` non-empty contiguous subarrays.

Find and print the minimum possible value of the largest sum among these `K` subarrays.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing `nums`

Third line: Integer `K`

## Output Format

Print a single integer representing the minimized largest subarray sum.

## Explanation

There are two approaches to solve this problem.

- **Approach 1:** Linear Search
- **Approach 2:** Binary Search (Optimal)

For example,

Input

5

7 2 5 10 8

2

Output

18

<approaches>
## Approach 1: Linear Search

### Algorithm

1. Find the maximum element and the total sum of the array.
2. Try every possible largest subarray sum from `maximum element` to `total sum`.
3. For each value, greedily create subarrays such that each subarray sum does not exceed the current limit.
4. If the number of subarrays formed is less than or equal to `K`, that limit is valid.
5. The first valid limit is the answer.

---

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long nums[n];
    long long low=0,high=0;

    for(int i=0;i<n;i++)
    {
        scanf("%lld",&nums[i]);

        if(nums[i]>low)
            low=nums[i];

        high+=nums[i];
    }

    int k;
    scanf("%d",&k);

    for(long long limit=low;limit<=high;limit++)
    {
        int parts=1;
        long long sum=0;

        for(int i=0;i<n;i++)
        {
            if(sum+nums[i]<=limit)
                sum+=nums[i];
            else
            {
                parts++;
                sum=nums[i];
            }
        }

        if(parts<=k)
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

    vector<long long> nums(n);

    long long low=0,high=0;

    for(int i=0;i<n;i++)
    {
        cin>>nums[i];
        low=max(low,nums[i]);
        high+=nums[i];
    }

    int k;
    cin>>k;

    for(long long limit=low;limit<=high;limit++)
    {
        int parts=1;
        long long sum=0;

        for(long long x:nums)
        {
            if(sum+x<=limit)
                sum+=x;
            else
            {
                parts++;
                sum=x;
            }
        }

        if(parts<=k)
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

        long[] nums=new long[n];

        long low=0,high=0;

        for(int i=0;i<n;i++)
        {
            nums[i]=sc.nextLong();
            low=Math.max(low,nums[i]);
            high+=nums[i];
        }

        int k=sc.nextInt();

        for(long limit=low;limit<=high;limit++)
        {
            int parts=1;
            long sum=0;

            for(long x:nums)
            {
                if(sum+x<=limit)
                    sum+=x;
                else
                {
                    parts++;
                    sum=x;
                }
            }

            if(parts<=k)
            {
                System.out.print(limit);
                return;
            }
        }
    }
}
```
```Python
n = int(input())

nums = list(map(int, input().split()))

k = int(input())

low = max(nums)
high = sum(nums)

for limit in range(low, high + 1):

    parts = 1
    total = 0

    for x in nums:

        if total + x <= limit:
            total += x
        else:
            parts += 1
            total = x

    if parts <= k:
        print(limit)
        break
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] nums = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        int k = int.Parse(Console.ReadLine());

        long low = 0;
        long high = 0;

        foreach (long x in nums)
        {
            if (x > low)
                low = x;

            high += x;
        }

        for (long limit = low; limit <= high; limit++)
        {
            int parts = 1;
            long sum = 0;

            foreach (long x in nums)
            {
                if (sum + x <= limit)
                    sum += x;
                else
                {
                    parts++;
                    sum = x;
                }
            }

            if (parts <= k)
            {
                Console.Write(limit);
                return;
            }
        }
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const nums = [];

let low = 0;
let high = 0;

for (let i = 0; i < n; i++)
{
    nums.push(input[idx]);
    low = Math.max(low, input[idx]);
    high += input[idx];
    idx++;
}

const k = input[idx];

for (let limit = low; limit <= high; limit++)
{
    let parts = 1;
    let sum = 0;

    for (const x of nums)
    {
        if (sum + x <= limit)
            sum += x;
        else
        {
            parts++;
            sum = x;
        }
    }

    if (parts <= k)
    {
        console.log(limit);
        return;
    }
}
```

### Output
Input

5

7 2 5 10 8

2

Output

18

# Time Complexity
O(N × TotalSum)

# Space Complexity
O(1)

## Approach 2: Binary Search (Optimal)

### Algorithm

1. Find the maximum element and the total sum of the array.
2. Set `low` as the maximum element and `high` as the total sum.
3. While `low <= high`:

- Compute `mid`.
- Greedily split the array into subarrays such that each subarray sum is at most `mid`.
- If the number of subarrays is less than or equal to `K`, store the answer and search for a smaller value.
- Otherwise, search for a larger value.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long nums[n];
    long long low=0,high=0;

    for(int i=0;i<n;i++)
    {
        scanf("%lld",&nums[i]);

        if(nums[i]>low)
            low=nums[i];

        high+=nums[i];
    }

    int k;
    scanf("%d",&k);

    long long ans=high;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;

        int parts=1;
        long long sum=0;

        for(int i=0;i<n;i++)
        {
            if(sum+nums[i]<=mid)
                sum+=nums[i];
            else
            {
                parts++;
                sum=nums[i];
            }
        }

        if(parts<=k)
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

    vector<long long> nums(n);

    long long low=0,high=0;

    for(int i=0;i<n;i++)
    {
        cin>>nums[i];
        low=max(low,nums[i]);
        high+=nums[i];
    }

    int k;
    cin>>k;

    long long ans=high;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;

        int parts=1;
        long long sum=0;

        for(long long x:nums)
        {
            if(sum+x<=mid)
                sum+=x;
            else
            {
                parts++;
                sum=x;
            }
        }

        if(parts<=k)
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

        long[] nums=new long[n];

        long low=0,high=0;

        for(int i=0;i<n;i++)
        {
            nums[i]=sc.nextLong();
            low=Math.max(low,nums[i]);
            high+=nums[i];
        }

        int k=sc.nextInt();

        long ans=high;

        while(low<=high)
        {
            long mid=low+(high-low)/2;

            int parts=1;
            long sum=0;

            for(long x:nums)
            {
                if(sum+x<=mid)
                    sum+=x;
                else
                {
                    parts++;
                    sum=x;
                }
            }

            if(parts<=k)
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
n = int(input())

nums = list(map(int, input().split()))

k = int(input())

low = max(nums)
high = sum(nums)

ans = high

while low <= high:

    mid = low + (high - low) // 2

    parts = 1
    total = 0

    for x in nums:

        if total + x <= mid:
            total += x
        else:
            parts += 1
            total = x

    if parts <= k:
        ans = mid
        high = mid - 1
    else:
        low = mid + 1

print(ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] nums = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        int k = int.Parse(Console.ReadLine());

        long low = 0;
        long high = 0;

        foreach (long x in nums)
        {
            if (x > low)
                low = x;

            high += x;
        }

        long ans = high;

        while (low <= high)
        {
            long mid = low + (high - low) / 2;

            int parts = 1;
            long sum = 0;

            foreach (long x in nums)
            {
                if (sum + x <= mid)
                    sum += x;
                else
                {
                    parts++;
                    sum = x;
                }
            }

            if (parts <= k)
            {
                ans = mid;
                high = mid - 1;
            }
            else
            {
                low = mid + 1;
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

const nums = [];

let low = 0;
let high = 0;

for (let i = 0; i < n; i++)
{
    nums.push(input[idx]);
    low = Math.max(low, input[idx]);
    high += input[idx];
    idx++;
}

const k = input[idx];

let ans = high;

while (low <= high)
{
    const mid = low + Math.floor((high - low) / 2);

    let parts = 1;
    let sum = 0;

    for (const x of nums)
    {
        if (sum + x <= mid)
            sum += x;
        else
        {
            parts++;
            sum = x;
        }
    }

    if (parts <= k)
    {
        ans = mid;
        high = mid - 1;
    }
    else
    {
        low = mid + 1;
    }
}

console.log(ans);
```

### Output
Input

5

7 2 5 10 8

2

Output

18

# Time Complexity
O(N × log(TotalSum))

# Space Complexity
O(1)

</approaches>




