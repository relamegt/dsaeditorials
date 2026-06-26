# Square Root (Floor Value) - Solution

## Problem Statement

Given a non-negative integer `N`, find and print the floor value of its square root.

The floor value of the square root of `N` is the greatest integer `X` such that `X × X <= N`.

## Input Format

First line: A single integer `N`.

## Output Format

Print a single integer representing the floor value of `sqrt(N)`.

## Explanation

Since `N` can be as large as `10^18`, checking every number one by one is inefficient. Binary Search efficiently finds the largest integer whose square is less than or equal to `N`.

For example,

Input

10

Output

3

## Algorithm

1. Read the value of `N`.
2. Initialize `low = 0`, `high = N`, and `answer = 0`.
3. While `low <= high`:

- Compute `mid`.
- If `mid <= N / mid` (to avoid overflow), store `mid` as the current answer and search the right half.
- Otherwise, search the left half.

1. Print `answer`.

```C
#include <stdio.h>

int main()
{
    unsigned long long n;
    scanf("%llu",&n);

    unsigned long long low=0;
    unsigned long long high=n;
    unsigned long long answer=0;

    while(low<=high)
    {
        unsigned long long mid=low+(high-low)/2;

        if(mid==0 || mid<=n/mid)
        {
            answer=mid;
            low=mid+1;
        }
        else
        {
            high=mid-1;
        }
    }

    printf("%llu",answer);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main()
{
    unsigned long long n;
    cin>>n;

    unsigned long long low=0;
    unsigned long long high=n;
    unsigned long long answer=0;

    while(low<=high)
    {
        unsigned long long mid=low+(high-low)/2;

        if(mid==0 || mid<=n/mid)
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

        long n=sc.nextLong();

        long low=0;
        long high=n;
        long answer=0;

        while(low<=high)
        {
            long mid=low+(high-low)/2;

            if(mid==0 || mid<=n/mid)
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

low=0
high=n
answer=0

while low<=high:

    mid=low+(high-low)//2

    if mid==0 or mid<=n//mid:
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
        ulong n=ulong.Parse(Console.ReadLine());

        ulong low=0;
        ulong high=n;
        ulong answer=0;

        while(low<=high)
        {
            ulong mid=low+(high-low)/2;

            if(mid==0 || mid<=n/mid)
            {
                answer=mid;
                low=mid+1;
            }
            else
            {
                high=mid-1;
            }
        }

        Console.Write(answer);
    }
}
```
```JavaScript
const n=BigInt(require("fs").readFileSync(0,"utf8").trim());

let low=0n;
let high=n;
let answer=0n;

while(low<=high)
{
    const mid=low+(high-low)/2n;

    if(mid===0n || mid<=n/mid)
    {
        answer=mid;
        low=mid+1n;
    }
    else
    {
        high=mid-1n;
    }
}

console.log(answer.toString());
```

### Output
Input

10

Output

3

# Time Complexity
O(log N)

# Space Complexity
O(1)




