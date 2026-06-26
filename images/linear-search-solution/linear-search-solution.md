# Linear Search- Solution

## Problem Statement

Given an array of integers `arr` of size `N` and an integer `X`, find the index of the first occurrence of `X` in the array. If `X` is not present, print `-1`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers

Third line: Integer `X`

## Output Format

Print a single integer representing the 0-based index of the first occurrence of `X`, or `-1` if it is not found.

## Explanation

There is one optimal approach to solve this problem.

- **Linear Search:** Traverse the array from left to right and return the first index where the element equals `X`.

For example,

Input

5

3 1 4 1 5

1

Output

1

### Algorithm

1. Read the array and the target element `X`.
2. Traverse the array from left to right.
3. If the current element equals `X`, print its index and stop.
4. If the loop finishes without finding `X`, print `-1`.

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

    for(int i=0;i<n;i++)
    {
        if(arr[i]==x)
        {
            printf("%d",i);
            return 0;
        }
    }

    printf("-1");

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

    for(int i=0;i<n;i++)
    {
        if(arr[i]==x)
        {
            cout<<i;
            return 0;
        }
    }

    cout<<-1;

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

        for(int i=0;i<n;i++)
        {
            if(arr[i]==x)
            {
                System.out.print(i);
                return;
            }
        }

        System.out.print(-1);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

x=int(input())

for i in range(n):

    if arr[i]==x:
        print(i)
        exit()

print(-1)
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

        for(int i = 0; i < n; i++)
        {
            if(arr[i] == x)
            {
                Console.Write(i);
                return;
            }
        }

        Console.Write(-1);
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

for(let i = 0; i < n; i++)
{
    if(arr[i] === x)
    {
        console.log(i);
        return;
    }
}

console.log(-1);
```

### Output
Input

5

3 1 4 1 5

1

Output

1

# Time Complexity
O(N)

# Space Complexity
O(1)




