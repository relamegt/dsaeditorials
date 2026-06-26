# K-th Element of Two Sorted Arrays - Solution

## Problem Statement

Given two sorted arrays `arr1` and `arr2` of sizes `N` and `M` respectively, and an integer `K`, find the element that would appear at position `K` in the combined sorted array.

The position `K` is **1-based**.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing `arr1`

Third line: Integer `M`

Fourth line: `M` space-separated integers representing `arr2`

Fifth line: Integer `K`

## Output Format

Print a single integer representing the `K`-th element in the merged sorted order.

## Explanation

There are three approaches to solve this problem.

- **Approach 1:** Merge Both Arrays
- **Approach 2:** Two Pointers Without Extra Space
- **Approach 3:** Binary Search (Optimal)

For example,

Input

4

2 3 6 7

4

1 4 8 10

5

Output

6

<approaches>
## Approach 1: Merge Both Arrays

### Algorithm

1. Merge both sorted arrays into a single sorted array.
2. After merging, print the element at index `K - 1`.

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

    int k;
    scanf("%d",&k);

    int merged[n+m];

    int i=0,j=0,p=0;

    while(i<n && j<m)
    {
        if(arr1[i]<=arr2[j])
            merged[p++]=arr1[i++];
        else
            merged[p++]=arr2[j++];
    }

    while(i<n)
        merged[p++]=arr1[i++];

    while(j<m)
        merged[p++]=arr2[j++];

    printf("%d",merged[k-1]);

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

    int k;
    cin>>k;

    vector<int> merged;

    int i=0,j=0;

    while(i<n && j<m)
    {
        if(arr1[i]<=arr2[j])
            merged.push_back(arr1[i++]);
        else
            merged.push_back(arr2[j++]);
    }

    while(i<n)
        merged.push_back(arr1[i++]);

    while(j<m)
        merged.push_back(arr2[j++]);

    cout<<merged[k-1];

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

        int k=sc.nextInt();

        int[] merged=new int[n+m];

        int i=0,j=0,p=0;

        while(i<n && j<m)
        {
            if(arr1[i]<=arr2[j])
                merged[p++]=arr1[i++];
            else
                merged[p++]=arr2[j++];
        }

        while(i<n)
            merged[p++]=arr1[i++];

        while(j<m)
            merged[p++]=arr2[j++];

        System.out.print(merged[k-1]);
    }
}
```
```Python
n = int(input())

arr1 = list(map(int, input().split()))

m = int(input())

arr2 = list(map(int, input().split()))

k = int(input())

merged = []

i = 0
j = 0

while i < n and j < m:

    if arr1[i] <= arr2[j]:
        merged.append(arr1[i])
        i += 1
    else:
        merged.append(arr2[j])
        j += 1

while i < n:
    merged.append(arr1[i])
    i += 1

while j < m:
    merged.append(arr2[j])
    j += 1

print(merged[k - 1])
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr1 = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int m = int.Parse(Console.ReadLine());

        int[] arr2 = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int k = int.Parse(Console.ReadLine());

        List<int> merged = new List<int>();

        int i = 0;
        int j = 0;

        while (i < n && j < m)
        {
            if (arr1[i] <= arr2[j])
                merged.Add(arr1[i++]);
            else
                merged.Add(arr2[j++]);
        }

        while (i < n)
            merged.Add(arr1[i++]);

        while (j < m)
            merged.Add(arr2[j++]);

        Console.Write(merged[k - 1]);
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

const k = input[idx++];

const merged = [];

let i = 0;
let j = 0;

while (i < n && j < m)
{
    if (arr1[i] <= arr2[j])
        merged.push(arr1[i++]);
    else
        merged.push(arr2[j++]);
}

while (i < n)
    merged.push(arr1[i++]);

while (j < m)
    merged.push(arr2[j++]);

