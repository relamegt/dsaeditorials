# Count Indices to Balance Even and Odd Sums - Solution

## Problem Statement

Given an array `arr[]`, count the number of indices such that deleting the element at that index and shifting all elements after it one position left results in an array where the sum of elements at even indices equals the sum at odd indices.

## Input Format

First line: Integer `n`

Second line: `n` space-separated integers

## Output Format

Print a single integer representing the count of valid indices.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Remove every element one by one and recompute even and odd index sums.
- **Prefix and Suffix Sums (Optimal):** Maintain prefix and suffix sums for even and odd indices to evaluate each removal in constant time.

For example,

Input

4

2 1 6 4

Output

1

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. For every index:

- Remove that element conceptually.
- Traverse the remaining array.
- Compute sums at even and odd indices after shifting.

1. If both sums are equal, increment the answer.
2. Print the answer.

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

    for(int remove=0;remove<n;remove++)
    {
        int even=0;
        int odd=0;
        int index=0;

        for(int i=0;i<n;i++)
        {
            if(i==remove)
                continue;

            if(index%2==0)
                even+=arr[i];
            else
                odd+=arr[i];

            index++;
        }

        if(even==odd)
            ans++;
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

    for(int remove=0;remove<n;remove++)
    {
        int even=0;
        int odd=0;
        int index=0;

        for(int i=0;i<n;i++)
        {
            if(i==remove)
                continue;

            if(index%2==0)
                even+=arr[i];
            else
                odd+=arr[i];

            index++;
        }

        if(even==odd)
            ans++;
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

        for(int remove=0;remove<n;remove++)
        {
            int even=0;
            int odd=0;
            int index=0;

            for(int i=0;i<n;i++)
            {
                if(i==remove)
                    continue;

                if(index%2==0)
                    even+=arr[i];
                else
                    odd+=arr[i];

                index++;
            }

            if(even==odd)
                ans++;
        }

        System.out.print(ans);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

ans=0

for remove in range(n):

    even=0
    odd=0
    index=0

    for i in range(n):

        if i==remove:
            continue

        if index%2==0:
            even+=arr[i]
        else:
            odd+=arr[i]

        index+=1

    if even==odd:
        ans+=1

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

        for(int remove = 0; remove < n; remove++)
        {
            int even = 0;
            int odd = 0;
            int index = 0;

            for(int i = 0; i < n; i++)
            {
                if(i == remove)
                    continue;

                if(index % 2 == 0)
                    even += arr[i];
                else
                    odd += arr[i];

                index++;
            }

            if(even == odd)
                ans++;
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

for(let remove = 0; remove < n; remove++)
{
    let even = 0;
    let odd = 0;
    let index = 0;

    for(let i = 0; i < n; i++)
    {
        if(i === remove)
            continue;

        if(index % 2 === 0)
            even += arr[i];
        else
            odd += arr[i];

        index++;
    }

    if(even === odd)
        ans++;
}

console.log(ans);
```

### Output
Input

4

2 1 6 4

Output

1

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Prefix and Suffix Sums (Optimal)

### Algorithm

1. Compute the total sum of elements at even indices and odd indices.
2. Initialize prefix sums for even and odd positions as `0`.
3. Traverse the array from left to right.
4. For each index:

- Remove the current element.
- Elements after the removed index shift one position left, so their parity changes.
- Compute:
- New even sum = prefixEven + (totalOdd − prefixOdd − currentOddContribution)
- New odd sum = prefixOdd + (totalEven − prefixEven − currentEvenContribution)
- If the new even and odd sums are equal, increment the answer.
- Update the appropriate prefix sum.

1. Print the answer.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    int totalEven=0;
    int totalOdd=0;

    for(int i=0;i<n;i++)
    {
        scanf("%d",&arr[i]);

        if(i%2==0)
            totalEven+=arr[i];
        else
            totalOdd+=arr[i];
    }

    int prefixEven=0;
    int prefixOdd=0;
    int ans=0;

    for(int i=0;i<n;i++)
    {
        int even,odd;

        if(i%2==0)
        {
            even=prefixEven+(totalOdd-prefixOdd);
            odd=prefixOdd+(totalEven-prefixEven-arr[i]);
        }
        else
        {
            even=prefixEven+(totalOdd-prefixOdd-arr[i]);
            odd=prefixOdd+(totalEven-prefixEven);
        }

        if(even==odd)
            ans++;

        if(i%2==0)
            prefixEven+=arr[i];
        else
            prefixOdd+=arr[i];
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

    int totalEven=0;
    int totalOdd=0;

    for(int i=0;i<n;i++)
    {
        cin>>arr[i];

        if(i%2==0)
            totalEven+=arr[i];
        else
            totalOdd+=arr[i];
    }

    int prefixEven=0;
    int prefixOdd=0;
    int ans=0;

    for(int i=0;i<n;i++)
    {
        int even,odd;

        if(i%2==0)
        {
            even=prefixEven+(totalOdd-prefixOdd);
            odd=prefixOdd+(totalEven-prefixEven-arr[i]);
        }
        else
        {
            even=prefixEven+(totalOdd-prefixOdd-arr[i]);
            odd=prefixOdd+(totalEven-prefixEven);
        }

        if(even==odd)
            ans++;

        if(i%2==0)
            prefixEven+=arr[i];
        else
            prefixOdd+=arr[i];
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

        int totalEven=0;
        int totalOdd=0;

        for(int i=0;i<n;i++)
        {
            arr[i]=sc.nextInt();

            if(i%2==0)
                totalEven+=arr[i];
            else
                totalOdd+=arr[i];
        }

        int prefixEven=0;
        int prefixOdd=0;
        int ans=0;

        for(int i=0;i<n;i++)
        {
            int even,odd;

            if(i%2==0)
            {
                even=prefixEven+(totalOdd-prefixOdd);
                odd=prefixOdd+(totalEven-prefixEven-arr[i]);
            }
            else
            {
                even=prefixEven+(totalOdd-prefixOdd-arr[i]);
                odd=prefixOdd+(totalEven-prefixEven);
            }

            if(even==odd)
                ans++;

            if(i%2==0)
                prefixEven+=arr[i];
            else
                prefixOdd+=arr[i];
        }

        System.out.print(ans);
    }
}
```
```Python
n = int(input())

arr = list(map(int, input().split()))

totalEven = 0
totalOdd = 0

for i in range(n):

    if i % 2 == 0:
        totalEven += arr[i]
    else:
        totalOdd += arr[i]

prefixEven = 0
prefixOdd = 0
ans = 0

for i in range(n):

    if i % 2 == 0:
        even = prefixEven + (totalOdd - prefixOdd)
        odd = prefixOdd + (totalEven - prefixEven - arr[i])
    else:
        even = prefixEven + (totalOdd - prefixOdd - arr[i])
        odd = prefixOdd + (totalEven - prefixEven)

    if even == odd:
        ans += 1

    if i % 2 == 0:
        prefixEven += arr[i]
    else:
        prefixOdd += arr[i]

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

        int totalEven = 0;
        int totalOdd = 0;

        for(int i = 0; i < n; i++)
        {
            if(i % 2 == 0)
                totalEven += arr[i];
            else
                totalOdd += arr[i];
        }

        int prefixEven = 0;
        int prefixOdd = 0;
        int ans = 0;

        for(int i = 0; i < n; i++)
        {
            int even, odd;

            if(i % 2 == 0)
            {
                even = prefixEven + (totalOdd - prefixOdd);
                odd = prefixOdd + (totalEven - prefixEven - arr[i]);
            }
            else
            {
                even = prefixEven + (totalOdd - prefixOdd - arr[i]);
                odd = prefixOdd + (totalEven - prefixEven);
            }

            if(even == odd)
                ans++;

            if(i % 2 == 0)
                prefixEven += arr[i];
            else
                prefixOdd += arr[i];
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

let totalEven = 0;
let totalOdd = 0;

for(let i = 0; i < n; i++)
{
    arr.push(input[idx]);

    if(i % 2 === 0)
        totalEven += input[idx];
    else
        totalOdd += input[idx];

    idx++;
}

let prefixEven = 0;
let prefixOdd = 0;
let ans = 0;

for(let i = 0; i < n; i++)
{
    let even, odd;

    if(i % 2 === 0)
    {
        even = prefixEven + (totalOdd - prefixOdd);
        odd = prefixOdd + (totalEven - prefixEven - arr[i]);
    }
    else
    {
        even = prefixEven + (totalOdd - prefixOdd - arr[i]);
        odd = prefixOdd + (totalEven - prefixEven);
    }

    if(even === odd)
        ans++;

    if(i % 2 === 0)
        prefixEven += arr[i];
    else
        prefixOdd += arr[i];
}

console.log(ans);
```

### Output
Input

4

2 1 6 4

Output

1

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




