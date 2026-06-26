# Trapping Rain Water - Solution

## Problem Statement

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

## Input Format

First line: Integer `n`

Second line: `n` space-separated integers representing the heights.

## Output Format

Print a single integer representing the total units of trapped rain water.

## Explanation

There are three common approaches to solve this problem.

- **Brute Force:** For every index, find the tallest bar on its left and right by scanning the array.
- **Prefix and Suffix Maximum Arrays:** Precompute left and right maximum heights for every index.
- **Two Pointer Technique (Optimal):** Maintain left and right pointers with running maximum heights.

For example,

Input

12

0 1 0 2 1 0 1 3 2 1 2 1

Output

6

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. For every index:

- Find the tallest bar on the left.
- Find the tallest bar on the right.
- Water trapped at the current index is:

     `min(leftMax, rightMax) - height[i]`.

1. Add the trapped water for every index.
2. Print the total trapped water.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int height[n];

    for(int i=0;i<n;i++)
        scanf("%d",&height[i]);

    int water=0;

    for(int i=0;i<n;i++)
    {
        int leftMax=height[i];
        int rightMax=height[i];

        for(int j=0;j<=i;j++)
            if(height[j]>leftMax)
                leftMax=height[j];

        for(int j=i;j<n;j++)
            if(height[j]>rightMax)
                rightMax=height[j];

        water+=(leftMax<rightMax?leftMax:rightMax)-height[i];
    }

    printf("%d",water);

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

    vector<int> height(n);

    for(int i=0;i<n;i++)
        cin>>height[i];

    int water=0;

    for(int i=0;i<n;i++)
    {
        int leftMax=height[i];
        int rightMax=height[i];

        for(int j=0;j<=i;j++)
            leftMax=max(leftMax,height[j]);

        for(int j=i;j<n;j++)
            rightMax=max(rightMax,height[j]);

        water+=min(leftMax,rightMax)-height[i];
    }

    cout<<water;

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

        int[] height=new int[n];

        for(int i=0;i<n;i++)
            height[i]=sc.nextInt();

        int water=0;

        for(int i=0;i<n;i++)
        {
            int leftMax=height[i];
            int rightMax=height[i];

            for(int j=0;j<=i;j++)
                leftMax=Math.max(leftMax,height[j]);

            for(int j=i;j<n;j++)
                rightMax=Math.max(rightMax,height[j]);

            water+=Math.min(leftMax,rightMax)-height[i];
        }

        System.out.print(water);
    }
}
```
```Python
n=int(input())

height=list(map(int,input().split()))

water=0

for i in range(n):

    leftMax=height[i]
    rightMax=height[i]

    for j in range(i+1):
        leftMax=max(leftMax,height[j])

    for j in range(i,n):
        rightMax=max(rightMax,height[j])

    water+=min(leftMax,rightMax)-height[i]

print(water)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] height = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int water = 0;

        for(int i = 0; i < n; i++)
        {
            int leftMax = height[i];
            int rightMax = height[i];

            for(int j = 0; j <= i; j++)
                leftMax = Math.Max(leftMax, height[j]);

            for(int j = i; j < n; j++)
                rightMax = Math.Max(rightMax, height[j]);

            water += Math.Min(leftMax, rightMax) - height[i];
        }

        Console.Write(water);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const height = [];

for(let i = 0; i < n; i++)
    height.push(input[idx++]);

let water = 0;

for(let i = 0; i < n; i++)
{
    let leftMax = height[i];
    let rightMax = height[i];

    for(let j = 0; j <= i; j++)
        leftMax = Math.max(leftMax, height[j]);

    for(let j = i; j < n; j++)
        rightMax = Math.max(rightMax, height[j]);

    water += Math.min(leftMax, rightMax) - height[i];
}

