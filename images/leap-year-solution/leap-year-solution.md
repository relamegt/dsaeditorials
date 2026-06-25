# Leap Year - Solution

## Problem Statement

Given an integer **Y** representing a year, determine whether it is a leap year in the Gregorian calendar.

A year is a leap year if:

- it is divisible by **400**, or
- it is divisible by **4** but not divisible by **100**.

Print **Leap Year** if the given year is a leap year; otherwise print **Not Leap Year**.

### Input Format

A single integer **Y**.

### Output Format

Print **Leap Year** if **Y** is a leap year.

Otherwise, print **Not Leap Year**.

## Explanation

A leap year occurs every 4 years, but years divisible by 100 are not leap years unless they are also divisible by 400.

Examples:

- **2000** is divisible by 400, so it is a leap year.
- **1900** is divisible by 100 but not by 400, so it is not a leap year.

## Algorithm

1. Read the integer **Y**.
2. If **Y** is divisible by **400**, print **"Leap Year"**.
3. Otherwise, if **Y** is divisible by **4** and not divisible by **100**, print **"Leap Year"**.
4. Otherwise, print **"Not Leap Year"**.

```cpp
#include <iostream>
using namespace std;

int main() {
    long long Y;
    cin >> Y;

    if (Y % 400 == 0 || (Y % 4 == 0 && Y % 100 != 0))
        cout << "Leap Year";
    else
        cout << "Not Leap Year";

    return 0;
}
```
```c
#include <stdio.h>

int main() {
    long long Y;
    scanf("%lld", &Y);

    if (Y % 400 == 0 || (Y % 4 == 0 && Y % 100 != 0))
        printf("Leap Year\n");
    else
        printf("Not Leap Year\n");

    return 0;
}
```
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long Y = sc.nextLong();

        if (Y % 400 == 0 || (Y % 4 == 0 && Y % 100 != 0))
            System.out.println("Leap Year");
        else
            System.out.println("Not Leap Year");
    }
}
```
```python
Y = int(input())

if Y % 400 == 0 or (Y % 4 == 0 and Y % 100 != 0):
    print("Leap Year")
else:
    print("Not Leap Year")
```
```c#
using System;

class Program
{
    static void Main()
    {
        long Y = long.Parse(Console.ReadLine());

        if (Y % 400 == 0 || (Y % 4 == 0 && Y % 100 != 0))
            Console.WriteLine("Leap Year");
        else
            Console.WriteLine("Not Leap Year");
    }
}
```

### Output
For Input:
2000
Output:
Leap Year

# Time Complexity
O(1)

# Space Complexity
O(1)

