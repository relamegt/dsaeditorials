# All Divisors of a Number- Solution

## Problem Statement

Given a positive integer `N`, print all its divisors in ascending order on a single line separated by spaces.

### Input Format

A single integer `N`.

### Output Format

Print all divisors of `N` in ascending order, separated by spaces.

## Explanation

There are two common approaches to print all divisors of a number.

- **Brute Force:** Check every number from `1` to `N`. If a number divides `N` exactly, it is a divisor.
- **Using Divisor Pairs (Recommended):** Divisors always occur in pairs. Instead of checking all numbers up to `N`, check only up to `√N`. Print the smaller divisors immediately and store the larger paired divisors. Finally, print the stored divisors in reverse order to maintain ascending order.

For example, when `N = 12`:

- Divisor pairs are:
- `(1, 12)`
- `(2, 6)`
- `(3, 4)`

Printing them in ascending order gives:

`1 2 3 4 6 12`

Output:
1 2 3 4 6 12

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the integer `N`.
2. Traverse every integer from `1` to `N`.
3. For each integer:

- Check whether `N` is divisible by it using the modulus operator.
- If the remainder is `0`, print the number.

1. Continue until all numbers are checked.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    for (int i = 1; i <= N; i++) {
        if (N % i == 0)
            printf("%d ", i);
    }

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    int N;
    cin >> N;

    for (int i = 1; i <= N; i++) {
        if (N % i == 0)
            cout << i << " ";
    }

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        for (int i = 1; i <= N; i++) {
            if (N % i == 0)
                System.out.print(i + " ");
        }
    }
}
```
```Python
N = int(input())

for i in range(1, N + 1):
    if N % i == 0:
        print(i, end=" ")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        for (int i = 1; i <= N; i++)
        {
            if (N % i == 0)
                Console.Write(i + " ");
        }
    }
}
```

### Output
For Input:
12

Output:
1 2 3 4 6 12

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Using Divisor Pairs (Recommended)

### Algorithm

1. Read the integer `N`.
2. Create an empty list to store the larger divisors.
3. Traverse from `1` while `i × i ≤ N`.
4. If `i` divides `N` exactly:

- Print `i` immediately because it is one of the smaller divisors.
- Find the paired divisor `N / i`.
- If the paired divisor is different from `i`, store it in the list.

1. After the loop, traverse the stored list in reverse order and print each element.
2. This ensures all divisors are printed in ascending order.

```C
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);

    int divisors[50000];
    int count = 0;

    for (int i = 1; i * i <= N; i++) {
        if (N % i == 0) {
            printf("%d ", i);

            if (i != N / i)
                divisors[count++] = N / i;
        }
    }

    for (int i = count - 1; i >= 0; i--)
        printf("%d ", divisors[i]);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int N;
    cin >> N;

    vector<int> divisors;

    for (int i = 1; i * i <= N; i++) {
        if (N % i == 0) {
            cout << i << " ";

            if (i != N / i)
                divisors.push_back(N / i);
        }
    }

    for (int i = divisors.size() - 1; i >= 0; i--)
        cout << divisors[i] << " ";

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        ArrayList<Integer> divisors = new ArrayList<>();

        for (int i = 1; i * i <= N; i++) {
            if (N % i == 0) {
                System.out.print(i + " ");

                if (i != N / i)
                    divisors.add(N / i);
            }
        }

        for (int i = divisors.size() - 1; i >= 0; i--)
            System.out.print(divisors.get(i) + " ");
    }
}
```
```Python
N = int(input())

divisors = []

i = 1

while i * i <= N:
    if N % i == 0:
        print(i, end=" ")

        if i != N // i:
            divisors.append(N // i)

    i += 1

for i in range(len(divisors) - 1, -1, -1):
    print(divisors[i], end=" ")
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        List<int> divisors = new List<int>();

        for (int i = 1; i * i <= N; i++)
        {
            if (N % i == 0)
            {
                Console.Write(i + " ");

                if (i != N / i)
                    divisors.Add(N / i);
            }
        }

        for (int i = divisors.Count - 1; i >= 0; i--)
            Console.Write(divisors[i] + " ");
    }
}
```

### Output
For Input:
12

Output:
1 2 3 4 6 12

# Time Complexity
O(√N)

# Space Complexity
O(√N)

</approaches>




