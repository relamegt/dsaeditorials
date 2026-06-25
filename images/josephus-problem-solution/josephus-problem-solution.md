# Josephus Problem - Solution

## Problem Statement

There are `N` people standing in a circle numbered from `1` to `N`. Starting from person `1`, every `K`th person is eliminated. After each elimination, counting resumes from the next remaining person. This process continues until only one person remains.

Find the position (1-indexed) of the last surviving person.

### Input Format

A single line containing two space-separated integers `N` and `K`.

### Output Format

Print a single integer representing the 1-indexed position of the last surviving person.

## Explanation

There are two common approaches to solve this problem.

- **Simulation:** Store all people in a circular structure. Repeatedly count `K` people, eliminate the `K`th person, and continue until only one person remains.
- **Josephus Recurrence (Recommended):** Instead of simulating eliminations, use the recurrence relation to directly compute the survivor in linear time using constant extra space.

For example, when `N = 7` and `K = 3`:

- Elimination order: `3 → 6 → 2 → 7 → 5 → 1`
- The only remaining person is: `4`

Output: 4

<approaches>
## Approach 1: Simulation

### Algorithm

1. Read the integers `N` and `K`.
2. Store all people from `1` to `N` in a list.
3. Start counting from the first person.
4. Move `(K - 1)` positions ahead (circularly).
5. Remove that person from the list.
6. Continue counting from the next remaining person.
7. Repeat until only one person remains.
8. Print the remaining person's number.

```C
#include <stdio.h>
#include <stdlib.h>

int main() {
    int N, K;
    scanf("%d %d", &N, &K);

    int *people = (int *)malloc(N * sizeof(int));

    for (int i = 0; i < N; i++)
        people[i] = i + 1;

    int size = N;
    int index = 0;

    while (size > 1) {

        index = (index + K - 1) % size;

        for (int i = index; i < size - 1; i++)
            people[i] = people[i + 1];

        size--;
    }

    printf("%d", people[0]);

    free(people);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {

    int N, K;
    cin >> N >> K;

    vector<int> people;

    for (int i = 1; i <= N; i++)
        people.push_back(i);

    int index = 0;

    while (people.size() > 1) {

        index = (index + K - 1) % people.size();

        people.erase(people.begin() + index);
    }

    cout << people[0];

    return 0;
}
```
```Java
import java.util.*;

public class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();
        int K = sc.nextInt();

        ArrayList<Integer> people = new ArrayList<>();

        for (int i = 1; i <= N; i++)
            people.add(i);

        int index = 0;

        while (people.size() > 1) {

            index = (index + K - 1) % people.size();

            people.remove(index);
        }

        System.out.print(people.get(0));
    }
}
```
```Python
N, K = map(int, input().split())

people = list(range(1, N + 1))

index = 0

while len(people) > 1:
    index = (index + K - 1) % len(people)
    people.pop(index)

print(people[0])
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        string[] input = Console.ReadLine().Split();

        int N = int.Parse(input[0]);
        int K = int.Parse(input[1]);

        List<int> people = new List<int>();

        for (int i = 1; i <= N; i++)
            people.Add(i);

        int index = 0;

        while (people.Count > 1)
        {
            index = (index + K - 1) % people.Count;

            people.RemoveAt(index);
        }

        Console.Write(people[0]);
    }
}
```

### Output
For Input:
7 3

Output:
4

# Time Complexity
O(N²)

# Space Complexity
O(N)

## Approach 2: Using Josephus Recurrence (Recommended)

### Algorithm

1. Read the integers `N` and `K`.
2. Initialize `survivor = 0`. This represents the survivor's position using **0-based indexing** when there is only one person.
3. Iterate from `2` to `N`:

- Update the survivor using the recurrence:

     `survivor = (survivor + K) % i`

- This computes the survivor for a circle of `i` people based on the survivor for `i - 1` people.

1. Convert the final answer to **1-based indexing** by adding `1`.
2. Print the result.

```C
#include <stdio.h>

int main() {
    int N, K;
    scanf("%d %d", &N, &K);

    int survivor = 0;

    for (int i = 2; i <= N; i++) {
        survivor = (survivor + K) % i;
    }

    printf("%d", survivor + 1);

    return 0;
}
```
```cpp
#include <iostream>
using namespace std;

int main() {
    int N, K;
    cin >> N >> K;

    int survivor = 0;

    for (int i = 2; i <= N; i++) {
        survivor = (survivor + K) % i;
    }

    cout << survivor + 1;

    return 0;
}
```
```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();
        int K = sc.nextInt();

        int survivor = 0;

        for (int i = 2; i <= N; i++) {
            survivor = (survivor + K) % i;
        }

        System.out.print(survivor + 1);
    }
}
```
```Python
N, K = map(int, input().split())

survivor = 0

for i in range(2, N + 1):
    survivor = (survivor + K) % i

print(survivor + 1)
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] input = Console.ReadLine().Split();

        int N = int.Parse(input[0]);
        int K = int.Parse(input[1]);

        int survivor = 0;

        for (int i = 2; i <= N; i++)
        {
            survivor = (survivor + K) % i;
        }

        Console.Write(survivor + 1);
    }
}
```

### Output
For Input:
7 3

Output:
4

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>



**Note:** The Josephus recurrence is the preferred solution for this problem because it computes the answer directly without simulating eliminations. It reduces the time complexity from **O(N²)** to **O(N)** while also reducing the extra space from **O(N)** to **O(1)**.
