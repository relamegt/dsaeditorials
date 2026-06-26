# Determinant of a Matrix - Solution

## Problem Statement

Given a square matrix of size `N × N`, find its determinant.

The determinant is a single integer value associated with a square matrix.

## Input Format

First line: Integer `N` representing the size of the matrix.

Next `N` lines: `N` space-separated integers representing the matrix.

## Output Format

Print a single integer representing the determinant of the matrix.

## Explanation

There is one standard approach to solve this problem using recursive expansion by cofactors.

For example,

Input

2

3 2

2 3

Output

5

## Algorithm

1. Read the matrix.
2. If the matrix size is `1`, return its only element.
3. If the matrix size is `2`, apply the determinant formula directly.
4. Otherwise, expand along the first row.
5. For every element in the first row:

- Construct its minor matrix.
- Recursively compute its determinant.
- Add or subtract the contribution based on its position.

1. Print the final determinant.

```C
#include <stdio.h>

long long determinant(long long a[10][10], int n)
{
    if(n == 1)
        return a[0][0];

    if(n == 2)
        return a[0][0] * a[1][1] - a[0][1] * a[1][0];

    long long det = 0;
    long long temp[10][10];

    for(int col = 0; col < n; col++)
    {
        int r = 0;

        for(int i = 1; i < n; i++)
        {
            int c = 0;

            for(int j = 0; j < n; j++)
            {
                if(j == col)
                    continue;

                temp[r][c++] = a[i][j];
            }

            r++;
        }

        long long sign = (col % 2 == 0) ? 1 : -1;

        det += sign * a[0][col] * determinant(temp, n - 1);
    }

    return det;
}

int main()
{
    int n;
    scanf("%d", &n);

    long long a[10][10];

    for(int i = 0; i < n; i++)
        for(int j = 0; j < n; j++)
            scanf("%lld", &a[i][j]);

    printf("%lld", determinant(a, n));

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

long long determinant(long long a[10][10], int n)
{
    if(n == 1)
        return a[0][0];

    if(n == 2)
        return a[0][0] * a[1][1] - a[0][1] * a[1][0];

    long long det = 0;
    long long temp[10][10];

    for(int col = 0; col < n; col++)
    {
        int r = 0;

        for(int i = 1; i < n; i++)
        {
            int c = 0;

            for(int j = 0; j < n; j++)
            {
                if(j == col)
                    continue;

                temp[r][c++] = a[i][j];
            }

            r++;
        }

        long long sign = (col % 2 == 0) ? 1 : -1;

        det += sign * a[0][col] * determinant(temp, n - 1);
    }

    return det;
}

int main()
{
    int n;
    cin >> n;

    long long a[10][10];

    for(int i = 0; i < n; i++)
        for(int j = 0; j < n; j++)
            cin >> a[i][j];

    cout << determinant(a, n);

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    static long determinant(long[][] a, int n)
    {
        if(n == 1)
            return a[0][0];

        if(n == 2)
            return a[0][0] * a[1][1] - a[0][1] * a[1][0];

        long det = 0;

        for(int col = 0; col < n; col++)
        {
            long[][] temp = new long[n - 1][n - 1];

            int r = 0;

            for(int i = 1; i < n; i++)
            {
                int c = 0;

                for(int j = 0; j < n; j++)
                {
                    if(j == col)
                        continue;

                    temp[r][c++] = a[i][j];
                }

                r++;
            }

            long sign = (col % 2 == 0) ? 1 : -1;

            det += sign * a[0][col] * determinant(temp, n - 1);
        }

        return det;
    }

    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        long[][] a = new long[n][n];

        for(int i = 0; i < n; i++)
            for(int j = 0; j < n; j++)
                a[i][j] = sc.nextLong();

        System.out.print(determinant(a, n));
    }
}
```
```Python
def determinant(a):

    n = len(a)

    if n == 1:
        return a[0][0]

    if n == 2:
        return a[0][0] * a[1][1] - a[0][1] * a[1][0]

    det = 0

    for col in range(n):

        temp = []

        for i in range(1, n):
            row = []

            for j in range(n):
                if j != col:
                    row.append(a[i][j])

            temp.append(row)

        sign = 1 if col % 2 == 0 else -1

        det += sign * a[0][col] * determinant(temp)

    return det

n = int(input())

a = [list(map(int, input().split())) for _ in range(n)]

print(determinant(a))
```
```C#
using System;

class Program
{
    static long Determinant(long[][] a, int n)
    {
        if(n == 1)
            return a[0][0];

        if(n == 2)
            return a[0][0] * a[1][1] - a[0][1] * a[1][0];

        long det = 0;

        for(int col = 0; col < n; col++)
        {
            long[][] temp = new long[n - 1][];

            for(int i = 0; i < n - 1; i++)
                temp[i] = new long[n - 1];

            int r = 0;

            for(int i = 1; i < n; i++)
            {
                int c = 0;

                for(int j = 0; j < n; j++)
                {
                    if(j == col)
                        continue;

                    temp[r][c++] = a[i][j];
                }

                r++;
            }

            long sign = (col % 2 == 0) ? 1 : -1;

            det += sign * a[0][col] * Determinant(temp, n - 1);
        }

        return det;
    }

    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[][] a = new long[n][];

        for(int i = 0; i < n; i++)
            a[i] = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        Console.Write(Determinant(a, n));
    }
}
```
```JavaScript
function determinant(a)
{
    const n = a.length;

    if(n === 1)
        return a[0][0];

    if(n === 2)
        return a[0][0] * a[1][1] - a[0][1] * a[1][0];

    let det = 0;

    for(let col = 0; col < n; col++)
    {
        const temp = [];

        for(let i = 1; i < n; i++)
        {
            const row = [];

            for(let j = 0; j < n; j++)
            {
                if(j !== col)
                    row.push(a[i][j]);
            }

            temp.push(row);
        }

        const sign = col % 2 === 0 ? 1 : -1;

        det += sign * a[0][col] * determinant(temp);
    }

    return det;
}

const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const a = Array.from({length: n}, () => Array(n));

for(let i = 0; i < n; i++)
    for(let j = 0; j < n; j++)
        a[i][j] = input[idx++];

console.log(determinant(a));
```

### Output
Input

2

3 2

2 3

Output

5

# Time Complexity
O(N!)

# Space Complexity
O(N²)




