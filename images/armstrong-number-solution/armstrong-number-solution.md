# Armstrong Number - Solution

## Problem Statement

Given a positive integer `N`, determine whether it is an Armstrong number.

An Armstrong number (also called a narcissistic number) of `d` digits is a number where the sum of its digits each raised to the power `d` equals the number itself.

For example, `153` has `3` digits and:

`1³ + 5³ + 3³ = 153`

### Input Format

A single integer `N`.

### Output Format

Print `Yes` if `N` is an Armstrong number, otherwise print `No`.

## Explanation

To determine whether a number is an Armstrong number:

1. Count the total number of digits in the number.
2. Extract each digit one by one.
3. Raise every digit to the power of the total number of digits.
4. Add all these values together.
5. If the final sum equals the original number, then it is an Armstrong number.

For example, when `N = 153`:

- Number of digits = `3`
- Digits are `1`, `5`, and `3`
- `1³ = 1`
- `5³ = 125`
- `3³ = 27`
- Sum = `1 + 125 + 27 = 153`

Since the sum equals the original number, the answer is:

Output:
Yes

## Algorithm

1. Read the integer `N`.
2. Store a copy of the original number.
3. Count the total number of digits in the number.
4. Initialize `sum = 0`.
5. Again traverse all the digits of the original number:

- Extract the last digit using `N % 10`.
- Raise the extracted digit to the power equal to the number of digits.
- Add the result to `sum`.
- Remove the last digit using integer division (`N = N / 10`).

1. Compare `sum` with the original number.
2. If both are equal, print `Yes`; otherwise, print `No`.

```C
#include <stdio.h>
#include <math.h>

int main() {
    int N;
    scanf("%d", &N);

    int original = N;
    int temp = N;
    int digits = 0;

    while (temp > 0) {
        digits++;
        temp /= 10;
    }

    temp = N;
    long long sum = 0;

    while (temp > 0) {
        int digit = temp % 10;
        sum += (long long)pow(digit, digits);
        temp /= 10;
    }

    if (sum == original)
        printf("Yes");
    else
        printf("No");

    return 0;
}
```
```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    int N;
    cin >> N;

    int original = N;
    int temp = N;
    int digits = 0;

    while (temp > 0) {
        digits++;
        temp /= 10;
    }

    temp = N;
    long long sum = 0;

    while (temp > 0) {
        int digit = temp % 10;
        sum += (long long)pow(digit, digits);
        temp /= 10;
    }

    if (sum == original)
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

        int N = sc.nextInt();

        int original = N;
        int temp = N;
        int digits = 0;

        while (temp > 0) {
            digits++;
            temp /= 10;
        }

        temp = N;
        long sum = 0;

        while (temp > 0) {
            int digit = temp % 10;
            sum += (long)Math.pow(digit, digits);
            temp /= 10;
        }

        if (sum == original)
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```
```Python
N = int(input())

original = N
temp = N
digits = 0

while temp > 0:
    digits += 1
    temp //= 10

temp = N
sum = 0

while temp > 0:
    digit = temp % 10
    sum += digit ** digits
    temp //= 10

if sum == original:
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
        int N = int.Parse(Console.ReadLine());

        int original = N;
        int temp = N;
        int digits = 0;

        while (temp > 0)
        {
            digits++;
            temp /= 10;
        }

        temp = N;
        long sum = 0;

        while (temp > 0)
        {
            int digit = temp % 10;
            sum += (long)Math.Pow(digit, digits);
            temp /= 10;
        }

        if (sum == original)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}
```

### Output
For Input:
153
Output:
Yes

# Time Complexity
O(log₁₀N)

# Space Complexity
O(1)

