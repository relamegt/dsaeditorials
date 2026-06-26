# Sort an Array of 0s and 1s - Solution

## Problem Statement

Given an array `arr` of size `N` containing only `0`s and `1`s, sort the array in non-decreasing order.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing `arr`

## Output Format

Print the sorted array as `N` space-separated integers.

## Explanation

There are three approaches to solve this problem.

- **Approach 1:** Sorting
- **Approach 2:** Counting 0s and 1s
- **Approach 3:** Two Pointers (Optimal)

For example,

Input

5

0 1 1 0 1

Output

0 0 1 1 1

<approaches>
## Approach 1: Sorting

### Algorithm

1. Read the array.
2. Sort the array in non-decreasing order.
3. Print the sorted array.

```C
#include <stdio.h>
#include <stdlib.h>

int cmp(const void *a,const void *b)
{
    return (*(int*)a-*(int*)b);
}

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    qsort(arr,n,sizeof(int),cmp);

    for(int i=0;i<n;i++)
        printf("%d ",arr[i]);

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

    for(int x:arr)
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

        int[] arr=new int[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextInt();

        Arrays.sort(arr);

        for(int x:arr)
            System.out.print(x+" ");
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

arr.sort()

print(*arr)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        int[] arr=Array.ConvertAll(Console.ReadLine().Split(),int.Parse);

        Array.Sort(arr);

        Console.WriteLine(string.Join(" ",arr));
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const arr=[];

for(let i=0;i<n;i++)
    arr.push(input[idx++]);

arr.sort((a,b)=>a-b);

console.log(arr.join(" "));
```

### Output
Input

5

0 1 1 0 1

Output

0 0 1 1 1

# Time Complexity
O(N log N)

# Space Complexity
O(1) (excluding sorting space used by the language implementation)

## Approach 2: Counting 0s and 1s

### Algorithm

1. Traverse the array and count the number of `0`s.
2. Fill the first `count0` positions with `0`.
3. Fill the remaining positions with `1`.
4. Print the array.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];
    int count0=0;

    for(int i=0;i<n;i++)
    {
        scanf("%d",&arr[i]);

        if(arr[i]==0)
            count0++;
    }

    for(int i=0;i<count0;i++)
        arr[i]=0;

    for(int i=count0;i<n;i++)
        arr[i]=1;

    for(int i=0;i<n;i++)
        printf("%d ",arr[i]);

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

    int count0=0;

    for(int i=0;i<n;i++)
    {
        cin>>arr[i];

        if(arr[i]==0)
            count0++;
    }

    for(int i=0;i<count0;i++)
        arr[i]=0;

    for(int i=count0;i<n;i++)
        arr[i]=1;

    for(int x:arr)
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

        int[] arr=new int[n];

        int count0=0;

        for(int i=0;i<n;i++)
        {
            arr[i]=sc.nextInt();

            if(arr[i]==0)
                count0++;
        }

        for(int i=0;i<count0;i++)
            arr[i]=0;

        for(int i=count0;i<n;i++)
            arr[i]=1;

        for(int x:arr)
            System.out.print(x+" ");
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

count0=arr.count(0)

for i in range(count0):
    arr[i]=0

for i in range(count0,n):
    arr[i]=1

print(*arr)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        int[] arr=Array.ConvertAll(Console.ReadLine().Split(),int.Parse);

        int count0=0;

        foreach(int x in arr)
        {
            if(x==0)
                count0++;
        }

        for(int i=0;i<count0;i++)
            arr[i]=0;

        for(int i=count0;i<n;i++)
            arr[i]=1;

        Console.WriteLine(string.Join(" ",arr));
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const arr=[];

let count0=0;

for(let i=0;i<n;i++)
{
    arr.push(input[idx]);

    if(input[idx]===0)
        count0++;

    idx++;
}

for(let i=0;i<count0;i++)
    arr[i]=0;

for(let i=count0;i<n;i++)
    arr[i]=1;

console.log(arr.join(" "));
```

### Output
Input

5

0 1 1 0 1

Output

0 0 1 1 1

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 3: Two Pointers (Optimal)

### Algorithm

1. Initialize two pointers:

- `left = 0`
- `right = N - 1`

1. Move `left` forward while it points to `0`.
2. Move `right` backward while it points to `1`.
3. If `left < right`, swap the elements.
4. Repeat until `left >= right`.
5. Print the sorted array.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    int left=0;
    int right=n-1;

    while(left<right)
    {
        while(left<right && arr[left]==0)
            left++;

        while(left<right && arr[right]==1)
            right--;

        if(left<right)
        {
            int temp=arr[left];
            arr[left]=arr[right];
            arr[right]=temp;

            left++;
            right--;
        }
    }

    for(int i=0;i<n;i++)
        printf("%d ",arr[i]);

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

    int left=0;
    int right=n-1;

    while(left<right)
    {
        while(left<right && arr[left]==0)
            left++;

        while(left<right && arr[right]==1)
            right--;

        if(left<right)
        {
            swap(arr[left],arr[right]);
            left++;
            right--;
        }
    }

    for(int x:arr)
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

        int[] arr=new int[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextInt();

        int left=0;
        int right=n-1;

        while(left<right)
        {
            while(left<right && arr[left]==0)
                left++;

            while(left<right && arr[right]==1)
                right--;

            if(left<right)
            {
                int temp=arr[left];
                arr[left]=arr[right];
                arr[right]=temp;

                left++;
                right--;
            }
        }

        for(int x:arr)
            System.out.print(x+" ");
    }
}
```
```Python
n = int(input())

arr = list(map(int, input().split()))

left = 0
right = n - 1

while left < right:

    while left < right and arr[left] == 0:
        left += 1

    while left < right and arr[right] == 1:
        right -= 1

    if left < right:
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1

print(*arr)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int left = 0;
        int right = n - 1;

        while (left < right)
        {
            while (left < right && arr[left] == 0)
                left++;

            while (left < right && arr[right] == 1)
                right--;

            if (left < right)
            {
                int temp = arr[left];
                arr[left] = arr[right];
                arr[right] = temp;

                left++;
                right--;
            }
        }

        Console.WriteLine(string.Join(" ", arr));
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const arr = [];

for (let i = 0; i < n; i++)
    arr.push(input[idx++]);

let left = 0;
let right = n - 1;

while (left < right)
{
    while (left < right && arr[left] === 0)
        left++;

    while (left < right && arr[right] === 1)
        right--;

    if (left < right)
    {
        [arr[left], arr[right]] = [arr[right], arr[left]];
        left++;
        right--;
    }
}

console.log(arr.join(" "));
```

### Output
Input

5

0 1 1 0 1

Output

0 0 1 1 1

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




