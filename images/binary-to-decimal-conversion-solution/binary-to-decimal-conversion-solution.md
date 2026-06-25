# Binary to Decimal Conversion - Solution

## Problem Statement

Given a binary number represented as a string `B`, convert it to its decimal equivalent.

### Input Format

A single string `B` consisting of characters `'0'` and `'1'`.

### Output Format

Print a single integer representing the decimal equivalent of `B`.

## Explanation

There are two common approaches to convert a binary number to decimal.

- **Using Positional Values:** Traverse the binary string from right to left. Multiply each bit by its corresponding power of `2` and add the results.
- **Using Accumulation (Recommended):** Traverse the binary string from left to right. For each bit, multiply the current decimal value by `2` and add the current bit. This is similar to constructing a decimal number digit by digit.

For example, when `B = 1010`:

- Start with `decimal = 0`
- Read `1`: `0 × 2 + 1 = 1`
- Read `0`: `1 × 2 + 0 = 2`
- Read `1`: `2 × 2 + 1 = 5`
- Read `0`: `5 × 2 + 0 = 10`

Output:
10

<approaches>
## Approach 1: Using Positional Values

### Algorithm

1. Read the binary string `B`.
2. Initialize `decimal = 0` and `power = 1`.
3. Traverse the string from right to left.
4. For each character:

- Convert the character to its numeric value (`0` or `1`).
- Multiply the bit by the current power of `2` and add it to `decimal`.
- Update the power by multiplying it by `2`.

1. Print `decimal`.

```C
#include <stdio.h>
#include <string.h>

int main() {
    char B[65];
    scanf("%s", B);

    unsigned long long decimal = 0;
    unsigned long long power = 1;

    for (int i = strlen(B) - 1; i >= 0; i--) {
        decimal += (B[i] - '0') * power;
        power *= 2;
    }

    printf("%llu", decimal);

    return 0;
}
```
```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string B;
    cin >> B;

    unsigned long long decimal = 0;
    unsigned long long power = 1;

    for (int i = B.length() - 1; i >= 0; i--) {
        decimal += (B[i] - '0') * power;
        power *= 2;
    }

    cout << decimal;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        String B = sc.next();

        long decimal = 0;
        long power = 1;

        for (int i = B.length() - 1; i >= 0; i--) {
            decimal += (B.charAt(i) - '0') * power;
            power *= 2;
        }

        System.out.print(decimal);
    }
}
```
```Python
B = input()

decimal = 0
power = 1

for i in range(len(B) - 1, -1, -1):
    decimal += int(B[i]) * power
    power *= 2

print(decimal)
```
```C#
using System;

class Program
{
    static void Main()
    {
        string B = Console.ReadLine();

        ulong decimalValue = 0;
        ulong power = 1;

        for (int i = B.Length - 1; i >= 0; i--)
        {
            decimalValue += (ulong)(B[i] - '0') * power;
            power *= 2;
        }

        Console.Write(decimalValue);
    }
}
```

### Output
For Input:
1010
Output:
10

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Using Accumulation (Recommended)

### Algorithm

1. Read the binary string `B`.
2. Initialize `decimal = 0`.
3. Traverse the binary string from left to right.
4. For each bit:

- Multiply the current decimal value by `2`.
- Add the numeric value of the current bit (`0` or `1`).

1. After processing all bits, print `decimal`.

```C
#include <stdio.h>

int main() {
    char B[65];
    scanf("%s", B);

    unsigned long long decimal = 0;

    for (int i = 0; B[i] != ''; i++) {
        decimal = decimal * 2 + (B[i] - '0');
    }

    printf("%llu", decimal);

    return 0;
}
```
```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string B;
    cin >> B;

    unsigned long long decimal = 0;

    for (char bit : B) {
        decimal = decimal * 2 + (bit - '0');
    }

    cout << decimal;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        String B = sc.next();

        long decimal = 0;

        for (int i = 0; i < B.length(); i++) {
            decimal = decimal * 2 + (B.charAt(i) - '0');
        }

        System.out.print(decimal);
    }
}
```
```Python
B = input()

decimal = 0

for bit in B:
    decimal = decimal * 2 + int(bit)

print(decimal)
```
```C#
using System;

class Program
{
    static void Main()
    {
        string B = Console.ReadLine();

        ulong decimalValue = 0;

        foreach (char bit in B)
        {
            decimalValue = decimalValue * 2 + (ulong)(bit - '0');
        }

        Console.Write(decimalValue);
    }
}
```

### Output
For Input:
1010
Output:
10

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>

