# Divisibility by 11 - Solution

## Problem Statement

Given a large non-negative integer represented as a string `S`, determine whether it is divisible by `11`.

### Input Format

A single string `S` representing a non-negative integer.

### Output Format

Print `Yes` if the number is divisible by `11`, otherwise print `No`.

**Note:** The input may be a very large number that cannot fit in a 64-bit integer.

## Explanation

There are two common approaches to determine whether a number is divisible by `11`.

- **Convert the Entire String to a Number:** Convert the complete string into an integer and check whether it is divisible by `11`. This approach works only for numbers that fit within standard integer data types.
- **Alternating Sum Rule (Recommended):** A number is divisible by `11` if the difference between the sum of digits in odd positions and the sum of digits in even positions is divisible by `11`. This method works even for extremely large numbers represented as strings.

For example, when `S = "121"`:

- Sum of digits at odd positions = `1 + 1 = 2`
- Sum of digits at even positions = `2`
- Difference = `2 - 2 = 0`
- Since `0` is divisible by `11`, the number is divisible by `11`.

Output:
Yes

<approaches>
## Approach 1: Convert Entire Number (For Small Numbers)

### Algorithm

1. Read the number.
2. Convert the complete input into an integer.
3. Find the remainder when dividing the number by `11`.
4. If the remainder is `0`, print `Yes`.
5. Otherwise, print `No`.

```C
#include <stdio.h>

int main() {
    unsigned long long num;
    scanf("%llu", &num);

    if (num % 11 == 0)
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

    if (num % 11 == 0)
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

        if (num % 11 == 0)
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```
```Python
num = int(input())

if num % 11 == 0:
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

        if (num % 11 == 0)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}
```

### Output
For Input:
121

Output:
Yes

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Using the Alternating Sum Rule (Recommended)

### Algorithm

1. Read the string `S`.
2. Initialize two variables:

- `oddSum = 0`
- `evenSum = 0`

1. Traverse the string from left to right.
2. For each digit:

- Convert the character into its numeric value.
- If its position is odd, add it to `oddSum`.
- Otherwise, add it to `evenSum`.

1. Compute the absolute difference between `oddSum` and `evenSum`.
2. If the difference is divisible by `11`, print `Yes`; otherwise, print `No`.

```C
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main() {
    char S[100005];
    scanf("%s", S);

    int oddSum = 0, evenSum = 0;

    for (int i = 0; S[i] != ''; i++) {
        if (i % 2 == 0)
            oddSum += S[i] - '0';
        else
            evenSum += S[i] - '0';
    }

    if (abs(oddSum - evenSum) % 11 == 0)
        printf("Yes");
    else
        printf("No");

    return 0;
}
```
```cpp
#include <iostream>
#include <string>
#include <cmath>
using namespace std;

int main() {
    string S;
    cin >> S;

    int oddSum = 0, evenSum = 0;

    for (int i = 0; i < S.length(); i++) {
        if (i % 2 == 0)
            oddSum += S[i] - '0';
        else
            evenSum += S[i] - '0';
    }

    if (abs(oddSum - evenSum) % 11 == 0)
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

        int oddSum = 0;
        int evenSum = 0;

        for (int i = 0; i < S.length(); i++) {
            if (i % 2 == 0)
                oddSum += S.charAt(i) - '0';
            else
                evenSum += S.charAt(i) - '0';
        }

        if (Math.abs(oddSum - evenSum) % 11 == 0)
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```
```Python
S = input()

oddSum = 0
evenSum = 0

for i in range(len(S)):
    if i % 2 == 0:
        oddSum += int(S[i])
    else:
        evenSum += int(S[i])

if abs(oddSum - evenSum) % 11 == 0:
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

        int oddSum = 0;
        int evenSum = 0;

        for (int i = 0; i < S.Length; i++)
        {
            if (i % 2 == 0)
                oddSum += S[i] - '0';
            else
                evenSum += S[i] - '0';
        }

        if (Math.Abs(oddSum - evenSum) % 11 == 0)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}
```

### Output
For Input:
121

Output:
Yes

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>



###
