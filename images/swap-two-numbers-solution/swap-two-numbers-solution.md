# Swap Two Numbers - Solution

## Problem Statement

Given two integers `A` and `B`, swap their values and print the swapped numbers.

Print the new value of `A` followed by the new value of `B`.

### Input Format

A single line containing two space-separated integers `A` and `B`.

### Output Format

Print two space-separated integers representing the swapped values of `A` and `B`.

## Explanation

There are two common ways to swap two numbers:

- **Using a Temporary Variable:** Store one value temporarily, then exchange the values.
- **Without Using a Temporary Variable:** Swap the values using arithmetic operations.

For example, when `A = 3` and `B = 5`:

Output:
5 3

<approaches>
## Approach 1: Using a Temporary Variable

### Algorithm

1. Read the integers `A` and `B`.
2. Store the value of `A` in a temporary variable.
3. Assign the value of `B` to `A`.
4. Assign the temporary value to `B`.
5. Print the swapped values.

```C
#include <stdio.h>

int main() {
    long long A, B;
    scanf("%lld %lld", &A, &B);

    long long temp = A;
    A = B;
    B = temp;

    printf("%lld %lld", A, B);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long A, B;
    cin >> A >> B;

    long long temp = A;
    A = B;
    B = temp;

    cout << A << " " << B;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long A = sc.nextLong();
        long B = sc.nextLong();

        long temp = A;
        A = B;
        B = temp;

        System.out.print(A + " " + B);
    }
}
```
```Python
A, B = map(int, input().split())

temp = A
A = B
B = temp

print(A, B)
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] input = Console.ReadLine().Split();

        long A = long.Parse(input[0]);
        long B = long.Parse(input[1]);

        long temp = A;
        A = B;
        B = temp;

        Console.Write(A + " " + B);
    }
}
```

### Output
For Input:
3 5
Output:
5 3

# Time Complexity
O(1)

# Space Complexity
O(1)

## Approach 2: Without Using a Temporary Variable

### Algorithm

1. Read the integers `A` and `B`.
2. Set `A = A + B`.
3. Set `B = A - B`.
4. Set `A = A - B`.
5. Print the swapped values.

```C
#include <stdio.h>

int main() {
    long long A, B;
    scanf("%lld %lld", &A, &B);

    A = A + B;
    B = A - B;
    A = A - B;

    printf("%lld %lld", A, B);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long A, B;
    cin >> A >> B;

    A = A + B;
    B = A - B;
    A = A - B;

    cout << A << " " << B;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long A = sc.nextLong();
        long B = sc.nextLong();

        A = A + B;
        B = A - B;
        A = A - B;

        System.out.print(A + " " + B);
    }
}
```
```Python
A, B = map(int, input().split())

A = A + B
B = A - B
A = A - B

print(A, B)
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] input = Console.ReadLine().Split();

        long A = long.Parse(input[0]);
        long B = long.Parse(input[1]);

        A = A + B;
        B = A - B;
        A = A - B;

        Console.Write(A + " " + B);
    }
}
```

### Output
For Input:
3 5
Output:
5 3

# Time Complexity
O(1)

# Space Complexity
O(1)

</approaches>

