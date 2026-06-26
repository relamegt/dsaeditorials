# Original Array from given Prefix Sums - Solution

## Problem Statement

Given a prefix sum array `p[]` of size `N`, reconstruct and print the original array `arr[]` from which this prefix sum was computed.

Recall:

- `p[0] = arr[0]`
- `p[i] = p[i-1] + arr[i]` for `i >= 1`

Therefore,

- `arr[0] = p[0]`
- `arr[i] = p[i] - p[i-1]`

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing the prefix sum array.

## Output Format

Print the reconstructed original array.

## Explanation

Since every element after the first is simply the difference between two consecutive prefix sums, the original array can be reconstructed in a single traversal.

For example,

Input

5

10 13 16 19 24

Output

10 3 3 3 5

## Algorithm

1. Read `N`.
2. Read the prefix sum array.
3. Print the first element as it is.
4. For every index from `1` to `N-1`:

- Compute `prefix[i] - prefix[i-1]`.
- Print the result.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d",&N);

    long long prefix[N];

    for(int i=0;i<N;i++)
        scanf("%lld",&prefix[i]);

    printf("%lld",prefix[0]);

    for(int i=1;i<N;i++)
        printf(" %lld",prefix[i]-prefix[i-1]);

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

    vector<long long> prefix(N);

    for(int i=0;i<N;i++)
        cin>>prefix[i];

    cout<<prefix[0];

    for(int i=1;i<N;i++)
        cout<<" "<<prefix[i]-prefix[i-1];

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

        long[] prefix=new long[N];

        for(int i=0;i<N;i++)
            prefix[i]=sc.nextLong();

        System.out.print(prefix[0]);

        for(int i=1;i<N;i++)
            System.out.print(" "+(prefix[i]-prefix[i-1]));
    }
}
```
```Python
N=int(input())

prefix=list(map(int,input().split()))

print(prefix[0],end="")

for i in range(1,N):
    print(prefix[i]-prefix[i-1],end=" ")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] prefix = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        Console.Write(prefix[0]);

        for(int i = 1; i < N; i++)
            Console.Write(" " + (prefix[i] - prefix[i - 1]));
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(BigInt);

let idx = 0;

const N = Number(input[idx++]);

const prefix = [];

for(let i = 0; i < N; i++)
    prefix.push(input[idx++]);

let answer = [];

answer.push(prefix[0].toString());

for(let i = 1; i < N; i++)
    answer.push((prefix[i] - prefix[i - 1]).toString());

console.log(answer.join(" "));
```

### Output
Input

5

10 13 16 19 24

Output

10 3 3 3 5

# Time Complexity
O(N)

# Space Complexity
O(N)

###



**Note :** The auxiliary space used by the algorithm is **O(1)** since the reconstruction is computed directly from the prefix array. The input array itself occupies **O(N)** space.
