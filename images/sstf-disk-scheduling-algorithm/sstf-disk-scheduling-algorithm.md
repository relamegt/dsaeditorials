# SSTF Disk Scheduling Algorithm

Shortest Seek Time First (SSTF) is a disk scheduling algorithm that selects the pending disk request closest to the current head position for servicing, rather than processing requests in arrival order. By always servicing the nearest track, SSTF minimizes immediate seek distance and significantly reduces average response time compared to FCFS.

## SSTF Algorithm Steps

1. Store all pending track requests in a request array. Record the initial head position.
2. Compute the absolute distance of each unvisited track from the current head position.
3. Select the unvisited track with the minimum distance from the head.
4. Add that minimum distance to the total seek count.
5. Update the head position to the track just serviced.
6. Repeat steps 2 through 5 until all tracks have been serviced.

## Example Trace

```text
Request Sequence = {176, 79, 34, 60, 92, 11, 41, 114}
Initial Head Position = 50
```

Service order and distance calculations:

| Step | From | To | Distance |
| --- | --- | --- | --- |
| 1 | 50 | 41 | 9 |
| 2 | 41 | 34 | 7 |
| 3 | 34 | 11 | 23 |
| 4 | 11 | 60 | 49 |
| 5 | 60 | 79 | 19 |
| 6 | 79 | 92 | 13 |
| 7 | 92 | 114 | 22 |
| 8 | 114 | 176 | 62 |

```text
Total Seek Count = 9 + 7 + 23 + 49 + 19 + 13 + 22 + 62 = 204

Shortcut: (50 - 11) + (176 - 11) = 39 + 165 = 204
```

**Seek Sequence:** 50 → 41 → 34 → 11 → 60 → 79 → 92 → 114 → 176

## Implementation

The implementation uses a helper structure with two fields: `distance` (absolute difference from head to track) and `accessed` (boolean flag to avoid re-servicing a track). At each iteration, all unaccessed tracks are re-evaluated for distance and the minimum is selected.

