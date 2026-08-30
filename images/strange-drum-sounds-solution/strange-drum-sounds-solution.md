# Strange Drum Sounds - Solution

## Problem Statement

You have two drums in front of you: a left drum and a right drum. A hit on the left can be recorded as "L", and a hit on the right as "R".

The strange forces that rule this world are fickle: sometimes, a blow sounds once, and sometimes it sounds twice. Therefore, a hit on the left drum could have sounded as either "L" or "LL", and a hit on the right drum could have sounded as either "R" or "RR".

The sequence of hits made is recorded in the string $p$, and the sounds heard are in the string $s$. Given $p$ and $s$, determine whether it is true that the string $s$ could have been the result of the hits from the string $p$.

For example, if $p="LR"$, then the result of the hits could be any of the strings "LR", "LRR", "LLR", and "LLRR", but the strings "LLLR" or "LRL" cannot.

## Input Format

- The first line contains an integer $t$ ($1 \le t \le 10^4$) — the number of test cases.
- The first line contains the string $p$ ($1 \le |p| \le 2 \cdot 10^5$) consisting only of the characters 'R' and 'L', where $|p|$ denotes the length of $p$.
- The second line contains the string $s$ ($1 \le |p| \le |s| \le 2 \cdot 10^5$) consisting only of the characters 'R' and 'L'.

It is guaranteed that the sum of $|s|$ does not exceed $2 \cdot 10^5$ across all test cases.

## Output Format

For each set of input data, output "YES" if $s$ can be the heard sound from hits $p$, and "NO" otherwise. You may output in any case.

## Explanation

First, let's consider a simple case: suppose that the hit sequence $p$ and heard sound $s$ consist of only a single character type (e.g. all `'L'`s). If $p$ has length $n$, each hit can sound once or twice. Thus, the heard sound $s$ must have length $m$ between $n$ and $2n$ ($n \le m \le 2n$).

Now, observe that any general string $p$ and $s$ can be partitioned into consecutive "blocks" of identical characters (Run-Length Encoding / RLE). For $s$ to be a valid heard sound from hits $p$:

1. $p$ and $s$ must start with the same character (`p[0] == s[0]`).
2. $|p| \le |s| \le 2|p|$.
3. When compressed into block counts, $p$ and $s$ must have the exact same number of blocks (`aa.size() == bb.size()`).
4. For each block $i$, the length of block $i$ in $s$ (`bb[i]`) must satisfy `aa[i] <= bb[i] <= 2 * aa[i]` where `aa[i]` is the block length in $p$.

### Algorithm

1. Read the number of test cases $t$.
2. For each testcase ($p$, $s$):

- Check if $|s| &lt; |p|$ or $|s| &gt; 2|p|$ or `p[0] != s[0]`. If so, return "NO".
- Compress $p$ into block length array `aa`.
- Compress $s$ into block length array `bb`.
- If `aa.size() != bb.size()`, return "NO".
- For each block index $i$, check if `aa[i] <= bb[i] <= 2 * aa[i]`. If invalid for any block, return "NO".
- Return "YES" if all blocks are valid.

