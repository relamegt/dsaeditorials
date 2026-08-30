# Same Differences - Solution

## Problem Statement

You are given an array $a$ of $n$ integers. Count the number of pairs of indices $(i, j)$ such that $1 \le i &lt; j \le n$ and $a_j - a_i = j - i$.

## Input Format

- The first line contains an integer $t$ ($1 \le t \le 10^4$) — the number of test cases.
- The first line contains one integer $n$ ($1 \le n \le 2 \cdot 10^5$) - the length of array $a$.
- The second line contains $n$ space-separated integers $a_1, a_2, \dots, a_n$ ($1 \le a_i \le n$).

## Output Format

Output a single integer representing the number of valid pairs of indices $(i, j)$ such that $i &lt; j$ and $a_j - a_i = j - i$.

## Explanation

Let's rewrite the given equality:
$$a_j - a_i = j - i$$

By rearranging terms (grouping index-related terms together):
$$a_j - j = a_i - i$$

Let's define a new value for each element:
$$b_i = a_i - i$$

Now, the condition simplifies to finding the number of pairs $(i, j)$ such that $i &lt; j$ and $b_i = b_j$.

We can calculate this efficiently using a frequency hash map while traversing the array from left to right:

1. Initialize a hash map `freq` and `res = 0` (`long` type to avoid 64-bit integer overflow).
2. For each element at 0-indexed position $i$:

- Compute `val = a[i] - i`.
- Add `freq[val]` to `res`.
- Increment `freq[val]` by $1$.

### Algorithm

1. Read input.
2. For each testcase:

- Initialize frequency map `freq` and `res = 0` (`long` / `long long` / `BigInt`).
- Iterate index $i$ from $0$ to $n - 1$:
- Read $x = a[i]$.
- Calculate `val = x - i`.
- `res += freq[val]`
- `freq[val] += 1`
- Output `res`.

```C
#include <stdio.h>
#include <stdlib.h>

#define TABLE_SIZE 400009

static int hash_func(int key) {
    int h = key % TABLE_SIZE;
    if (h < 0) h += TABLE_SIZE;
    return h;
}

void solve_c() {
    int n;
    if (scanf("%d", &n) != 1) return;

    int *keys = (int*)calloc(TABLE_SIZE, sizeof(int));
    int *vals = (int*)calloc(TABLE_SIZE, sizeof(int));
    int *used = (int*)calloc(TABLE_SIZE, sizeof(int));

    long long res = 0;
    for (int i = 0; i < n; i++) {
        int x;
        scanf("%d", &x);
        int diff = x - i;

        int idx = hash_func(diff);
        while (used[idx] && keys[idx] != diff) {
            idx = (idx + 1) % TABLE_SIZE;
        }

        if (used[idx]) {
            res += vals[idx];
            vals[idx]++;
        } else {
            used[idx] = 1;
            keys[idx] = diff;
            vals[idx] = 1;
        }
    }
    printf("%lld\n", res);

    free(keys);
    free(vals);
    free(used);
}

int main() {
    int t;
    if (scanf("%d", &t) == 1) {
        while (t--) solve_c();
    }
    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

void solve() {
    int n;
    if (!(cin >> n)) {
        return;
    }

    unordered_map<int, int> freq;
    long long res = 0;

    for (int i = 0; i < n; i++) {
        int x;
        cin >> x;
        x -= i;
        res += freq[x];
        freq[x]++;
    }

    cout << res << "\n";
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);

    int t;
    if (cin >> t) {
        while (t--) {
            solve();
        }
    }
    return 0;
}
```
```Java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;

        String line = br.readLine();
        if (line == null || line.trim().isEmpty()) return;
        st = new StringTokenizer(line);
        if (!st.hasMoreTokens()) return;
        int t = Integer.parseInt(st.nextToken());

        StringBuilder sb = new StringBuilder();
        while (t-- > 0) {
            while (st == null || !st.hasMoreTokens()) {
                line = br.readLine();
                if (line == null) break;
                st = new StringTokenizer(line);
            }
            if (line == null) break;

            int n = Integer.parseInt(st.nextToken());
            Map<Integer, Integer> map = new HashMap<>();
            long count = 0;

            for (int i = 0; i < n; i++) {
                while (st == null || !st.hasMoreTokens()) {
                    line = br.readLine();
                    if (line == null) break;
                    st = new StringTokenizer(line);
                }
                int val = Integer.parseInt(st.nextToken()) - i;
                int existing = map.getOrDefault(val, 0);
                count += existing;
                map.put(val, existing + 1);
            }
            sb.append(count).append("\n");
        }
        System.out.print(sb.toString());
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
    t = int(input_data[ptr])
    ptr += 1
    out = []
    for _ in range(t):
        n = int(input_data[ptr])
        ptr += 1
        freq = defaultdict(int)
        res = 0
        for i in range(n):
            val = int(input_data[ptr + i]) - i
            res += freq[val]
            freq[val] += 1
        ptr += n
        out.append(str(res))
    print('\n'.join(out))

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
        if (tokens.Length == 0) return;
        int ptr = 0;
        int t = int.Parse(tokens[ptr++]);
        while (t-- > 0 && ptr < tokens.Length) {
            int n = int.Parse(tokens[ptr++]);
            var freq = new Dictionary<int, int>();
            long res = 0;
            for (int i = 0; i < n; i++) {
                int val = int.Parse(tokens[ptr++]) - i;
                if (freq.TryGetValue(val, out int count)) {
                    res += count;
                    freq[val] = count + 1;
                } else {
                    freq[val] = 1;
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
    if (!tokens || tokens.length === 0 || tokens[0] === '') return;
    let ptr = 0;
    const t = parseInt(tokens[ptr++]);
    const out = [];
    for (let tc = 0; tc < t; tc++) {
        if (ptr >= tokens.length) break;
        const n = parseInt(tokens[ptr++]);
        const map = new Map();
        let res = 0n;
        for (let i = 0; i < n; i++) {
            const val = parseInt(tokens[ptr++]) - i;
            const count = map.get(val) || 0n;
            res += count;
            map.set(val, count + 1n);
        }
        out.push(res.toString());
    }
    console.log(out.join('\n'));
}

main();
```

### Output
Input

1
6
3 5 1 4 6 6

Output

1

# Time Complexity
O(N) per testcase.

# Space Complexity
O(N) per testcase.

