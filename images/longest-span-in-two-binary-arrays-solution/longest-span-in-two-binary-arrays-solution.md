# Longest Span in Two Binary Arrays - Solution

## Problem Statement

Given two binary arrays `a1[]` and `a2[]` of equal length `N`, find the length of the longest span `(i, j)` such that the sum of elements from index `i` to `j` is the same in both arrays.

If no such span exists, return `0`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing `a1`

Third line: `N` space-separated integers representing `a2`

## Output Format

Print a single integer representing the length of the longest valid span.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Check every possible span and compare the sums.
- **Prefix Difference + Hash Map (Optimal):** Maintain the difference between prefix sums of the two arrays. If the same difference appears again, the span between those indices has equal sums.

For example,

Input

6

0 1 0 0 0 0

1 0 1 0 0 1

Output

4

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read both arrays.
2. Consider every possible starting index.
3. Extend the ending index one by one.
4. Maintain the sums of both arrays.
5. Whenever both sums become equal, update the maximum span length.
6. Print the maximum length.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d",&N);

    int a1[N],a2[N];

    for(int i=0;i<N;i++)
        scanf("%d",&a1[i]);

    for(int i=0;i<N;i++)
        scanf("%d",&a2[i]);

    int ans=0;

    for(int i=0;i<N;i++)
    {
        int sum1=0;
        int sum2=0;

        for(int j=i;j<N;j++)
        {
            sum1+=a1[j];
            sum2+=a2[j];

            if(sum1==sum2 && j-i+1>ans)
                ans=j-i+1;
        }
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
    int N;
    cin>>N;

    vector<int> a1(N),a2(N);

    for(int i=0;i<N;i++)
        cin>>a1[i];

    for(int i=0;i<N;i++)
        cin>>a2[i];

    int ans=0;

    for(int i=0;i<N;i++)
    {
        int sum1=0;
        int sum2=0;

        for(int j=i;j<N;j++)
        {
            sum1+=a1[j];
            sum2+=a2[j];

            if(sum1==sum2)
                ans=max(ans,j-i+1);
        }
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

        int N=sc.nextInt();

        int[] a1=new int[N];
        int[] a2=new int[N];

        for(int i=0;i<N;i++)
            a1[i]=sc.nextInt();

        for(int i=0;i<N;i++)
            a2[i]=sc.nextInt();

        int ans=0;

        for(int i=0;i<N;i++)
        {
            int sum1=0;
            int sum2=0;

            for(int j=i;j<N;j++)
            {
                sum1+=a1[j];
                sum2+=a2[j];

                if(sum1==sum2)
                    ans=Math.max(ans,j-i+1);
            }
        }

        System.out.print(ans);
    }
}
```
```Python
N=int(input())

a1=list(map(int,input().split()))

a2=list(map(int,input().split()))

ans=0

for i in range(N):

    sum1=0
    sum2=0

    for j in range(i,N):

        sum1+=a1[j]
        sum2+=a2[j]

        if sum1==sum2:
            ans=max(ans,j-i+1)

print(ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] a1 = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);
        int[] a2 = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int ans = 0;

        for(int i = 0; i < N; i++)
        {
            int sum1 = 0;
            int sum2 = 0;

            for(int j = i; j < N; j++)
            {
                sum1 += a1[j];
                sum2 += a2[j];

                if(sum1 == sum2)
                    ans = Math.Max(ans, j - i + 1);
            }
        }

        Console.Write(ans);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const N = input[idx++];

const a1 = [];
const a2 = [];

for(let i = 0; i < N; i++)
    a1.push(input[idx++]);

for(let i = 0; i < N; i++)
    a2.push(input[idx++]);

let ans = 0;

for(let i = 0; i < N; i++)
{
    let sum1 = 0;
    let sum2 = 0;

    for(let j = i; j < N; j++)
    {
        sum1 += a1[j];
        sum2 += a2[j];

        if(sum1 === sum2)
            ans = Math.max(ans, j - i + 1);
    }
}

console.log(ans);
```

### Output
Input

6

0 1 0 0 0 0

1 0 1 0 0 1

Output

4

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Prefix Difference + Hash Map (Optimal)

### Algorithm

1. Read both arrays.
2. Initialize:

- `prefix1 = 0`
- `prefix2 = 0`
- Hash map to store the first occurrence of each prefix difference.

1. Store difference `0` at index `-1`.
2. Traverse both arrays:

- Update both prefix sums.
- Compute `diff = prefix1 - prefix2`.
- If `diff` has appeared before, update the answer using the distance between indices.
- Otherwise store its first occurrence.

1. Print the maximum span length.

```C
#include <stdio.h>
#include <stdlib.h>

