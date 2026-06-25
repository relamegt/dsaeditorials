# Divisibility by 4 - Solution

## Problem Statement

Given a large non-negative integer represented as a string `S`, determine whether it is divisible by `4`.

### Input Format

A single string `S` representing a non-negative integer.

### Output Format

Print `Yes` if the number is divisible by `4`, otherwise print `No`.

**Note:** The input may be a very large number that cannot fit in standard integer types.

## Explanation

There are two common approaches to determine whether a number is divisible by `4`.

- **Convert the Entire String to a Number:** Convert the complete string into an integer and check whether it is divisible by `4`. This approach works only for numbers that fit within standard integer data types.
- **Check the Last Two Digits (Recommended):** A number is divisible by `4` if and only if the number formed by its last two digits is divisible by `4`. Since only the last two digits are needed, this approach works even for very large numbers.

For example, when `S = "1236"`:

- Last two digits are `36`.
- `36 % 4 = 0`.

Hence, the number is divisible by `4`.

Output:
Yes

<approaches>
## Approach 1: Convert Entire Number (For Small Numbers)

### Algorithm

1. Read the string `S`.
2. Convert the entire string into an integer.
3. Find the remainder when dividing the number by `4`.
4. If the remainder is `0`, print `Yes`.
5. Otherwise, print `No`.

Output:
Yes

```C
#include <stdio.h>

int main() {
    unsigned long long num;
    scanf("%llu", &num);

    if (num % 4 == 0)
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

    if (num % 4 == 0)
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

        if (num % 4 == 0)
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```
```Python
num = int(input())

if num % 4 == 0:
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

        if (num % 4 == 0)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}
```

### Output
For Input:
1236

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Check the Last Two Digits (Recommended)

### Algorithm

1. Read the string `S`.
2. If the string contains only one digit:

- Convert that digit into a number.

1. Otherwise:

- Extract the last two digits of the string.
- Form the two-digit number using those digits.

1. Check whether the obtained number is divisible by `4`.
2. If it is divisible, print `Yes`; otherwise, print `No`.

Output:
Yes

```C
#include <stdio.h>
#include <string.h>

int main() {
    char S[100005];
    scanf("%s", S);

    int n = strlen(S);
    int num;

    if (n == 1)
        num = S[0] - '0';
    else
        num = (S[n - 2] - '0') * 10 + (S[n - 1] - '0');

    if (num % 4 == 0)
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

    int n = S.length();
    int num;

    if (n == 1)
        num = S[0] - '0';
    else
        num = (S[n - 2] - '0') * 10 + (S[n - 1] - '0');

    if (num % 4 == 0)
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

        int n = S.length();
        int num;

        if (n == 1)
            num = S.charAt(0) - '0';
        else
            num = (S.charAt(n - 2) - '0') * 10 + (S.charAt(n - 1) - '0');

        if (num % 4 == 0)
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```
```Python
S = input()

if len(S) == 1:
    num = int(S)
else:
    num = int(S[-2:])

if num % 4 == 0:
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

        int num;

        if (S.Length == 1)
            num = S[0] - '0';
        else
            num = (S[S.Length - 2] - '0') * 10 + (S[S.Length - 1] - '0');

        if (num % 4 == 0)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}
```

### Output
For Input:
1236

# Time Complexity
O(1)

# Space Complexity
O(1)

</approaches>

