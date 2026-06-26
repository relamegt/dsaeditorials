# Median of Two Sorted Arrays - Solution

## Problem Statement

Given two sorted arrays `arr1` and `arr2` of sizes `N` and `M` respectively, find the median of the combined sorted array.

- If the total number of elements is odd, the median is the middle element.
- If the total number of elements is even, the median is the average of the two middle elements.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing `arr1`

Third line: Integer `M`

Fourth line: `M` space-separated integers representing `arr2`

## Output Format

Print the median.

- If the median is an integer value, print it without trailing decimal zeros.
- Otherwise, print it as a decimal value ending in `.5`.

## Explanation

There are three approaches to solve this problem.

- **Approach 1:** Merge Both Arrays
- **Approach 2:** Two Pointers Without Extra Space
- **Approach 3:** Binary Search (Optimal)

For example,

Input

2

1 3

1

2

Output

2

<approaches>
## Approach 1: Merge Both Arrays

### Algorithm

1. Merge both sorted arrays into a single sorted array.
2. Find the total number of elements.
3. If the total count is odd, print the middle element.
4. Otherwise, print the average of the two middle elements.

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

    int merged[n+m];

    int i=0,j=0,k=0;

    while(i<n && j<m)
    {
        if(arr1[i]<=arr2[j])
            merged[k++]=arr1[i++];
        else
            merged[k++]=arr2[j++];
    }

    while(i<n)
        merged[k++]=arr1[i++];

    while(j<m)
        merged[k++]=arr2[j++];

    int total=n+m;

    if(total%2)
        printf("%d",merged[total/2]);
    else
    {
        int a=merged[total/2-1];
        int b=merged[total/2];

        if((a+b)%2==0)
            printf("%d",(a+b)/2);
        else
            printf("%.1f",(a+b)/2.0);
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

    int total=n+m;

    if(total%2)
        cout<<merged[total/2];
    else
    {
        int a=merged[total/2-1];
        int b=merged[total/2];

        if((a+b)%2==0)
            cout<<(a+b)/2;
        else
            cout<<(a+b)/2.0;
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

        int[] merged=new int[n+m];

        int i=0,j=0,k=0;

        while(i<n && j<m)
        {
            if(arr1[i]<=arr2[j])
                merged[k++]=arr1[i++];
            else
                merged[k++]=arr2[j++];
        }

        while(i<n)
            merged[k++]=arr1[i++];

        while(j<m)
            merged[k++]=arr2[j++];

        int total=n+m;

        if(total%2==1)
            System.out.print(merged[total/2]);
        else
        {
            int a=merged[total/2-1];
            int b=merged[total/2];

            if((a+b)%2==0)
                System.out.print((a+b)/2);
            else
                System.out.print((a+b)/2.0);
        }
    }
}
```
```Python
n = int(input())

arr1 = list(map(int, input().split()))

m = int(input())

arr2 = list(map(int, input().split()))

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

total = n + m

