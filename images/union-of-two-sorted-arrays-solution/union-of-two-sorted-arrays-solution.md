# Union of Two Sorted Arrays - Solution

## Problem Statement

Given two sorted arrays `arr1` and `arr2` of sizes `N` and `M` respectively, find their union.

The output must contain all distinct elements present in either array, in sorted order.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing `arr1`

Third line: Integer `M`

Fourth line: `M` space-separated integers representing `arr2`

## Output Format

Print the union as space-separated integers in sorted order.

## Explanation

There are two approaches to solve this problem.

- **Approach 1:** Hash Set
- **Approach 2:** Two Pointers (Optimal)

For example,

Input

5

1 2 2 3 4

4

2 4 4 6

Output

1 2 3 4 6

<approaches>
## Approach 1: Hash Set

### Algorithm

1. Read both arrays.
2. Insert all elements from both arrays into a hash set.
3. Convert the set into a sorted list.
4. Print all elements in sorted order.

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

    int ans[n+m];
    int k=0;

    for(int i=0;i<n;i++)
    {
        int found=0;

        for(int j=0;j<k;j++)
        {
            if(ans[j]==arr1[i])
            {
                found=1;
                break;
            }
        }

        if(!found)
            ans[k++]=arr1[i];
    }

    for(int i=0;i<m;i++)
    {
        int found=0;

        for(int j=0;j<k;j++)
        {
            if(ans[j]==arr2[i])
            {
                found=1;
                break;
            }
        }

        if(!found)
            ans[k++]=arr2[i];
    }

    qsort(ans,k,sizeof(int),cmp);

    for(int i=0;i<k;i++)
        printf("%d ",ans[i]);

    return 0;
}
```
```cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
    int n,m;
    cin>>n;

    set<int> s;

    for(int i=0;i<n;i++)
    {
        int x;
        cin>>x;
        s.insert(x);
    }

    cin>>m;

    for(int i=0;i<m;i++)
    {
        int x;
        cin>>x;
        s.insert(x);
    }

    for(int x:s)
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

        TreeSet<Integer> set=new TreeSet<>();

        for(int i=0;i<n;i++)
            set.add(sc.nextInt());

        int m=sc.nextInt();

        for(int i=0;i<m;i++)
            set.add(sc.nextInt());

        for(int x:set)
            System.out.print(x+" ");
    }
}
```
```Python
n = int(input())

arr1 = list(map(int, input().split()))

m = int(input())

arr2 = list(map(int, input().split()))

ans = sorted(set(arr1) | set(arr2))

print(*ans)
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

        SortedSet<long> set = new SortedSet<long>();

        foreach (long x in arr1)
            set.Add(x);

        foreach (long x in arr2)
            set.Add(x);

        foreach (long x in set)
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

const ans = [...new Set([...arr1, ...arr2])].sort((a, b) => a - b);

console.log(ans.join(" "));
```

### Output
Input

5

1 2 2 3 4

4

2 4 4 6

Output

1 2 3 4 6

# Time Complexity
O((N + M) * log(N + M))

# Space Complexity
O(N + M)

## Approach 2: Two Pointers (Optimal)

### Algorithm

1. Initialize two pointers `i` and `j` at the beginning of both arrays.
2. Compare the current elements of both arrays.
3. Add the smaller element to the answer if it is not already added, then move the corresponding pointer.
4. If both elements are equal, add it once and move both pointers.
5. After one array is exhausted, add the remaining distinct elements from the other array.
6. Print the resulting union.

```C
#include <stdio.h>

