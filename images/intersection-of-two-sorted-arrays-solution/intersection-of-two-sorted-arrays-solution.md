# Intersection of Two Sorted Arrays - Solution

## Problem Statement

Given two sorted arrays `arr1` and `arr2` of sizes `N` and `M` respectively, find their intersection.

Each element in the output must appear only once, and the output must be in sorted order.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing `arr1`

Third line: Integer `M`

Fourth line: `M` space-separated integers representing `arr2`

## Output Format

Print the intersection as space-separated integers in sorted order.

If there is no common element, print `-1`.

## Explanation

There are two approaches to solve this problem.

- **Approach 1:** Hash Set
- **Approach 2:** Two Pointers (Optimal)

For example,

Input

5

1 2 2 3 4

4

2 2 4 6

Output

2 4

<approaches>
## Approach 1: Hash Set

### Algorithm

1. Read both arrays.
2. Insert all elements of the first array into a hash set.
3. Traverse the second array.
4. If an element exists in the hash set, add it to another set storing the intersection.
5. Print the intersection in sorted order.
6. If no common elements exist, print `-1`.

```C
#include <stdio.h>
#include <stdlib.h>

int cmp(const void *a,const void *b)
{
    return (*(int *)a-*(int *)b);
}

int main()
{
    int n,m;

    scanf("%d",&n);

    int arr1[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr1[i]);

    scanf("%d",&m);

    int arr2[m];

    for(int i=0;i<m;i++)
        scanf("%d",&arr2[i]);

    int ans[n<m?n:m];
    int k=0;

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
        {
            if(arr1[i]==arr2[j])
            {
                int found=0;

                for(int x=0;x<k;x++)
                {
                    if(ans[x]==arr1[i])
                    {
                        found=1;
                        break;
                    }
                }

                if(!found)
                    ans[k++]=arr1[i];

                break;
            }
        }
    }

    if(k==0)
    {
        printf("-1");
        return 0;
    }

    qsort(ans,k,sizeof(int),cmp);

    for(int i=0;i<k;i++)
        printf("%d ",ans[i]);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <set>
using namespace std;

int main()
{
    int n,m;

    cin>>n;

    vector<int> arr1(n);

    for(int i=0;i<n;i++)
        cin>>arr1[i];

    cin>>m;

    vector<int> arr2(m);

    for(int i=0;i<m;i++)
        cin>>arr2[i];

    set<int> s(arr1.begin(),arr1.end());
    set<int> ans;

    for(int x:arr2)
    {
        if(s.count(x))
            ans.insert(x);
    }

    if(ans.empty())
    {
        cout<<-1;
        return 0;
    }

    for(int x:ans)
        cout<<x<<" ";

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
            set.add(sc.nextInt());

        int m=sc.nextInt();

        TreeSet<Integer> ans=new TreeSet<>();

        for(int i=0;i<m;i++)
        {
            int x=sc.nextInt();

            if(set.contains(x))
                ans.add(x);
        }

        if(ans.isEmpty())
        {
            System.out.print(-1);
            return;
        }

        for(int x:ans)
            System.out.print(x+" ");
    }
}
```
```Python
n=int(input())

arr1=list(map(int,input().split()))

m=int(input())

arr2=list(map(int,input().split()))

s=set(arr1)
ans=sorted(set(arr2)&s)

if not ans:
    print(-1)
else:
    print(*ans)
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] arr1=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        int m=int.Parse(Console.ReadLine());

        long[] arr2=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        HashSet<long> set=new HashSet<long>(arr1);
        SortedSet<long> ans=new SortedSet<long>();

        foreach(long x in arr2)
        {
            if(set.Contains(x))
                ans.Add(x);
        }

        if(ans.Count==0)
        {
            Console.Write(-1);
            return;
        }

        foreach(long x in ans)
            Console.Write(x+" ");
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const arr1=[];

for(let i=0;i<n;i++)
    arr1.push(input[idx++]);

const m=input[idx++];

const arr2=[];

for(let i=0;i<m;i++)
    arr2.push(input[idx++]);

const set=new Set(arr1);
const ans=new Set();

for(const x of arr2)
{
    if(set.has(x))
        ans.add(x);
}

const result=[...ans].sort((a,b)=>a-b);

if(result.length===0)
    console.log(-1);
else
    console.log(result.join(" "));
```

### Output
Input

5

1 2 2 3 4

4

2 2 4 6

Output

2 4

# Time Complexity
O(N + M)

# Space Complexity
O(N)

## Approach 2: Two Pointers (Optimal)

### Algorithm

