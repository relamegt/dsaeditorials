# Print Integer - Solution

## Problem Statement

Given an integer N, print the same integer.

### Input Format

A single integer N.

### Output Format

Print the value of N on a single line.

## Explanation

The given integer is printed as it is.

## Algorithm

1. Read the integer `N`.
2. Print `N`.

```cpp
#include <iostream>
using namespace std;

int main() {
    long long N;
    cin >> N;
    cout << N << endl;
    return 0;
}
```
```c
#include <stdio.h>

int main() {
    long long N;
    scanf("%lld", &N);
    printf("%lld\n", N);
    return 0;
}
```
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        long N = sc.nextLong();
        System.out.println(N);
    }
}
```
```python
N = int(input())
print(N)
```
```c#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());
        Console.WriteLine(N);
    }
}
```

### Output
42

# Time Complexity
O(1)

# Space Complexity
O(1)

