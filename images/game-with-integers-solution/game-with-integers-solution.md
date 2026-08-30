# Game with Integers - Solution

## Problem Statement

Vanya and Vova are playing a game starting with an integer $n$.

On their turn, a player can either add $1$ to the current integer or subtract $1$. The players take turns, and Vanya starts first.

- Vanya wins if, after any of his moves, the integer becomes divisible by $3$.
- If $10$ moves pass and Vanya has not won, Vova wins.

Assuming both players play optimally, determine who will win the game.

## Input Format

- The first line contains an integer $t$ ($1 \le t \le 10^4$) — the number of test cases.
- A single line containing the integer $n$ ($1 \le n \le 1000$).

## Output Format

Output "First" (without quotes) if Vanya wins, and "Second" (without quotes) if Vova wins.

## Explanation

Consider the remainder when dividing $n$ by $3$ ($n \pmod 3$):

- **If $n \pmod 3 \neq 0$** (i.e., remainder is $1$ or $2$):

  Vanya can immediately add $1$ (if remainder is $2$) or subtract $1$ (if remainder is $1$) on his very first move to make $n$ divisible by $3$. Thus, Vanya ("First") wins in just $1$ move.

- **If $n \pmod 3 = 0$** (remainder is $0$):

  $n$ is already divisible by $3$. Any move Vanya makes will change $n$ such that it is no longer divisible by $3$. Vova can then make an opposing move to make $n$ divisible by $3$ again. This pattern continues indefinitely, preventing Vanya from leaving $n$ divisible by $3$ at the end of his turn. Thus, Vova ("Second") wins.

### Algorithm

1. Read input integer $n$.
2. For each test case integer $n$:

- If `n % 3 != 0`, output "First".
- If `n % 3 == 0`, output "Second".

```C
#include <stdio.h>

int main() {
    int t;
    if (scanf("%d", &t) == 1) {
        while (t--) {
            int n;
            scanf("%d", &n);
            if (n % 3 != 0) printf("First\n");
            else printf("Second\n");
        }
    }
    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

void solve() {
    int n;
    if (!(cin >> n)) {
        return;
    }
    if (n % 3 != 0) {
        cout << "First\n";
    } else {
        cout << "Second\n";
    }
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
                if (n % 3 != 0) System.out.println("First");
                else System.out.println("Second");
            }
        }
        sc.close();
    }
}
```
```Python
import sys

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
        if n % 3 != 0:
            out.append("First")
        else:
            out.append("Second")
    print('\n'.join(out))

if __name__ == '__main__':
    main()
```
```C#
using System;

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
            if (n % 3 != 0) Console.WriteLine("First");
            else Console.WriteLine("Second");
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
        if (n % 3 !== 0) out.push("First");
        else out.push("Second");
    }
    console.log(out.join('\n'));
}

main();
```

### Output
Input

2
1
3

Output

First
Second

# Time Complexity
O(1) per testcase.

# Space Complexity
O(1).

