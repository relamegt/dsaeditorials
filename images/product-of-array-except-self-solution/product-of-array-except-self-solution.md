# Product of Array Except Self - Solution

## Problem Statement

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

## Input Format

First line: Integer `n`

Second line: `n` space-separated integers

## Output Format

Print `n` space-separated integers representing the answer array.

## Explanation

There are three common approaches to solve this problem.

- **Brute Force:** Compute the product for every index by multiplying all other elements.
- **Division Method:** Compute the total product and divide by each element (works only when there are no zeros).
- **Prefix and Suffix Products (Optimal):** Compute prefix and suffix products separately and combine them without using division.

For example,

Input

4

1 2 3 4

Output

24 12 8 6

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. For every index `i`:

- Initialize `product = 1`.
- Traverse the array again.
- Multiply every element except `nums[i]`.

1. Print the resulting products.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    for(int i=0;i<n;i++)
    {
        long long product=1;

        for(int j=0;j<n;j++)
        {
            if(i!=j)
                product*=arr[j];
        }

        printf("%lld",product);

        if(i!=n-1)
            printf(" ");
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

    vector<long long> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    for(int i=0;i<n;i++)
    {
        long long product=1;

        for(int j=0;j<n;j++)
        {
            if(i!=j)
                product*=arr[j];
        }

        cout<<product;

        if(i!=n-1)
            cout<<" ";
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

        long[] arr=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        for(int i=0;i<n;i++)
        {
            long product=1;

            for(int j=0;j<n;j++)
            {
                if(i!=j)
                    product*=arr[j];
            }

            System.out.print(product);

            if(i!=n-1)
                System.out.print(" ");
        }
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

for i in range(n):

    product=1

    for j in range(n):

        if i!=j:
            product*=arr[j]

    print(product,end=" " if i!=n-1 else "")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        for(int i = 0; i < n; i++)
        {
            long product = 1;

            for(int j = 0; j < n; j++)
            {
                if(i != j)
                    product *= arr[j];
            }

            Console.Write(product);

            if(i != n - 1)
                Console.Write(" ");
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

let ans = [];

for(let i = 0; i < n; i++)
{
    let product = 1;

    for(let j = 0; j < n; j++)
    {
        if(i !== j)
            product *= arr[j];
    }

    ans.push(product);
}

console.log(ans.join(" "));
```

### Output
Input

4

1 2 3 4

Output

24 12 8 6

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Division Method

### Algorithm

1. Read the array.
2. Count the number of zeros in the array.
3. Compute the product of all non-zero elements.
4. Handle three cases:

- If more than one zero exists, every answer is `0`.
- If exactly one zero exists, only that position gets the product of non-zero elements.
- If no zeros exist, divide the total product by the current element.

1. Print the answer array.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    int zeros=0;
    long long product=1;

    for(int i=0;i<n;i++)
    {
        scanf("%lld",&arr[i]);

        if(arr[i]==0)
            zeros++;
        else
            product*=arr[i];
    }

    for(int i=0;i<n;i++)
    {
        if(zeros>1)
            printf("0");
        else if(zeros==1)
        {
            if(arr[i]==0)
                printf("%lld",product);
            else
                printf("0");
        }
        else
            printf("%lld",product/arr[i]);

        if(i!=n-1)
            printf(" ");
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

    vector<long long> arr(n);

    int zeros=0;
    long long product=1;

    for(int i=0;i<n;i++)
    {
        cin>>arr[i];

        if(arr[i]==0)
            zeros++;
        else
            product*=arr[i];
    }

    for(int i=0;i<n;i++)
    {
        if(zeros>1)
            cout<<0;
        else if(zeros==1)
        {
            if(arr[i]==0)
                cout<<product;
            else
                cout<<0;
        }
        else
            cout<<product/arr[i];

        if(i!=n-1)
            cout<<" ";
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

        long[] arr=new long[n];

        int zeros=0;
        long product=1;

        for(int i=0;i<n;i++)
        {
            arr[i]=sc.nextLong();

            if(arr[i]==0)
                zeros++;
            else
                product*=arr[i];
        }

        for(int i=0;i<n;i++)
        {
            if(zeros>1)
                System.out.print(0);
            else if(zeros==1)
            {
                if(arr[i]==0)
                    System.out.print(product);
                else
                    System.out.print(0);
            }
            else
                System.out.print(product/arr[i]);

            if(i!=n-1)
                System.out.print(" ");
        }
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

zeros=arr.count(0)

product=1

for value in arr:
    if value!=0:
        product*=value

for i in range(n):

    if zeros>1:
        print(0,end=" ")
    elif zeros==1:
        if arr[i]==0:
            print(product,end=" ")
        else:
            print(0,end=" ")
    else:
        print(product//arr[i],end=" " if i!=n-1 else "")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        int zeros = 0;
        long product = 1;

        foreach(long value in arr)
        {
            if(value == 0)
                zeros++;
            else
                product *= value;
        }

        for(int i = 0; i < n; i++)
        {
            if(zeros > 1)
                Console.Write(0);
            else if(zeros == 1)
            {
                if(arr[i] == 0)
                    Console.Write(product);
                else
                    Console.Write(0);
            }
            else
                Console.Write(product / arr[i]);

            if(i != n - 1)
                Console.Write(" ");
        }
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const arr = [];

let zeros = 0;
let product = 1;

for(let i = 0; i < n; i++)
{
    arr.push(input[idx]);

    if(input[idx] === 0)
        zeros++;
    else
        product *= input[idx];

    idx++;
}

const ans = [];

for(let i = 0; i < n; i++)
{
    if(zeros > 1)
        ans.push(0);
    else if(zeros === 1)
    {
        if(arr[i] === 0)
            ans.push(product);
        else
            ans.push(0);
    }
    else
        ans.push(product / arr[i]);
}

console.log(ans.join(" "));
```

### Output
Input

4

1 2 3 4

Output

24 12 8 6

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 3: Prefix and Suffix Products (Optimal)

### Algorithm

1. Create an answer array of size `n`.
2. Traverse from left to right while maintaining the prefix product.

- Store the current prefix product in `answer[i]`.

1. Traverse from right to left while maintaining the suffix product.

- Multiply `answer[i]` by the current suffix product.

1. Print the answer array.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];
    long long ans[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    long long prefix=1;

    for(int i=0;i<n;i++)
    {
        ans[i]=prefix;
        prefix*=arr[i];
    }

    long long suffix=1;

    for(int i=n-1;i>=0;i--)
    {
        ans[i]*=suffix;
        suffix*=arr[i];
    }

    for(int i=0;i<n;i++)
    {
        printf("%lld",ans[i]);

        if(i!=n-1)
            printf(" ");
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

    vector<long long> arr(n),ans(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    long long prefix=1;

    for(int i=0;i<n;i++)
    {
        ans[i]=prefix;
        prefix*=arr[i];
    }

    long long suffix=1;

    for(int i=n-1;i>=0;i--)
    {
        ans[i]*=suffix;
        suffix*=arr[i];
    }

    for(int i=0;i<n;i++)
    {
        cout<<ans[i];

        if(i!=n-1)
            cout<<" ";
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

        long[] arr=new long[n];
        long[] ans=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        long prefix=1;

        for(int i=0;i<n;i++)
        {
            ans[i]=prefix;
            prefix*=arr[i];
        }

        long suffix=1;

        for(int i=n-1;i>=0;i--)
        {
            ans[i]*=suffix;
            suffix*=arr[i];
        }

        for(int i=0;i<n;i++)
        {
            System.out.print(ans[i]);

            if(i!=n-1)
                System.out.print(" ");
        }
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

ans=[1]*n

prefix=1

for i in range(n):
    ans[i]=prefix
    prefix*=arr[i]

suffix=1

for i in range(n-1,-1,-1):
    ans[i]*=suffix
    suffix*=arr[i]

print(*ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long[] ans = new long[n];

        long prefix = 1;

        for(int i = 0; i < n; i++)
        {
            ans[i] = prefix;
            prefix *= arr[i];
        }

        long suffix = 1;

        for(int i = n - 1; i >= 0; i--)
        {
            ans[i] *= suffix;
            suffix *= arr[i];
        }

        for(int i = 0; i < n; i++)
        {
            Console.Write(ans[i]);

            if(i != n - 1)
                Console.Write(" ");
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

const ans = new Array(n);

let prefix = 1;

for(let i = 0; i < n; i++)
{
    ans[i] = prefix;
    prefix *= arr[i];
}

let suffix = 1;

for(let i = n - 1; i >= 0; i--)
{
    ans[i] *= suffix;
    suffix *= arr[i];
}

console.log(ans.join(" "));
```

### Output
Input

4

1 2 3 4

Output

24 12 8 6

# Time Complexity
O(N)

# Space Complexity
O(N)

</approaches>




