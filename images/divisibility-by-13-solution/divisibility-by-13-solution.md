# Divisibility by 13 - Solution

## Problem Statement

Given a large non-negative integer represented as a string `S`, determine whether it is divisible by `13`.

### Input Format

A single string `S` representing a non-negative integer.

### Output Format

Print `Yes` if the number is divisible by `13`, otherwise print `No`.

**Note:** The input may be a very large number that cannot fit in a 64-bit integer.

## Explanation

There are two common approaches to determine whether a number is divisible by `13`.

- **Convert the Entire String to a Number:** Convert the complete string into an integer and check whether it is divisible by `13`. This approach works only for numbers that fit within standard integer data types.
- **Compute the Remainder Digit by Digit (Recommended):** Process the number one digit at a time while maintaining the remainder modulo `13`. This works even for numbers containing up to `10^5` digits.

For example, when `S = "169"`:

- Start with `remainder = 0`
- Read `1` → `(0 × 10 + 1) % 13 = 1`
- Read `6` → `(1 × 10 + 6) % 13 = 3`
- Read `9` → `(3 × 10 + 9) % 13 = 0`

Since the final remainder is `0`, the number is divisible by `13`.

Output:
Yes

<approaches>
## Approach 1: Convert Entire Number (For Small Numbers)

### Algorithm

1. Read the number.
2. Convert the complete input into an integer.
3. Find the remainder when dividing the number by `13`.
4. If the remainder is `0`, print `Yes`.
5. Otherwise, print `No`.

```C
#include <stdio.h>

int main() {
    unsigned long long num;
    scanf("%llu", &num);

    if (num % 13 == 0)
        printf("Yes");
    else
        printf("No");

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    unsigned long long num;
    cin >> num;

    if (num % 13 == 0)
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long num = sc.nextLong();

        if (num % 13 == 0)
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```
```Python
num = int(input())

if num % 13 == 0:
    print("Yes")
else:
    print("No")
```
```C#
using System;

class Program
{
    static void Main()
    {
        ulong num = ulong.Parse(Console.ReadLine());

        if (num % 13 == 0)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}
```

### Output
For Input:
169
Output:
Yes

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Compute Remainder Digit by Digit (Recommended)

### Algorithm

1. Read the string `S`.
2. Initialize `remainder = 0`.
3. Traverse the string from left to right.
4. For each digit:

- Convert the character into its numeric value.
- Update the remainder using:

   `remainder = (remainder × 10 + digit) % 13`

1. After processing all digits, check the remainder.
2. If the remainder is `0`, print `Yes`; otherwise, print `No`.

```C
#include <stdio.h>

int main() {
    char S[100005];
    scanf("%s", S);

    int remainder = 0;

    for (int i = 0; S[i] != ''; i++) {
        remainder = (remainder * 10 + (S[i] - '0')) % 13;
    }

    if (remainder == 0)
        printf("Yes");
    else
        printf("No");

    return 0;
}
```
```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string S;
    cin >> S;

    int remainder = 0;

    for (char digit : S) {
        remainder = (remainder * 10 + (digit - '0')) % 13;
    }

    if (remainder == 0)
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        String S = sc.next();

        int remainder = 0;

        for (int i = 0; i < S.length(); i++) {
            remainder = (remainder * 10 + (S.charAt(i) - '0')) % 13;
        }

        if (remainder == 0)
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```
```Python
S = input()

remainder = 0

for digit in S:
    remainder = (remainder * 10 + int(digit)) % 13

if remainder == 0:
    print("Yes")
else:
    print("No")
```
```C#
using System;

class Program
{
    static void Main()
    {
        string S = Console.ReadLine();

        int remainder = 0;

        foreach (char digit in S)
        {
            remainder = (remainder * 10 + (digit - '0')) % 13;
        }

        if (remainder == 0)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}
```

### Output
For Input:
169
Output:
Yes

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>



###
