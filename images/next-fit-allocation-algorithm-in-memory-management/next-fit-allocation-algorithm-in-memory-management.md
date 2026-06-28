# Next Fit Allocation Algorithm in Memory Management

Next Fit is a placement algorithm used in contiguous memory management to allocate variable-sized blocks of memory dynamically. It is a modified variation of the First Fit algorithm. 

While First Fit always restarts its search from the very beginning of the memory block list for every new allocation request, Next Fit optimizes this search process by continuing the search from the position where the last successful allocation occurred.

## Mechanics of the Roving Pointer

The Next Fit algorithm achieves its search continuity by maintaining a **roving pointer**. This pointer tracks the index of the memory block that was most recently allocated. When a new memory request arrives:

1. The search starts at the block indicated by the roving pointer.
2. If the block has sufficient capacity, the memory is allocated, the block size is reduced, and the roving pointer remains at this location.
3. If the block is too small, the pointer steps to the next block sequentially, traversing the list in a circular fashion.
4. If the search circles back to the original starting block without finding any partition with sufficient capacity, the allocation request fails.

## Algorithm Steps

The execution flow of the Next Fit memory allocation scheme proceeds as follows:

1. **Initialize Memory Blocks:** Input the total count and individual sizes of the available memory blocks.
2. **Set Initial State:** Initialize all memory blocks to a free/unallocated state.
3. **Initialize Process List:** Input the total count and individual memory requirements of the incoming processes.
4. **Evaluate Allocations:** For each incoming process, evaluate memory block availability starting from the current roving pointer position.
5. **Successful Block Allocation:** If the current memory block has sufficient space to hold the process, allocate the requested memory to the process, reduce the remaining capacity of the block, and update the roving pointer to point to this block.
6. **Circular Search Traversal:** If the current memory block cannot accommodate the process, proceed to evaluate the subsequent blocks sequentially in a circular loop (looping back to the beginning of the block list if the end is reached) until a suitable block is found or all blocks have been checked.
7. **Generate Report:** Output the final memory block allocation map for all processes.

## Advantages of Next Fit

Next Fit addresses some of the key limitations of the standard First Fit algorithm:

- **Avoids Early Block Clumping:** First Fit continuously scans and fills the blocks at the beginning of memory, creating a cluster of small allocated blocks and tiny, fragmented gaps. Next Fit distributes allocations more uniformly across the entire memory space.
- **Improved Search Speed:** Because it does not restart from the beginning, the search loop avoids scanning already filled blocks at the head of the list, reducing average execution latency.
- **Balanced Resource Loading:** Spreading allocations evenly across the physical RAM prevents the build-up of fragmentation in a localized memory region.

## Allocation Walkthrough Example

Consider a system initialized with the following memory blocks and incoming process allocation requests:

- **Initial Block Sizes:** [15 KB, 25 KB, 45 KB, 10 KB]
- **Incoming Process Sizes:** [20 KB, 30 KB, 10 KB, 5 KB]

### Allocation Tracing Steps

1. **Process 1 (20 KB):** The search starts at Block 1 (15 KB), which is too small. It moves to Block 2 (25 KB), which is sufficient. Process 1 is allocated to Block 2. The block size becomes 5 KB. The roving pointer rests at Block 2 (index 1).
2. **Process 2 (30 KB):** The search continues from Block 2 (now 5 KB), which is too small. It moves to Block 3 (45 KB), which is sufficient. Process 2 is allocated to Block 3. The block size becomes 15 KB. The roving pointer rests at Block 3 (index 2).
3. **Process 3 (10 KB):** The search continues from Block 3 (now 15 KB), which is sufficient. Process 3 is allocated to Block 3. The block size becomes 5 KB. The roving pointer rests at Block 3 (index 2).
4. **Process 4 (5 KB):** The search continues from Block 3 (now 5 KB), which is sufficient. Process 4 is allocated to Block 3. The block size becomes 0 KB. The roving pointer rests at Block 3 (index 2).

## Implementations of Next Fit Algorithm

Below are the complete, compilation-ready implementations of the Next Fit memory allocation algorithm in five programming languages:

```Java
import java.util.*;

public class Main {
    static void nextFit(int blockSize[], int m, int processSize[], int n) {
        int allocation[] = new int[n];
        int j = 0;
        int t = m - 1;

        Arrays.fill(allocation, -1);

        for (int i = 0; i < n; i++) {
            while (j < m) {
                if (blockSize[j] >= processSize[i]) {
                    allocation[i] = j;
                    blockSize[j] -= processSize[i];
                    t = (j - 1 + m) % m; // Avoid negative modulo issues
                    break;
                }
                if (t == j) {
                    t = (j - 1 + m) % m;
                    break;
                }
                j = (j + 1) % m;
            }
        }

        System.out.print("\nProcess No.\tProcess Size\tBlock no.\n");
        for (int i = 0; i < n; i++) {
            System.out.print((i + 1) + "\t\t" + processSize[i] + "\t\t");
            if (allocation[i] != -1) {
                System.out.print((allocation[i] + 1));
            } else {
                System.out.print("Not Allocated");
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        int blockSize[] = {15, 25, 45, 10};
        int processSize[] = {20, 30, 10, 5};
        int m = blockSize.length;
        int n = processSize.length;
        nextFit(blockSize, m, processSize, n);
    }
}
```
```C
#include <stdio.h>
#include <string.h>

void nextFit(int blockSize[], int m, int processSize[], int n) {
    int allocation[n];
    memset(allocation, -1, sizeof(allocation));
    int j = 0;
    int t = m - 1;

    for (int i = 0; i < n; i++) {
        while (j < m) {
            if (blockSize[j] >= processSize[i]) {
                allocation[i] = j;
                blockSize[j] -= processSize[i];
                t = (j - 1 + m) % m;
                break;
            }
            if (t == j) {
                t = (j - 1 + m) % m;
                break;
            }
            j = (j + 1) % m;
        }
    }

    printf("\nProcess No.\tProcess Size\tBlock no.\n");
    for (int i = 0; i < n; i++) {
        printf("%d\t\t%d\t\t", i + 1, processSize[i]);
        if (allocation[i] != -1) {
            printf("%d\n", allocation[i] + 1);
        } else {
            printf("Not Allocated\n");
        }
    }
}

int main() {
    int blockSize[] = {15, 25, 45, 10};
    int processSize[] = {20, 30, 10, 5};
    int m = sizeof(blockSize) / sizeof(blockSize[0]);
    int n = sizeof(processSize) / sizeof(processSize[0]);
    nextFit(blockSize, m, processSize, n);
    return 0;
}
```
```Cpp
#include <iostream>
#include <vector>

void nextFit(std::vector<int>& blockSize, int m, const std::vector<int>& processSize, int n) {
    std::vector<int> allocation(n, -1);
    int j = 0;
    int t = m - 1;

    for (int i = 0; i < n; i++) {
        while (j < m) {
            if (blockSize[j] >= processSize[i]) {
                allocation[i] = j;
                blockSize[j] -= processSize[i];
                t = (j - 1 + m) % m;
                break;
            }
            if (t == j) {
                t = (j - 1 + m) % m;
                break;
            }
            j = (j + 1) % m;
        }
    }

    std::cout << "\nProcess No.\tProcess Size\tBlock no.\n";
    for (int i = 0; i < n; i++) {
        std::cout << i + 1 << "\t\t" << processSize[i] << "\t\t";
        if (allocation[i] != -1) {
            std::cout << allocation[i] + 1 << "\n";
        } else {
            std::cout << "Not Allocated\n";
        }
    }
}

int main() {
    std::vector<int> blockSize = {15, 25, 45, 10};
    std::vector<int> processSize = {20, 30, 10, 5};
    int m = blockSize.size();
    int n = processSize.size();
    nextFit(blockSize, m, processSize, n);
    return 0;
}
```
```Python
def next_fit(block_size, m, process_size, n):
    allocation = [-1] * n
    j = 0
    t = m - 1

    for i in range(n):
        while j < m:
            if block_size[j] >= process_size[i]:
                allocation[i] = j
                block_size[j] -= process_size[i]
                t = (j - 1 + m) % m
                break
            if t == j:
                t = (j - 1 + m) % m
                break
            j = (j + 1) % m

    print("\nProcess No.\tProcess Size\tBlock no.")
    for i in range(n):
        print(f"{i + 1}\t\t{process_size[i]}\t\t", end="")
        if allocation[i] != -1:
            print(allocation[i] + 1)
        else:
            print("Not Allocated")

if __name__ == "__main__":
    block_size = [15, 25, 45, 10]
    process_size = [20, 30, 10, 5]
    m = len(block_size)
    n = len(process_size)
    next_fit(block_size, m, process_size, n)
```
```JavaScript
function nextFit(blockSize, m, processSize, n) {
    const allocation = new Array(n).fill(-1);
    let j = 0;
    let t = m - 1;

    for (let i = 0; i < n; i++) {
        while (j < m) {
            if (blockSize[j] >= processSize[i]) {
                allocation[i] = j;
                blockSize[j] -= processSize[i];
                t = (j - 1 + m) % m;
                break;
            }
            if (t === j) {
                t = (j - 1 + m) % m;
                break;
            }
            j = (j + 1) % m;
        }
    }

    console.log("\nProcess No.\tProcess Size\tBlock no.");
    for (let i = 0; i < n; i++) {
        let blockStr = allocation[i] !== -1 ? (allocation[i] + 1) : "Not Allocated";
        console.log(`${i + 1}\t\t${processSize[i]}\t\t${blockStr}`);
    }
}

const blockSize = [15, 25, 45, 10];
const processSize = [20, 30, 10, 5];
const m = blockSize.length;
const n = processSize.length;
nextFit(blockSize, m, processSize, n);
```

## Example Output

When running the algorithm driver, you will receive the following allocation trace output:

```text
Process No.	Process Size	Block no.
1		20		2
2		30		3
3		10		3
4		5		3
```

## Complexity Analysis

- **Time Complexity:** O(N * M), where N is the number of processes and M is the number of memory blocks. In the worst-case scenario, the algorithm may scan all blocks for every single allocation request.
- **Auxiliary Space:** O(N) auxiliary space is required to store allocation results.

## Summary

Next Fit is a dynamic contiguous memory allocation placement algorithm that updates the First Fit technique using a roving pointer. By starting each new memory search from the index of the last allocated block instead of the beginning of memory, Next Fit prevents memory allocation clumping and reduces search time. While it does not completely eliminate external fragmentation, Next Fit balances execution speed with uniform memory load distribution in contiguous memory managers.