console.log(merged[k - 1]);
```

### Output
Input

4

2 3 6 7

4

1 4 8 10

5

Output

6

# Time Complexity
O(N + M)

# Space Complexity
O(N + M)

## Approach 2: Two Pointers Without Extra Space

### Algorithm

1. Initialize two pointers for both arrays.
2. Traverse both arrays as if merging them.
3. Maintain a counter for the merged position.
4. When the counter reaches `K`, print the current element.
5. No extra merged array is required.

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

    int k;
    scanf("%d",&k);

    int i=0,j=0,count=0;

    while(i<n || j<m)
    {
        int val;

        if(j==m || (i<n && arr1[i]<=arr2[j]))
            val=arr1[i++];
        else
            val=arr2[j++];

        count++;

        if(count==k)
        {
            printf("%d",val);
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
    int n,m;
    cin>>n;

    vector<int> arr1(n);

    for(int i=0;i<n;i++)
        cin>>arr1[i];

    cin>>m;

    vector<int> arr2(m);

    for(int i=0;i<m;i++)
        cin>>arr2[i];

    int k;
    cin>>k;

    int i=0,j=0,count=0;

    while(i<n || j<m)
    {
        int val;

        if(j==m || (i<n && arr1[i]<=arr2[j]))
            val=arr1[i++];
        else
            val=arr2[j++];

        count++;

        if(count==k)
        {
            cout<<val;
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

        int[] arr1=new int[n];

        for(int i=0;i<n;i++)
            arr1[i]=sc.nextInt();

        int m=sc.nextInt();

        int[] arr2=new int[m];

        for(int i=0;i<m;i++)
            arr2[i]=sc.nextInt();

        int k=sc.nextInt();

        int i=0,j=0,count=0;

        while(i<n || j<m)
        {
            int val;

            if(j==m || (i<n && arr1[i]<=arr2[j]))
                val=arr1[i++];
            else
                val=arr2[j++];

            count++;

            if(count==k)
            {
                System.out.print(val);
                break;
            }
        }
    }
}
```
```Python
n = int(input())

arr1 = list(map(int, input().split()))

m = int(input())

arr2 = list(map(int, input().split()))

k = int(input())

i = 0
j = 0
count = 0

while i < n or j < m:

    if j == m or (i < n and arr1[i] <= arr2[j]):
        val = arr1[i]
        i += 1
    else:
        val = arr2[j]
        j += 1

    count += 1

    if count == k:
        print(val)
        break
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr1 = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int m = int.Parse(Console.ReadLine());

        int[] arr2 = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int k = int.Parse(Console.ReadLine());

        int i = 0;
        int j = 0;
        int count = 0;

        while (i < n || j < m)
        {
            int val;

            if (j == m || (i < n && arr1[i] <= arr2[j]))
                val = arr1[i++];
            else
                val = arr2[j++];

            count++;

            if (count == k)
            {
                Console.Write(val);
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

const arr1 = [];

for (let i = 0; i < n; i++)
    arr1.push(input[idx++]);

const m = input[idx++];

const arr2 = [];

for (let i = 0; i < m; i++)
    arr2.push(input[idx++]);

const k = input[idx++];

let i = 0;
let j = 0;
let count = 0;

while (i < n || j < m)
{
    let val;

    if (j === m || (i < n && arr1[i] <= arr2[j]))
        val = arr1[i++];
    else
        val = arr2[j++];

    count++;

    if (count === k)
    {
        console.log(val);
        break;
    }
}
```

### Output
Input

4

2 3 6 7

4

1 4 8 10

5

Output

6

# Time Complexity
O(N + M)

# Space Complexity
O(1)

## Approach 3: Binary Search (Optimal)

### Algorithm

1. Always perform binary search on the smaller array.
2. Let `cut1` be the number of elements taken from the first array.
3. Let `cut2 = K - cut1` be the number of elements taken from the second array.
4. Check whether:

- `left1 <= right2`
- `left2 <= right1`

1. If the partition is valid, the answer is `max(left1, left2)`.
2. Otherwise, adjust the binary search range until the correct partition is found.

