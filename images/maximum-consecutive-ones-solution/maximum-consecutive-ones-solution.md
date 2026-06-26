# Maximum Consecutive Ones - Solution

## Problem Statement

Given a binary array `nums`, return the maximum number of consecutive `1`s in the array.

## Input Format

First line: Integer `n`

Second line: `n` space-separated integers (`0`s and `1`s)

## Output Format

Print a single integer representing the maximum number of consecutive `1`s.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** For every index containing `1`, count consecutive `1`s starting from that position.
- **Linear Traversal (Optimal):** Traverse the array once while maintaining the current streak of consecutive `1`s.

For example,

Input

6

1 1 0 1 1 1

Output

3

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. For every index:

- If the element is `1`, count how many consecutive `1`s follow it.
- Update the maximum count.

1. Print the maximum count.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    int ans=0;

    for(int i=0;i<n;i++)
    {
        if(arr[i]==1)
        {
            int count=0;

            for(int j=i;j<n && arr[j]==1;j++)
                count++;

            if(count>ans)
                ans=count;
        }
    }

    printf("%d",ans);

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

    int ans=0;

    for(int i=0;i<n;i++)
    {
        if(arr[i]==1)
        {
            int count=0;

            for(int j=i;j<n && arr[j]==1;j++)
                count++;

            ans=max(ans,count);
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

        int[] arr=new int[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextInt();

        int ans=0;

        for(int i=0;i<n;i++)
        {
            if(arr[i]==1)
            {
                int count=0;

                for(int j=i;j<n && arr[j]==1;j++)
                    count++;

                ans=Math.max(ans,count);
            }
        }

        System.out.print(ans);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

ans=0

for i in range(n):

    if arr[i]==1:

        count=0

        j=i

        while j<n and arr[j]==1:
            count+=1
            j+=1

        ans=max(ans,count)

print(ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int ans = 0;

        for(int i = 0; i < n; i++)
        {
            if(arr[i] == 1)
            {
                int count = 0;

                for(int j = i; j < n && arr[j] == 1; j++)
                    count++;

                ans = Math.Max(ans, count);
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

const arr = [];

for(let i = 0; i < n; i++)
    arr.push(input[idx++]);

let ans = 0;

for(let i = 0; i < n; i++)
{
    if(arr[i] === 1)
    {
        let count = 0;

        for(let j = i; j < n && arr[j] === 1; j++)
            count++;

        ans = Math.max(ans, count);
    }
}

console.log(ans);
```

### Output
Input

6

1 1 0 1 1 1

Output

3

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Linear Traversal (Optimal)

### Algorithm

1. Read the array.
2. Initialize `currentCount = 0` and `maxCount = 0`.
3. Traverse the array:

- If the current element is `1`, increment `currentCount`.
- Otherwise, reset `currentCount` to `0`.
- Update `maxCount`.

1. Print `maxCount`.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    int current=0;
    int maximum=0;

    for(int i=0;i<n;i++)
    {
        if(arr[i]==1)
            current++;
        else
            current=0;

        if(current>maximum)
            maximum=current;
    }

    printf("%d",maximum);

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

    int current=0;
    int maximum=0;

    for(int value:arr)
    {
        if(value==1)
            current++;
        else
            current=0;

        maximum=max(maximum,current);
    }

    cout<<maximum;

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

        int current=0;
        int maximum=0;

        for(int value:arr)
        {
            if(value==1)
                current++;
            else
                current=0;

            maximum=Math.max(maximum,current);
        }

        System.out.print(maximum);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

current=0
maximum=0

for value in arr:

    if value==1:
        current+=1
    else:
        current=0

    maximum=max(maximum,current)

print(maximum)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int current = 0;
        int maximum = 0;

        foreach(int value in arr)
        {
            if(value == 1)
                current++;
            else
                current = 0;

            maximum = Math.Max(maximum, current);
        }

        Console.Write(maximum);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

let current = 0;
let maximum = 0;

for(let i = 0; i < n; i++)
{
    if(input[idx++] === 1)
        current++;
    else
        current = 0;

    maximum = Math.max(maximum, current);
}

console.log(maximum);
```

### Output
Input

6

1 1 0 1 1 1

Output

3

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




