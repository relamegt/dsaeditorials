# Palindrome Number - Solution

## Problem Statement

Given an integer `N`, determine whether it is a palindrome.

A number is a palindrome if it reads the same forwards and backwards. Negative numbers are never palindromes.

### Input Format

A single integer `N`.

### Output Format

Print `Yes` if `N` is a palindrome, otherwise print `No`.

## Explanation

There are two common approaches to determine whether a number is a palindrome.

- **Using String Comparison:** Convert the number to a string and compare characters from the beginning and the end. If all corresponding characters are equal, the number is a palindrome.
- **Using Number Reversal (Recommended):** Reverse the digits of the number mathematically and compare the reversed number with the original number. This approach does not require any extra space for strings.

For example, when `N = 121`:

- Reverse of `121` is `121`.
- Since the reversed number is equal to the original number, it is a palindrome.

Output:
Yes

<approaches>
## Approach 1: Using String Comparison

### Algorithm

1. Read the integer `N`.
2. If `N` is negative, print `No` and stop.
3. Convert the number into a string.
4. Initialize two pointers:

- One pointing to the first character.
- Another pointing to the last character.

1. Compare the characters at both pointers.

- If they are different, print `No` and stop.
- Otherwise, move the left pointer one step forward and the right pointer one step backward.

1. Repeat until both pointers meet or cross each other.
2. If all characters matched, print `Yes`.

```C
#include <stdio.h>
#include <string.h>

int main() {
    long long N;
    scanf("%lld", &N);

    if (N < 0) {
        printf("No");
        return 0;
    }

    char str[20];
    sprintf(str, "%lld", N);

    int left = 0;
    int right = strlen(str) - 1;

    while (left < right) {
        if (str[left] != str[right]) {
            printf("No");
            return 0;
        }
        left++;
        right--;
    }

    printf("Yes");

    return 0;
}
```
```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    long long N;
    cin >> N;

    if (N < 0) {
        cout << "No";
        return 0;
    }

    string str = to_string(N);

    int left = 0;
    int right = str.length() - 1;

    while (left < right) {
        if (str[left] != str[right]) {
            cout << "No";
            return 0;
        }
        left++;
        right--;
    }

    cout << "Yes";

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();

        if (N < 0) {
            System.out.print("No");
            return;
        }

        String str = Long.toString(N);

        int left = 0;
        int right = str.length() - 1;

        while (left < right) {
            if (str.charAt(left) != str.charAt(right)) {
                System.out.print("No");
                return;
            }
            left++;
            right--;
        }

        System.out.print("Yes");
    }
}
```
```Python
N = int(input())

if N < 0:
    print("No")
else:
    s = str(N)

    left = 0
    right = len(s) - 1

    while left < right:
        if s[left] != s[right]:
            print("No")
            break
        left += 1
        right -= 1
    else:
        print("Yes")
```
```C#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());

        if (N < 0)
        {
            Console.Write("No");
            return;
        }

        string str = N.ToString();

        int left = 0;
        int right = str.Length - 1;

        while (left < right)
        {
            if (str[left] != str[right])
            {
                Console.Write("No");
                return;
            }

            left++;
            right--;
        }

        Console.Write("Yes");
    }
}
```

### Output
For Input:
121
Output:
Yes

# Time Complexity
O(log₁₀N)

# Space Complexity
O(log₁₀N)

## Approach 2: Using Number Reversal (Recommended)

### Algorithm

1. Read the integer `N`.
2. If `N` is negative, print `No` and stop.
3. Store a copy of the original number.
4. Initialize `reverse = 0`.
5. Repeat until the number becomes `0`:

- Extract the last digit using `N % 10`.
- Append the extracted digit to the reversed number using `reverse = reverse × 10 + digit`.
- Remove the last digit from the number using integer division (`N = N / 10`).

1. Compare the reversed number with the original number.
2. If they are equal, print `Yes`; otherwise, print `No`.

```C
#include <stdio.h>

int main() {
    long long N;
    scanf("%lld", &N);

    if (N < 0) {
        printf("No");
        return 0;
    }

    long long original = N;
    long long reverse = 0;

    while (N > 0) {
        int digit = N % 10;
        reverse = reverse * 10 + digit;
        N /= 10;
    }

    if (reverse == original)
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
    long long N;
    cin >> N;

    if (N < 0) {
        cout << "No";
        return 0;
    }

    long long original = N;
    long long reverse = 0;

    while (N > 0) {
        int digit = N % 10;
        reverse = reverse * 10 + digit;
        N /= 10;
    }

    if (reverse == original)
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

        long N = sc.nextLong();

        if (N < 0) {
            System.out.print("No");
            return;
        }

        long original = N;
        long reverse = 0;

        while (N > 0) {
            long digit = N % 10;
            reverse = reverse * 10 + digit;
            N /= 10;
        }

        if (reverse == original)
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```
```Python
N = int(input())

if N < 0:
    print("No")
else:
    original = N
    reverse = 0

    while N > 0:
        digit = N % 10
        reverse = reverse * 10 + digit
        N //= 10

    if reverse == original:
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
        long N = long.Parse(Console.ReadLine());

        if (N < 0)
        {
            Console.Write("No");
            return;
        }

        long original = N;
        long reverse = 0;

        while (N > 0)
        {
            long digit = N % 10;
            reverse = reverse * 10 + digit;
            N /= 10;
        }

        if (reverse == original)
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
O(log₁₀N)

# Space Complexity
O(1)

</approaches>

