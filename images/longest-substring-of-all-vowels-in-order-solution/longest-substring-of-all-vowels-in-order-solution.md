# Longest Substring of All Vowels in Order - Solution

## Problem Statement

A substring of a string consisting only of English vowels (`'a'`, `'e'`, `'i'`, `'o'`, `'u'`) is called **beautiful** if:

1. Every vowel (`'a'`, `'e'`, `'i'`, `'o'`, `'u'`) appears at least once in the substring.
2. The vowels in the substring appear in non-decreasing alphabetical order (i.e. all `'a'`s before `'e'`s, `'e'`s before `'i'`s, `'i'`s before `'o'`s, and `'o'`s before `'u'`s).

Given a string `word` consisting only of vowels, return the length of the **longest beautiful substring** of `word`. If no such substring exists, return `0`.

## Input Format

- The first line contains an integer $t$ ($1 \le t \le 10^4$) — the number of test cases.
- A single line containing the string `word` consisting only of lowercase English vowels (`'a'`, `'e'`, `'i'`, `'o'`, `'u'`).

## Output Format

Output a single integer representing the length of the longest beautiful substring.

## Explanation

We can solve this problem in a single pass using a **Two Pointer / Sliding Window** approach:

1. Maintain a left pointer `p` (the start of the current sorted substring window) and a `count` variable tracking the number of unique vowels encountered in non-decreasing order.
2. Traverse the string from index $i = 1$ to $n - 1$:

- If `word[i - 1] < word[i]`: We transition to the next vowel in strict alphabetical order (e.g. `'a'` $\to$ `'e'`). Increment `count` by $1$.
- Else if `word[i - 1] > word[i]`: The non-decreasing order is broken (e.g. `'u'` $\to$ `'a'`). Reset our current window start `p = i` and reset `count = 1`.
- If `word[i - 1] == word[i]`: The character is identical to the previous one, so the order is maintained without introducing a new unique vowel.

1. Whenever `count == 5` (all 5 vowels `'a'`, `'e'`, `'i'`, `'o'`, `'u'` have been encountered in order), update our maximum length:

   $$\text{ans} = \max(\text{ans}, i - p + 1)$$

### Algorithm

1. Initialize `ans = 0`, `p = 0`, `count = 1`.
2. Iterate $i$ from $1$ to `word.length() - 1`:

- If `word[i - 1] < word[i]`, `count++`.
- Else if `word[i - 1] > word[i]`, `p = i` and `count = 1`.
- If `count == 5`, `ans = max(ans, i - p + 1)`.

1. Return `ans`.

```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void solve_c(const char *word) {
    int n = strlen(word);
    int ans = 0, p = 0, count = 1;
    for (int i = 1; i < n; i++) {
        if (word[i - 1] < word[i]) {
            count++;
        } else if (word[i - 1] > word[i]) {
            p = i;
            count = 1;
        }
        if (count == 5) {
            int len = i - p + 1;
            if (len > ans) ans = len;
        }
    }
    printf("%d\n", ans);
}

int main() {
    static char word[500005];
    while (scanf("%s", word) == 1) {
        solve_c(word);
    }
    return 0;
}
```
```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

void solveTestCase() {
    string word;
    if (!(cin >> word)) return;
    int n = word.length();
    int ans = 0, p = 0, count = 1;
    for (int i = 1; i < n; i++) {
        if (word[i - 1] < word[i]) {
            count++;
        } else if (word[i - 1] > word[i]) {
            p = i;
            count = 1;
        }
        if (count == 5) {
            ans = max(ans, i - p + 1);
        }
    }
    cout << ans << "\n";
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
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        if (sc.hasNextInt()) {
            int t = sc.nextInt();
            while (t-- > 0) {
                String word = sc.next();
                int n = word.length();
                int ans = 0, p = 0, count = 1;
                for (int i = 1; i < n; i++) {
                    if (word.charAt(i - 1) < word.charAt(i)) {
                        count++;
                    } else if (word.charAt(i - 1) > word.charAt(i)) {
                        p = i;
                        count = 1;
                    }
                    if (count == 5) {
                        ans = Math.max(ans, i - p + 1);
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

def main():
    words = sys.stdin.read().split()
    for word in words:
        n = len(word)
        ans = 0
        p = 0
        count = 1
        for i in range(1, n):
            if word[i - 1] < word[i]:
                count += 1
            elif word[i - 1] > word[i]:
                p = i
                count = 1
            if count == 5:
                ans = max(ans, i - p + 1)
        print(ans)

if __name__ == '__main__':
    main()
```
```C#
using System;

class Solution {
    static void Main() {
        string input = Console.In.ReadToEnd();
        if (string.IsNullOrWhiteSpace(input)) return;
        string[] words = input.Split(new char[] { ' ', '\t', '\r', '\n' }, StringSplitOptions.RemoveEmptyEntries);
        foreach (string word in words) {
            int n = word.Length;
            int ans = 0, p = 0, count = 1;
            for (int i = 1; i < n; i++) {
                if (word[i - 1] < word[i]) {
                    count++;
                } else if (word[i - 1] > word[i]) {
                    p = i;
                    count = 1;
                }
                if (count == 5) {
                    ans = Math.Max(ans, i - p + 1);
                }
            }
            Console.WriteLine(ans);
        }
    }
}
```
```JavaScript
const fs = require('fs');

function main() {
    const input = fs.readFileSync(0, 'utf-8');
    const words = input.trim().split(/\s+/);
    if (!words || words.length === 0 || words[0] === '') return;
    for (const word of words) {
        const n = word.length;
        let ans = 0, p = 0, count = 1;
        for (let i = 1; i < n; i++) {
            if (word.charCodeAt(i - 1) < word.charCodeAt(i)) {
                count++;
            } else if (word.charCodeAt(i - 1) > word.charCodeAt(i)) {
                p = i;
                count = 1;
            }
            if (count === 5) {
                ans = Math.max(ans, i - p + 1);
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
aeiaelioouaaeeiouu
aeeeiiiioooauuuaeiou
a

Output

8
5
0

# Time Complexity
O(|word|) per testcase.

# Space Complexity
O(1).