if total % 2 == 1:
    print(merged[total // 2])
else:
    s = merged[total // 2 - 1] + merged[total // 2]

    if s % 2 == 0:
        print(s // 2)
    else:
        print(s / 2)
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

        int total = n + m;

        if (total % 2 == 1)
            Console.Write(merged[total / 2]);
        else
        {
            int sum = merged[total / 2 - 1] + merged[total / 2];

            if (sum % 2 == 0)
                Console.Write(sum / 2);
            else
                Console.Write(sum / 2.0);
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

const total = n + m;

if (total % 2 === 1)
{
    console.log(merged[Math.floor(total / 2)]);
}
else
{
    const sum = merged[total / 2 - 1] + merged[total / 2];

    if (sum % 2 === 0)
        console.log(sum / 2);
    else
        console.log((sum / 2).toFixed(1));
}
```

### Output
Input

2

1 3

1

2

Output

2

# Time Complexity
O(N + M)

# Space Complexity
O(N + M)

## Approach 2: Two Pointers Without Extra Space

### Algorithm

1. Find the total number of elements.
2. Traverse both arrays using two pointers as if merging them.
3. Keep track of only the current and previous merged elements.
4. When the middle position(s) are reached, compute the median.
5. Print the answer.

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

    int total = n + m;
    int mid1 = (total - 1) / 2;
    int mid2 = total / 2;

    int i = 0, j = 0;
    int count = -1;
    int prev = 0, curr = 0;

    while(i < n || j < m)
    {
        prev = curr;

        if(j == m || (i < n && arr1[i] <= arr2[j]))
            curr = arr1[i++];
        else
            curr = arr2[j++];

        count++;

        if(count == mid2)
            break;
    }

    if(total % 2)
        printf("%d", curr);
    else
    {
        int sum = prev + curr;

        if(sum % 2 == 0)
            printf("%d", sum / 2);
        else
            printf("%.1f", sum / 2.0);
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

    int total = n + m;
    int mid2 = total / 2;

    int i = 0, j = 0;
    int count = -1;
    int prev = 0, curr = 0;

    while(i < n || j < m)
    {
        prev = curr;

        if(j == m || (i < n && arr1[i] <= arr2[j]))
            curr = arr1[i++];
        else
            curr = arr2[j++];

        count++;

        if(count == mid2)
            break;
    }

    if(total % 2)
        cout << curr;
    else
    {
        int sum = prev + curr;

        if(sum % 2 == 0)
            cout << sum / 2;
        else
            cout << sum / 2.0;
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
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        int[] arr1 = new int[n];
        for(int i = 0; i < n; i++)
            arr1[i] = sc.nextInt();

        int m = sc.nextInt();

        int[] arr2 = new int[m];
        for(int i = 0; i < m; i++)
            arr2[i] = sc.nextInt();

        int total = n + m;
        int mid2 = total / 2;

        int i = 0, j = 0;
        int count = -1;
        int prev = 0, curr = 0;

        while(i < n || j < m)
        {
            prev = curr;

            if(j == m || (i < n && arr1[i] <= arr2[j]))
                curr = arr1[i++];
            else
                curr = arr2[j++];

            count++;

            if(count == mid2)
                break;
        }

        if(total % 2 == 1)
            System.out.print(curr);
        else
        {
            int sum = prev + curr;

            if(sum % 2 == 0)
                System.out.print(sum / 2);
            else
                System.out.print(sum / 2.0);
        }
    }
}
```
```Python
n = int(input())

arr1 = list(map(int, input().split()))

m = int(input())

arr2 = list(map(int, input().split()))

total = n + m

mid1 = (total - 1) // 2
mid2 = total // 2

i = 0
j = 0
count = -1

prev = 0
curr = 0

while i < n or j < m:

    prev = curr

    if j == m or (i < n and arr1[i] <= arr2[j]):
        curr = arr1[i]
        i += 1
    else:
        curr = arr2[j]
        j += 1

    count += 1

    if count == mid2:
        break

if total % 2 == 1:
    print(curr)
else:
    s = prev + curr

    if s % 2 == 0:
        print(s // 2)
    else:
        print(s / 2)
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

        int total = n + m;

        int mid2 = total / 2;

        int i = 0;
        int j = 0;
        int count = -1;

        int prev = 0;
        int curr = 0;

        while (i < n || j < m)
        {
            prev = curr;

            if (j == m || (i < n && arr1[i] <= arr2[j]))
                curr = arr1[i++];
            else
                curr = arr2[j++];

            count++;

            if (count == mid2)
                break;
        }

        if (total % 2 == 1)
        {
            Console.Write(curr);
        }
        else
        {
            int sum = prev + curr;

            if (sum % 2 == 0)
                Console.Write(sum / 2);
            else
                Console.Write(sum / 2.0);
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

const total = n + m;

const mid2 = Math.floor(total / 2);

let i = 0;
let j = 0;
let count = -1;

let prev = 0;
let curr = 0;

while (i < n || j < m)
{
    prev = curr;

    if (j === m || (i < n && arr1[i] <= arr2[j]))
        curr = arr1[i++];
    else
        curr = arr2[j++];

    count++;

    if (count === mid2)
        break;
}

if (total % 2 === 1)
{
    console.log(curr);
}
else
{
    const sum = prev + curr;

    if (sum % 2 === 0)
        console.log(sum / 2);
    else
        console.log((sum / 2).toFixed(1));
}
```

### Output
Input

2

1 3

1

2

Output

2

# Time Complexity
O(N + M)

# Space Complexity
O(1)

## Approach 3: Binary Search (Optimal)

### Algorithm

1. Always perform binary search on the smaller array.
2. Partition both arrays such that the left halves together contain half of the total elements.
3. Check whether the partition is valid:

- Left maximum of both arrays is less than or equal to the right minimum of both arrays.

1. If valid:

- For an odd total number of elements, return the maximum element on the left.
- For an even total number of elements, return the average of the maximum left and minimum right.

1. Otherwise, adjust the binary search range and repeat.

```C
#include <stdio.h>
#include <limits.h>

int max(int a,int b)
{
    return a>b?a:b;
}

int min(int a,int b)
{
    return a<b?a:b;
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

    if(n>m)
    {
        int *t=arr1;
        arr1[0]=arr1[0];
    }

    if(n>m)
    {
        int tempSize=n;
        n=m;
        m=tempSize;

        int temp[m];
        for(int i=0;i<m;i++)
            temp[i]=arr2[i];

        for(int i=0;i<n;i++)
            arr2[i]=arr1[i];

        for(int i=0;i<m;i++)
            arr1[i]=temp[i];
    }

    int low=0;
    int high=n;
    int total=n+m;

    while(low<=high)
    {
        int cut1=(low+high)/2;
        int cut2=(total+1)/2-cut1;

        int l1=(cut1==0)?INT_MIN:arr1[cut1-1];
        int l2=(cut2==0)?INT_MIN:arr2[cut2-1];

        int r1=(cut1==n)?INT_MAX:arr1[cut1];
        int r2=(cut2==m)?INT_MAX:arr2[cut2];

        if(l1<=r2 && l2<=r1)
        {
            if(total%2)
            {
                printf("%d",max(l1,l2));
            }
            else
            {
                int a=max(l1,l2);
                int b=min(r1,r2);

                if((a+b)%2==0)
                    printf("%d",(a+b)/2);
                else
                    printf("%.1f",(a+b)/2.0);
            }

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

    if(n>m)
    {
        swap(arr1,arr2);
        swap(n,m);
    }

    int low=0;
    int high=n;
    int total=n+m;

    while(low<=high)
    {
        int cut1=(low+high)/2;
        int cut2=(total+1)/2-cut1;

        int l1=(cut1==0)?INT_MIN:arr1[cut1-1];
        int l2=(cut2==0)?INT_MIN:arr2[cut2-1];

        int r1=(cut1==n)?INT_MAX:arr1[cut1];
        int r2=(cut2==m)?INT_MAX:arr2[cut2];

        if(l1<=r2 && l2<=r1)
        {
            if(total%2)
            {
                cout<<max(l1,l2);
            }
            else
            {
                int a=max(l1,l2);
                int b=min(r1,r2);

                if((a+b)%2==0)
                    cout<<(a+b)/2;
                else
                    cout<<(a+b)/2.0;
            }

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

        if(n>m)
        {
            int[] temp=arr1;
            arr1=arr2;
            arr2=temp;

            int t=n;
            n=m;
            m=t;
        }

        int low=0;
        int high=n;
        int total=n+m;

        while(low<=high)
        {
            int cut1=(low+high)/2;
            int cut2=(total+1)/2-cut1;

            int l1=(cut1==0)?Integer.MIN_VALUE:arr1[cut1-1];
            int l2=(cut2==0)?Integer.MIN_VALUE:arr2[cut2-1];

            int r1=(cut1==n)?Integer.MAX_VALUE:arr1[cut1];
            int r2=(cut2==m)?Integer.MAX_VALUE:arr2[cut2];

            if(l1<=r2 && l2<=r1)
            {
                if(total%2==1)
                {
                    System.out.print(Math.max(l1,l2));
                }
                else
                {
                    int a=Math.max(l1,l2);
                    int b=Math.min(r1,r2);

                    if((a+b)%2==0)
                        System.out.print((a+b)/2);
                    else
                        System.out.print((a+b)/2.0);
                }

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

if n > m:
    arr1, arr2 = arr2, arr1
    n, m = m, n

low = 0
high = n
total = n + m

while low <= high:

    cut1 = (low + high) // 2
    cut2 = (total + 1) // 2 - cut1

    l1 = float("-inf") if cut1 == 0 else arr1[cut1 - 1]
    l2 = float("-inf") if cut2 == 0 else arr2[cut2 - 1]

    r1 = float("inf") if cut1 == n else arr1[cut1]
    r2 = float("inf") if cut2 == m else arr2[cut2]

    if l1 <= r2 and l2 <= r1:

        if total % 2 == 1:
            print(max(l1, l2))
        else:
            s = max(l1, l2) + min(r1, r2)

            if s % 2 == 0:
                print(s // 2)
            else:
                print(s / 2)
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

        if (n > m)
        {
            (arr1, arr2) = (arr2, arr1);
            (n, m) = (m, n);
        }

        int low = 0;
        int high = n;
        int total = n + m;

        while (low <= high)
        {
            int cut1 = (low + high) / 2;
            int cut2 = (total + 1) / 2 - cut1;

            int l1 = cut1 == 0 ? int.MinValue : arr1[cut1 - 1];
            int l2 = cut2 == 0 ? int.MinValue : arr2[cut2 - 1];

            int r1 = cut1 == n ? int.MaxValue : arr1[cut1];
            int r2 = cut2 == m ? int.MaxValue : arr2[cut2];

            if (l1 <= r2 && l2 <= r1)
            {
                if (total % 2 == 1)
                {
                    Console.Write(Math.Max(l1, l2));
                }
                else
                {
                    int sum = Math.Max(l1, l2) + Math.Min(r1, r2);

                    if (sum % 2 == 0)
                        Console.Write(sum / 2);
                    else
                        Console.Write(sum / 2.0);
                }

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

if (n > m)
{
    [arr1, arr2] = [arr2, arr1];
    [n, m] = [m, n];
}

let low = 0;
let high = n;
const total = n + m;

while (low <= high)
{
    const cut1 = Math.floor((low + high) / 2);
    const cut2 = Math.floor((total + 1) / 2) - cut1;

    const l1 = cut1 === 0 ? -Infinity : arr1[cut1 - 1];
    const l2 = cut2 === 0 ? -Infinity : arr2[cut2 - 1];

    const r1 = cut1 === n ? Infinity : arr1[cut1];
    const r2 = cut2 === m ? Infinity : arr2[cut2];

    if (l1 <= r2 && l2 <= r1)
    {
        if (total % 2 === 1)
        {
            console.log(Math.max(l1, l2));
        }
        else
        {
            const sum = Math.max(l1, l2) + Math.min(r1, r2);

            if (sum % 2 === 0)
                console.log(sum / 2);
            else
                console.log((sum / 2).toFixed(1));
        }

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

2

1 3

1

2

Output

2

# Time Complexity
O(log(min(N, M)))

# Space Complexity
O(1)

</approaches>