1. Read both sorted arrays.
2. Initialize two pointers `i` and `j` to the beginning of the arrays.
3. If both elements are equal, add the element to the answer only if it is not already added, then move both pointers.
4. If `arr1[i] < arr2[j]`, increment `i`.
5. Otherwise, increment `j`.
6. If no common elements are found, print `-1`.

```C
#include <stdio.h>

int main()
{
    int n,m;

    scanf("%d",&n);

    int arr1[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr1[i]);

    scanf("%d",&m);

    int arr2[m];

    for(int i=0;i<m;i++)
        scanf("%d",&arr2[i]);

    int i=0,j=0;
    int found=0;
    int last=0;

    while(i<n && j<m)
    {
        if(arr1[i]==arr2[j])
        {
            if(!found || arr1[i]!=last)
            {
                printf("%d ",arr1[i]);
                last=arr1[i];
                found=1;
            }

            i++;
            j++;
        }
        else if(arr1[i]<arr2[j])
            i++;
        else
            j++;
    }

    if(!found)
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
    int n,m;

    cin>>n;

    vector<int> arr1(n);

    for(int i=0;i<n;i++)
        cin>>arr1[i];

    cin>>m;

    vector<int> arr2(m);

    for(int i=0;i<m;i++)
        cin>>arr2[i];

    int i=0,j=0;
    bool found=false;
    int last=0;

    while(i<n && j<m)
    {
        if(arr1[i]==arr2[j])
        {
            if(!found || arr1[i]!=last)
            {
                cout<<arr1[i]<<" ";
                last=arr1[i];
                found=true;
            }

            i++;
            j++;
        }
        else if(arr1[i]<arr2[j])
            i++;
        else
            j++;
    }

    if(!found)
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

        int[] arr1=new int[n];

        for(int i=0;i<n;i++)
            arr1[i]=sc.nextInt();

        int m=sc.nextInt();

        int[] arr2=new int[m];

        for(int i=0;i<m;i++)
            arr2[i]=sc.nextInt();

        int i=0,j=0;
        boolean found=false;
        int last=0;

        while(i<n && j<m)
        {
            if(arr1[i]==arr2[j])
            {
                if(!found || arr1[i]!=last)
                {
                    System.out.print(arr1[i]+" ");
                    last=arr1[i];
                    found=true;
                }

                i++;
                j++;
            }
            else if(arr1[i]<arr2[j])
                i++;
            else
                j++;
        }

        if(!found)
            System.out.print(-1);
    }
}
```
```Python
n = int(input())

arr1 = list(map(int, input().split()))

m = int(input())

arr2 = list(map(int, input().split()))

i = 0
j = 0

ans = []

while i < n and j < m:

    if arr1[i] == arr2[j]:

        if not ans or ans[-1] != arr1[i]:
            ans.append(arr1[i])

        i += 1
        j += 1

    elif arr1[i] < arr2[j]:
        i += 1
    else:
        j += 1

if ans:
    print(*ans)
else:
    print(-1)
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr1 = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        int m = int.Parse(Console.ReadLine());

        long[] arr2 = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        int i = 0;
        int j = 0;

        List<long> ans = new List<long>();

        while (i < n && j < m)
        {
            if (arr1[i] == arr2[j])
            {
                if (ans.Count == 0 || ans[ans.Count - 1] != arr1[i])
                    ans.Add(arr1[i]);

                i++;
                j++;
            }
            else if (arr1[i] < arr2[j])
            {
                i++;
            }
            else
            {
                j++;
            }
        }

        if (ans.Count == 0)
        {
            Console.Write(-1);
            return;
        }

        foreach (long x in ans)
            Console.Write(x + " ");
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const arr1 = [];

for (let i = 0; i < n; i++)
    arr1.push(input[idx++]);

const m = input[idx++];

const arr2 = [];

for (let i = 0; i < m; i++)
    arr2.push(input[idx++]);

let i = 0;
let j = 0;

const ans = [];

while (i < n && j < m)
{
    if (arr1[i] === arr2[j])
    {
        if (ans.length === 0 || ans[ans.length - 1] !== arr1[i])
            ans.push(arr1[i]);

        i++;
        j++;
    }
    else if (arr1[i] < arr2[j])
    {
        i++;
    }
    else
    {
        j++;
    }
}

if (ans.length === 0)
    console.log(-1);
else
    console.log(ans.join(" "));
```

### Output
Input

5

1 2 2 3 4

4

2 2 4 6

Output

2 4

# Time Complexity
O(N + M)

# Space Complexity
O(1) (excluding the output array)

</approaches>




