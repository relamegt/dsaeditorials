# Find the Nth Root of an Integer - Solution

## Problem Statement

Given two positive integers `N` and `M`, find the integer `X` such that `X` raised to the power `N` is equal to `M`.

If no such integer exists, print `-1`.

## Input Format

First line: Integer `N`

Second line: Integer `M`

## Output Format

Print a single integer representing the nth root of `M` if it is an integer, otherwise print `-1`.

## Explanation

There are two common approaches to solve this problem.

- **Linear Search:** Try every possible integer until the nth power equals or exceeds `M`.
- **Binary Search (Optimal):** Search over the possible values of the root using binary search and compare `midⁿ` with `M`.

For example,

Input

3

27

Output

3

<approaches>
## Approach 1: Linear Search

### Algorithm

1. Read `N` and `M`.
2. Iterate `X` from `1` while `X ≤ M`.
3. Compute `Xⁿ`.
4. If `Xⁿ == M`, print `X`.
5. If `Xⁿ > M`, stop the search.
6. If no such value exists, print `-1`.

### Time Complexity

O(M × N)

### Space Complexity

O(1)


## Approach 2: Binary Search (Optimal)

### Algorithm

1. Read `N` and `M`.
2. Initialize `low = 1` and `high = M`.
3. While `low <= high`:

- Compute `mid`.
- Compute `midⁿ` carefully, stopping early if the value exceeds `M`.
- If `midⁿ == M`, print `mid`.
- If `midⁿ < M`, search the right half.
- Otherwise, search the left half.

1. If no exact root is found, print `-1`.

```C
#include <stdio.h>

long long power(long long base,int exp,long long limit)
{
    long long result=1;

    while(exp--)
    {
        if(result>limit/base)
            return limit+1;

        result*=base;
    }

    return result;
}

int main()
{
    int n;
    long long m;

    scanf("%d",&n);
    scanf("%lld",&m);

    long long low=1;
    long long high=m;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;

        long long val=power(mid,n,m);

        if(val==m)
        {
            printf("%lld",mid);
            return 0;
        }

        if(val<m)
            low=mid+1;
        else
            high=mid-1;
    }

    printf("-1");

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

long long power(long long base,int exp,long long limit)
{
    long long result=1;

    while(exp--)
    {
        if(result>limit/base)
            return limit+1;

        result*=base;
    }

    return result;
}

int main()
{
    int n;
    long long m;

    cin>>n>>m;

    long long low=1;
    long long high=m;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;

        long long val=power(mid,n,m);

        if(val==m)
        {
            cout<<mid;
            return 0;
        }

        if(val<m)
            low=mid+1;
        else
            high=mid-1;
    }

    cout<<-1;

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    static long power(long base,int exp,long limit)
    {
        long result=1;

        while(exp-->0)
        {
            if(result>limit/base)
                return limit+1;

            result*=base;
        }

        return result;
    }

    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);

        int n=sc.nextInt();
        long m=sc.nextLong();

        long low=1;
        long high=m;

        while(low<=high)
        {
            long mid=low+(high-low)/2;

            long val=power(mid,n,m);

            if(val==m)
            {
                System.out.print(mid);
                return;
            }

            if(val<m)
                low=mid+1;
            else
                high=mid-1;
        }

        System.out.print(-1);
    }
}
```
```Python
def power(base,exp,limit):

    result=1

    while exp:

        if result>limit//base:
            return limit+1

        result*=base
        exp-=1

    return result

n=int(input())
m=int(input())

low=1
high=m

while low<=high:

    mid=low+(high-low)//2

    val=power(mid,n,m)

    if val==m:
        print(mid)
        break

    if val<m:
        low=mid+1
    else:
        high=mid-1
else:
    print(-1)
```
```C#
using System;

class Program
{
    static long Power(long b,int e,long limit)
    {
        long result=1;

        while(e-->0)
        {
            if(result>limit/b)
                return limit+1;

            result*=b;
        }

        return result;
    }

    static void Main()
    {
        int n=int.Parse(Console.ReadLine());
        long m=long.Parse(Console.ReadLine());

        long low=1;
        long high=m;

        while(low<=high)
        {
            long mid=low+(high-low)/2;

            long val=Power(mid,n,m);

            if(val==m)
            {
                Console.Write(mid);
                return;
            }

            if(val<m)
                low=mid+1;
            else
                high=mid-1;
        }

        Console.Write(-1);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(BigInt);

const n=Number(input[0]);
const m=input[1];

function power(base,exp,limit)
{
    let result=1n;

    for(let i=0;i<exp;i++)
    {
        if(result>limit/base)
            return limit+1n;

        result*=base;
    }

    return result;
}

let low=1n;
let high=m;

while(low<=high)
{
    const mid=low+(high-low)/2n;

    const val=power(mid,n,m);

    if(val===m)
    {
        console.log(mid.toString());
        return;
    }

    if(val<m)
        low=mid+1n;
    else
        high=mid-1n;
}

console.log(-1);
```

### Output
Input

3

27

Output

3

# Time Complexity
O(N × log M)

# Space Complexity
O(1)

</approaches>