#define SIZE 200003

typedef struct Node
{
    int key;
    int index;
    struct Node *next;
}Node;

Node *table[SIZE];

int hash(int x)
{
    if(x < 0)
        x = -x;
    return x % SIZE;
}

int find(int key, int *index)
{
    int h = hash(key);

    Node *temp = table[h];

    while(temp)
    {
        if(temp->key == key)
        {
            *index = temp->index;
            return 1;
        }

        temp = temp->next;
    }

    return 0;
}

void insert(int key, int index)
{
    int h = hash(key);

    Node *node = (Node*)malloc(sizeof(Node));

    node->key = key;
    node->index = index;
    node->next = table[h];

    table[h] = node;
}

int main()
{
    int N;
    scanf("%d",&N);

    int a1[N],a2[N];

    for(int i=0;i<N;i++)
        scanf("%d",&a1[i]);

    for(int i=0;i<N;i++)
        scanf("%d",&a2[i]);

    insert(0,-1);

    int prefix1=0;
    int prefix2=0;
    int ans=0;

    for(int i=0;i<N;i++)
    {
        prefix1+=a1[i];
        prefix2+=a2[i];

        int diff=prefix1-prefix2;

        int first;

        if(find(diff,&first))
        {
            if(i-first>ans)
                ans=i-first;
        }
        else
        {
            insert(diff,i);
        }
    }

    printf("%d",ans);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

int main()
{
    int N;
    cin >> N;

    vector<int> a1(N), a2(N);

    for(int i = 0; i < N; i++)
        cin >> a1[i];

    for(int i = 0; i < N; i++)
        cin >> a2[i];

    unordered_map<int,int> first;

    first[0] = -1;

    int prefix1 = 0;
    int prefix2 = 0;
    int ans = 0;

    for(int i = 0; i < N; i++)
    {
        prefix1 += a1[i];
        prefix2 += a2[i];

        int diff = prefix1 - prefix2;

        if(first.count(diff))
            ans = max(ans, i - first[diff]);
        else
            first[diff] = i;
    }

    cout << ans;

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

        int[] a1 = new int[N];
        int[] a2 = new int[N];

        for(int i = 0; i < N; i++)
            a1[i] = sc.nextInt();

        for(int i = 0; i < N; i++)
            a2[i] = sc.nextInt();

        HashMap<Integer,Integer> map = new HashMap<>();

        map.put(0, -1);

        int prefix1 = 0;
        int prefix2 = 0;
        int ans = 0;

        for(int i = 0; i < N; i++)
        {
            prefix1 += a1[i];
            prefix2 += a2[i];

            int diff = prefix1 - prefix2;

            if(map.containsKey(diff))
                ans = Math.max(ans, i - map.get(diff));
            else
                map.put(diff, i);
        }

        System.out.print(ans);
    }
}
```
```Python
N = int(input())

a1 = list(map(int, input().split()))
a2 = list(map(int, input().split()))

first = {0: -1}

prefix1 = 0
prefix2 = 0
ans = 0

for i in range(N):

    prefix1 += a1[i]
    prefix2 += a2[i]

    diff = prefix1 - prefix2

    if diff in first:
        ans = max(ans, i - first[diff])
    else:
        first[diff] = i

print(ans)
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] a1 = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);
        int[] a2 = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        Dictionary<int, int> first = new Dictionary<int, int>();

        first[0] = -1;

        int prefix1 = 0;
        int prefix2 = 0;
        int ans = 0;

        for(int i = 0; i < N; i++)
        {
            prefix1 += a1[i];
            prefix2 += a2[i];

            int diff = prefix1 - prefix2;

            if(first.ContainsKey(diff))
                ans = Math.Max(ans, i - first[diff]);
            else
                first[diff] = i;
        }

        Console.Write(ans);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const N = input[idx++];

const a1 = [];
const a2 = [];

for(let i = 0; i < N; i++)
    a1.push(input[idx++]);

for(let i = 0; i < N; i++)
    a2.push(input[idx++]);

const first = new Map();

first.set(0, -1);

let prefix1 = 0;
let prefix2 = 0;
let ans = 0;

for(let i = 0; i < N; i++)
{
    prefix1 += a1[i];
    prefix2 += a2[i];

    const diff = prefix1 - prefix2;

    if(first.has(diff))
        ans = Math.max(ans, i - first.get(diff));
    else
        first.set(diff, i);
}

console.log(ans);
```

### Output
Input

6

0 1 0 0 0 0

1 0 1 0 0 1

Output

4

# Time Complexity
O(N)

# Space Complexity
O(N)

</approaches>