```Java
class Node {
    int distance = 0;
    boolean accessed = false;
}

public class Main {

    static void calculateDifference(int[] queue, int head, Node[] diff) {
        for (int i = 0; i < diff.length; i++)
            diff[i].distance = Math.abs(queue[i] - head);
    }

    static int findMin(Node[] diff) {
        int index = -1, minimum = Integer.MAX_VALUE;
        for (int i = 0; i < diff.length; i++) {
            if (!diff[i].accessed && minimum > diff[i].distance) {
                minimum = diff[i].distance;
                index = i;
            }
        }
        return index;
    }

    static void sstf(int[] request, int head) {
        if (request.length == 0) return;

        Node[] diff = new Node[request.length];
        for (int i = 0; i < diff.length; i++) diff[i] = new Node();

        int seekCount = 0;
        int[] seekSequence = new int[request.length + 1];

        for (int i = 0; i < request.length; i++) {
            seekSequence[i] = head;
            calculateDifference(request, head, diff);
            int index = findMin(diff);
            diff[index].accessed = true;
            seekCount += diff[index].distance;
            head = request[index];
        }
        seekSequence[seekSequence.length - 1] = head;

        System.out.println("Total number of seek operations = " + seekCount);
        System.out.print("Seek Sequence: ");
        for (int val : seekSequence) System.out.print(val + " ");
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = {176, 79, 34, 60, 92, 11, 41, 114};
        sstf(arr, 50);
    }
}
```
```C
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
#include <stdbool.h>

void calculateDifference(int queue[], int n, int head, int diff[]) {
    for (int i = 0; i < n; i++)
        diff[i] = abs(queue[i] - head);
}

int findMin(int diff[], bool accessed[], int n) {
    int index = -1, minimum = INT_MAX;
    for (int i = 0; i < n; i++) {
        if (!accessed[i] && minimum > diff[i]) {
            minimum = diff[i];
            index = i;
        }
    }
    return index;
}

void sstf(int request[], int n, int head) {
    if (n == 0) return;

    int diff[n];
    bool accessed[n];
    for (int i = 0; i < n; i++) accessed[i] = false;

    int seekCount = 0;
    int seekSequence[n + 1];

    for (int i = 0; i < n; i++) {
        seekSequence[i] = head;
        calculateDifference(request, n, head, diff);
        int index = findMin(diff, accessed, n);
        accessed[index] = true;
        seekCount += diff[index];
        head = request[index];
    }
    seekSequence[n] = head;

    printf("Total number of seek operations = %d\n", seekCount);
    printf("Seek Sequence: ");
    for (int i = 0; i <= n; i++) printf("%d ", seekSequence[i]);
    printf("\n");
}

int main() {
    int arr[] = {176, 79, 34, 60, 92, 11, 41, 114};
    int n = sizeof(arr) / sizeof(arr[0]);
    sstf(arr, n, 50);
    return 0;
}
```
```Cpp
#include <iostream>
#include <vector>
#include <cstdlib>
#include <climits>
using namespace std;

void calculateDifference(vector<int>& queue, int head, vector<int>& diff) {
    for (int i = 0; i < (int)queue.size(); i++)
        diff[i] = abs(queue[i] - head);
}

int findMin(vector<int>& diff, vector<bool>& accessed) {
    int index = -1, minimum = INT_MAX;
    for (int i = 0; i < (int)diff.size(); i++) {
        if (!accessed[i] && minimum > diff[i]) {
            minimum = diff[i];
            index = i;
        }
    }
    return index;
}

void sstf(vector<int>& request, int head) {
    int n = request.size();
    if (n == 0) return;

    vector<int> diff(n, 0);
    vector<bool> accessed(n, false);
    int seekCount = 0;
    vector<int> seekSequence(n + 1);

    for (int i = 0; i < n; i++) {
        seekSequence[i] = head;
        calculateDifference(request, head, diff);
        int index = findMin(diff, accessed);
        accessed[index] = true;
        seekCount += diff[index];
        head = request[index];
    }
    seekSequence[n] = head;

    cout << "Total number of seek operations = " << seekCount << endl;
    cout << "Seek Sequence: ";
    for (int val : seekSequence) cout << val << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {176, 79, 34, 60, 92, 11, 41, 114};
    sstf(arr, 50);
    return 0;
}
```
```Python
def calculate_difference(queue, head):
    return [abs(track - head) for track in queue]

def find_min(diff, accessed):
    index, minimum = -1, float('inf')
    for i in range(len(diff)):
        if not accessed[i] and diff[i] < minimum:
            minimum = diff[i]
            index = i
    return index

def sstf(request, head):
    n = len(request)
    if n == 0:
        return

    accessed = [False] * n
    seek_count = 0
    seek_sequence = []

    for _ in range(n):
        seek_sequence.append(head)
        diff = calculate_difference(request, head)
        index = find_min(diff, accessed)
        accessed[index] = True
        seek_count += diff[index]
        head = request[index]

    seek_sequence.append(head)
    print(f"Total number of seek operations = {seek_count}")
    print("Seek Sequence:", " ".join(map(str, seek_sequence)))

if __name__ == "__main__":
    arr = [176, 79, 34, 60, 92, 11, 41, 114]
    sstf(arr, 50)
```
```JavaScript
function calculateDifference(queue, head) {
    return queue.map(track => Math.abs(track - head));
}

function findMin(diff, accessed) {
    let index = -1, minimum = Infinity;
    for (let i = 0; i < diff.length; i++) {
        if (!accessed[i] && diff[i] < minimum) {
            minimum = diff[i];
            index = i;
        }
    }
    return index;
}

function sstf(request, head) {
    const n = request.length;
    if (n === 0) return;

    const accessed = new Array(n).fill(false);
    let seekCount = 0;
    const seekSequence = [];

    for (let i = 0; i < n; i++) {
        seekSequence.push(head);
        const diff = calculateDifference(request, head);
        const index = findMin(diff, accessed);
        accessed[index] = true;
        seekCount += diff[index];
        head = request[index];
    }
    seekSequence.push(head);

    console.log("Total number of seek operations = " + seekCount);
    console.log("Seek Sequence: " + seekSequence.join(" "));
}

const arr = [176, 79, 34, 60, 92, 11, 41, 114];
sstf(arr, 50);
```
```CSharp
using System;
using System.Collections.Generic;

class SSTF {

    static int[] CalculateDifference(int[] queue, int head) {
        int[] diff = new int[queue.Length];
        for (int i = 0; i < queue.Length; i++)
            diff[i] = Math.Abs(queue[i] - head);
        return diff;
    }

    static int FindMin(int[] diff, bool[] accessed) {
        int index = -1, minimum = int.MaxValue;
        for (int i = 0; i < diff.Length; i++) {
            if (!accessed[i] && diff[i] < minimum) {
                minimum = diff[i];
                index = i;
            }
        }
        return index;
    }

    static void Run(int[] request, int head) {
        int n = request.Length;
        if (n == 0) return;

        bool[] accessed = new bool[n];
        int seekCount = 0;
        List<int> seekSequence = new List<int>();

        for (int i = 0; i < n; i++) {
            seekSequence.Add(head);
            int[] diff = CalculateDifference(request, head);
            int index = FindMin(diff, accessed);
            accessed[index] = true;
            seekCount += diff[index];
            head = request[index];
        }
        seekSequence.Add(head);

        Console.WriteLine("Total number of seek operations = " + seekCount);
        Console.WriteLine("Seek Sequence: " + string.Join(" ", seekSequence));
    }

    static void Main() {
        int[] arr = {176, 79, 34, 60, 92, 11, 41, 114};
        Run(arr, 50);
    }
}
```

## Output

```text
Total number of seek operations = 204
Seek Sequence: 50 41 34 11 60 79 92 114 176
```

**Time Complexity:** O(N²) — For each of the N requests, all N distances are recomputed to find the minimum.
**Auxiliary Space:** O(N) — For the `diff`, `accessed`, and `seekSequence` arrays.

## Advantages and Disadvantages

### Advantages

- Significantly better average seek time and throughput than FCFS.
- Reduces average response and waiting time in most workloads.
- Preferred in batch processing systems where throughput is prioritized over fairness.

### Disadvantages

- Requests far from the current head position may suffer indefinite starvation if new nearby requests keep arriving.
- High variance in response time since some requests are consistently favored over others.
- Direction switching overhead: repeated reversals can slow performance under uneven request distributions.

> **Note:** SSTF achieves lower average seek time than FCFS but is not optimal in all cases. It is vulnerable to starvation, making it unsuitable for interactive systems that require guaranteed response times. SCAN-family algorithms are generally preferred when both performance and fairness are required.

## Summary

SSTF disk scheduling selects the closest unserviced track to the current head position at each step, minimizing seek distance per operation. For the request sequence `{176, 79, 34, 60, 92, 11, 41, 114}` with head at 50, SSTF produces a total seek count of 204. While SSTF outperforms FCFS in throughput and average response time, it risks starving distant requests and exhibits high response time variance, limiting its use to non-interactive, throughput-focused environments.