int main()
{
    int n, m;
    scanf("%d", &n);

    int arr1[n];

    for(int i = 0; i < n; i++)
        scanf("%d", &arr1[i]);

    scanf("%d", &m);

    int arr2[m];

    for(int i = 0; i < m; i++)
        scanf("%d", &arr2[i]);

    int i = 0, j = 0;
    int first = 1;
    int last = 0;

    while(i < n && j < m)
    {
        int val;

        if(arr1[i] < arr2[j])
            val = arr1[i++];
        else if(arr1[i] > arr2[j])
            val = arr2[j++];
        else
        {
            val = arr1[i];
            i++;
            j++;
        }

        if(first || val != last)
        {
            printf("%d ", val);
            last = val;
            first = 0;
        }
    }

    while(i < n)
    {
        if(first || arr1[i] != last)
        {
            printf("%d ", arr1[i]);
            last = arr1[i];
            first = 0;
        }
        i++;
    }

    while(j < m)
    {
        if(first || arr2[j] != last)
        {
            printf("%d ", arr2[j]);
            last = arr2[j];
            first = 0;
        }
        j++;
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
    int n, m;
    cin >> n;

    vector<int> arr1(n);

    for(int i = 0; i < n; i++)
        cin >> arr1[i];

    cin >> m;

    vector<int> arr2(m);

    for(int i = 0; i < m; i++)
        cin >> arr2[i];

    int i = 0, j = 0;
    vector<int> ans;

    while(i < n && j < m)
    {
        if(arr1[i] < arr2[j])
        {
            if(ans.empty() || ans.back() != arr1[i])
                ans.push_back(arr1[i]);
            i++;
        }
        else if(arr1[i] > arr2[j])
        {
            if(ans.empty() || ans.back() != arr2[j])
                ans.push_back(arr2[j]);
            j++;
        }
        else
        {
            if(ans.empty() || ans.back() != arr1[i])
                ans.push_back(arr1[i]);
            i++;
            j++;
        }
    }

    while(i < n)
    {
        if(ans.empty() || ans.back() != arr1[i])
            ans.push_back(arr1[i]);
        i++;
    }

    while(j < m)
    {
        if(ans.empty() || ans.back() != arr2[j])
            ans.push_back(arr2[j]);
        j++;
    }

    for(int x : ans)
        cout << x << " ";

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        int[] arr1 = new int[n];

        for(int i = 0; i < n; i++)
            arr1[i] = sc.nextInt();

        int m = sc.nextInt();

        int[] arr2 = new int[m];

        for(int i = 0; i < m; i++)
            arr2[i] = sc.nextInt();

        int i = 0, j = 0;

        ArrayList<Integer> ans = new ArrayList<>();

        while(i < n && j < m)
        {
            if(arr1[i] < arr2[j])
            {
                if(ans.isEmpty() || ans.get(ans.size() - 1) != arr1[i])
                    ans.add(arr1[i]);
                i++;
            }
            else if(arr1[i] > arr2[j])
            {
                if(ans.isEmpty() || ans.get(ans.size() - 1) != arr2[j])
                    ans.add(arr2[j]);
                j++;
            }
            else
            {
                if(ans.isEmpty() || ans.get(ans.size() - 1) != arr1[i])
                    ans.add(arr1[i]);
                i++;
                j++;
            }
        }

        while(i < n)
        {
            if(ans.isEmpty() || ans.get(ans.size() - 1) != arr1[i])
                ans.add(arr1[i]);
            i++;
        }

        while(j < m)
        {
            if(ans.isEmpty() || ans.get(ans.size() - 1) != arr2[j])
                ans.add(arr2[j]);
            j++;
        }

        for(int x : ans)
            System.out.print(x + " ");
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

    if arr1[i] < arr2[j]:
        if not ans or ans[-1] != arr1[i]:
            ans.append(arr1[i])
        i += 1

    elif arr1[i] > arr2[j]:
        if not ans or ans[-1] != arr2[j]:
            ans.append(arr2[j])
        j += 1

    else:
        if not ans or ans[-1] != arr1[i]:
            ans.append(arr1[i])
        i += 1
        j += 1

while i < n:
    if not ans or ans[-1] != arr1[i]:
        ans.append(arr1[i])
    i += 1

while j < m:
    if not ans or ans[-1] != arr2[j]:
        ans.append(arr2[j])
    j += 1

print(*ans)
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
            if (arr1[i] < arr2[j])
            {
                if (ans.Count == 0 || ans[ans.Count - 1] != arr1[i])
                    ans.Add(arr1[i]);
                i++;
            }
            else if (arr1[i] > arr2[j])
            {
                if (ans.Count == 0 || ans[ans.Count - 1] != arr2[j])
                    ans.Add(arr2[j]);
                j++;
            }
            else
            {
                if (ans.Count == 0 || ans[ans.Count - 1] != arr1[i])
                    ans.Add(arr1[i]);
                i++;
                j++;
            }
        }

        while (i < n)
        {
            if (ans.Count == 0 || ans[ans.Count - 1] != arr1[i])
                ans.Add(arr1[i]);
            i++;
        }

        while (j < m)
        {
            if (ans.Count == 0 || ans[ans.Count - 1] != arr2[j])
                ans.Add(arr2[j]);
            j++;
        }

        Console.WriteLine(string.Join(" ", ans));
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
    if (arr1[i] < arr2[j])
    {
        if (ans.length === 0 || ans[ans.length - 1] !== arr1[i])
            ans.push(arr1[i]);
        i++;
    }
    else if (arr1[i] > arr2[j])
    {
        if (ans.length === 0 || ans[ans.length - 1] !== arr2[j])
            ans.push(arr2[j]);
        j++;
    }
    else
    {
        if (ans.length === 0 || ans[ans.length - 1] !== arr1[i])
            ans.push(arr1[i]);
        i++;
        j++;
    }
}

while (i < n)
{
    if (ans.length === 0 || ans[ans.length - 1] !== arr1[i])
        ans.push(arr1[i]);
    i++;
}

while (j < m)
{
    if (ans.length === 0 || ans[ans.length - 1] !== arr2[j])
        ans.push(arr2[j]);
    j++;
}

console.log(ans.join(" "));
```

### Output
Input

5

1 2 2 3 4

4

2 4 4 6

Output

1 2 3 4 6

# Time Complexity
O(N + M)

# Space Complexity
O(N + M)

</approaches>