console.log(water);
```

### Output
Input

12

0 1 0 2 1 0 1 3 2 1 2 1

Output

6

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Prefix and Suffix Maximum Arrays

### Algorithm

1. Create two arrays:

- `leftMax[i]` = maximum height from index `0` to `i`.
- `rightMax[i]` = maximum height from index `i` to `n-1`.

1. Fill both arrays.
2. For every index:

- Water trapped = `min(leftMax[i], rightMax[i]) - height[i]`.

1. Sum the trapped water.
2. Print the answer.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int height[n];
    int leftMax[n];
    int rightMax[n];

    for(int i=0;i<n;i++)
        scanf("%d",&height[i]);

    leftMax[0]=height[0];

    for(int i=1;i<n;i++)
        leftMax[i]=leftMax[i-1]>height[i]?leftMax[i-1]:height[i];

    rightMax[n-1]=height[n-1];

    for(int i=n-2;i>=0;i--)
        rightMax[i]=rightMax[i+1]>height[i]?rightMax[i+1]:height[i];

    int water=0;

    for(int i=0;i<n;i++)
    {
        int limit=leftMax[i]<rightMax[i]?leftMax[i]:rightMax[i];
        water+=limit-height[i];
    }

    printf("%d",water);

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

    vector<int> height(n);
    vector<int> leftMax(n),rightMax(n);

    for(int i=0;i<n;i++)
        cin>>height[i];

    leftMax[0]=height[0];

    for(int i=1;i<n;i++)
        leftMax[i]=max(leftMax[i-1],height[i]);

    rightMax[n-1]=height[n-1];

    for(int i=n-2;i>=0;i--)
        rightMax[i]=max(rightMax[i+1],height[i]);

    int water=0;

    for(int i=0;i<n;i++)
        water+=min(leftMax[i],rightMax[i])-height[i];

    cout<<water;

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

        int[] height=new int[n];
        int[] leftMax=new int[n];
        int[] rightMax=new int[n];

        for(int i=0;i<n;i++)
            height[i]=sc.nextInt();

        leftMax[0]=height[0];

        for(int i=1;i<n;i++)
            leftMax[i]=Math.max(leftMax[i-1],height[i]);

        rightMax[n-1]=height[n-1];

        for(int i=n-2;i>=0;i--)
            rightMax[i]=Math.max(rightMax[i+1],height[i]);

        int water=0;

        for(int i=0;i<n;i++)
            water+=Math.min(leftMax[i],rightMax[i])-height[i];

        System.out.print(water);
    }
}
```
```Python
n=int(input())

height=list(map(int,input().split()))

leftMax=[0]*n
rightMax=[0]*n

leftMax[0]=height[0]

for i in range(1,n):
    leftMax[i]=max(leftMax[i-1],height[i])

rightMax[-1]=height[-1]

for i in range(n-2,-1,-1):
    rightMax[i]=max(rightMax[i+1],height[i])

water=0

for i in range(n):
    water+=min(leftMax[i],rightMax[i])-height[i]

print(water)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] height = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int[] leftMax = new int[n];
        int[] rightMax = new int[n];

        leftMax[0] = height[0];

        for(int i = 1; i < n; i++)
            leftMax[i] = Math.Max(leftMax[i - 1], height[i]);

        rightMax[n - 1] = height[n - 1];

        for(int i = n - 2; i >= 0; i--)
            rightMax[i] = Math.Max(rightMax[i + 1], height[i]);

        int water = 0;

        for(int i = 0; i < n; i++)
            water += Math.Min(leftMax[i], rightMax[i]) - height[i];

        Console.Write(water);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const height = [];

for(let i = 0; i < n; i++)
    height.push(input[idx++]);

const leftMax = new Array(n);
const rightMax = new Array(n);

leftMax[0] = height[0];

for(let i = 1; i < n; i++)
    leftMax[i] = Math.max(leftMax[i - 1], height[i]);

rightMax[n - 1] = height[n - 1];

for(let i = n - 2; i >= 0; i--)
    rightMax[i] = Math.max(rightMax[i + 1], height[i]);

let water = 0;

for(let i = 0; i < n; i++)
    water += Math.min(leftMax[i], rightMax[i]) - height[i];

console.log(water);
```

### Output
Input

12

