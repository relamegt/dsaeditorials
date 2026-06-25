# Greatest of Two Numbers - Solution

## Problem Statement

Given two integers **A** and **B**, print the greater value.

If both values are equal, print that value.

### Input Format

A single line containing two space-separated integers **A** and **B**.

### Output Format

Print a single integer — the greater of the two numbers.

## Explanation

The task is to compare the two given integers and print the larger one.

If both integers are equal, print that value.

## Algorithm

1. Read two integers **A** and **B**.
2. Compare **A** and **B**.
3. If **A** is greater than **B**, print **A**.
4. Otherwise, print **B** (this also handles the case when both are equal).

```cpp
#include <iostream>
using namespace std;

int main() {
    long long A, B;
    cin >> A >> B;

    if (A > B)
        cout << A;
    else
        cout << B;

    return 0;
}
```
```c
#include <stdio.h>

int main() {
    long long A, B;
    scanf("%lld %lld", &A, &B);

    if (A > B)
        printf("%lld\n", A);
    else
        printf("%lld\n", B);

    return 0;
}
```
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long A = sc.nextLong();
        long B = sc.nextLong();

        if (A > B)
            System.out.println(A);
        else
            System.out.println(B);
    }
}
```
```python
A, B = map(int, input().split())
print(max(A, B))
```
```c#
using System;

class Program
{
    static void Main()
    {
        string[] input = Console.ReadLine().Split();
        long A = long.Parse(input[0]);
        long B = long.Parse(input[1]);

        if (A > B)
            Console.WriteLine(A);
        else
            Console.WriteLine(B);
    }
}
```

### Output
For Input:
10 20
Output:
20

# Time Complexity
O(1)

# Space Complexity
O(1)

