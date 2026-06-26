# Smallest Positive Missing - Solution

## Problem Statement

Given an array `arr[]`, find the smallest positive integer (greater than `0`) that is missing from the array.

## Input Format

First line: Integer `n`

Second line: `n` space-separated integers

## Output Format

Print a single integer representing the smallest missing positive integer.

## Explanation

There are three common approaches to solve this problem.

- **Brute Force:** Check every positive integer starting from `1` by scanning the array.
- **Hashing:** Store all positive integers in a hash set and find the first missing one.
- **Index Placement (Optimal):** Place every positive integer `x` at index `x-1` and identify the first incorrect position.

For example,

Input

5

1 2 0 3 4

Output

5

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. For every integer starting from `1` to `n + 1`:

- Scan the entire array.
- Check whether the current number exists.

1. Print the first missing positive integer.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    for(int x=1;x<=n+1;x++)
    {
        int found=0;

        for(int i=0;i<n;i++)
        {
            if(arr[i]==x)
            {
                found=1;
                break;
            }
        }

        if(!found)
        {
            printf("%d",x);
            break;
        }
    }

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

    for(int x=1;x<=n+1;x++)
    {
        bool found=false;

        for(int value:arr)
        {
            if(value==x)
            {
                found=true;
                break;
            }
        }

        if(!found)
        {
            cout<<x;
            break;
        }
    }

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

        for(int x=1;x<=n+1;x++)
        {
            boolean found=false;

            for(int value:arr)
            {
                if(value==x)
                {
                    found=true;
                    break;
                }
            }

            if(!found)
            {
                System.out.print(x);
                break;
            }
        }
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

for x in range(1,n+2):

    found=False

    for value in arr:

        if value==x:
            found=True
            break

    if not found:
        print(x)
        break
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        for(int x = 1; x <= n + 1; x++)
        {
            bool found = false;

            foreach(int value in arr)
            {
                if(value == x)
                {
                    found = true;
                    break;
                }
            }

            if(!found)
            {
                Console.Write(x);
                break;
            }
        }
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

for(let x = 1; x <= n + 1; x++)
{
    let found = false;

    for(const value of arr)
    {
        if(value === x)
        {
            found = true;
            break;
        }
    }

    if(!found)
    {
        console.log(x);
        break;
    }
}
```

### Output
Input

5

1 2 0 3 4

Output

5

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Hashing

### Algorithm

1. Read the array.
2. Insert every positive element into a hash set.
3. Traverse numbers from `1` to `n + 1`.
4. Print the first number that is not present in the hash set.

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

    int answer=1;

    for(int i=0;i<n;i++)
    {
        if(arr[i]==answer)
            answer++;
    }

    printf("%d",answer);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <unordered_set>
using namespace std;

int main()
{
    int n;
    cin>>n;

    vector<int> arr(n);
    unordered_set<int> st;

    for(int i=0;i<n;i++)
    {
        cin>>arr[i];

        if(arr[i]>0)
            st.insert(arr[i]);
    }

    int answer=1;

    while(st.count(answer))
        answer++;

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

        HashSet<Integer> set=new HashSet<>();

        for(int i=0;i<n;i++)
        {
            int value=sc.nextInt();

            if(value>0)
                set.add(value);
        }

        int answer=1;

        while(set.contains(answer))
            answer++;

        System.out.print(answer);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

s=set()

for value in arr:

    if value>0:
        s.add(value)

answer=1

while answer in s:
    answer+=1

print(answer)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        HashSet<int> set = new HashSet<int>();

        foreach(int value in arr)
        {
            if(value > 0)
                set.Add(value);
        }

        int answer = 1;

        while(set.Contains(answer))
            answer++;

        Console.Write(answer);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const set = new Set();

for(let i = 0; i < n; i++)
{
    const value = input[idx++];

    if(value > 0)
        set.add(value);
}

let answer = 1;

while(set.has(answer))
    answer++;

console.log(answer);
```

### Output
Input

5

1 2 0 3 4

Output

5

# Time Complexity
O(N)

# Space Complexity
O(N)

## Approach 3: Index Placement (Optimal)

### Algorithm

1. Traverse the array.
2. While the current value is in the range `1` to `n` and is not already in its correct position:

- Swap it with the element at index `value - 1`.

1. After all valid numbers are placed, traverse the array again.
2. The first index `i` where `arr[i] != i + 1` gives the smallest missing positive as `i + 1`.
3. If every position is correct, print `n + 1`.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    for(int i=0;i<n;i++)
    {
        while(arr[i]>=1 && arr[i]<=n && arr[arr[i]-1]!=arr[i])
        {
            int temp=arr[i];
            arr[i]=arr[temp-1];
            arr[temp-1]=temp;
        }
    }

    for(int i=0;i<n;i++)
    {
        if(arr[i]!=i+1)
        {
            printf("%d",i+1);
            return 0;
        }
    }

    printf("%d",n+1);

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

    for(int i=0;i<n;i++)
    {
        while(arr[i]>=1 && arr[i]<=n && arr[arr[i]-1]!=arr[i])
            swap(arr[i],arr[arr[i]-1]);
    }

    for(int i=0;i<n;i++)
    {
        if(arr[i]!=i+1)
        {
            cout<<i+1;
            return 0;
        }
    }

    cout<<n+1;

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

        for(int i=0;i<n;i++)
        {
            while(arr[i]>=1 && arr[i]<=n && arr[arr[i]-1]!=arr[i])
            {
                int temp=arr[i];
                arr[i]=arr[temp-1];
                arr[temp-1]=temp;
            }
        }

        for(int i=0;i<n;i++)
        {
            if(arr[i]!=i+1)
            {
                System.out.print(i+1);
                return;
            }
        }

        System.out.print(n+1);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

for i in range(n):

    while 1<=arr[i]<=n and arr[arr[i]-1]!=arr[i]:
        arr[arr[i]-1],arr[i]=arr[i],arr[arr[i]-1]

for i in range(n):

    if arr[i]!=i+1:
        print(i+1)
        exit()

print(n+1)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        for(int i = 0; i < n; i++)
        {
            while(arr[i] >= 1 && arr[i] <= n && arr[arr[i] - 1] != arr[i])
            {
                int temp = arr[i];
                arr[i] = arr[temp - 1];
                arr[temp - 1] = temp;
            }
        }

        for(int i = 0; i < n; i++)
        {
            if(arr[i] != i + 1)
            {
                Console.Write(i + 1);
                return;
            }
        }

        Console.Write(n + 1);
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

for(let i = 0; i < n; i++)
{
    while(arr[i] >= 1 && arr[i] <= n && arr[arr[i] - 1] !== arr[i])
    {
        let temp = arr[i];
        arr[i] = arr[temp - 1];
        arr[temp - 1] = temp;
    }
}

for(let i = 0; i < n; i++)
{
    if(arr[i] !== i + 1)
    {
        console.log(i + 1);
        return;
    }
}

console.log(n + 1);
```

### Output
Input

5

1 2 0 3 4

Output

5

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




