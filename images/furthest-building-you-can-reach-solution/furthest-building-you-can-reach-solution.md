# Furthest Building You Can Reach - Solution

## Problem Statement

You are given an integer array `heights` representing the heights of buildings, an integer `bricks`, and an integer `ladders`.

You start your journey at building `0` and move to building `i + 1` while moving from building `i` to `i + 1`:

- If `heights[i+1] <= heights[i]`, you do not need ladders or bricks.
- If `heights[i+1] > heights[i]`, you can use either `heights[i+1] - heights[i]` bricks OR `1` ladder.

Return the **furthest building index** (0-indexed) you can reach if you use your given ladders and bricks optimally.

## Input Format

- The first line contains an integer $t$ ($1 \le t \le 10^4$) — the number of test cases.
- The first line contains three space-separated integers: $n$ ($1 \le n \le 10^5$), $bricks$ ($0 \le bricks \le 10^9$), and $ladders$ ($0 \le ladders \le n$).
- The second line contains $n$ space-separated integers representing array `heights` ($1 \le heights[i] \le 10^6$).

## Output Format

Output a single integer representing the furthest building index (0-indexed) you can reach.

## Explanation

A greedy strategy with a **Min Priority Queue (Min-Heap)** allows us to make optimal decisions efficiently:

1. As we move from building $i$ to building $i+1$, if `heights[i+1] > heights[i]`, we tentatively use a **ladder** for this climb by pushing the climb difference `diff = heights[i+1] - heights[i]` into a **Min Priority Queue**.
2. If the number of climbs in our min-heap exceeds our available `ladders` (`minHeap.size() > ladders`):

- We pop the smallest climb from the min-heap and cover it using `bricks` instead (`bricks -= minHeap.poll()`).

1. If at any point our available `bricks` drop below `0` (`bricks < 0`):

- We cannot reach building $i+1$, so we stop and return the current building index $i$.

1. If we traverse all buildings, return $n - 1$.

### Algorithm

1. Initialize a Min Priority Queue to store climbs covered by ladders.
2. Loop through building indices $i$ from $0$ to $n - 2$:

- Compute `diff = heights[i+1] - heights[i]`.
- If `diff <= 0`, continue.
- Push `diff` into `minHeap`.
- If `minHeap.size() > ladders`:
- Deduct the smallest climb from `bricks`: `bricks -= minHeap.poll()`.
- If `bricks < 0`:
- Return $i$.

1. If the loop completes, return $n - 1$.

