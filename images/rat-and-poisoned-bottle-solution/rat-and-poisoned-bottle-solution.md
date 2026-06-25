# Rat and Poisoned Bottle - Solution

## Problem Statement

You have `B` bottles of wine, exactly one of which is poisoned. You can use rats to test the bottles in a single round.

A rat dies if and only if it drinks from the poisoned bottle. By giving different combinations of bottles to different rats, each rat can represent one binary bit.

Given the number of bottles `B`, determine the minimum number of rats required to uniquely identify the poisoned bottle.

### Input Format

A single integer `B`.

### Output Format

Print a single integer representing the minimum number of rats required.

## Explanation

There are two common approaches to solve this problem.

- **Iterative Doubling:** Each additional rat doubles the number of unique outcomes. Keep doubling the number of distinguishable bottles until it becomes at least `B`.
- **Using Logarithm (Recommended):** Since `R` rats can distinguish `2^R` bottles, find the smallest integer `R` such that `2^R ≥ B`. This is simply `⌈log₂(B)⌉`.

For example, when `B = 8`:

- 0 rats → `1` bottle
- 1 rat → `2` bottles
- 2 rats → `4` bottles
- 3 rats → `8` bottles

Therefore, the minimum number of rats required is `3`.

Output: 3

<approaches>
## Approach 1: Iterative Doubling

### Algorithm

1. Read the integer `B`.
2. If `B` is `1`, print `0`.
3. Initialize:

- `rats = 0`
- `capacity = 1`

1. While `capacity < B`:

- Double `capacity`.
- Increment `rats`.

1. Print `rats`.

```C
#include <stdio.h>

int main() {
    long long B;
    scanf("%lld", &B);

    int rats = 0;
    long long capacity = 1;

    while (capacity < B) {
        capacity *= 2;
        rats++;
    }

    printf("%d", rats);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    long long B;
    cin >> B;

    int rats = 0;
    long long capacity = 1;

    while (capacity < B) {
        capacity *= 2;
        rats++;
    }

    cout << rats;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long B = sc.nextLong();

        int rats = 0;
        long capacity = 1;

        while (capacity < B) {
            capacity *= 2;
            rats++;
        }

        System.out.print(rats);
    }
}
```
```Python
B = int(input())

rats = 0
capacity = 1

while capacity < B:
    capacity *= 2
    rats += 1

print(rats)
```
```C#
using System;

class Program
{
    static void Main()
    {
        long B = long.Parse(Console.ReadLine());

        int rats = 0;
        long capacity = 1;

        while (capacity < B)
        {
            capacity *= 2;
            rats++;
        }

        Console.Write(rats);
    }
}
```

### Output
For Input:
8

Output:
3

# Time Complexity
O(log B)

# Space Complexity
O(1)

## Approach 2: Using Logarithm (Recommended)

### Algorithm

1. Read the integer `B`.
2. If `B` is `1`, print `0`.
3. Compute:

   `rats = ⌈log₂(B)⌉`

1. Print `rats`.

```C
#include <stdio.h>
#include <math.h>

int main() {
    long long B;
    scanf("%lld", &B);

    if (B == 1)
        printf("0");
    else
        printf("%d", (int)ceil(log2((double)B)));

    return 0;
}
```
```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    long long B;
    cin >> B;

    if (B == 1)
        cout << 0;
    else
        cout << (int)ceil(log2((double)B));

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long B = sc.nextLong();

        if (B == 1)
            System.out.print(0);
        else
            System.out.print((int)Math.ceil(Math.log(B) / Math.log(2)));
    }
}
```
```Python
import math

B = int(input())

if B == 1:
    print(0)
else:
    print(math.ceil(math.log2(B)))
```
```C#
using System;

class Program
{
    static void Main()
    {
        long B = long.Parse(Console.ReadLine());

        if (B == 1)
            Console.Write(0);
        else
            Console.Write((int)Math.Ceiling(Math.Log(B, 2)));
    }
}
```

### Output
For Input:
8

Output:
3

# Time Complexity
O(1)

# Space Complexity
O(1)

</approaches>



**Note:** The Josephus recurrence is the preferred solution for this problem because it computes the answer directly without simulating eliminations. It reduces the time complexity from **O(N²)** to **O(N)** while also reducing the extra space from **O(N)** to **O(1)**.
