# Repeating and Missing Number - Solution

## Problem Statement

Given an unsorted array `arr[]` of size `N` containing integers from `1` to `N`, exactly one number is missing and exactly one number is repeated.

Find and print the repeating number followed by the missing number.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated integers.

### Output Format

Print two integers separated by a space:

`repeating missing`

## Explanation

There are two common approaches to solve this problem.

- **Using a Frequency Array:** Count the occurrences of every number from `1` to `N`. The number with frequency `2` is the repeating number, and the number with frequency `0` is the missing number.
- **Using Mathematical Formula (Recommended):** Compare the expected sum and sum of squares with the actual values to obtain two equations. Solve these equations to find the repeating and missing numbers in O(1) extra space.

For example, when the array is: `3 1 3 4`
Expected numbers: `1 2 3 4`

- `3` appears twice.
- `2` is missing.

Output: 3 2

<approaches>
## Approach 1: Using a Frequency Array

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Create a frequency array of size `N + 1` initialized to `0`.
4. Traverse the array and increment the frequency of every element.
5. Traverse numbers from `1` to `N`.
6. If frequency is `2`, it is the repeating number.
7. If frequency is `0`, it is the missing number.
8. Print the repeating number followed by the missing number.

```C
#include <stdio.h>

int main()
{
    int N;
    scanf("%d", &N);

    int arr[N];
    int freq[N + 1];

    for (int i = 0; i <= N; i++)
        freq[i] = 0;

    for (int i = 0; i < N; i++)
    {
        scanf("%d", &arr[i]);
        freq[arr[i]]++;
    }

    int repeating = -1;
    int missing = -1;

    for (int i = 1; i <= N; i++)
    {
        if (freq[i] == 2)
            repeating = i;
        else if (freq[i] == 0)
            missing = i;
    }

    printf("%d %d", repeating, missing);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int N;
    cin >> N;

    vector<int> freq(N + 1, 0);

    for (int i = 0; i < N; i++)
    {
        int x;
        cin >> x;
        freq[x]++;
    }

    int repeating = -1;
    int missing = -1;

    for (int i = 1; i <= N; i++)
    {
        if (freq[i] == 2)
            repeating = i;
        else if (freq[i] == 0)
            missing = i;
    }

    cout << repeating << " " << missing;

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

        int[] freq = new int[N + 1];

        for (int i = 0; i < N; i++)
        {
            int x = sc.nextInt();
            freq[x]++;
        }

        int repeating = -1;
        int missing = -1;

        for (int i = 1; i <= N; i++)
        {
            if (freq[i] == 2)
                repeating = i;
            else if (freq[i] == 0)
                missing = i;
        }

        System.out.print(repeating + " " + missing);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

freq = [0] * (N + 1)

for x in arr:
    freq[x] += 1

repeating = -1
missing = -1

for i in range(1, N + 1):
    if freq[i] == 2:
        repeating = i
    elif freq[i] == 0:
        missing = i

print(repeating, missing)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int[] freq = new int[N + 1];

        foreach (int x in arr)
            freq[x]++;

        int repeating = -1;
        int missing = -1;

        for (int i = 1; i <= N; i++)
        {
            if (freq[i] == 2)
                repeating = i;
            else if (freq[i] == 0)
                missing = i;
        }

        Console.Write(repeating + " " + missing);
    }
}
```

### Output
For Input:
4
3 1 3 4

Output:
3 2

# Time Complexity
O(N)

# Space Complexity
O(N)

## Approach 2: Using Mathematical Formula (Recommended)

### Algorithm

1. Read the integer `N`.
2. Read the array.
3. Compute:

- Actual sum of array.
- Actual sum of squares of array elements.

1. Compute:

- Expected sum of numbers from `1` to `N`.
- Expected sum of squares from `1²` to `N²`.

1. Let:

- `difference = actualSum - expectedSum = repeating - missing`
- `squareDifference = actualSquareSum - expectedSquareSum`

1. Compute:

- `sum = squareDifference / difference = repeating + missing`

1. Solve:

- `repeating = (difference + sum) / 2`
- `missing = sum - repeating`

1. Print the repeating number followed by the missing number.

```C
#include <stdio.h>

int main()
{
    long long N;
    scanf("%lld", &N);

    long long sum = 0, squareSum = 0;

    for (long long i = 0; i < N; i++)
    {
        long long x;
        scanf("%lld", &x);

        sum += x;
        squareSum += x * x;
    }

    long long expectedSum = N * (N + 1) / 2;
    long long expectedSquareSum = N * (N + 1) * (2 * N + 1) / 6;

    long long difference = sum - expectedSum;
    long long squareDifference = squareSum - expectedSquareSum;

    long long total = squareDifference / difference;

    long long repeating = (difference + total) / 2;
    long long missing = total - repeating;

    printf("%lld %lld", repeating, missing);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main()
{
    long long N;
    cin >> N;

    long long sum = 0, squareSum = 0;

    for (long long i = 0; i < N; i++)
    {
        long long x;
        cin >> x;

        sum += x;
        squareSum += x * x;
    }

    long long expectedSum = N * (N + 1) / 2;
    long long expectedSquareSum = N * (N + 1) * (2 * N + 1) / 6;

    long long difference = sum - expectedSum;
    long long squareDifference = squareSum - expectedSquareSum;

    long long total = squareDifference / difference;

    long long repeating = (difference + total) / 2;
    long long missing = total - repeating;

    cout << repeating << " " << missing;

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

        long N = sc.nextLong();

        long sum = 0;
        long squareSum = 0;

        for (int i = 0; i < N; i++)
        {
            long x = sc.nextLong();

            sum += x;
            squareSum += x * x;
        }

        long expectedSum = N * (N + 1) / 2;
        long expectedSquareSum = N * (N + 1) * (2 * N + 1) / 6;

        long difference = sum - expectedSum;
        long squareDifference = squareSum - expectedSquareSum;

        long total = squareDifference / difference;

        long repeating = (difference + total) / 2;
        long missing = total - repeating;

        System.out.print(repeating + " " + missing);
    }
}
```
```Python
N = int(input())

arr = list(map(int, input().split()))

actualSum = sum(arr)
actualSquareSum = sum(x * x for x in arr)

expectedSum = N * (N + 1) // 2
expectedSquareSum = N * (N + 1) * (2 * N + 1) // 6

difference = actualSum - expectedSum
squareDifference = actualSquareSum - expectedSquareSum

total = squareDifference // difference

repeating = (difference + total) // 2
missing = total - repeating

print(repeating, missing)
```
```C#
using System;

class Program
{
    static void Main()
    {
        long N = long.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long actualSum = 0;
        long actualSquareSum = 0;

        foreach (long x in arr)
        {
            actualSum += x;
            actualSquareSum += x * x;
        }

        long expectedSum = N * (N + 1) / 2;
        long expectedSquareSum = N * (N + 1) * (2 * N + 1) / 6;

        long difference = actualSum - expectedSum;
        long squareDifference = actualSquareSum - expectedSquareSum;

        long total = squareDifference / difference;

        long repeating = (difference + total) / 2;
        long missing = total - repeating;

        Console.Write(repeating + " " + missing);
    }
}
```

### Output
For Input:
4
3 1 3 4

Output:
3 2

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




