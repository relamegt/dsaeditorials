# Good Subarrays - Solution

## Problem Statement

You are given a string $s$ of length $n$ consisting of decimal digits from $'0'$ to $'9'$. Let the digits of the string be $a_1, a_2, \dots, a_n$ (where $a_i$ is the numerical value of the $i$-th character of $s$).

A subarray $a_l, a_{l+1}, \dots, a_r$ (with $1 \le l \le r \le n$) is called **good** if the sum of elements of this subarray is equal to its length:
$$\sum_{i=l}^r a_i = r - l + 1$$

Calculate the total number of good subarrays of the string $s$.

## Input Format

- The first line contains an integer $t$ ($1 \le t \le 10^4$) — the number of test cases.
- The first line contains one integer $n$ ($1 \le n \le 10^5$) — the length of the string $s$.
- The second line contains a string $s$ consisting of $n$ decimal digits representing $a_1, a_2, \dots, a_n$.

## Output Format

Output a single integer representing the total number of good subarrays of the string $s$.

## Explanation

Let $p_x = \sum_{j=0}^{x-1} a_j$ be the prefix sum of the first $x$ elements (with $p_0 = 0$).

The sum of elements in the subarray from index $l$ to index $r$ (1-indexed, $1 \le l \le r \le n$) is:
$$\text{sum} = p_r - p_{l-1}$$

The length of this subarray is:
$$\text{length} = r - l + 1$$

The subarray is good if $\text{sum} = \text{length}$:
$$p_r - p_{l-1} = r - (l - 1)$$

Rearranging terms to group indices together:
$$p_r - r = p_{l-1} - (l - 1)$$

Let $x_i = p_i - i$ for $i \in [0, n]$.

The condition simplifies to finding the number of pairs $(i, j)$ with $0 \le i &lt; j \le n$ such that $x_j = x_i$.

We can maintain the frequency of $x_i$ using a hash map as we compute prefix sums from left to right:

1. Initialize a hash map `d` with `d[0] = 1` (since $p_0 - 0 = 0$).
2. Maintain a running prefix sum `s = 0`.
3. For each index $i$ from $0$ to $n-1$:

- `s += a[i]`
- Compute `x = s - (i + 1)`
- Add `d[x]` to total answer `res`
- Increment `d[x]` by $1$

### Algorithm

1. Read the number of test cases $t$.
2. For each testcase:

- Initialize `d = {0: 1}`, `res = 0`, `s = 0`.
- Iterate over each digit $a[i]$ ($0 \le i &lt; n$):
- `s += int(a[i])`
- `x = s - i - 1`
- `res += d[x]`
- `d[x] += 1`
- Output `res`.

