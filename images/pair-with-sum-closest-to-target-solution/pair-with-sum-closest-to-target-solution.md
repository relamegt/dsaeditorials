# Pair with Sum Closest to Target - Solution

## Problem Statement

Given an array `arr[]` and an integer `target`, find a pair of elements `(a, b)` such that the sum `a + b` is closest to `target`.

Return the pair in sorted order.

If multiple pairs have the same closest sum, return the pair having the **maximum absolute difference**.

If no such pair exists, print nothing.

## Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

Third line: Integer `target`.

## Output Format

Print two space-separated integers representing the required pair.

If no pair exists, print an empty output.

## Explanation

There are two common approaches for solving this problem.

- **Sorting + Two Pointers (Recommended)** — Sort the array and use two pointers to efficiently search for the closest sum.
- **Brute Force** — Check every possible pair and choose the best one.

For example,

Input

4

1 4 5 7

8

Output

1 7

<approaches>
## Approach 1: Sorting + Two Pointers (Recommended)

### Algorithm

1. Read the array and target.
2. If the array contains fewer than two elements, print nothing.
3. Sort the array.
4. Initialize two pointers:

- `left = 0`
- `right = N - 1`

1. For every pair:

- Compute current sum.
- Compute its distance from the target.
- Update the answer if:
- distance is smaller, or
- distance is equal but absolute difference between numbers is larger.

1. If sum is smaller than target, move `left`.
2. Otherwise move `right`.
3. Print the selected pair.

```C
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a,const void *b)
{
    return (*(int*)a)-(*(int*)b);
}

int main()
{
    int N;
    scanf("%d",&N);

    if(N<2)
        return 0;

    int arr[N];

    for(int i=0;i<N;i++)
        scanf("%d",&arr[i]);

    int target;
    scanf("%d",&target);

    qsort(arr,N,sizeof(int),compare);

    int left=0;
    int right=N-1;

    int ans1=arr[0];
    int ans2=arr[1];

    int best=abs(ans1+ans2-target);

    while(left<right)
    {
        int sum=arr[left]+arr[right];
        int diff=abs(sum-target);

        if(diff<best ||
          (diff==best &&
           abs(arr[right]-arr[left])>abs(ans2-ans1)))
        {
            best=diff;
            ans1=arr[left];
            ans2=arr[right];
        }

        if(sum<target)
            left++;
        else
            right--;
    }

    printf("%d %d",ans1,ans2);

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
    int N;
    cin>>N;

    if(N<2)
        return 0;

    vector<int> arr(N);

    for(int i=0;i<N;i++)
        cin>>arr[i];

    int target;
    cin>>target;

    sort(arr.begin(),arr.end());

    int left=0;
    int right=N-1;

    int ans1=arr[0];
    int ans2=arr[1];

    int best=abs(ans1+ans2-target);

    while(left<right)
    {
        int sum=arr[left]+arr[right];
        int diff=abs(sum-target);

        if(diff<best ||
          (diff==best &&
           abs(arr[right]-arr[left])>abs(ans2-ans1)))
        {
            best=diff;
            ans1=arr[left];
            ans2=arr[right];
        }

        if(sum<target)
            left++;
        else
            right--;
    }

    cout<<ans1<<" "<<ans2;

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

        int N=sc.nextInt();

        if(N<2)
            return;

        int[] arr=new int[N];

        for(int i=0;i<N;i++)
            arr[i]=sc.nextInt();

        int target=sc.nextInt();

        Arrays.sort(arr);

        int left=0;
        int right=N-1;

        int ans1=arr[0];
        int ans2=arr[1];

        int best=Math.abs(ans1+ans2-target);

        while(left<right)
        {
            int sum=arr[left]+arr[right];
            int diff=Math.abs(sum-target);

            if(diff<best ||
              (diff==best &&
               Math.abs(arr[right]-arr[left])>
               Math.abs(ans2-ans1)))
            {
                best=diff;
                ans1=arr[left];
                ans2=arr[right];
            }

            if(sum<target)
                left++;
            else
                right--;
        }

        System.out.print(ans1+" "+ans2);
    }
}
```
```Python
N=int(input())

if N<2:
    exit()

arr=list(map(int,input().split()))

target=int(input())

arr.sort()

left=0
right=N-1

ans1=arr[0]
ans2=arr[1]

best=abs(ans1+ans2-target)

while left<right:

    s=arr[left]+arr[right]

    diff=abs(s-target)

    if diff<best or (
        diff==best and
        abs(arr[right]-arr[left])>
        abs(ans2-ans1)
    ):
        best=diff
        ans1=arr[left]
        ans2=arr[right]

    if s<target:
        left+=1
    else:
        right-=1

print(ans1,ans2)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        if (N < 2)
            return;

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int target = int.Parse(Console.ReadLine());

        Array.Sort(arr);

        int left = 0;
        int right = N - 1;

        int ans1 = arr[0];
        int ans2 = arr[1];

        int best = Math.Abs(ans1 + ans2 - target);

        while (left < right)
        {
            int sum = arr[left] + arr[right];
            int diff = Math.Abs(sum - target);

            if (diff < best ||
               (diff == best &&
                Math.Abs(arr[right] - arr[left]) > Math.Abs(ans2 - ans1)))
            {
                best = diff;
                ans1 = arr[left];
                ans2 = arr[right];
            }

            if (sum < target)
                left++;
            else
                right--;
        }

        Console.Write(ans1 + " " + ans2);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const N = input[idx++];

if (N < 2)
    process.exit(0);

const arr = [];

for (let i = 0; i < N; i++)
    arr.push(input[idx++]);

const target = input[idx++];

arr.sort((a, b) => a - b);

let left = 0;
let right = N - 1;

let ans1 = arr[0];
let ans2 = arr[1];

let best = Math.abs(ans1 + ans2 - target);

while (left < right)
{
    const sum = arr[left] + arr[right];
    const diff = Math.abs(sum - target);

    if (diff < best ||
       (diff === best &&
        Math.abs(arr[right] - arr[left]) > Math.abs(ans2 - ans1)))
    {
        best = diff;
        ans1 = arr[left];
        ans2 = arr[right];
    }

    if (sum < target)
        left++;
    else
        right--;
}

console.log(ans1 + " " + ans2);
```

