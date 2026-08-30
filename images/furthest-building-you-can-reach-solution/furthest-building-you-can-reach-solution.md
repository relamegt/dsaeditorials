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
} MinHeap;

void heap_push(MinHeap *h, int val) {
    h->data[h->size] = val;
    int i = h->size++;
    while (i > 0) {
        int p = (i - 1) / 2;
        if (h->data[p] <= h->data[i]) break;
        int tmp = h->data[p]; h->data[p] = h->data[i]; h->data[i] = tmp;
        i = p;
    }
}

int heap_pop(MinHeap *h) {
    int top = h->data[0];
    int bottom = h->data[--h->size];
    if (h->size > 0) {
        h->data[0] = bottom;
        int i = 0;
        while (1) {
            int l = 2 * i + 1, r = 2 * i + 2, smallest = i;
            if (l < h->size && h->data[l] < h->data[smallest]) smallest = l;
            if (r < h->size && h->data[r] < h->data[smallest]) smallest = r;
            if (smallest == i) break;
            int tmp = h->data[i]; h->data[i] = h->data[smallest]; h->data[smallest] = tmp;
            i = smallest;
        }
    }
    return top;
}

void solve_c() {
    int n, ladders;
    long long bricks;
    if (scanf("%d %lld %d", &n, &bricks, &ladders) != 3) return;

    int *heights = (int*)malloc(n * sizeof(int));
    for (int i = 0; i < n; i++) scanf("%d", &heights[i]);

    MinHeap h;
    h.data = (int*)malloc(n * sizeof(int));
    h.size = 0;

    int ans = n - 1;
    for (int i = 0; i < n - 1; i++) {
        int diff = heights[i + 1] - heights[i];
        if (diff > 0) {
            heap_push(&h, diff);
            if (h.size > ladders) {
                bricks -= heap_pop(&h);
            }
            if (bricks < 0) {
                ans = i;
                break;
            }
        }
    }
    printf("%d\n", ans);
    free(heights);
    free(h.data);
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
#include <queue>
using namespace std;

void solve() {
    int n;
    long long bricks;
    int ladders;
    if (!(cin >> n >> bricks >> ladders)) {
        return;
    }

    vector<int> heights(n);
    for (int i = 0; i < n; i++) {
        cin >> heights[i];
    }

    priority_queue<int, vector<int>, greater<int>> pq;
    for (int i = 0; i < n - 1; i++) {
        int diff = heights[i + 1] - heights[i];
        if (diff > 0) {
            pq.push(diff);
            if ((int)pq.size() > ladders) {
                bricks -= pq.top();
                pq.pop();
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
            solve();
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
            while (t-- > 0 && sc.hasNextInt()) {
                int n = sc.nextInt();
                long bricks = sc.nextLong();
                int ladders = sc.nextInt();
                int[] heights = new int[n];
                for (int i = 0; i < n; i++) heights[i] = sc.nextInt();

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
        sc.close();
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
    t = int(input_data[ptr])
    ptr += 1
    out = []
    for _ in range(t):
        n = int(input_data[ptr])
        bricks = int(input_data[ptr + 1])
        ladders = int(input_data[ptr + 2])
        ptr += 3
        heights = [int(x) for x in input_data[ptr : ptr + n]]
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
        out.append(str(ans))
    print('\n'.join(out))

if __name__ == '__main__':
    main()
```
```C#
using System;
using System.Collections.Generic;

class Solution {
    class MinHeap {
        private List<int> list = new List<int>();
        public int Count => list.Count;
        public void Add(int item) {
            list.Add(item);
            int i = list.Count - 1;
            while (i > 0) {
                int p = (i - 1) / 2;
                if (list[p] <= list[i]) break;
                int tmp = list[p]; list[p] = list[i]; list[i] = tmp;
                i = p;
            }
        }
        public int Pop() {
            int root = list[0];
            int last = list[list.Count - 1];
            list.RemoveAt(list.Count - 1);
            if (list.Count > 0) {
                list[0] = last;
                int i = 0;
                while (true) {
                    int l = 2 * i + 1, r = 2 * i + 2, smallest = i;
                    if (l < list.Count && list[l] < list[smallest]) smallest = l;
                    if (r < list.Count && list[r] < list[smallest]) smallest = r;
                    if (smallest == i) break;
                    int tmp = list[i]; list[i] = list[smallest]; list[smallest] = tmp;
                    i = smallest;
                }
            }
            return root;
        }
    }

    static void Main() {
        string input = Console.In.ReadToEnd();
        if (string.IsNullOrWhiteSpace(input)) return;
        string[] tokens = input.Split(new char[] { ' ', '\t', '\r', '\n' }, StringSplitOptions.RemoveEmptyEntries);
        if (tokens.Length == 0) return;
        int ptr = 0;
        int t = int.Parse(tokens[ptr++]);
        while (t-- > 0 && ptr < tokens.Length) {
            int n = int.Parse(tokens[ptr++]);
            long bricks = long.Parse(tokens[ptr++]);
            int ladders = int.Parse(tokens[ptr++]);
            int[] heights = new int[n];
            for (int i = 0; i < n; i++) heights[i] = int.Parse(tokens[ptr++]);

            MinHeap minHeap = new MinHeap();
            int ans = n - 1;
            for (int i = 0; i < n - 1; i++) {
                int diff = heights[i + 1] - heights[i];
                if (diff > 0) {
                    minHeap.Add(diff);
                    if (minHeap.Count > ladders) {
                        bricks -= minHeap.Pop();
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
    constructor() { this.heap = []; }
    push(val) {
        this.heap.push(val);
        let i = this.heap.length - 1;
        while (i > 0) {
            let p = Math.floor((i - 1) / 2);
            if (this.heap[p] <= this.heap[i]) break;
            [this.heap[p], this.heap[i]] = [this.heap[i], this.heap[p]];
            i = p;
        }
    }
    pop() {
        if (this.heap.length === 0) return 0;
        const top = this.heap[0];
        const bottom = this.heap.pop();
        if (this.heap.length > 0) {
            this.heap[0] = bottom;
            let i = 0;
            while (true) {
                let l = 2 * i + 1, r = 2 * i + 2, smallest = i;
                if (l < this.heap.length && this.heap[l] < this.heap[smallest]) smallest = l;
                if (r < this.heap.length && this.heap[r] < this.heap[smallest]) smallest = r;
                if (smallest === i) break;
                [this.heap[i], this.heap[smallest]] = [this.heap[smallest], this.heap[i]];
                i = smallest;
            }
        }
        return top;
    }
    size() { return this.heap.length; }
}

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
        out.push(ans.toString());
    }
    console.log(out.join('\n'));
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