```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define TABLE_SIZE 400009

static int hash_func(int key) {
    int h = key % TABLE_SIZE;
    if (h < 0) h += TABLE_SIZE;
    return h;
}

void solve_c(int n, char *a) {
    int *keys = (int*)calloc(TABLE_SIZE, sizeof(int));
    long long *vals = (long long*)calloc(TABLE_SIZE, sizeof(long long));
    int *used = (int*)calloc(TABLE_SIZE, sizeof(int));

    int idx0 = hash_func(0);
    used[idx0] = 1;
    keys[idx0] = 0;
    vals[idx0] = 1;

    long long res = 0;
    int s = 0;
    for (int i = 0; i < n; i++) {
        s += a[i] - '0';
        int x = s - i - 1;

        int idx = hash_func(x);
        while (used[idx] && keys[idx] != x) {
            idx = (idx + 1) % TABLE_SIZE;
        }

        if (used[idx]) {
            res += vals[idx];
            vals[idx]++;
        } else {
            used[idx] = 1;
            keys[idx] = x;
            vals[idx] = 1;
        }
    }
    printf("%lld\n", res);

    free(keys);
    free(vals);
    free(used);
}

int main() {
    int n;
    static char a[200005];
    while (scanf("%d %s", &n, a) == 2) {
        solve_c(n, a);
    }
    return 0;
}
```
```cpp
#include <iostream>
#include <string>
#include <vector>
#include <unordered_map>
using namespace std;

void solveTestCase() {
    int n;
    if (!(cin >> n)) return;
    string a;
    cin >> a;
    unordered_map<int, long long> d;
    d[0] = 1;
    long long res = 0;
    int s = 0;
    for (int i = 0; i < n; i++) {
        s += a[i] - '0';
        int x = s - i - 1;
        res += d[x];
        d[x]++;
    }
    cout << res << "\n";
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    int t;
    if (cin >> t) {
        while (t--) {
            solveTestCase();
        }
    }
    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        if (sc.hasNextInt()) {
            int t = sc.nextInt();
            while (t-- > 0) {
                int n = sc.nextInt();
                String a = sc.next();

                Map<Integer, Integer> d = new HashMap<>();
                d.put(0, 1);

                long res = 0;
                long s = 0;

                for (int i = 0; i < n; i++) {
                    s += (a.charAt(i) - '0');
                    int x = (int)(s - (i + 1));
                    int count = d.getOrDefault(x, 0);
                    res += count;
                    d.put(x, count + 1);
                }

                System.out.println(res);
            }
        }
        sc.close();
    }
}
```
```Python
import sys
from collections import defaultdict

def main():
    input_data = sys.stdin.read().split()
    if not input_data:
        return
    ptr = 0
    while ptr < len(input_data):
        n = int(input_data[ptr])
        if ptr + 1 >= len(input_data):
            break
        a = input_data[ptr + 1]
        ptr += 2

        d = defaultdict(int)
        d[0] = 1
        res = 0
        s = 0
        for i in range(n):
            s += int(a[i])
            x = s - i - 1
            res += d[x]
            d[x] += 1
        print(res)

if __name__ == '__main__':
    main()
```
```C#
using System;
using System.Collections.Generic;

class Solution {
    static void Main() {
        string input = Console.In.ReadToEnd();
        if (string.IsNullOrWhiteSpace(input)) return;
        string[] tokens = input.Split(new char[] { ' ', '\t', '\r', '\n' }, StringSplitOptions.RemoveEmptyEntries);
        int ptr = 0;
        while (ptr < tokens.Length) {
            int n = int.Parse(tokens[ptr++]);
            if (ptr >= tokens.Length) break;
            string a = tokens[ptr++];

            var d = new Dictionary<int, long>();
            d[0] = 1;
            long res = 0;
            int s = 0;
            for (int i = 0; i < n; i++) {
                s += a[i] - '0';
                int x = s - i - 1;
                if (d.TryGetValue(x, out long count)) {
                    res += count;
                    d[x] = count + 1;
                } else {
                    d[x] = 1;
                }
            }
            Console.WriteLine(res);
        }
    }
}
```
```JavaScript
const fs = require('fs');

function main() {
    const input = fs.readFileSync(0, 'utf-8');
    const tokens = input.trim().split(/\s+/);
    if (!tokens || tokens.length < 2) return;
    let ptr = 0;
    while (ptr < tokens.length) {
        const nStr = tokens[ptr++];
        if (!nStr) break;
        const n = parseInt(nStr, 10);
        if (isNaN(n) || ptr >= tokens.length) break;
        const a = tokens[ptr++];

        const d = new Map();
        d.set(0, 1n);
        let res = 0n;
        let s = 0;
        for (let i = 0; i < n; i++) {
            s += (a.charCodeAt(i) - 48);
            const x = s - i - 1;
            const count = d.get(x) || 0n;
            res += count;
            d.set(x, count + 1n);
        }
        console.log(res.toString());
    }
}

main();
```

### Output
Input

3
3
120
5
11011
6
600005

Output

3
6
1

# Time Complexity
O(N) per testcase.

# Space Complexity
O(N) per testcase.

