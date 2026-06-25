# Dominant Pairs - Solution

## Problem Statement

Given an array `arr[]` of even size `N`, count the number of dominant pairs `(i, j)` such that:

- `0 <= i < N/2`
- `N/2 <= j < N`
- `arr[i] >= 5 × arr[j]`

Print the total number of dominant pairs.

## Input Format

First line: Integer `N` (even).

Second line: `N` space-separated integers.

## Output Format

Print a single integer representing the number of dominant pairs.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Check every possible pair between the two halves.
- **Sorting + Two Pointers (Optimal):** Sort both halves independently and efficiently count valid pairs.

For example,

Input

4

10 3 3 1

Output

2

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. Divide the array into two halves.
3. For every element in the first half:

- Compare it with every element in the second half.

1. If `arr[i] >= 5 × arr[j]`, increment the answer.
2. Print the total count.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d",&N);

    long long arr[N];

    for(int i=0;i<N;i++)
        scanf("%lld",&arr[i]);

    long long count=0;

    for(int i=0;i<N/2;i++)
    {
        for(int j=N/2;j<N;j++)
        {
            if(arr[i]>=5LL*arr[j])
                count++;
        }
    }

    printf("%lld",count);

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

    long long count=0;

    for(int i=0;i<N/2;i++)
    {
        for(int j=N/2;j<N;j++)
        {
            if(arr[i]>=5LL*arr[j])
                count++;
        }
    }

    cout<<count;

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

        long count=0;

        for(int i=0;i<N/2;i++)
        {
            for(int j=N/2;j<N;j++)
            {
                if(arr[i]>=5L*arr[j])
                    count++;
            }
        }

        System.out.print(count);
    }
}
```
```Python
N=int(input())

arr=list(map(int,input().split()))

count=0

for i in range(N//2):

    for j in range(N//2,N):

        if arr[i]>=5*arr[j]:
            count+=1

print(count)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long count = 0;

        for(int i = 0; i < N / 2; i++)
        {
            for(int j = N / 2; j < N; j++)
            {
                if(arr[i] >= 5L * arr[j])
                    count++;
            }
        }

        Console.Write(count);
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

let count = 0n;

for(let i = 0; i < N / 2; i++)
{
    for(let j = N / 2; j < N; j++)
    {
        if(arr[i] >= 5n * arr[j])
            count++;
    }
}

console.log(count.toString());
```

### Output
Input

4

10 3 3 1

Output

2

# Time Complexity
O((N/2)²) ≈ O(N²)

# Space Complexity
O(1)

## Approach 2: Sorting + Two Pointers (Optimal)

### Algorithm

1. Read the array.
2. Copy the first half and second half into two separate arrays.
3. Sort both halves independently.
4. Initialize a pointer `j = 0` for the second half.
5. Traverse every element in the sorted first half.
6. While `firstHalf[i] >= 5 × secondHalf[j]`, move `j` forward.
7. The value of `j` gives the number of valid pairs for the current element.
8. Add `j` to the answer.
9. Print the final count.

```C
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a,const void *b)
{
    long long x=*(long long*)a;
    long long y=*(long long*)b;

    if(x<y) return -1;
    if(x>y) return 1;
    return 0;
}

int main()
{
    int N;
    scanf("%d",&N);

    int half=N/2;

    long long left[half],right[half];

    for(int i=0;i<half;i++)
        scanf("%lld",&left[i]);

    for(int i=0;i<half;i++)
        scanf("%lld",&right[i]);

    qsort(left,half,sizeof(long long),compare);
    qsort(right,half,sizeof(long long),compare);

    long long ans=0;

    int j=0;

    for(int i=0;i<half;i++)
    {
        while(j<half && left[i]>=5LL*right[j])
            j++;

        ans+=j;
    }

    printf("%lld",ans);

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

    int half=N/2;

    vector<long long> left(half),right(half);

    for(int i=0;i<half;i++)
        cin>>left[i];

    for(int i=0;i<half;i++)
        cin>>right[i];

    sort(left.begin(),left.end());
    sort(right.begin(),right.end());

    long long ans=0;

    int j=0;

    for(int i=0;i<half;i++)
    {
        while(j<half && left[i]>=5LL*right[j])
            j++;

        ans+=j;
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

        int N=sc.nextInt();

        int half=N/2;

        long[] left=new long[half];
        long[] right=new long[half];

        for(int i=0;i<half;i++)
            left[i]=sc.nextLong();

        for(int i=0;i<half;i++)
            right[i]=sc.nextLong();

        Arrays.sort(left);
        Arrays.sort(right);

        long ans=0;

        int j=0;

        for(int i=0;i<half;i++)
        {
            while(j<half && left[i]>=5L*right[j])
                j++;

            ans+=j;
        }

        System.out.print(ans);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

half = N // 2

left = arr[:half]
right = arr[half:]

left.sort()
right.sort()

count = 0

j = 0

for i in range(half):

    while j < half and left[i] >= 5 * right[j]:
        j += 1

    count += j

print(count)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        int half = N / 2;

        long[] left = new long[half];
        long[] right = new long[half];

        Array.Copy(arr, 0, left, 0, half);
        Array.Copy(arr, half, right, 0, half);

        Array.Sort(left);
        Array.Sort(right);

        long count = 0;

        int j = 0;

        for(int i = 0; i < half; i++)
        {
            while(j < half && left[i] >= 5L * right[j])
                j++;

            count += j;
        }

        Console.Write(count);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(BigInt);

let idx = 0;

const N = Number(input[idx++]);

const half = N / 2;

const left = [];
const right = [];

for(let i = 0; i < half; i++)
    left.push(input[idx++]);

for(let i = 0; i < half; i++)
    right.push(input[idx++]);

left.sort((a, b) => (a < b ? -1 : 1));
right.sort((a, b) => (a < b ? -1 : 1));

let count = 0n;

let j = 0;

for(let i = 0; i < half; i++)
{
    while(j < half && left[i] >= 5n * right[j])
        j++;

    count += BigInt(j);
}

console.log(count.toString());
```

### Output
Input

4

10 3 3 1

Output

2

# Time Complexity
O(N log N)

# Space Complexity
O(N)

</approaches>