0 1 0 2 1 0 1 3 2 1 2 1

Output

6

# Time Complexity
O(N)

# Space Complexity
O(N)

## Approach 3: Two Pointer Technique (Optimal)

### Algorithm

1. Initialize two pointers:

- `left = 0`
- `right = n - 1`

1. Maintain:

- `leftMax`
- `rightMax`

1. While `left < right`:

- If `height[left] <= height[right]`:
- Update `leftMax`.
- Add trapped water at `left`.
- Move `left` forward.
- Otherwise:
- Update `rightMax`.
- Add trapped water at `right`.
- Move `right` backward.

1. Print the total trapped water.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    int height[n];

    for(int i=0;i<n;i++)
        scanf("%d",&height[i]);

    int left=0;
    int right=n-1;
    int leftMax=0;
    int rightMax=0;
    int water=0;

    while(left<right)
    {
        if(height[left]<=height[right])
        {
            if(height[left]>=leftMax)
                leftMax=height[left];
            else
                water+=leftMax-height[left];

            left++;
        }
        else
        {
            if(height[right]>=rightMax)
                rightMax=height[right];
            else
                water+=rightMax-height[right];

            right--;
        }
    }

    printf("%d",water);

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

    vector<int> height(n);

    for(int i=0;i<n;i++)
        cin>>height[i];

    int left=0;
    int right=n-1;
    int leftMax=0;
    int rightMax=0;
    int water=0;

    while(left<right)
    {
        if(height[left]<=height[right])
        {
            if(height[left]>=leftMax)
                leftMax=height[left];
            else
                water+=leftMax-height[left];

            left++;
        }
        else
        {
            if(height[right]>=rightMax)
                rightMax=height[right];
            else
                water+=rightMax-height[right];

            right--;
        }
    }

    cout<<water;

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

        int[] height=new int[n];

        for(int i=0;i<n;i++)
            height[i]=sc.nextInt();

        int left=0;
        int right=n-1;
        int leftMax=0;
        int rightMax=0;
        int water=0;

        while(left<right)
        {
            if(height[left]<=height[right])
            {
                if(height[left]>=leftMax)
                    leftMax=height[left];
                else
                    water+=leftMax-height[left];

                left++;
            }
            else
            {
                if(height[right]>=rightMax)
                    rightMax=height[right];
                else
                    water+=rightMax-height[right];

                right--;
            }
        }

        System.out.print(water);
    }
}
```
```Python
n=int(input())

height=list(map(int,input().split()))

left=0
right=n-1
leftMax=0
rightMax=0
water=0

while left<right:

    if height[left]<=height[right]:

        if height[left]>=leftMax:
            leftMax=height[left]
        else:
            water+=leftMax-height[left]

        left+=1

    else:

        if height[right]>=rightMax:
            rightMax=height[right]
        else:
            water+=rightMax-height[right]

        right-=1

print(water)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] height = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int left = 0;
        int right = n - 1;
        int leftMax = 0;
        int rightMax = 0;
        int water = 0;

        while(left < right)
        {
            if(height[left] <= height[right])
            {
                if(height[left] >= leftMax)
                    leftMax = height[left];
                else
                    water += leftMax - height[left];

                left++;
            }
            else
            {
                if(height[right] >= rightMax)
                    rightMax = height[right];
                else
                    water += rightMax - height[right];

                right--;
            }
        }

        Console.Write(water);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const height = [];

for(let i = 0; i < n; i++)
    height.push(input[idx++]);

let left = 0;
let right = n - 1;
let leftMax = 0;
let rightMax = 0;
let water = 0;

while(left < right)
{
    if(height[left] <= height[right])
    {
        if(height[left] >= leftMax)
            leftMax = height[left];
        else
            water += leftMax - height[left];

        left++;
    }
    else
    {
        if(height[right] >= rightMax)
            rightMax = height[right];
        else
            water += rightMax - height[right];

        right--;
    }
}

console.log(water);
```

### Output
Input

12

0 1 0 2 1 0 1 3 2 1 2 1

Output

6

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




