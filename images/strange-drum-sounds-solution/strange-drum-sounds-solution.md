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
#include <string.h>
#include <stdlib.h>

int get_run_lengths(const char *s, int *arr) {
    int cnt = 1;
    int len = 0;
    int n = strlen(s);
    for (int i = 1; i < n; i++) {
        if (s[i] != s[i - 1]) {
            arr[len++] = cnt;
            cnt = 1;
        } else {
            cnt++;
        }
    }
    arr[len++] = cnt;
    return len;
}

void solve_c() {
    char p[500005], s[500005];
    if (scanf("%s %s", p, s) != 2) return;

    int n = strlen(p), m = strlen(s);
    if (m < n || m > 2 * n || p[0] != s[0]) {
        printf("NO\n");
        return;
    }

    int *aa = (int*)malloc((n + 5) * sizeof(int));
    int *bb = (int*)malloc((m + 5) * sizeof(int));

    int lenA = get_run_lengths(p, aa);
    int lenB = get_run_lengths(s, bb);

    if (lenA != lenB) {
        printf("NO\n");
        free(aa);
        free(bb);
        return;
    }

    int ok = 1;
    for (int i = 0; i < lenA; i++) {
        if (bb[i] < aa[i] || bb[i] > 2 * aa[i]) {
            ok = 0;
            break;
        }
    }
    printf("%s\n", ok ? "YES" : "NO");
    free(aa);
    free(bb);
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
#include <string>
#include <vector>
using namespace std;

void solve() {
    string p, s;
    if (!(cin >> p >> s)) {
        return;
    }

    int n = p.size();
    int m = s.size();

    if (m < n || m > 2 * n || p[0] != s[0]) {
        cout << "NO\n";
        return;
    }

    vector<int> bP, bS;
    for (int i = 0; i < n; ) {
        int j = i;
        while (j < n && p[j] == p[i]) {
            j++;
        }
        bP.push_back(j - i);
        i = j;
    }

    for (int i = 0; i < m; ) {
        int j = i;
        while (j < m && s[j] == s[i]) {
            j++;
        }
        bS.push_back(j - i);
        i = j;
    }

    if (bP.size() != bS.size()) {
        cout << "NO\n";
        return;
    }

    for (size_t k = 0; k < bP.size(); k++) {
        if (bS[k] < bP[k] || bS[k] > 2 * bP[k]) {
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
            while (t-- > 0 && sc.hasNext()) {
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

def get_run_lengths(s):
    res = []
    cnt = 1
    for i in range(1, len(s)):
        if s[i] != s[i - 1]:
            res.append(cnt)
            cnt = 1
        else:
            cnt += 1
    res.append(cnt)
    return res

def main():
    input_data = sys.stdin.read().split()
    if not input_data:
        return
    ptr = 0
    t = int(input_data[ptr])
    ptr += 1
    out = []
    for _ in range(t):
        p = input_data[ptr]
        s = input_data[ptr + 1]
        ptr += 2

        n, m = len(p), len(s)
        if m < n or m > 2 * n or p[0] != s[0]:
            out.append("NO")
            continue

        aa = get_run_lengths(p)
        bb = get_run_lengths(s)

        if len(aa) != len(bb):
            out.append("NO")
            continue

        ok = True
        for i in range(len(aa)):
            if bb[i] < aa[i] or bb[i] > 2 * aa[i]:
                ok = False
                break
        out.append("YES" if ok else "NO")
    print('\n'.join(out))

if __name__ == '__main__':
    main()
```
```C#
using System;
using System.Collections.Generic;

class Solution {
    static List<int> GetRunLengths(string str) {
        var list = new List<int>();
        int cnt = 1;
        for (int i = 1; i < str.Length; i++) {
            if (str[i] != str[i - 1]) {
                list.Add(cnt);
                cnt = 1;
            } else {
                cnt++;
            }
        }
        list.Add(cnt);
        return list;
    }

    static void Main() {
        string input = Console.In.ReadToEnd();
        if (string.IsNullOrWhiteSpace(input)) return;
        string[] tokens = input.Split(new char[] { ' ', '\t', '\r', '\n' }, StringSplitOptions.RemoveEmptyEntries);
        if (tokens.Length == 0) return;
        int ptr = 0;
        int t = int.Parse(tokens[ptr++]);
        while (t-- > 0 && ptr < tokens.Length) {
            string p = tokens[ptr++];
            string s = tokens[ptr++];

            int n = p.Length;
            int m = s.Length;

            if (m < n || m > 2 * n || p[0] != s[0]) {
                Console.WriteLine("NO");
                continue;
            }

            List<int> aa = GetRunLengths(p);
            List<int> bb = GetRunLengths(s);

            if (aa.Count != bb.Count) {
                Console.WriteLine("NO");
                continue;
            }

            bool ok = true;
            for (int i = 0; i < aa.Count; i++) {
                if (bb[i] < aa[i] || bb[i] > 2 * aa[i]) {
                    ok = false;
                    break;
                }
            }
            Console.WriteLine(ok ? "YES" : "NO");
        }
    }
}
```
```JavaScript
const fs = require('fs');

function getRunLengths(str) {
    const list = [];
    let cnt = 1;
    for (let i = 1; i < str.length; i++) {
        if (str[i] !== str[i - 1]) {
            list.push(cnt);
            cnt = 1;
        } else {
            cnt++;
        }
    }
    list.push(cnt);
    return list;
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
        const p = tokens[ptr++];
        const s = tokens[ptr++];

        const n = p.length;
        const m = s.length;

        if (m < n || m > 2 * n || p[0] !== s[0]) {
            out.push("NO");
            continue;
        }

        const aa = getRunLengths(p);
        const bb = getRunLengths(s);

        if (aa.length !== bb.length) {
            out.push("NO");
            continue;
        }

        let ok = true;
        for (let i = 0; i < aa.length; i++) {
            if (bb[i] < aa[i] || bb[i] > 2 * aa[i]) {
                ok = false;
                break;
            }
        }
        out.push(ok ? "YES" : "NO");
    }
    console.log(out.join('\n'));
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

