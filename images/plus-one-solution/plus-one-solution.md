# Plus One - Solution

## Problem Statement

You are given a non-negative integer represented as an array of digits `arr[]`, where `arr[0]` is the most significant digit. Add `1` to the number and return the resulting array of digits.

The digits do not contain any leading zeros, except for the number `0` itself.

### Input Format

First line: Integer `N` — number of digits.

Second line: `N` space-separated digits.

### Output Format

Print the resulting digits separated by spaces.

## Explanation

There are two common approaches to solve this problem.

- **Convert to Number (Not Suitable for Large Inputs):** Convert the array into an integer, add `1`, and convert it back into digits. This approach works only for small numbers.
- **Digit-by-Digit Addition (Recommended):** Start from the last digit and add `1`. If the digit becomes `10`, set it to `0` and carry `1` to the previous digit. Continue until no carry remains. If a carry still exists after processing all digits, print an extra leading `1`.

For example, when the digits are: `9 9 9`

- Add `1` to the last digit → carry generated.
- Continue carrying to the previous digits.
- All digits become `0`.
- A carry remains, so add a leading `1`.

Result: `1 0 0 0`

Output:  0 0 0

<approaches>
## Approach 1: Convert to Number (For Small Inputs)

### Algorithm

1. Read the integer `N`.
2. Read the digits.
3. Convert the digits into a single integer.
4. Add `1` to the integer.
5. Extract its digits.
6. Print the resulting digits.

> **Note:** This approach is only suitable for small inputs because the number may exceed the range of standard integer types.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long number = 0;

    for (int i = 0; i < N; i++)
    {
        int digit;
        scanf("%d", &digit);
        number = number * 10 + digit;
    }

    number++;

    long long divisor = 1;
    long long temp = number;

    while (temp >= 10)
    {
        divisor *= 10;
        temp /= 10;
    }

    while (divisor > 0)
    {
        printf("%lld ", number / divisor);
        number %= divisor;
        divisor /= 10;
    }

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main()
{
    int N;
    cin >> N;

    long long number = 0;

    for (int i = 0; i < N; i++)
    {
        int digit;
        cin >> digit;
        number = number * 10 + digit;
    }

    number++;

    long long divisor = 1;
    long long temp = number;

    while (temp >= 10)
    {
        divisor *= 10;
        temp /= 10;
    }

    while (divisor > 0)
    {
        cout << number / divisor << " ";
        number %= divisor;
        divisor /= 10;
    }

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        long number = 0;

        for (int i = 0; i < N; i++)
        {
            int digit = sc.nextInt();
            number = number * 10 + digit;
        }

        number++;

        long divisor = 1;
        long temp = number;

        while (temp >= 10)
        {
            divisor *= 10;
            temp /= 10;
        }

        while (divisor > 0)
        {
            System.out.print(number / divisor + " ");
            number %= divisor;
            divisor /= 10;
        }
    }
}
```
```Python
N = int(input())

digits = list(map(int, input().split()))

number = 0

for digit in digits:
    number = number * 10 + digit

number += 1

print(*list(map(int, str(number))))
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        string[] input = Console.ReadLine().Split();

        long number = 0;

        foreach (string s in input)
            number = number * 10 + int.Parse(s);

        number++;

        foreach (char c in number.ToString())
            Console.Write(c + " ");
    }
}
```

### Output
For Input:
4
1 2 3 4

Output:
1 2 3 5

# Time Complexity
O(N)

# Space Complexity
O(1)

## Approach 2: Digit-by-Digit Addition (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array of digits.
3. Traverse the array from the last digit towards the first.
4. Add `1` to the current digit.
5. If the digit becomes less than `10`, print the array because no carry remains.
6. Otherwise:

- Set the digit to `0`.
- Carry `1` to the previous digit.

1. If all digits become `0`, print a leading `1` followed by all digits.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    int arr[N];

    for (int i = 0; i < N; i++)
        scanf("%d", &arr[i]);

    for (int i = N - 1; i >= 0; i--)
    {
        arr[i]++;

        if (arr[i] < 10)
        {
            for (int j = 0; j < N; j++)
                printf("%d ", arr[j]);
            return 0;
        }

        arr[i] = 0;
    }

    printf("1 ");

    for (int i = 0; i < N; i++)
        printf("%d ", arr[i]);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main()
{
    int N;
    cin >> N;

    int arr[N];

    for (int i = 0; i < N; i++)
        cin >> arr[i];

    for (int i = N - 1; i >= 0; i--)
    {
        arr[i]++;

        if (arr[i] < 10)
        {
            for (int x : arr)
                cout << x << " ";
            return 0;
        }

        arr[i] = 0;
    }

    cout << 1 << " ";

    for (int x : arr)
        cout << x << " ";

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        int[] arr = new int[N];

        for (int i = 0; i < N; i++)
            arr[i] = sc.nextInt();

        for (int i = N - 1; i >= 0; i--)
        {
            arr[i]++;

            if (arr[i] < 10)
            {
                for (int x : arr)
                    System.out.print(x + " ");
                return;
            }

            arr[i] = 0;
        }

        System.out.print("1 ");

        for (int x : arr)
            System.out.print(x + " ");
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

for i in range(N - 1, -1, -1):
    arr[i] += 1

    if arr[i] < 10:
        print(*arr)
        exit()

    arr[i] = 0

print(1, *arr)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        for (int i = N - 1; i >= 0; i--)
        {
            arr[i]++;

            if (arr[i] < 10)
            {
                foreach (int x in arr)
                    Console.Write(x + " ");

                return;
            }

            arr[i] = 0;
        }

        Console.Write("1 ");

        foreach (int x in arr)
            Console.Write(x + " ");
    }
}
```

### Output
For Input:
4
1 2 3 4

Output:
1 2 3 5

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




