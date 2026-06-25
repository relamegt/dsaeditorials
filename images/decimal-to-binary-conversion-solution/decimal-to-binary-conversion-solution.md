# Decimal to Binary Conversion - Solution

## Problem Statement

Given a non-negative integer `N` in decimal, convert it to its binary representation and print it.

### Input Format

A single integer `N`.

### Output Format

Print the binary representation of `N` as a string without leading zeros. If `N = 0`, print `0`.

## Explanation

There are two common approaches to convert a decimal number to binary.

- **Using Division by 2 (Recommended):** Repeatedly divide the number by `2`. The remainder obtained in each step is a binary digit. Since the remainders are obtained from right to left, reverse them at the end.
- **Using Bit Manipulation:** Check each bit of the number starting from the most significant set bit down to the least significant bit and print each bit.

For example, when `N = 10`:

- `10 ÷ 2 = 5`, remainder = `0`
- `5 ÷ 2 = 2`, remainder = `1`
- `2 ÷ 2 = 1`, remainder = `0`
- `1 ÷ 2 = 0`, remainder = `1`

Reading the remainders from bottom to top gives:

`1010`

Output:
1010

<approaches>
## Approach 1: Using Division by 2 (Recommended)

### Algorithm

1. Read the integer `N`.
2. If `N` is `0`, print `0`.
3. Initialize an empty string.
4. Repeat until `N` becomes `0`:

- Find the remainder when dividing `N` by `2` using `N % 2`.
- Append the remainder to the string.
- Divide `N` by `2` using integer division.

1. Reverse the obtained string because the binary digits were collected from right to left.
2. Print the reversed string.

```C
#include <stdio.h>
#include <string.h>

int main() {
    unsigned long long N;
    scanf("%llu", &N);

    if (N == 0) {
        printf("0");
        return 0;
    }

    char binary[65];
    int index = 0;

    while (N > 0) {
        binary[index++] = (N % 2) + '0';
        N /= 2;
    }

    for (int i = index - 1; i >= 0; i--)
        printf("%c", binary[i]);

    return 0;
}
```
```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

int main() {
    unsigned long long N;
    cin >> N;

    if (N == 0) {
        cout << 0;
        return 0;
    }

    string binary = "";

    while (N > 0) {
        binary += char((N % 2) + '0');
        N /= 2;
    }

    reverse(binary.begin(), binary.end());

    cout << binary;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();

        if (N == 0) {
            System.out.print(0);
            return;
        }

        StringBuilder binary = new StringBuilder();

        while (N > 0) {
            binary.append(N % 2);
            N /= 2;
        }

        System.out.print(binary.reverse());
    }
}
```
```Python
N = int(input())

if N == 0:
    print(0)
else:
    binary = ""

    while N > 0:
        binary += str(N % 2)
        N //= 2

    print(binary[::-1])
```
```C#
using System;
using System.Text;

class Program
{
    static void Main()
    {
        ulong N = ulong.Parse(Console.ReadLine());

        if (N == 0)
        {
            Console.Write(0);
            return;
        }

        StringBuilder binary = new StringBuilder();

        while (N > 0)
        {
            binary.Append(N % 2);
            N /= 2;
        }

        char[] arr = binary.ToString().ToCharArray();
        Array.Reverse(arr);

        Console.Write(new string(arr));
    }
}
```

### Output
For Input:
10
Output:
1010

# Time Complexity
O(log₂N)

# Space Complexity
O(log₂N)

## Approach 2: Using Bit Manipulation

### Algorithm

1. Read the integer `N`.
2. If `N` is `0`, print `0`.
3. Find the position of the most significant set bit.
4. Starting from that bit down to bit `0`:

- Check whether the current bit is set using the bitwise AND operator.
- Print `1` if the bit is set; otherwise print `0`.

1. The printed bits form the binary representation of the number.

```C
#include <stdio.h>

int main() {
    unsigned long long N;
    scanf("%llu", &N);

    if (N == 0) {
        printf("0");
        return 0;
    }

    int msb = 63;

    while (((N >> msb) & 1) == 0)
        msb--;

    for (int i = msb; i >= 0; i--)
        printf("%llu", (N >> i) & 1ULL);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    unsigned long long N;
    cin >> N;

    if (N == 0) {
        cout << 0;
        return 0;
    }

    int msb = 63;

    while (((N >> msb) & 1) == 0)
        msb--;

    for (int i = msb; i >= 0; i--)
        cout << ((N >> i) & 1);

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();

        if (N == 0) {
            System.out.print(0);
            return;
        }

        int msb = 63;

        while (((N >> msb) & 1) == 0)
            msb--;

        for (int i = msb; i >= 0; i--)
            System.out.print((N >> i) & 1);
    }
}
```
```Python
N = int(input())

if N == 0:
    print(0)
else:
    msb = N.bit_length() - 1

    for i in range(msb, -1, -1):
        print((N >> i) & 1, end="")
```
```C#
using System;

class Program
{
    static void Main()
    {
        ulong N = ulong.Parse(Console.ReadLine());

        if (N == 0)
        {
            Console.Write(0);
            return;
        }

        int msb = 63;

        while (((N >> msb) & 1) == 0)
            msb--;

        for (int i = msb; i >= 0; i--)
            Console.Write((N >> i) & 1);
    }
}
```

### Output
For Input:
10
Output:
1010

# Time Complexity
O(log₂N)

# Space Complexity
O(1)

</approaches>

