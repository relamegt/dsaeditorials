# Missing Ranges of Numbers- Solution

## Problem Statement

You are given an inclusive range `[lower, upper]` and a sorted unique integer array `nums[]` of size `N`, where all elements are within `[lower, upper]`.

Return all missing ranges — ranges `[a, b]` such that every integer from `a` to `b` is absent from `nums[]` and is within `[lower, upper]`.

Output each range as:

- `a` if `a == b`
- `a b` otherwise

If there are no missing ranges, print `NONE`.

### Input Format

First line: Integer `N`.

Second line: `N` space-separated sorted unique integers, or `-` if `N = 0`.

Third line: Two integers `lower` and `upper`.

### Output Format

Print each missing range on a new line.

- If the range contains one number, print only that number.
- Otherwise print `start end`.
- Print `NONE` if there are no missing ranges.

## Explanation

The array is already sorted, so we can scan it only once.

Maintain a variable `previous` which represents the last number that has already been processed.

Initially, no numbers before `lower` are processed, so set: `previous = lower - 1`

Now process every array element one by one.

For every current number:

- Missing range starts from `previous + 1`.
- Missing range ends at `current - 1`.

If the starting value is less than or equal to the ending value, that range is missing and should be printed.

After processing the current number, update: `previous = current`

Finally, after all elements are processed, there may still be numbers missing between the last array element and `upper`.

Check:

- Start = `previous + 1`
- End = `upper`

If this range is valid, print it.

If no range was printed during the entire process, print `NONE`.

For example,

Input:

5

0 1 3 50 75

0 99

Missing ranges are:

2

4 49

51 74

76 99

## Algorithm

1. Read the integer `N`.
2. Read the array if `N > 0`.
3. Read `lower` and `upper`.
4. Initialize `previous = lower - 1`.
5. Initialize a boolean variable `found = false`.
6. Traverse every element of the array.
7. For every element:

- Compute `start = previous + 1`.
- Compute `end = current - 1`.
- If `start <= end`:
- Print the range.
- Mark `found = true`.
- Update `previous = current`.

1. After the loop:

- Compute `start = previous + 1`.
- Compute `end = upper`.
- If `start <= end`, print the range.

1. If no range was printed, print `NONE`.

```C
#include <stdio.h>
#include <stdbool.h>

int main()
{
    int N;
    scanf("%d", &N);

    long long nums[N];

    if (N > 0)
    {
        for (int i = 0; i < N; i++)
            scanf("%lld", &nums[i]);
    }
    else
    {
        char temp[2];
        scanf("%s", temp);
    }

    long long lower, upper;
    scanf("%lld %lld", &lower, &upper);

    long long previous = lower - 1;
    bool found = false;

    for (int i = 0; i < N; i++)
    {
        long long start = previous + 1;
        long long end = nums[i] - 1;

        if (start <= end)
        {
            found = true;

            if (start == end)
                printf("%lld
", start);
            else
                printf("%lld %lld
", start, end);
        }

        previous = nums[i];
    }

    long long start = previous + 1;
    long long end = upper;

    if (start <= end)
    {
        found = true;

        if (start == end)
            printf("%lld
", start);
        else
            printf("%lld %lld
", start, end);
    }

    if (!found)
        printf("NONE");

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

    vector<long long> nums(N);

    if (N > 0)
    {
        for (int i = 0; i < N; i++)
            cin >> nums[i];
    }
    else
    {
        string temp;
        cin >> temp;
    }

    long long lower, upper;
    cin >> lower >> upper;

    long long previous = lower - 1;
    bool found = false;

    for (long long current : nums)
    {
        long long start = previous + 1;
        long long end = current - 1;

        if (start <= end)
        {
            found = true;

            if (start == end)
                cout << start << "
";
            else
                cout << start << " " << end << "
";
        }

        previous = current;
    }

    long long start = previous + 1;
    long long end = upper;

    if (start <= end)
    {
        found = true;

        if (start == end)
            cout << start << "
";
        else
            cout << start << " " << end << "
";
    }

    if (!found)
        cout << "NONE";

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

        long[] nums = new long[N];

        if (N > 0)
        {
            for (int i = 0; i < N; i++)
                nums[i] = sc.nextLong();
        }
        else
        {
            sc.next();
        }

        long lower = sc.nextLong();
        long upper = sc.nextLong();

        long previous = lower - 1;

        boolean found = false;

        for (long current : nums)
        {
            long start = previous + 1;
            long end = current - 1;

            if (start <= end)
            {
                found = true;

                if (start == end)
                    System.out.println(start);
                else
                    System.out.println(start + " " + end);
            }

            previous = current;
        }

        long start = previous + 1;
        long end = upper;

        if (start <= end)
        {
            found = true;

            if (start == end)
                System.out.println(start);
            else
                System.out.println(start + " " + end);
        }

        if (!found)
            System.out.print("NONE");
    }
}
```
```Python
N = int(input())

if N > 0:
    nums = list(map(int, input().split()))
else:
    input()
    nums = []

lower, upper = map(int, input().split())

previous = lower - 1
found = False

for current in nums:
    start = previous + 1
    end = current - 1

    if start <= end:
        found = True

        if start == end:
            print(start)
        else:
            print(start, end)

    previous = current

start = previous + 1
end = upper

if start <= end:
    found = True

    if start == end:
        print(start)
    else:
        print(start, end)

if not found:
    print("NONE")
```
```C#
using System;

class Program
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());

        long[] nums;

        if (N > 0)
        {
            nums = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);
        }
        else
        {
            Console.ReadLine();
            nums = new long[0];
        }

        string[] input = Console.ReadLine().Split();
        long lower = long.Parse(input[0]);
        long upper = long.Parse(input[1]);

        long previous = lower - 1;
        bool found = false;

        foreach (long current in nums)
        {
            long start = previous + 1;
            long end = current - 1;

            if (start <= end)
            {
                found = true;

                if (start == end)
                    Console.WriteLine(start);
                else
                    Console.WriteLine(start + " " + end);
            }

            previous = current;
        }

        long finalStart = previous + 1;
        long finalEnd = upper;

        if (finalStart <= finalEnd)
        {
            found = true;

            if (finalStart == finalEnd)
                Console.WriteLine(finalStart);
            else
                Console.WriteLine(finalStart + " " + finalEnd);
        }

        if (!found)
            Console.Write("NONE");
    }
}
```

### Output
For Input:
5

0 1 3 50 75

0 99

Output:
2
4 49
51 74
76 99

# Time Complexity
O(N)

# Space Complexity
O(1)