### Output
Input

4

1 4 5 7

8

Output

1 7

# Time Complexity
O(N log N)

# Space Complexity
O(1)

## Approach 2: Brute Force

### Algorithm

1. Read the array and target.
2. If `N < 2`, print nothing.
3. Initialize the first pair as the answer.
4. Check every possible pair.
5. Compute:

- Difference from target.
- Absolute difference between the pair.

1. Update the answer whenever:

- Current pair is closer to target.
- Same closeness but larger absolute difference.

1. Print the final pair.

```C
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int N;
    scanf("%d", &N);

    if (N < 2)
        return 0;

    int arr[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    int target;
    scanf("%d", &target);

    int ans1 = arr[0];
    int ans2 = arr[1];

    int best = abs(ans1 + ans2 - target);

    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {
            int diff = abs(arr[i] + arr[j] - target);

            if (diff < best ||
               (diff == best &&
                abs(arr[j] - arr[i]) > abs(ans2 - ans1)))
            {
                best = diff;
                ans1 = arr[i];
                ans2 = arr[j];
            }
        }
    }

    if (ans1 > ans2)
    {
        int t = ans1;
        ans1 = ans2;
        ans2 = t;
    }

    printf("%d %d", ans1, ans2);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;

int main()
{
    int N;
    cin >> N;

    if (N < 2)
        return 0;

    vector<int> arr(N);

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    int target;
    cin >> target;

    int ans1 = arr[0];
    int ans2 = arr[1];

    int best = abs(ans1 + ans2 - target);

    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {
            int diff = abs(arr[i] + arr[j] - target);

            if (diff < best ||
               (diff == best &&
                abs(arr[j] - arr[i]) > abs(ans2 - ans1)))
            {
                best = diff;
                ans1 = arr[i];
                ans2 = arr[j];
            }
        }
    }

    if (ans1 > ans2)
        swap(ans1, ans2);

    cout << ans1 << " " << ans2;

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        if (N < 2)
            return;

        int[] arr = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        int target = sc.nextInt();

        int ans1 = arr[0];
        int ans2 = arr[1];

        int best = Math.abs(ans1 + ans2 - target);

        for (int i = 0; i < N; i++)
        {
            for (int j = i + 1; j < N; j++)
            {
                int diff = Math.abs(arr[i] + arr[j] - target);

                if (diff < best ||
                   (diff == best &&
                    Math.abs(arr[j] - arr[i]) >
                    Math.abs(ans2 - ans1)))
                {
                    best = diff;
                    ans1 = arr[i];
                    ans2 = arr[j];
                }
            }
        }

        if (ans1 > ans2)
        {
            int t = ans1;
            ans1 = ans2;
            ans2 = t;
        }

        System.out.print(ans1 + " " + ans2);
    }
}
```
```Python
N = int(input())

if N < 2:
    exit()

arr = list(map(int, input().split()))

target = int(input())

ans1 = arr[0]
ans2 = arr[1]

best = abs(ans1 + ans2 - target)

for i in range(N):
    for j in range(i + 1, N):

        diff = abs(arr[i] + arr[j] - target)

        if diff < best or (
            diff == best and
            abs(arr[j] - arr[i]) > abs(ans2 - ans1)
        ):
            best = diff
            ans1 = arr[i]
            ans2 = arr[j]

if ans1 > ans2:
    ans1, ans2 = ans2, ans1

print(ans1, ans2)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        if (N < 2)
            return;

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int target = int.Parse(Console.ReadLine());

        int ans1 = arr[0];
        int ans2 = arr[1];

        int best = Math.Abs(ans1 + ans2 - target);

        for (int i = 0; i < N; i++)
        {
            for (int j = i + 1; j < N; j++)
            {
                int diff = Math.Abs(arr[i] + arr[j] - target);

                if (diff < best ||
                   (diff == best &&
                    Math.Abs(arr[j] - arr[i]) > Math.Abs(ans2 - ans1)))
                {
                    best = diff;
                    ans1 = arr[i];
                    ans2 = arr[j];
                }
            }
        }

        if (ans1 > ans2)
        {
            int temp = ans1;
            ans1 = ans2;
            ans2 = temp;
        }

        Console.Write(ans1 + " " + ans2);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const N = input[idx++];

if (N < 2)
    process.exit(0);

const arr = [];

for (let i = 0; i < N; i++)
    arr.push(input[idx++]);

const target = input[idx++];

let ans1 = arr[0];
let ans2 = arr[1];

let best = Math.abs(ans1 + ans2 - target);

for (let i = 0; i < N; i++)
{
    for (let j = i + 1; j < N; j++)
    {
        const diff = Math.abs(arr[i] + arr[j] - target);

        if (
            diff < best ||
            (
                diff === best &&
                Math.abs(arr[j] - arr[i]) > Math.abs(ans2 - ans1)
            )
        )
        {
            best = diff;
            ans1 = arr[i];
            ans2 = arr[j];
        }
    }
}

if (ans1 > ans2)
{
    const temp = ans1;
    ans1 = ans2;
    ans2 = temp;
}

console.log(ans1 + " " + ans2);
```

### Output
Input

4

1 4 5 7

8

Output

1 7

# Time Complexity
O(N²)

# Space Complexity
O(1)

</approaches>