```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void solve_c(char *p, char *s) {
    int n = strlen(p);
    int m = strlen(s);
    if (m < n || m > 2 * n || p[0] != s[0]) {
        printf("NO\n");
        return;
    }
    int *aa = (int*)malloc(n * sizeof(int));
    int aa_sz = 0;
    int cnt = 1;
    for (int i = 1; i < n; i++) {
        if (p[i] != p[i-1]) {
            aa[aa_sz++] = cnt;
            cnt = 1;
        } else cnt++;
    }
    aa[aa_sz++] = cnt;

    int *bb = (int*)malloc(m * sizeof(int));
    int bb_sz = 0;
    cnt = 1;
    for (int i = 1; i < m; i++) {
        if (s[i] != s[i-1]) {
            bb[bb_sz++] = cnt;
            cnt = 1;
        } else cnt++;
    }
    bb[bb_sz++] = cnt;

    if (aa_sz != bb_sz) {
        printf("NO\n");
        free(aa);
        free(bb);
        return;
    }
    for (int i = 0; i < aa_sz; i++) {
        if (aa[i] > bb[i] || aa[i] * 2 < bb[i]) {
            printf("NO\n");
            free(aa);
            free(bb);
            return;
        }
    }
    printf("YES\n");
    free(aa);
    free(bb);
}

int main() {
    static char p[200005];
    static char s[200005];
    while (scanf("%s %s", p, s) == 2) {
        solve_c(p, s);
    }
    return 0;
}
```
```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

void solveTestCase() {
    string p, s;
    if (!(cin >> p >> s)) return;
    int n = p.size();
    int m = s.size();
    if (m < n || m > 2 * n || p[0] != s[0]) {
        cout << "NO\n";
        return;
    }
    vector<int> aa, bb;
    int cnt = 1;
    for (int i = 1; i < n; i++) {
        if (p[i] != p[i-1]) {
            aa.push_back(cnt);
            cnt = 1;
        } else cnt++;
    }
    aa.push_back(cnt);

    cnt = 1;
    for (int i = 1; i < m; i++) {
        if (s[i] != s[i-1]) {
            bb.push_back(cnt);
            cnt = 1;
        } else cnt++;
    }
    bb.push_back(cnt);

    if (aa.size() != bb.size()) {
        cout << "NO\n";
        return;
    }
    for (size_t i = 0; i < aa.size(); i++) {
        if (aa[i] > bb[i] || aa[i] * 2 < bb[i]) {
            cout << "NO\n";
            return;
        }
    }
    cout << "YES\n";
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
                String p = sc.next();
                String s = sc.next();

                int n = p.length();
                int m = s.length();

                if (m < n || m > 2 * n || p.charAt(0) != s.charAt(0)) {
                    System.out.println("NO");
                    continue;
                }

                List<Integer> aa = getRunLengths(p);
                List<Integer> bb = getRunLengths(s);

                if (aa.size() != bb.size()) {
                    System.out.println("NO");
                    continue;
                }

                boolean ok = true;
                for (int i = 0; i < aa.size(); i++) {
                    int countA = aa.get(i);
                    int countB = bb.get(i);
                    if (countB < countA || countB > 2 * countA) {
                        ok = false;
                        break;
                    }
                }

                System.out.println(ok ? "YES" : "NO");
            }
        }
        sc.close();
    }

    private static List<Integer> getRunLengths(String str) {
        List<Integer> list = new ArrayList<>();
        int cnt = 1;
        for (int i = 1; i < str.length(); i++) {
            if (str.charAt(i) != str.charAt(i - 1)) {
                list.add(cnt);
                cnt = 1;
            } else {
                cnt++;
            }
        }
        list.add(cnt);
        return list;
    }
}
```
```Python
import sys

def solve(p, s):
    n, m = len(p), len(s)
    if m < n or m > 2 * n or p[0] != s[0]:
        return "NO"
    aa = []
    cnt = 1
    for i in range(1, n):
        if p[i] != p[i-1]:
            aa.append(cnt)
            cnt = 1
        else:
            cnt += 1
    aa.append(cnt)

    bb = []
    cnt = 1
    for i in range(1, m):
        if s[i] != s[i-1]:
            bb.append(cnt)
            cnt = 1
        else:
            cnt += 1
    bb.append(cnt)

    if len(aa) != len(bb):
        return "NO"
    for i in range(len(aa)):
        if aa[i] > bb[i] or aa[i] * 2 < bb[i]:
            return "NO"
    return "YES"

def main():
    lines = sys.stdin.read().split()
    if not lines:
        return
    ptr = 0
    while ptr < len(lines):
        p = lines[ptr]
        if ptr + 1 >= len(lines):
            break
        s = lines[ptr + 1]
        ptr += 2
        print(solve(p, s))

if __name__ == '__main__':
    main()
```
```C#
using System;
using System.Collections.Generic;

class Solution {
    static string Solve(string p, string s) {
        int n = p.Length, m = s.Length;
        if (m < n || m > 2 * n || p[0] != s[0]) return "NO";
        List<int> aa = new List<int>();
        int cnt = 1;
        for (int i = 1; i < n; i++) {
            if (p[i] != p[i - 1]) {
                aa.Add(cnt);
                cnt = 1;
            } else cnt++;
        }
        aa.Add(cnt);

        List<int> bb = new List<int>();
        cnt = 1;
        for (int i = 1; i < m; i++) {
            if (s[i] != s[i - 1]) {
                bb.Add(cnt);
                cnt = 1;
            } else cnt++;
        }
        bb.Add(cnt);

        if (aa.Count != bb.Count) return "NO";
        for (int i = 0; i < aa.Count; i++) {
            if (aa[i] > bb[i] || aa[i] * 2 < bb[i]) return "NO";
        }
        return "YES";
    }

    static void Main() {
        string input = Console.In.ReadToEnd();
        if (string.IsNullOrWhiteSpace(input)) return;
        string[] tokens = input.Split(new char[] { ' ', '\t', '\r', '\n' }, StringSplitOptions.RemoveEmptyEntries);
        int ptr = 0;
        while (ptr < tokens.Length) {
            string p = tokens[ptr++];
            if (ptr >= tokens.Length) break;
            string s = tokens[ptr++];
            Console.WriteLine(Solve(p, s));
        }
    }
}
```
```JavaScript
const fs = require('fs');

function solve(p, s) {
    const n = p.length, m = s.length;
    if (m < n || m > 2 * n || p[0] !== s[0]) return "NO";
    const aa = [];
    let cnt = 1;
    for (let i = 1; i < n; i++) {
        if (p[i] !== p[i - 1]) {
            aa.push(cnt);
            cnt = 1;
        } else cnt++;
    }
    aa.push(cnt);

    const bb = [];
    cnt = 1;
    for (let i = 1; i < m; i++) {
        if (s[i] !== s[i - 1]) {
            bb.push(cnt);
            cnt = 1;
        } else cnt++;
    }
    bb.push(cnt);

    if (aa.length !== bb.length) return "NO";
    for (let i = 0; i < aa.length; i++) {
        if (aa[i] > bb[i] || aa[i] * 2 < bb[i]) return "NO";
    }
    return "YES";
}

function main() {
    const input = fs.readFileSync(0, 'utf-8');
    const tokens = input.trim().split(/\s+/);
    if (!tokens || tokens.length < 2) return;
    let ptr = 0;
    while (ptr < tokens.length) {
        const p = tokens[ptr++];
        if (ptr >= tokens.length) break;
        const s = tokens[ptr++];
        console.log(solve(p, s));
    }
}

main();
```

### Output
Input

3
R
RR
LRLR
LRLR
LR
LLLR

Output

YES
YES
NO

# Time Complexity
O(|p| + |s|) per testcase.

# Space Complexity
O(|p| + |s|) per testcase.

