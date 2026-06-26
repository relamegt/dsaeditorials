# Smallest Positive Integer That Cannot Be Represented as Subset Sum - Solution

## Problem Statement

Given an array `arr[]` of positive integers, find the smallest positive integer that cannot be represented as the sum of any subset of the given array.

## Input Format

First line: Integer `n`

Second line: `n` space-separated positive integers

## Output Format

Print a single integer representing the smallest positive integer that cannot be represented as a subset sum.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Generate all possible subset sums and find the first missing positive integer.
- **Greedy (Optimal):** Sort the array and continuously extend the range of representable sums.

For example,

Input

4

1 2 3 8

Output

7

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Generate every possible subset using recursion or bitmasking.
2. Compute the sum of every subset.
3. Store all subset sums.
4. Starting from `1`, find the first positive integer that is not present.
5. Print that integer.

```C
#include <stdio.h>
#include <stdlib.h>

int contains(int sums[], int size, int target)
{
    for(int i=0;i<size;i++)
        if(sums[i]==target)
            return 1;
    return 0;
}

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    int total=1<<n;
    int *sums=(int*)malloc(total*sizeof(int));

    int size=0;

    for(int mask=0;mask<total;mask++)
    {
        int sum=0;

        for(int i=0;i<n;i++)
        {
            if(mask&(1<<i))
                sum+=arr[i];
        }

        sums[size++]=sum;
    }

    int answer=1;

    while(contains(sums,size,answer))
        answer++;

    printf("%d",answer);

    free(sums);

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

    vector<int> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    vector<int> sums;

    int total=1<<n;

    for(int mask=0;mask<total;mask++)
    {
        int sum=0;

        for(int i=0;i<n;i++)
        {
            if(mask&(1<<i))
                sum+=arr[i];
        }

        sums.push_back(sum);
    }

    int answer=1;

    while(true)
    {
        bool found=false;

        for(int value:sums)
        {
            if(value==answer)
            {
                found=true;
                break;
            }
        }

        if(!found)
            break;

        answer++;
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

        int[] arr=new int[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextInt();

        ArrayList<Integer> sums=new ArrayList<>();

        int total=1<<n;

        for(int mask=0;mask<total;mask++)
        {
            int sum=0;

            for(int i=0;i<n;i++)
            {
                if((mask&(1<<i))!=0)
                    sum+=arr[i];
            }

            sums.add(sum);
        }

        int answer=1;

        while(true)
        {
            if(!sums.contains(answer))
                break;

            answer++;
        }

        System.out.print(answer);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

sums=[]

for mask in range(1<<n):

    total=0

    for i in range(n):

        if mask&(1<<i):
            total+=arr[i]

    sums.append(total)

answer=1

while answer in sums:
    answer+=1

print(answer)
```
```C#
using System;

class Program
{
    static bool Contains(int[] sums, int size, int target)
    {
        for(int i = 0; i < size; i++)
        {
            if(sums[i] == target)
                return true;
        }

        return false;
    }

    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int total = 1 << n;
        int[] sums = new int[total];

        int size = 0;

        for(int mask = 0; mask < total; mask++)
        {
            int sum = 0;

            for(int i = 0; i < n; i++)
            {
                if((mask & (1 << i)) != 0)
                    sum += arr[i];
            }

            sums[size++] = sum;
        }

        int answer = 1;

        while(Contains(sums, size, answer))
            answer++;

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

const sums = [];

const total = 1 << n;

for(let mask = 0; mask < total; mask++)
{
    let sum = 0;

    for(let i = 0; i < n; i++)
    {
        if(mask & (1 << i))
            sum += arr[i];
    }

    sums.push(sum);
}

let answer = 1;

while(sums.includes(answer))
    answer++;

console.log(answer);
```

### Output
Input

4

1 2 3 8

Output

7

# Time Complexity
O(N × 2ᴺ)

# Space Complexity
O(2ᴺ)

## Approach 2: Greedy (Optimal)

### Algorithm

1. Sort the array in ascending order.
2. Initialize `reachable = 1`, which represents the smallest value that cannot yet be formed.
3. Traverse the sorted array:

- If the current element is greater than `reachable`, stop because `reachable` cannot be formed.
- Otherwise, extend the reachable range by adding the current element:

     `reachable += arr[i]`.

1. Print `reachable`, which is the smallest unrepresentable sum.

```C
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a,const void *b)
{
    return (*(int*)a)-(*(int*)b);
}

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    qsort(arr,n,sizeof(int),compare);

    long long reachable=1;

    for(int i=0;i<n;i++)
    {
        if(arr[i]>reachable)
            break;

        reachable+=arr[i];
    }

    printf("%lld",reachable);

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
    int n;
    cin>>n;

    vector<int> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    sort(arr.begin(),arr.end());

    long long reachable=1;

    for(int value:arr)
    {
        if(value>reachable)
            break;

        reachable+=value;
    }

    cout<<reachable;

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

        int[] arr=new int[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextInt();

        Arrays.sort(arr);

        long reachable=1;

        for(int value:arr)
        {
            if(value>reachable)
                break;

            reachable+=value;
        }

        System.out.print(reachable);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

arr.sort()

reachable=1

for value in arr:

    if value>reachable:
        break

    reachable+=value

print(reachable)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        Array.Sort(arr);

        long reachable = 1;

        foreach(int value in arr)
        {
            if(value > reachable)
                break;

            reachable += value;
        }

        Console.Write(reachable);
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

arr.sort((a, b) => a - b);

let reachable = 1;

for(const value of arr)
{
    if(value > reachable)
        break;

    reachable += value;
}

console.log(reachable);
```

### Output
Input

4

1 2 3 8

Output

7

# Time Complexity
O(N log N)

# Space Complexity
O(1)

</approaches>




