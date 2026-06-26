# Majority Element (> n/2) - Solution

## Problem Statement

Given an array `nums` of size `n`, return the majority element.

The majority element is the element that appears more than `floor(n / 2)` times. It is guaranteed that the majority element always exists.

## Input Format

First line: Integer `n`

Second line: `n` space-separated integers

## Output Format

Print the majority element.

## Explanation

There are three common approaches to solve this problem.

- **Brute Force:** Count the frequency of every element by scanning the array repeatedly.
- **Hash Map:** Store frequencies using a hash map and return the element whose frequency exceeds `n/2`.
- **Boyer-Moore Voting Algorithm (Optimal):** Maintain a candidate and a counter to identify the majority element in one traversal.

For example,

Input

3

3 2 3

Output

3

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. For every element:

- Count how many times it appears in the array.

1. If the count exceeds `n / 2`, print that element.
2. Stop after finding the majority element.

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
        int count=0;

        for(int j=0;j<n;j++)
        {
            if(arr[i]==arr[j])
                count++;
        }

        if(count>n/2)
        {
            printf("%lld",arr[i]);
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
    int n;
    cin>>n;

    vector<long long> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    for(int i=0;i<n;i++)
    {
        int count=0;

        for(int j=0;j<n;j++)
        {
            if(arr[i]==arr[j])
                count++;
        }

        if(count>n/2)
        {
            cout<<arr[i];
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

        long[] arr=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        for(int i=0;i<n;i++)
        {
            int count=0;

            for(int j=0;j<n;j++)
            {
                if(arr[i]==arr[j])
                    count++;
            }

            if(count>n/2)
            {
                System.out.print(arr[i]);
                break;
            }
        }
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

for i in range(n):

    count=0

    for j in range(n):

        if arr[i]==arr[j]:
            count+=1

    if count>n//2:
        print(arr[i])
        break
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
            int count = 0;

            for(int j = 0; j < n; j++)
            {
                if(arr[i] == arr[j])
                    count++;
            }

            if(count > n / 2)
            {
                Console.Write(arr[i]);
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

const arr = [];

for(let i = 0; i < n; i++)
    arr.push(input[idx++]);

for(let i = 0; i < n; i++)
{
    let count = 0;

    for(let j = 0; j < n; j++)
    {
        if(arr[i] === arr[j])
            count++;
    }

    if(count > Math.floor(n / 2))
    {
        console.log(arr[i]);
        break;
    }
}
```

### Output
Input

3

3 2 3

Output

3

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Hash Map

### Algorithm

1. Read the array.
2. Create a hash map to store the frequency of each element.
3. Traverse the array and update the frequency of every element.
4. Traverse the hash map and print the element whose frequency is greater than `n / 2`.

```C
#include <stdio.h>
#include <stdlib.h>

#define SIZE 100003

typedef struct Node
{
    long long key;
    int freq;
    struct Node *next;
} Node;

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
    Node *node = find(key);

    if(node)
    {
        node->freq++;
        return;
    }

    int h = hash(key);

    node = (Node*)malloc(sizeof(Node));

    node->key = key;
    node->freq = 1;
    node->next = table[h];

    table[h] = node;
}

int main()
{
    int n;
    scanf("%d",&n);

    for(int i=0;i<n;i++)
    {
        long long x;
        scanf("%lld",&x);

        insert(x);
    }

    for(int i=0;i<SIZE;i++)
    {
        Node *temp = table[i];

        while(temp)
        {
            if(temp->freq > n/2)
            {
                printf("%lld", temp->key);
                return 0;
            }

            temp = temp->next;
        }
    }

    return 0;
}
```
```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

int main()
{
    int n;
    cin >> n;

    unordered_map<long long, int> freq;

    for(int i = 0; i < n; i++)
    {
        long long x;
        cin >> x;

        freq[x]++;
    }

    for(auto it : freq)
    {
        if(it.second > n / 2)
        {
            cout << it.first;
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
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        HashMap<Long, Integer> map = new HashMap<>();

        for(int i = 0; i < n; i++)
        {
            long x = sc.nextLong();

            map.put(x, map.getOrDefault(x, 0) + 1);
        }

        for(Map.Entry<Long, Integer> entry : map.entrySet())
        {
            if(entry.getValue() > n / 2)
            {
                System.out.print(entry.getKey());
                break;
            }
        }
    }
}
```
```Python
n = int(input())

arr = list(map(int, input().split()))

freq = {}

for value in arr:
    freq[value] = freq.get(value, 0) + 1

for key in freq:
    if freq[key] > n // 2:
        print(key)
        break
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        Dictionary<long, int> freq = new Dictionary<long, int>();

        foreach(long value in arr)
        {
            if(freq.ContainsKey(value))
                freq[value]++;
            else
                freq[value] = 1;
        }

        foreach(var item in freq)
        {
            if(item.Value > n / 2)
            {
                Console.Write(item.Key);
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

const freq = new Map();

for(let i = 0; i < n; i++)
{
    const value = input[idx++];

    freq.set(value, (freq.get(value) || 0) + 1);
}

for(const [key, value] of freq)
{
    if(value > Math.floor(n / 2))
    {
        console.log(key);
        break;
    }
}
```

### Output
Input

3

3 2 3

Output

3

# Time Complexity
O(N)

# Space Complexity
O(N)

## Approach 3: Boyer-Moore Voting Algorithm (Optimal)

### Algorithm

1. Read the array.
2. Initialize:

- `candidate = 0`
- `count = 0`

1. Traverse the array:

- If `count == 0`, make the current element the candidate.
- If the current element equals the candidate, increment `count`.
- Otherwise, decrement `count`.

1. Since a majority element is guaranteed to exist, the final candidate is the answer.
2. Print the candidate.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long candidate = 0;
    int count = 0;

    for(int i = 0; i < n; i++)
    {
        long long x;
        scanf("%lld",&x);

        if(count == 0)
            candidate = x;

        if(x == candidate)
            count++;
        else
            count--;
    }

    printf("%lld", candidate);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main()
{
    int n;
    cin >> n;

    long long candidate = 0;
    int count = 0;

    for(int i = 0; i < n; i++)
    {
        long long x;
        cin >> x;

        if(count == 0)
            candidate = x;

        if(x == candidate)
            count++;
        else
            count--;
    }

    cout << candidate;

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

        long candidate = 0;
        int count = 0;

        for(int i = 0; i < n; i++)
        {
            long x = sc.nextLong();

            if(count == 0)
                candidate = x;

            if(x == candidate)
                count++;
            else
                count--;
        }

        System.out.print(candidate);
    }
}
```
```Python
n = int(input())

arr = list(map(int, input().split()))

candidate = 0
count = 0

for value in arr:

    if count == 0:
        candidate = value

    if value == candidate:
        count += 1
    else:
        count -= 1

print(candidate)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long candidate = 0;
        int count = 0;

        foreach(long value in arr)
        {
            if(count == 0)
                candidate = value;

            if(value == candidate)
                count++;
            else
                count--;
        }

        Console.Write(candidate);
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

let candidate = 0;
let count = 0;

for(let i = 0; i < n; i++)
{
    const value = input[idx++];

    if(count === 0)
        candidate = value;

    if(value === candidate)
        count++;
    else
        count--;
}

console.log(candidate);
```

### Output
Input

3

3 2 3

Output

3

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




