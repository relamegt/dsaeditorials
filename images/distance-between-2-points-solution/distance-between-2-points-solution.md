# Distance Between 2 Points - Solution

## Problem Statement

Given two points `(x1, y1)` and `(x2, y2)` in a 2D plane, compute the Euclidean distance between them.

Print the answer rounded to **2 decimal places**.

### Input Format

A single line containing four space-separated integers:

`x1 y1 x2 y2`

### Output Format

Print a single floating-point number representing the Euclidean distance rounded to **2 decimal places**.

## Explanation

The Euclidean distance between two points is calculated using the distance formula:

`Distance = √((x2 - x1)² + (y2 - y1)²)`

The steps are:

- Find the difference between the x-coordinates.
- Find the difference between the y-coordinates.
- Square both differences.
- Add the squared values.
- Take the square root of the sum.
- Print the result rounded to two decimal places.

For example, when the points are `(0, 0)` and `(3, 4)`:

- Difference in x-coordinates = `3 - 0 = 3`
- Difference in y-coordinates = `4 - 0 = 4`
- Square the differences: `3² = 9`, `4² = 16`
- Add them: `9 + 16 = 25`
- Square root of `25` is `5`

Output:
5.00

## Algorithm

1. Read the four integers `x1`, `y1`, `x2`, and `y2`.
2. Compute the difference between the x-coordinates as `dx = x2 - x1`.
3. Compute the difference between the y-coordinates as `dy = y2 - y1`.
4. Square both differences and add them.
5. Take the square root of the obtained value to get the Euclidean distance.
6. Print the distance rounded to **2 decimal places**.

```C
#include <stdio.h>
#include <math.h>

int main() {
    double x1, y1, x2, y2;
    scanf("%lf %lf %lf %lf", &x1, &y1, &x2, &y2);

    double dx = x2 - x1;
    double dy = y2 - y1;

    double distance = sqrt(dx * dx + dy * dy);

    printf("%.2lf", distance);

    return 0;
}
```
```cpp
#include <iostream>
#include <cmath>
#include <iomanip>
using namespace std;

int main() {
    double x1, y1, x2, y2;
    cin >> x1 >> y1 >> x2 >> y2;

    double dx = x2 - x1;
    double dy = y2 - y1;

    double distance = sqrt(dx * dx + dy * dy);

    cout << fixed << setprecision(2) << distance;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        double x1 = sc.nextDouble();
        double y1 = sc.nextDouble();
        double x2 = sc.nextDouble();
        double y2 = sc.nextDouble();

        double dx = x2 - x1;
        double dy = y2 - y1;

        double distance = Math.sqrt(dx * dx + dy * dy);

        System.out.printf("%.2f", distance);
    }
}
```
```Python
import math

x1, y1, x2, y2 = map(float, input().split())

dx = x2 - x1
dy = y2 - y1

distance = math.sqrt(dx * dx + dy * dy)

print(f"{distance:.2f}")
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] input = Console.ReadLine().Split();

        double x1 = double.Parse(input[0]);
        double y1 = double.Parse(input[1]);
        double x2 = double.Parse(input[2]);
        double y2 = double.Parse(input[3]);

        double dx = x2 - x1;
        double dy = y2 - y1;

        double distance = Math.Sqrt(dx * dx + dy * dy);

        Console.Write("{0:F2}", distance);
    }
}
```

### Output
For Input:
0 0 3 4
Output:
5.00

# Time Complexity
O(1)

# Space Complexity
O(1)

