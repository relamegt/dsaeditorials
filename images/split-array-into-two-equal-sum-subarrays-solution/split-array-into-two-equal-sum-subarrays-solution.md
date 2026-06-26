# Split Array into Two Equal Sum Subarrays - Solution

## Problem Statement

Given an array of integers `arr[]`, determine whether it is possible to split the array into two **non-empty contiguous subarrays** such that the sum of both subarrays is equal.

Elements cannot be reordered.

Return `true` if such a split exists, otherwise return `false`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers

## Output Format

Print `true` if such a split exists, otherwise print `false`.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Try every possible split position and calculate the sums of both subarrays.
- **Prefix Sum (Optimal):** Compute the total sum once and maintain a running prefix sum.

For example,

Input

4

4 1 2 3

Output

true

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. Try every possible split position from `0` to `N-2`.
3. Compute the sum of the left subarray.
4. Compute the sum of the right subarray.
5. If both sums are equal, print `true`.
6. If no valid split exists, print `false`.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d",&N);

    long long arr[N];

    for(int i=0;i<N;i++)
        scanf("%lld",&arr[i]);

    for(int split=0;split<N-1;split++)
    {
        long long left=0;
        long long right=0;

        for(int i=0;i<=split;i++)
            left+=arr[i];

        for(int i=split+1;i<N;i++)
            right+=arr[i];

        if(left==right)
        {
            printf("true");
            return 0;
        }
    }

    printf("false");

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int N;
    cin>>N;

    vector<long long> arr(N);

    for(int i=0;i<N;i++)
        cin>>arr[i];

    for(int split=0;split<N-1;split++)
    {
        long long left=0;
        long long right=0;

        for(int i=0;i<=split;i++)
            left+=arr[i];

        for(int i=split+1;i<N;i++)
            right+=arr[i];

        if(left==right)
        {
            cout<<"true";
            return 0;
        }
    }

    cout<<"false";

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

        long[] arr=new long[N];

        for(int i=0;i<N;i++)
            arr[i]=sc.nextLong();

        for(int split=0;split<N-1;split++)
        {
            long left=0;
            long right=0;

            for(int i=0;i<=split;i++)
                left+=arr[i];

            for(int i=split+1;i<N;i++)
                right+=arr[i];

            if(left==right)
            {
                System.out.print("true");
                return;
            }
        }

        System.out.print("false");
    }
}
```
```Python
N=int(input())

arr=list(map(int,input().split()))

for split in range(N-1):

    left=0
    right=0

    for i in range(split+1):
        left+=arr[i]

    for i in range(split+1,N):
        right+=arr[i]

    if left==right:
        print("true")
        exit()

print("false")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        for(int split = 0; split < N - 1; split++)
        {
            long left = 0;
            long right = 0;

            for(int i = 0; i <= split; i++)
                left += arr[i];

            for(int i = split + 1; i < N; i++)
                right += arr[i];

            if(left == right)
            {
                Console.Write("true");
                return;
            }
        }

        Console.Write("false");
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(BigInt);

let idx = 0;

const N = Number(input[idx++]);

const arr = [];

for(let i = 0; i < N; i++)
    arr.push(input[idx++]);

for(let split = 0; split < N - 1; split++)
{
    let left = 0n;
    let right = 0n;

    for(let i = 0; i <= split; i++)
        left += arr[i];

    for(let i = split + 1; i < N; i++)
        right += arr[i];

    if(left === right)
    {
        console.log("true");
        process.exit(0);
    }
}

console.log("false");
```

### Output
Input

4

4 1 2 3

Output

true

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Prefix Sum (Optimal)

### Algorithm

1. Read the array.
2. Compute the total sum of the array.
3. Initialize `leftSum = 0`.
4. Traverse the array from index `0` to `N-2` (to ensure both subarrays are non-empty).
5. Add the current element to `leftSum`.
6. Compute `rightSum = totalSum - leftSum`.
7. If `leftSum == rightSum`, print `true`.
8. If no such split exists after traversal, print `false`.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long arr[N];
    long long total = 0;

    for(int i = 0; i < N; i++)
    {
        scanf("%lld", &arr[i]);
        total += arr[i];
    }

    long long left = 0;

    for(int i = 0; i < N - 1; i++)
    {
        left += arr[i];

        if(left == total - left)
        {
            printf("true");
            return 0;
        }
    }

    printf("false");

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int N;
    cin >> N;

    vector<long long> arr(N);

    long long total = 0;

    for(int i = 0; i < N; i++)
    {
        cin >> arr[i];
        total += arr[i];
    }

    long long left = 0;

    for(int i = 0; i < N - 1; i++)
    {
        left += arr[i];

        if(left == total - left)
        {
            cout << "true";
            return 0;
        }
    }

    cout << "false";

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

        long[] arr = new long[N];

        long total = 0;

        for(int i = 0; i < N; i++)
        {
            arr[i] = sc.nextLong();
            total += arr[i];
        }

        long left = 0;

        for(int i = 0; i < N - 1; i++)
        {
            left += arr[i];

            if(left == total - left)
            {
                System.out.print("true");
                return;
            }
        }

        System.out.print("false");
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

total = sum(arr)

left = 0

for i in range(N - 1):

    left += arr[i]

    if left == total - left:
        print("true")
        exit()

print("false")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long total = 0;

        foreach(long value in arr)
            total += value;

        long left = 0;

        for(int i = 0; i < N - 1; i++)
        {
            left += arr[i];

            if(left == total - left)
            {
                Console.Write("true");
                return;
            }
        }

        Console.Write("false");
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(BigInt);

let idx = 0;

const N = Number(input[idx++]);

const arr = [];

let total = 0n;

for(let i = 0; i < N; i++)
{
    arr.push(input[idx]);
    total += input[idx];
    idx++;
}

let left = 0n;

for(let i = 0; i < N - 1; i++)
{
    left += arr[i];

    if(left === total - left)
    {
        console.log("true");
        process.exit(0);
    }
}

console.log("false");
```

### Output
Input

4

4 1 2 3

Output

true

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




