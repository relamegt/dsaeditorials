# Floor in a Sorted Array - Solution

## Problem Statement

Given a sorted array of integers `arr` of size `N` in non-decreasing order and an integer `X`, find the index of the floor of `X`.

The floor of `X` is the largest element in the array that is less than or equal to `X`. Print the 0-based index of that element. If such an element does not exist, print `-1`.

If multiple occurrences of the floor value exist, print the index of the last occurrence.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers in non-decreasing order

Third line: Integer `X`

## Output Format

Print a single integer representing the index of the floor of `X`, or `-1` if no floor exists.

## Explanation

There are two common approaches to solve this problem.

- **Linear Search:** Traverse the array and keep updating the last valid floor index.
- **Binary Search (Optimal):** Use binary search to locate the last element less than or equal to `X`.

For example,

Input

6

1 2 4 6 8 10

5

Output

2

<approaches>
## Approach 1: Linear Search

### Algorithm

1. Read the sorted array and `X`.
2. Initialize `answer = -1`.
3. Traverse the array from left to right.
4. Whenever `arr[i] <= X`, update `answer = i`.
5. Print `answer`.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    long long x;
    scanf("%lld",&x);

    int answer=-1;

    for(int i=0;i<n;i++)
    {
        if(arr[i]<=x)
            answer=i;
    }

    printf("%d",answer);

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

    for(int i=0;i<n;i++)
        cin>>arr[i];

    long long x;
    cin>>x;

    int answer=-1;

    for(int i=0;i<n;i++)
    {
        if(arr[i]<=x)
            answer=i;
    }

    cout<<answer;

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

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        long x=sc.nextLong();

        int answer=-1;

        for(int i=0;i<n;i++)
        {
            if(arr[i]<=x)
                answer=i;
        }

        System.out.print(answer);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

x=int(input())

answer=-1

for i in range(n):

    if arr[i]<=x:
        answer=i

print(answer)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long x = long.Parse(Console.ReadLine());

        int answer = -1;

        for(int i = 0; i < n; i++)
        {
            if(arr[i] <= x)
                answer = i;
        }

        Console.Write(answer);
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

const x = input[idx++];

let answer = -1;

for(let i = 0; i < n; i++)
{
    if(arr[i] <= x)
        answer = i;
}

console.log(answer);
```

### Output
Input

6

1 2 4 6 8 10

5

Output

2

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Binary Search (Optimal)

### Algorithm

1. Read the sorted array and `X`.
2. Initialize `low = 0`, `high = N - 1`, and `answer = -1`.
3. While `low <= high`:

- Compute `mid`.
- If `arr[mid] <= X`, update `answer = mid` and search in the right half.
- Otherwise, search in the left half.

1. Print `answer`.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    long long x;
    scanf("%lld",&x);

    int low=0;
    int high=n-1;
    int answer=-1;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]<=x)
        {
            answer=mid;
            low=mid+1;
        }
        else
        {
            high=mid-1;
        }
    }

    printf("%d",answer);

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

    for(int i=0;i<n;i++)
        cin>>arr[i];

    long long x;
    cin>>x;

    int low=0;
    int high=n-1;
    int answer=-1;

    while(low<=high)
    {
        int mid=low+(high-low)/2;

        if(arr[mid]<=x)
        {
            answer=mid;
            low=mid+1;
        }
        else
        {
            high=mid-1;
        }
    }

    cout<<answer;

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

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        long x=sc.nextLong();

        int low=0;
        int high=n-1;
        int answer=-1;

        while(low<=high)
        {
            int mid=low+(high-low)/2;

            if(arr[mid]<=x)
            {
                answer=mid;
                low=mid+1;
            }
            else
            {
                high=mid-1;
            }
        }

        System.out.print(answer);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

x=int(input())

low=0
high=len(arr)-1
answer=-1

while low<=high:

    mid=low+(high-low)//2

    if arr[mid]<=x:
        answer=mid
        low=mid+1
    else:
        high=mid-1

print(answer)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long x = long.Parse(Console.ReadLine());

        int low = 0;
        int high = n - 1;
        int answer = -1;

        while(low <= high)
        {
            int mid = low + (high - low) / 2;

            if(arr[mid] <= x)
            {
                answer = mid;
                low = mid + 1;
            }
            else
            {
                high = mid - 1;
            }
        }

        Console.Write(answer);
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

const x = input[idx++];

let low = 0;
let high = n - 1;
let answer = -1;

while(low <= high)
{
    const mid = low + Math.floor((high - low) / 2);

    if(arr[mid] <= x)
    {
        answer = mid;
        low = mid + 1;
    }
    else
    {
        high = mid - 1;
    }
}

console.log(answer);
```

### Output
Input

6

1 2 4 6 8 10

5

Output

2

# Time Complexity
O(log N)

# Space Complexity
O(1)

</approaches>




