# Square Root - Solution

## Problem Statement

Given a non-negative integer `N`, compute the floor value of its square root.

The floor square root of `N` is the largest integer `x` such that:

`x × x ≤ N`

### Input Format

A single integer `N`.

### Output Format

Print a single integer representing the floor value of the square root of `N`.

## Explanation

There are two common approaches to find the floor square root of a number.

- **Linear Search:** Start from `0` and keep checking successive integers until the square exceeds `N`. The previous integer is the floor square root.
- **Binary Search (Recommended):** Since the square root lies between `0` and `N`, repeatedly divide the search space into two halves. Check whether the square of the middle element is less than or equal to `N` and accordingly search in the left or right half.

For example, when `N = 15`:

- `3 × 3 = 9 ≤ 15`
- `4 × 4 = 16 > 15`

Hence, the floor square root is `3`.

<approaches>
## Approach 1: Linear Search

### Algorithm

1. Read the integer `N`.
2. Initialize `answer = 0`.
3. Start checking numbers from `0` onwards.
4. For each number:

- Compute its square.
- If the square is less than or equal to `N`, update `answer`.
- Otherwise, stop the loop because the square has exceeded `N`.

1. Print `answer`.

```C
#include <stdio.h>

int main() {
    unsigned long long N;
    scanf("%llu", &N);

    unsigned long long answer = 0;

    for (unsigned long long i = 0; i * i <= N; i++) {
        answer = i;
    }

    printf("%llu", answer);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    unsigned long long N;
    cin >> N;

    unsigned long long answer = 0;

    for (unsigned long long i = 0; i * i <= N; i++) {
        answer = i;
    }

    cout << answer;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();

        long answer = 0;

        for (long i = 0; i * i <= N; i++) {
            answer = i;
        }

        System.out.print(answer);
    }
}
```
```Python
N = int(input())

answer = 0
i = 0

while i * i <= N:
    answer = i
    i += 1

print(answer)
```
```C#
using System;

class Program
{
    static void Main()
    {
        ulong N = ulong.Parse(Console.ReadLine());

        ulong answer = 0;

        for (ulong i = 0; i * i <= N; i++)
        {
            answer = i;
        }

        Console.Write(answer);
    }
}
```

### Output
For Input:
16
Output:
4

# Time Complexity
O(√N)

# Space Complexity
O(1)

## Approach 2: Binary Search (Recommended)

### Algorithm

1. Read the integer `N`.
2. If `N` is `0` or `1`, print `N`.
3. Initialize:

- `low = 0`
- `high = N`
- `answer = 0`

1. Repeat while `low ≤ high`:

- Find the middle value using `mid = low + (high - low) / 2`.
- If `mid × mid ≤ N`:
- Store `mid` as the current answer.
- Search in the right half by setting `low = mid + 1`.
- Otherwise:
- Search in the left half by setting `high = mid - 1`.

1. After the search completes, print `answer`.

```C
#include <stdio.h>

int main() {
    unsigned long long N;
    scanf("%llu", &N);

    if (N == 0 || N == 1) {
        printf("%llu", N);
        return 0;
    }

    unsigned long long low = 0, high = N, answer = 0;

    while (low <= high) {
        unsigned long long mid = low + (high - low) / 2;

        if (mid <= N / mid) {
            answer = mid;
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    printf("%llu", answer);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    unsigned long long N;
    cin >> N;

    if (N == 0 || N == 1) {
        cout << N;
        return 0;
    }

    unsigned long long low = 0, high = N, answer = 0;

    while (low <= high) {
        unsigned long long mid = low + (high - low) / 2;

        if (mid <= N / mid) {
            answer = mid;
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    cout << answer;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long N = sc.nextLong();

        if (N == 0 || N == 1) {
            System.out.print(N);
            return;
        }

        long low = 0, high = N, answer = 0;

        while (low <= high) {
            long mid = low + (high - low) / 2;

            if (mid <= N / mid) {
                answer = mid;
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        System.out.print(answer);
    }
}
```
```Python
N = int(input())

if N == 0 or N == 1:
    print(N)
else:
    low = 0
    high = N
    answer = 0

    while low <= high:
        mid = low + (high - low) // 2

        if mid <= N // mid:
            answer = mid
            low = mid + 1
        else:
            high = mid - 1

    print(answer)
```
```C#
using System;

class Program
{
    static void Main()
    {
        ulong N = ulong.Parse(Console.ReadLine());

        if (N == 0 || N == 1)
        {
            Console.Write(N);
            return;
        }

        ulong low = 0, high = N, answer = 0;

        while (low <= high)
        {
            ulong mid = low + (high - low) / 2;

            if (mid <= N / mid)
            {
                answer = mid;
                low = mid + 1;
            }
            else
            {
                high = mid - 1;
            }
        }

        Console.Write(answer);
    }
}
```

### Output
For Input:
16
Output:
4

# Time Complexity
O(log N)

# Space Complexity
O(1)

</approaches>

