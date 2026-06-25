# Even or Odd - Solution

## Problem Statement

Given an integer **`N`** , determine whether it is even or odd.

Print **`Even`**  if **`N`**  is divisible by **`2`** . Otherwise, print **`Odd`** .

### Input Format

A single integer **`N`** .

### Output Format

Print `Even`  if the number is even.

Print `Odd`  if the number is odd.

## Explanation

An integer is `even`  if it is divisible by **`2`**  with no remainder.

An integer is **`odd`**  if dividing it by **`2`**  leaves a remainder of **`1`** .

For example:

- `8`  is divisible by **`2`** , so it is **`Even`** .
- **`7`**  is not divisible by **`2`** , so it is **`Odd`** .

## Algorithm

1. Read the integer **`N`**
2. Check if **`N % 2 == 0`**
3. If true, print **`"Even"`**
4. Otherwise, print **`"Odd"`**

```C
#include <stdio.h>

int main() {
    long long N;
    scanf("%lld", &N);

    if (N % 2 == 0)
        printf("Even\n");
    else
        printf("Odd\n");

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long N;
    cin >> N;

    if (N % 2 == 0)
        cout << "Even";
    else
        cout << "Odd";

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();

        if (N % 2 == 0)
            System.out.println("Even");
        else
            System.out.println("Odd");
    }
}
```
```Python
N = int(input())

if N % 2 == 0:
    print("Even")
else:
    print("Odd")
```
```C#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());

        if (N % 2 == 0)
            Console.WriteLine("Even");
        else
            Console.WriteLine("Odd");
    }
}
```

### Output
For Input:
8
Output:
Even

# Time Complexity
O(1)

# Space Complexity
O(1)

