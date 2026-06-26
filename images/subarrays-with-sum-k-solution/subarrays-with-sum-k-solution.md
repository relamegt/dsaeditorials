# Subarrays with Sum K - Solution

## Problem Statement

Given an array of integers `arr[]` and an integer `K`, return the total number of contiguous subarrays whose sum is exactly equal to `K`.

## Input Format

First line: Two integers `N` and `K`

Second line: `N` space-separated integers

## Output Format

Print a single integer representing the number of subarrays whose sum equals `K`.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Check every possible subarray and calculate its sum.
- **Prefix Sum + Hash Map (Optimal):** Store the frequency of prefix sums to count valid subarrays in linear time.

For example,

Input

5 2

1 1 1 1 1

Output

4

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array and value `K`.
2. Consider every possible starting index.
3. Extend the subarray one element at a time while maintaining its sum.
4. Whenever the sum becomes equal to `K`, increment the answer.
5. Print the final answer.

```C
#include <stdio.h>

int main()
{
    int N, K;
    scanf("%d %d", &N, &K);

    int arr[N];

    for(int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    long long count = 0;

    for(int i = 0; i < N; i++)
    {
        long long sum = 0;

        for(int j = i; j < N; j++)
        {
            sum += arr[j];

            if(sum == K)
                count++;
        }
    }

    printf("%lld", count);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int N, K;
    cin >> N >> K;

    vector<int> arr(N);

    for(int i = 0; i < N; i++)
        cin >> arr[i];

    long long count = 0;

    for(int i = 0; i < N; i++)
    {
        long long sum = 0;

        for(int j = i; j < N; j++)
        {
            sum += arr[j];

            if(sum == K)
                count++;
        }
    }

    cout << count;

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
        int K = sc.nextInt();

        int[] arr = new int[N];

        for(int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        long count = 0;

        for(int i = 0; i < N; i++)
        {
            long sum = 0;

            for(int j = i; j < N; j++)
            {
                sum += arr[j];

                if(sum == K)
                    count++;
            }
        }

        System.out.print(count);
    }
}
```
```Python
N, K = map(int, input().split())

arr = list(map(int, input().split()))

count = 0

for i in range(N):

    total = 0

    for j in range(i, N):

        total += arr[j]

        if total == K:
            count += 1

print(count)
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] first = Console.ReadLine().Split();

        int N = int.Parse(first[0]);
        int K = int.Parse(first[1]);

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        long count = 0;

        for(int i = 0; i < N; i++)
        {
            long sum = 0;

            for(int j = i; j < N; j++)
            {
                sum += arr[j];

                if(sum == K)
                    count++;
            }
        }

        Console.Write(count);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const N = input[idx++];
const K = input[idx++];

const arr = [];

for(let i = 0; i < N; i++)
    arr.push(input[idx++]);

let count = 0;

for(let i = 0; i < N; i++)
{
    let sum = 0;

    for(let j = i; j < N; j++)
    {
        sum += arr[j];

        if(sum === K)
            count++;
    }
}

console.log(count);
```

### Output
Input

5 2

1 1 1 1 1

Output

4

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Prefix Sum + Hash Map (Optimal)

### Algorithm

1. Read the array and value `K`.
2. Create a hash map to store the frequency of prefix sums.
3. Initialize the map with `(0, 1)` since a prefix sum equal to `K` forms a valid subarray from index `0`.
4. Traverse the array while maintaining the prefix sum.
5. For every prefix sum:

- Check whether `(prefixSum - K)` exists in the map.
- If it exists, add its frequency to the answer.
- Store/update the current prefix sum in the map.

1. Print the final answer.

```C
#include <stdio.h>
#include <stdlib.h>

#define SIZE 40009

typedef struct Node
{
    long long key;
    long long freq;
    struct Node *next;
}Node;

Node *table[SIZE];

int hash(long long x)
{
    if(x < 0)
        x = -x;

    return x % SIZE;
}

Node* find(long long key)
{
    int h = hash(key);

    Node *temp = table[h];

    while(temp)
    {
        if(temp->key == key)
            return temp;

        temp = temp->next;
    }

    return NULL;
}

void insert(long long key)
{
    int h = hash(key);

    Node *node = find(key);

    if(node)
    {
        node->freq++;
        return;
    }

    node = (Node*)malloc(sizeof(Node));

    node->key = key;
    node->freq = 1;
    node->next = table[h];

    table[h] = node;
}

int main()
{
    int N, K;
    scanf("%d %d", &N, &K);

    long long prefix = 0;
    long long ans = 0;

    insert(0);

    for(int i = 0; i < N; i++)
    {
        int x;
        scanf("%d", &x);

        prefix += x;

        Node *node = find(prefix - K);

        if(node)
            ans += node->freq;

        insert(prefix);
    }

    printf("%lld", ans);

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
    int N, K;
    cin >> N >> K;

    vector<int> arr(N);

    for(int i = 0; i < N; i++)
        cin >> arr[i];

    unordered_map<long long, long long> freq;

    freq[0] = 1;

    long long prefix = 0;
    long long ans = 0;

    for(int i = 0; i < N; i++)
    {
        prefix += arr[i];

        ans += freq[prefix - K];

        freq[prefix]++;
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
        int K = sc.nextInt();

        HashMap<Long, Long> freq = new HashMap<>();

        freq.put(0L, 1L);

        long prefix = 0;
        long ans = 0;

        for(int i = 0; i < N; i++)
        {
            prefix += sc.nextInt();

            ans += freq.getOrDefault(prefix - K, 0L);

            freq.put(prefix, freq.getOrDefault(prefix, 0L) + 1);
        }

        System.out.print(ans);
    }
}
```
```Python
N, K = map(int, input().split())

arr = list(map(int, input().split()))

freq = {0: 1}

prefix = 0
count = 0

for value in arr:

    prefix += value

    count += freq.get(prefix - K, 0)

    freq[prefix] = freq.get(prefix, 0) + 1

print(count)
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        string[] first = Console.ReadLine().Split();

        int N = int.Parse(first[0]);
        int K = int.Parse(first[1]);

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        Dictionary<long, long> freq = new Dictionary<long, long>();

        freq[0] = 1;

        long prefix = 0;
        long count = 0;

        foreach(int value in arr)
        {
            prefix += value;

            if(freq.ContainsKey(prefix - K))
                count += freq[prefix - K];

            if(freq.ContainsKey(prefix))
                freq[prefix]++;
            else
                freq[prefix] = 1;
        }

        Console.Write(count);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const N = input[idx++];
const K = input[idx++];

const freq = new Map();

freq.set(0, 1);

let prefix = 0;
let count = 0;

for(let i = 0; i < N; i++)
{
    prefix += input[idx++];

    count += freq.get(prefix - K) || 0;

    freq.set(prefix, (freq.get(prefix) || 0) + 1);
}

console.log(count);
```

### Output
Input

5 2

1 1 1 1 1

Output

4

# Time Complexity
O(N)

# Space Complexity
O(N)

</approaches>




