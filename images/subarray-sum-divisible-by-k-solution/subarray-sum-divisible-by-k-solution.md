# Subarray Sum Divisible by K - Solution

## Problem Statement

Given an integer array `arr[]` of size `N` and an integer `K`, count the number of non-empty subarrays whose sum is divisible by `K`.

## Input Format

First line: Two integers `N` and `K`

Second line: `N` space-separated integers

## Output Format

Print a single integer representing the count of subarrays whose sum is divisible by `K`.

## Explanation

There are two common approaches to solve this problem.

- **Brute Force:** Compute the sum of every possible subarray and check if it is divisible by `K`.
- **Prefix Sum + Frequency Array/Hash Map (Optimal):** Use prefix sum remainders to count valid subarrays efficiently.

For example,

Input

6 5

4 5 0 -2 -3 1

Output

7

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array and value `K`.
2. Consider every possible starting index.
3. Extend the subarray one element at a time while maintaining its sum.
4. If the current sum is divisible by `K`, increment the answer.
5. After checking all subarrays, print the answer.

```C
#include <stdio.h>

int main()
{
    int N, K;
    scanf("%d %d", &N, &K);

    int arr[N];

    for(int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    long long ans = 0;

    for(int i = 0; i < N; i++)
    {
        long long sum = 0;

        for(int j = i; j < N; j++)
        {
            sum += arr[j];

            if(sum % K == 0)
                ans++;
        }
    }

    printf("%lld", ans);

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

    long long ans = 0;

    for(int i = 0; i < N; i++)
    {
        long long sum = 0;

        for(int j = i; j < N; j++)
        {
            sum += arr[j];

            if(sum % K == 0)
                ans++;
        }
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

        int[] arr = new int[N];

        for(int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        long ans = 0;

        for(int i = 0; i < N; i++)
        {
            long sum = 0;

            for(int j = i; j < N; j++)
            {
                sum += arr[j];

                if(sum % K == 0)
                    ans++;
            }
        }

        System.out.print(ans);
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

        if total % K == 0:
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

                if(sum % K == 0)
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

        if(sum % K === 0)
            count++;
    }
}

console.log(count);
```

### Output
Input

6 5

4 5 0 -2 -3 1

Output

7

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Prefix Sum + Frequency Array (Optimal)

### Algorithm

1. Read the array and integer `K`.
2. Create a frequency array of size `K` and initialize `frequency[0] = 1`.
3. Initialize `prefixSum = 0` and `answer = 0`.
4. Traverse the array:

- Add the current element to `prefixSum`.
- Compute `remainder = ((prefixSum % K) + K) % K`.
- Add `frequency[remainder]` to the answer.
- Increment `frequency[remainder]`.

1. Print the final answer.

```C
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int N, K;
    scanf("%d %d", &N, &K);

    int arr[N];

    for(int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    long long *freq = (long long*)calloc(K, sizeof(long long));

    freq[0] = 1;

    long long ans = 0;
    long long prefix = 0;

    for(int i = 0; i < N; i++)
    {
        prefix += arr[i];

        int rem = ((prefix % K) + K) % K;

        ans += freq[rem];

        freq[rem]++;
    }

    printf("%lld", ans);

    free(freq);

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

    vector<long long> freq(K, 0);

    freq[0] = 1;

    long long prefix = 0;
    long long ans = 0;

    for(int i = 0; i < N; i++)
    {
        prefix += arr[i];

        int rem = ((prefix % K) + K) % K;

        ans += freq[rem];

        freq[rem]++;
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

        long[] freq = new long[K];

        freq[0] = 1;

        long prefix = 0;
        long ans = 0;

        for(int i = 0; i < N; i++)
        {
            prefix += sc.nextInt();

            int rem = (int)((prefix % K + K) % K);

            ans += freq[rem];

            freq[rem]++;
        }

        System.out.print(ans);
    }
}
```
```Python
N, K = map(int, input().split())

arr = list(map(int, input().split()))

freq = [0] * K

freq[0] = 1

prefix = 0
count = 0

for value in arr:

    prefix += value

    rem = ((prefix % K) + K) % K

    count += freq[rem]

    freq[rem] += 1

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

        long[] freq = new long[K];

        freq[0] = 1;

        long prefix = 0;
        long count = 0;

        foreach(int value in arr)
        {
            prefix += value;

            int rem = (int)((prefix % K + K) % K);

            count += freq[rem];

            freq[rem]++;
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

const freq = new Array(K).fill(0);

freq[0] = 1;

let prefix = 0;
let count = 0;

for(let i = 0; i < N; i++)
{
    prefix += input[idx++];

    let rem = ((prefix % K) + K) % K;

    count += freq[rem];

    freq[rem]++;
}

console.log(count);
```

### Output
Input

6 5

4 5 0 -2 -3 1

Output

7

# Time Complexity
O(N)

# Space Complexity
O(K)

</approaches>




