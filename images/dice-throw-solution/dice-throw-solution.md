# Dice Throw - Solution

## Problem Statement

You are given the number showing on one face of a standard six-faced dice. Find the number on the face opposite to it.

In a standard dice:

- `1` is opposite to `6`
- `2` is opposite to `5`
- `3` is opposite to `4`

Print the number on the opposite face.

### Input Format

A single integer `N` representing the number on the visible face of the dice.

### Output Format

Print a single integer representing the number on the opposite face.

## Explanation

In a standard dice, the sum of the numbers on opposite faces is always `7`.

Therefore, the opposite face can be calculated using:

`Opposite = 7 - N`

For example, when `N = 2`:

Output:
5

## Algorithm

1. Read the integer `N`.
2. Compute the opposite face as `7 - N`.
3. Print the result.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    printf("%d", 7 - N);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    int N;
    cin >> N;

    cout << 7 - N;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        System.out.print(7 - N);
    }
}
```
```Python
N = int(input())

print(7 - N)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        Console.Write(7 - N);
    }
}
```

### Output
For Input:
2
Output:
5

# Time Complexity
O(1)

# Space Complexity
O(1)