```C
#include <stdio.h>
#include <limits.h>

int max(int a,int b)
{
    return a>b?a:b;
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

    int k;
    scanf("%d",&k);

    if(n>m)
    {
        int temp[m];

        for(int i=0;i<m;i++)
            temp[i]=arr2[i];

        int tempN=n;

        n=m;
        m=tempN;

        for(int i=0;i<n;i++)
            arr2[i]=arr1[i];

        for(int i=0;i<m;i++)
            arr1[i]=temp[i];
    }

    int low=k-m>0?k-m:0;
    int high=k<n?k:n;

    while(low<=high)
    {
        int cut1=(low+high)/2;
        int cut2=k-cut1;

        int l1=cut1==0?INT_MIN:arr1[cut1-1];
        int l2=cut2==0?INT_MIN:arr2[cut2-1];

        int r1=cut1==n?INT_MAX:arr1[cut1];
        int r2=cut2==m?INT_MAX:arr2[cut2];

        if(l1<=r2 && l2<=r1)
        {
            printf("%d",max(l1,l2));
            return 0;
        }

        if(l1>r2)
            high=cut1-1;
        else
            low=cut1+1;
    }

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>
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

    int k;
    cin>>k;

    if(n>m)
    {
        swap(arr1,arr2);
        swap(n,m);
    }

    int low=max(0,k-m);
    int high=min(k,n);

    while(low<=high)
    {
        int cut1=(low+high)/2;
        int cut2=k-cut1;

        int l1=cut1==0?INT_MIN:arr1[cut1-1];
        int l2=cut2==0?INT_MIN:arr2[cut2-1];

        int r1=cut1==n?INT_MAX:arr1[cut1];
        int r2=cut2==m?INT_MAX:arr2[cut2];

        if(l1<=r2 && l2<=r1)
        {
            cout<<max(l1,l2);
            return 0;
        }

        if(l1>r2)
            high=cut1-1;
        else
            low=cut1+1;
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

        int[] arr1=new int[n];

        for(int i=0;i<n;i++)
            arr1[i]=sc.nextInt();

        int m=sc.nextInt();

        int[] arr2=new int[m];

        for(int i=0;i<m;i++)
            arr2[i]=sc.nextInt();

        int k=sc.nextInt();

        if(n>m)
        {
            int[] temp=arr1;
            arr1=arr2;
            arr2=temp;

            int t=n;
            n=m;
            m=t;
        }

        int low=Math.max(0,k-m);
        int high=Math.min(k,n);

        while(low<=high)
        {
            int cut1=(low+high)/2;
            int cut2=k-cut1;

            int l1=cut1==0?Integer.MIN_VALUE:arr1[cut1-1];
            int l2=cut2==0?Integer.MIN_VALUE:arr2[cut2-1];

            int r1=cut1==n?Integer.MAX_VALUE:arr1[cut1];
            int r2=cut2==m?Integer.MAX_VALUE:arr2[cut2];

            if(l1<=r2 && l2<=r1)
            {
                System.out.print(Math.max(l1,l2));
                return;
            }

            if(l1>r2)
                high=cut1-1;
            else
                low=cut1+1;
        }
    }
}
```
```Python
n = int(input())

arr1 = list(map(int, input().split()))

m = int(input())

arr2 = list(map(int, input().split()))

k = int(input())

if n > m:
    arr1, arr2 = arr2, arr1
    n, m = m, n

low = max(0, k - m)
high = min(k, n)

while low <= high:

    cut1 = (low + high) // 2
    cut2 = k - cut1

    l1 = float("-inf") if cut1 == 0 else arr1[cut1 - 1]
    l2 = float("-inf") if cut2 == 0 else arr2[cut2 - 1]

    r1 = float("inf") if cut1 == n else arr1[cut1]
    r2 = float("inf") if cut2 == m else arr2[cut2]

    if l1 <= r2 and l2 <= r1:
        print(max(l1, l2))
        break

    elif l1 > r2:
        high = cut1 - 1
    else:
        low = cut1 + 1
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr1 = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int m = int.Parse(Console.ReadLine());

        int[] arr2 = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int k = int.Parse(Console.ReadLine());

        if (n > m)
        {
            (arr1, arr2) = (arr2, arr1);
            (n, m) = (m, n);
        }

        int low = Math.Max(0, k - m);
        int high = Math.Min(k, n);

        while (low <= high)
        {
            int cut1 = (low + high) / 2;
            int cut2 = k - cut1;

            int l1 = cut1 == 0 ? int.MinValue : arr1[cut1 - 1];
            int l2 = cut2 == 0 ? int.MinValue : arr2[cut2 - 1];

            int r1 = cut1 == n ? int.MaxValue : arr1[cut1];
            int r2 = cut2 == m ? int.MaxValue : arr2[cut2];

            if (l1 <= r2 && l2 <= r1)
            {
                Console.Write(Math.Max(l1, l2));
                return;
            }

            if (l1 > r2)
                high = cut1 - 1;
            else
                low = cut1 + 1;
        }
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

let n = input[idx++];

let arr1 = [];

for (let i = 0; i < n; i++)
    arr1.push(input[idx++]);

let m = input[idx++];

let arr2 = [];

for (let i = 0; i < m; i++)
    arr2.push(input[idx++]);

const k = input[idx++];

if (n > m)
{
    [arr1, arr2] = [arr2, arr1];
    [n, m] = [m, n];
}

let low = Math.max(0, k - m);
let high = Math.min(k, n);

while (low <= high)
{
    const cut1 = Math.floor((low + high) / 2);
    const cut2 = k - cut1;

    const l1 = cut1 === 0 ? -Infinity : arr1[cut1 - 1];
    const l2 = cut2 === 0 ? -Infinity : arr2[cut2 - 1];

    const r1 = cut1 === n ? Infinity : arr1[cut1];
    const r2 = cut2 === m ? Infinity : arr2[cut2];

    if (l1 <= r2 && l2 <= r1)
    {
        console.log(Math.max(l1, l2));
        break;
    }

    if (l1 > r2)
        high = cut1 - 1;
    else
        low = cut1 + 1;
}
```

### Output
Input

4

2 3 6 7

4

1 4 8 10

5

Output

6

# Time Complexity
O(log(min(N, M)))

# Space Complexity
O(1)

</approaches>