```C
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int *data;
    int size;
    int capacity;
} MinHeap;

MinHeap* createHeap(int cap) {
    MinHeap *h = (MinHeap*)malloc(sizeof(MinHeap));
    h->data = (int*)malloc(sizeof(int) * (cap + 5));
    h->size = 0;
    h->capacity = cap;
    return h;
}

void heapPush(MinHeap *h, int val) {
    int i = h->size++;
    h->data[i] = val;
    while (i > 0) {
        int p = (i - 1) / 2;
        if (h->data[p] > h->data[i]) {
            int tmp = h->data[p];
            h->data[p] = h->data[i];
            h->data[i] = tmp;
            i = p;
        } else break;
    }
}

int heapPop(MinHeap *h) {
    if (h->size == 0) return 0;
    int top = h->data[0];
    int bottom = h->data[--h->size];
    if (h->size > 0) {
        h->data[0] = bottom;
        int i = 0;
        while (2 * i + 1 < h->size) {
            int left = 2 * i + 1, right = left + 1, smallest = i;
            if (h->data[left] < h->data[smallest]) smallest = left;
            if (right < h->size && h->data[right] < h->data[smallest]) smallest = right;
            if (smallest != i) {
                int tmp = h->data[i];
                h->data[i] = h->data[smallest];
                h->data[smallest] = tmp;
                i = smallest;
            } else break;
        }
    }
    return top;
}

void freeHeap(MinHeap *h) {
    free(h->data);
    free(h);
}

void solve_c(int n, long long bricks, int ladders, int *heights) {
    MinHeap *minHeap = createHeap(n);
    int ans = n - 1;
    for (int i = 0; i < n - 1; i++) {
        int diff = heights[i + 1] - heights[i];
        if (diff > 0) {
            heapPush(minHeap, diff);
            if (minHeap->size > ladders) {
                bricks -= heapPop(minHeap);
            }
            if (bricks < 0) {
                ans = i;
                break;
            }
        }
    }
    printf("%d\n", ans);
    freeHeap(minHeap);
}

int main() {
    int n, ladders;
    long long bricks;
    while (scanf("%d %lld %d", &n, &bricks, &ladders) == 3) {
        int *heights = (int*)malloc(sizeof(int) * n);
        for (int i = 0; i < n; i++) scanf("%d", &heights[i]);
        solve_c(n, bricks, ladders, heights);
        free(heights);
    }
    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>
using namespace std;

void solveTestCase() {
    int n;
    long long bricks;
    int ladders;
    if (!(cin >> n >> bricks >> ladders)) return;
    vector<int> heights(n);
    for (int i = 0; i < n; i++) {
        cin >> heights[i];
    }
    priority_queue<int, vector<int>, greater<int>> minHeap;
    for (int i = 0; i < n - 1; i++) {
        int diff = heights[i + 1] - heights[i];
        if (diff > 0) {
            minHeap.push(diff);
            if (minHeap.size() > ladders) {
                bricks -= minHeap.top();
                minHeap.pop();
            }
            if (bricks < 0) {
                cout << i << "\n";
                return;
            }
        }
    }
    cout << n - 1 << "\n";
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
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String line;
        while ((line = br.readLine()) != null) {
            line = line.trim();
            if (line.isEmpty()) continue;
            String[] parts = line.split("\s+");
            if (parts.length < 3) continue;
            int n = Integer.parseInt(parts[0]);
            long bricks = Long.parseLong(parts[1]);
            int ladders = Integer.parseInt(parts[2]);

            String heightsLine = br.readLine();
            if (heightsLine == null) break;
            String[] hParts = heightsLine.trim().split("\s+");
            int[] heights = new int[n];
            for (int i = 0; i < n; i++) {
                heights[i] = Integer.parseInt(hParts[i]);
            }

            PriorityQueue<Integer> minHeap = new PriorityQueue<>();
            int ans = n - 1;
            for (int i = 0; i < n - 1; i++) {
                int diff = heights[i + 1] - heights[i];
                if (diff > 0) {
                    minHeap.add(diff);
                    if (minHeap.size() > ladders) {
                        bricks -= minHeap.poll();
                    }
                    if (bricks < 0) {
                        ans = i;
                        break;
                    }
                }
            }
            System.out.println(ans);
        }
    }
}
```
```Python
import sys
import heapq

def main():
    input_data = sys.stdin.read().split()
    if not input_data:
        return
    ptr = 0
    while ptr < len(input_data):
        n = int(input_data[ptr])
        bricks = int(input_data[ptr + 1])
        ladders = int(input_data[ptr + 2])
        ptr += 3

        heights = [int(x) for x in input_data[ptr:ptr + n]]
        ptr += n

        min_heap = []
        ans = n - 1
        for i in range(n - 1):
            diff = heights[i + 1] - heights[i]
            if diff > 0:
                heapq.heappush(min_heap, diff)
                if len(min_heap) > ladders:
                    bricks -= heapq.heappop(min_heap)
                if bricks < 0:
                    ans = i;
                    break
        print(ans)

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
            long bricks = long.Parse(tokens[ptr++]);
            int ladders = int.Parse(tokens[ptr++]);

            int[] heights = new int[n];
            for (int i = 0; i < n; i++) heights[i] = int.Parse(tokens[ptr++]);

            PriorityQueue<int, int> minHeap = new PriorityQueue<int, int>();
            int ans = n - 1;
            for (int i = 0; i < n - 1; i++) {
                int diff = heights[i + 1] - heights[i];
                if (diff > 0) {
                    minHeap.Enqueue(diff, diff);
                    if (minHeap.Count > ladders) {
                        bricks -= minHeap.Dequeue();
                    }
                    if (bricks < 0) {
                        ans = i;
                        break;
                    }
                }
            }
            Console.WriteLine(ans);
        }
    }
}
```
```JavaScript
const fs = require('fs');

class MinHeap {
    constructor() {
        this.heap = [];
    }
    push(val) {
        this.heap.push(val);
        this._up(this.heap.length - 1);
    }
    pop() {
        if (this.heap.length === 0) return null;
        const top = this.heap[0];
        const bottom = this.heap.pop();
        if (this.heap.length > 0) {
            this.heap[0] = bottom;
            this._down(0);
        }
        return top;
    }
    size() {
        return this.heap.length;
    }
    _up(i) {
        while (i > 0) {
            const p = (i - 1) >> 1;
            if (this.heap[p] > this.heap[i]) {
                [this.heap[p], this.heap[i]] = [this.heap[i], this.heap[p]];
                i = p;
            } else break;
        }
    }
    _down(i) {
        const len = this.heap.length;
        while ((i << 1) + 1 < len) {
            let left = (i << 1) + 1, right = left + 1, smallest = i;
            if (this.heap[left] < this.heap[smallest]) smallest = left;
            if (right < len && this.heap[right] < this.heap[smallest]) smallest = right;
            if (smallest !== i) {
                [this.heap[i], this.heap[smallest]] = [this.heap[smallest], this.heap[i]];
                i = smallest;
            } else break;
        }
    }
}

function main() {
    const input = fs.readFileSync(0, 'utf-8');
    const tokens = input.trim().split(/\s+/);
    if (!tokens || tokens.length === 0 || tokens[0] === '') return;
    let ptr = 0;
    while (ptr < tokens.length) {
        const n = parseInt(tokens[ptr++]);
        if (isNaN(n)) break;
        let bricks = BigInt(tokens[ptr++]);
        const ladders = parseInt(tokens[ptr++]);

        const heights = [];
        for (let i = 0; i < n; i++) heights.push(parseInt(tokens[ptr++]));

        const minHeap = new MinHeap();
        let ans = n - 1;
        for (let i = 0; i < n - 1; i++) {
            const diff = heights[i + 1] - heights[i];
            if (diff > 0) {
                minHeap.push(diff);
                if (minHeap.size() > ladders) {
                    bricks -= BigInt(minHeap.pop());
                }
                if (bricks < 0n) {
                    ans = i;
                    break;
                }
            }
        }
        console.log(ans);
    }
}

main();
```

### Output
Input

3
7 5 1
4 2 7 6 9 14 12
8 10 2
4 12 2 7 3 18 20 3
4 0 0
14 3 19 3

Output

4
7
1

# Time Complexity
O(N log L) per testcase.

# Space Complexity
O(L) per testcase.

