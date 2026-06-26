# Subarray with 0 Sum - Solution

## Problem Statement

Given an array `arr[]` of `N` integers, determine whether there exists a subarray (contiguous sequence of at least one element) whose sum is equal to `0`.

Return **Yes** if such a subarray exists, otherwise return **No**.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers

## Output Format

Print `Yes` or `No`.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Check the sum of every possible subarray.
- **Prefix Sum + Hash Set (Optimal):** Store prefix sums in a hash set. If a prefix sum repeats or becomes zero, a zero-sum subarray exists.

For example,

Input

5

4 2 -3 1 6

Output

Yes

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. Consider every possible starting index.
3. Extend the subarray one element at a time while maintaining its sum.
4. If the sum becomes `0`, print `Yes`.
5. If all subarrays are checked and none has sum `0`, print `No`.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d",&N);

    long long arr[N];

    for(int i=0;i<N;i++)
        scanf("%lld",&arr[i]);

    for(int i=0;i<N;i++)
    {
        long long sum=0;

        for(int j=i;j<N;j++)
        {
            sum+=arr[j];

            if(sum==0)
            {
                printf("Yes");
                return 0;
            }
        }
    }

    printf("No");

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int N;
    cin>>N;

    vector<long long> arr(N);

    for(int i=0;i<N;i++)
        cin>>arr[i];

    for(int i=0;i<N;i++)
    {
        long long sum=0;

        for(int j=i;j<N;j++)
        {
            sum+=arr[j];

            if(sum==0)
            {
                cout<<"Yes";
                return 0;
            }
        }
    }

    cout<<"No";

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

        int N=sc.nextInt();

        long[] arr=new long[N];

        for(int i=0;i<N;i++)
            arr[i]=sc.nextLong();

        for(int i=0;i<N;i++)
        {
            long sum=0;

            for(int j=i;j<N;j++)
            {
                sum+=arr[j];

                if(sum==0)
                {
                    System.out.print("Yes");
                    return;
                }
            }
        }

        System.out.print("No");
    }
}
```
```Python
N=int(input())

arr=list(map(int,input().split()))

for i in range(N):

    total=0

    for j in range(i,N):

        total+=arr[j]

        if total==0:
            print("Yes")
            exit()

print("No")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        for(int i = 0; i < N; i++)
        {
            long sum = 0;

            for(int j = i; j < N; j++)
            {
                sum += arr[j];

                if(sum == 0)
                {
                    Console.Write("Yes");
                    return;
                }
            }
        }

        Console.Write("No");
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(BigInt);

let idx = 0;

const N = Number(input[idx++]);

const arr = [];

for(let i = 0; i < N; i++)
    arr.push(input[idx++]);

for(let i = 0; i < N; i++)
{
    let sum = 0n;

    for(let j = i; j < N; j++)
    {
        sum += arr[j];

        if(sum === 0n)
        {
            console.log("Yes");
            process.exit(0);
        }
    }
}

console.log("No");
```

### Output
Input

5

4 2 -3 1 6

Output

Yes

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Prefix Sum + Hash Set (Optimal)

### Algorithm

1. Read the array.
2. Initialize an empty hash set to store prefix sums.
3. Initialize `prefixSum = 0`.
4. Traverse the array:

- Add the current element to `prefixSum`.
- If `prefixSum == 0`, print `Yes`.
- If `prefixSum` is already present in the hash set, print `Yes`.
- Otherwise, insert `prefixSum` into the hash set.

1. If the traversal completes without finding such a case, print `No`.

```C
#include <stdio.h>
#include <stdlib.h>

#define SIZE 200003

typedef struct Node
{
    long long value;
    struct Node *next;
}Node;

Node* table[SIZE];

int hash(long long x)
{
    if(x < 0)
        x = -x;

    return x % SIZE;
}

int exists(long long x)
{
    int h = hash(x);

    Node *temp = table[h];

    while(temp)
    {
        if(temp->value == x)
            return 1;

        temp = temp->next;
    }

    return 0;
}

void insert(long long x)
{
    int h = hash(x);

    Node *node = (Node*)malloc(sizeof(Node));

    node->value = x;
    node->next = table[h];

    table[h] = node;
}

int main()
{
    int N;
    scanf("%d",&N);

    long long sum = 0;

    for(int i = 0; i < N; i++)
    {
        long long x;
        scanf("%lld",&x);

        sum += x;

        if(sum == 0 || exists(sum))
        {
            printf("Yes");
            return 0;
        }

        insert(sum);
    }

    printf("No");

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
    int N;
    cin >> N;

    vector<long long> arr(N);

    for(int i = 0; i < N; i++)
        cin >> arr[i];

    unordered_set<long long> prefix;

    long long sum = 0;

    for(int i = 0; i < N; i++)
    {
        sum += arr[i];

        if(sum == 0 || prefix.count(sum))
        {
            cout << "Yes";
            return 0;
        }

        prefix.insert(sum);
    }

    cout << "No";

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

        int N = sc.nextInt();

        HashSet<Long> set = new HashSet<>();

        long sum = 0;

        for(int i = 0; i < N; i++)
        {
            sum += sc.nextLong();

            if(sum == 0 || set.contains(sum))
            {
                System.out.print("Yes");
                return;
            }

            set.add(sum);
        }

        System.out.print("No");
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

seen = set()

prefix = 0

for value in arr:

    prefix += value

    if prefix == 0 or prefix in seen:
        print("Yes")
        exit()

    seen.add(prefix)

print("No")
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        HashSet<long> set = new HashSet<long>();

        long prefix = 0;

        foreach(long value in arr)
        {
            prefix += value;

            if(prefix == 0 || set.Contains(prefix))
            {
                Console.Write("Yes");
                return;
            }

            set.Add(prefix);
        }

        Console.Write("No");
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(BigInt);

let idx = 0;

const N = Number(input[idx++]);

const seen = new Set();

let prefix = 0n;

for(let i = 0; i < N; i++)
{
    prefix += input[idx++];

    const key = prefix.toString();

    if(prefix === 0n || seen.has(key))
    {
        console.log("Yes");
        process.exit(0);
    }

    seen.add(key);
}

console.log("No");
```

### Output
Input

5

4 2 -3 1 6

Output

Yes

# Time Complexity
O(N)

# Space Complexity
O(N)

</approaches>




