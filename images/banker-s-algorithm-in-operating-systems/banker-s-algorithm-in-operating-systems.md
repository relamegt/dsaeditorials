# Banker's Algorithm in Operating Systems

The Banker's Algorithm is a classic resource allocation and deadlock avoidance algorithm. Named after its structural similarity to a banking system—where a banker does not allocate cash lines unless the remaining cash can satisfy at least one customer's line of credit—the algorithm checks whether allocating resources keeps the operating system in a safe state. It tracks resource demands, active allocations, and available resource limits to prevent processes from entering deadlock.

## Key Operating System States

### Safe State

A system is in a safe state if there exists at least one execution sequence (known as a Safe Sequence) of processes such that each process can obtain its maximum required resources, run to completion, release its allocated resources, and allow all subsequent processes to finish without deadlock.

### Unsafe State

An unsafe state occurs when the remaining available resources cannot guarantee that all processes can execute to completion. An unsafe state is not a deadlock, but it represents a configuration where a deadlock could occur if processes request their maximum declared resources.

### Example of an Unsafe State

Consider a manufacturing unit with three robotic arms (Arm 1, Arm 2, Arm 3) and a total pool of 7 drill bit resources.

- **Available Resources:** 1 drill bit
- **Current Allocations:** Arm 1 holds 2; Arm 2 holds 3; Arm 3 holds 1. (Total allocated = 6)
- **Maximum Demands:** Arm 1 requires 4; Arm 2 requires 5; Arm 3 requires 3.

We compute the remaining resource requirements using $\text{Need} = \text{Maximum Demand} - \text{Allocation}$:

| Process | Maximum Demand | Allocation | Need |
| --- | --- | --- | --- |
| **Arm 1** | 4 | 2 | 2 |
| **Arm 2** | 5 | 3 | 2 |
| **Arm 3** | 3 | 1 | 2 |

Here, Arm 1, Arm 2, and Arm 3 each require 2 additional drill bits to finish their work. However, only 1 drill bit is available. Because the system cannot satisfy the remaining need of any single process, no process can complete and release its resources, placing the system in an unsafe state.

## Core Data Structures

To track allocation status, the algorithm utilizes four matrices and vectors (where $n$ is the number of processes and $m$ is the number of resource types):

1. **Available Vector:** A 1D array of size $m$ indicating the number of free resource instances of each type. $\text{Available}[j] = k$ means $k$ instances of resource type $R_j$ are currently free.
2. **Max Matrix:** A 2D array of size $n \times m$ defining the maximum resource demand of each process. $\text{Max}[i][j] = k$ means process $P_i$ can request at most $k$ instances of resource type $R_j$.
3. **Allocation Matrix:** A 2D array of size $n \times m$ defining the number of resources currently allocated to each process. $\text{Allocation}[i][j] = k$ means process $P_i$ currently holds $k$ instances of resource type $R_j$.
4. **Need Matrix:** A 2D array of size $n \times m$ indicating the remaining resource needs of each process. $\text{Need}[i][j] = \text{Max}[i][j] - \text{Allocation}[i][j]$.

## Banker's Algorithm Procedures

The Banker's Algorithm is divided into two distinct procedures: the Safety Algorithm and the Resource Request Algorithm.

### 1. Safety Algorithm

The Safety Algorithm simulates execution to verify if a system configuration is safe.

1. **Initialize:**

- Let $\text{Work} = \text{Available}$.
- Let $\text{Finish}[i] = \text{false}$ for all processes $i = 0, 1, \dots, n-1$.

1. **Find a process $P_i$ that satisfies:**

- $\text{Finish}[i] == \text{false}$
- $\text{Need}[i] \le \text{Work}$
- If no such process exists, skip to step 4.

1. **Simulate completion:**

- Update $\text{Work} = \text{Work} + \text{Allocation}[i]$
- Set $\text{Finish}[i] = \text{true}$
- Return to step 2 to evaluate remaining processes.

1. **Evaluate System Safety:**

- If $\text{Finish}[i] == \text{true}$ for all $i$, the system is in a safe state.

### 2. Resource Request Algorithm

This algorithm determines if a new resource request from a process $P_i$ can be safely granted.

1. **Check Demand Limit:** If $\text{Request}[i] \le \text{Need}[i]$, proceed; otherwise, throw an error since the process has exceeded its declared maximum claim.
2. **Check Resource Availability:** If $\text{Request}[i] \le \text{Available}$, proceed; otherwise, process $P_i$ must wait because sufficient resources are not currently free.
3. **Simulate Allocation:** Temporarily modify state variables:

- $\text{Available} = \text{Available} - \text{Request}[i]$
- $\text{Allocation}[i] = \text{Allocation}[i] + \text{Request}[i]$
- $\text{Need}[i] = \text{Need}[i] - \text{Request}[i]$

1. **Evaluate Security:** Execute the Safety Algorithm on the modified state.

- If the resulting state is safe, grant the resource allocation.
- If the state is unsafe, roll back the simulated allocations and force process $P_i$ to wait.

## Safe State and Sequence Analysis Example

Consider a system running five tasks (Task 0 through Task 4) competing for three types of compute resources: CPU Cores (A), RAM GB (B), and GPU Cores (C). The total system capacity consists of 10 CPU Cores, 5 RAM GB, and 7 GPU Cores.

Suppose the system has the following active states:

- **Allocation Matrix:**
- Task 0: {0, 1, 0}
- Task 1: {2, 0, 0}
- Task 2: {3, 0, 2}
- Task 3: {2, 1, 1}
- Task 4: {0, 0, 2}
- **Maximum Demand Matrix:**
- Task 0: {7, 5, 3}
- Task 1: {3, 2, 2}
- Task 2: {9, 0, 2}
- Task 3: {2, 2, 2}
- Task 4: {4, 3, 3}
- **Available Resources Vector:**
- {3, 3, 2}

We calculate the **Need Matrix** ($\text{Max} - \text{Allocation}$):

- Task 0: {7, 4, 3}
- Task 1: {1, 2, 2}
- Task 2: {6, 0, 0}
- Task 3: {0, 1, 1}
- Task 4: {4, 3, 1}

Running the Safety Algorithm yields a valid execution sequence. Task 1 can execute first since its need {1, 2, 2} is less than or equal to the available resource vector {3, 3, 2}. Once Task 1 completes and releases its resources, the available vector increases, allowing Task 3, Task 4, Task 0, and Task 2 to execute in sequence.

The safe sequence is: `Task 1 -> Task 3 -> Task 4 -> Task 0 -> Task 2`.

## Implementations of the Banker's Algorithm

Below are the complete, compilation-ready implementations of the Banker's Algorithm check, demonstrating safety sequence evaluations in five programming languages:

```Java
public class BankerAlgorithm {
    public static void main(String[] args) {
        // P0, P1, P2, P3, P4 are the names of Process

        int n = 5; // Indicates the Number of processes
        int r = 3; // Indicates the Number of resources
        int[][] alloc = {{0, 0, 1}, // P0 // This is Allocation Matrix
                          {3, 0, 0}, // P1
                          {1, 0, 1}, // P2
                          {2, 3, 2}, // P3
                          {0, 0, 3}}; // P4

        int[][] max = {{7, 6, 3}, // P0 // MAX Matrix
                        {3, 2, 2}, // P1
                        {8, 0, 2}, // P2
                        {2, 1, 2}, // P3
                        {5, 2, 3}}; // P4

        int[] avail = {2, 3, 2}; // These are Available Resources

        int[] f = new int[n];
        int[] ans = new int[n];
        int ind = 0;
        int[][] need = new int[n][r];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < r; j++) {
                need[i][j] = max[i][j] - alloc[i][j];
            }
        }

        int y = 0;
        for (int k = 0; k < n; k++) {
            for (int i = 0; i < n; i++) {
                if (f[i] == 0) {
                    int flag = 0;
                    for (int j = 0; j < r; j++) {
                        if (need[i][j] > avail[j]) {
                            flag = 1;
                            break;
                        }
                    }

                    if (flag == 0) {
                        ans[ind++] = i;
                        for (y = 0; y < r; y++) {
                            avail[y] += alloc[i][y];
                        }
                        f[i] = 1;
                    }
                }
            }
        }

        System.out.print("The SAFE Sequence is as follows\n");
        for (int i = 0; i < n - 1; i++) {
            System.out.print(" P" + ans[i] + " ->");
        }
        System.out.println(" P" + ans[n - 1]);
    }
}
```
```C
#include <stdio.h>
#include <stdbool.h>

#define PROCESS_COUNT 5
#define RESOURCE_COUNT 3

int main() {
    int alloc[PROCESS_COUNT][RESOURCE_COUNT] = {
        {0, 0, 1},
        {3, 0, 0},
        {1, 0, 1},
        {2, 3, 2},
        {0, 0, 3}
    };

    int max[PROCESS_COUNT][RESOURCE_COUNT] = {
        {7, 6, 3},
        {3, 2, 2},
        {8, 0, 2},
        {2, 1, 2},
        {5, 2, 3}
    };

    int avail[RESOURCE_COUNT] = {2, 3, 2};

    int f[PROCESS_COUNT] = {0};
    int ans[PROCESS_COUNT];
    int ind = 0;
    int need[PROCESS_COUNT][RESOURCE_COUNT];

    for (int i = 0; i < PROCESS_COUNT; i++) {
        for (int j = 0; j < RESOURCE_COUNT; j++) {
            need[i][j] = max[i][j] - alloc[i][j];
        }
    }

    for (int k = 0; k < PROCESS_COUNT; k++) {
        for (int i = 0; i < PROCESS_COUNT; i++) {
            if (f[i] == 0) {
                int flag = 0;
                for (int j = 0; j < RESOURCE_COUNT; j++) {
                    if (need[i][j] > avail[j]) {
                        flag = 1;
                        break;
                    }
                }

                if (flag == 0) {
                    ans[ind++] = i;
                    for (int y = 0; y < RESOURCE_COUNT; y++) {
                        avail[y] += alloc[i][y];
                    }
                    f[i] = 1;
                }
            }
        }
    }

    printf("The SAFE Sequence is as follows\n");
    for (int i = 0; i < PROCESS_COUNT - 1; i++) {
        printf(" P%d ->", ans[i]);
    }
    printf(" P%d\n", ans[PROCESS_COUNT - 1]);

    return 0;
}
```
```Cpp
#include <iostream>
#include <vector>

int main() {
    int n = 5;
    int r = 3;
    std::vector<std::vector<int>> alloc = {
        {0, 0, 1},
        {3, 0, 0},
        {1, 0, 1},
        {2, 3, 2},
        {0, 0, 3}
    };

    std::vector<std::vector<int>> max = {
        {7, 6, 3},
        {3, 2, 2},
        {8, 0, 2},
        {2, 1, 2},
        {5, 2, 3}
    };

    std::vector<int> avail = {2, 3, 2};

    std::vector<int> f(n, 0);
    std::vector<int> ans(n);
    int ind = 0;
    std::vector<std::vector<int>> need(n, std::vector<int>(r));

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < r; j++) {
            need[i][j] = max[i][j] - alloc[i][j];
        }
    }

    for (int k = 0; k < n; k++) {
        for (int i = 0; i < n; i++) {
            if (f[i] == 0) {
                int flag = 0;
                for (int j = 0; j < r; j++) {
                    if (need[i][j] > avail[j]) {
                        flag = 1;
                        break;
                    }
                }

                if (flag == 0) {
                    ans[ind++] = i;
                    for (int y = 0; y < r; y++) {
                        avail[y] += alloc[i][y];
                    }
                    f[i] = 1;
                }
            }
        }
    }

    std::cout << "The SAFE Sequence is as follows\n";
    for (int i = 0; i < n - 1; i++) {
        std::cout << " P" << ans[i] << " ->";
    }
    std::cout << " P" << ans[n - 1] << "\n";

    return 0;
}
```
```Python
if __name__ == "__main__":
    n = 5
    r = 3
    
    alloc = [
        [0, 0, 1],
        [3, 0, 0],
        [1, 0, 1],
        [2, 3, 2],
        [0, 0, 3]
    ]

    max_demand = [
        [7, 6, 3],
        [3, 2, 2],
        [8, 0, 2],
        [2, 1, 2],
        [5, 2, 3]
    ]

    avail = [2, 3, 2]

    f = [0] * n
    ans = [0] * n
    ind = 0
    need = [[0 for _ in range(r)] for _ in range(n)]

    for i in range(n):
        for j in range(r):
            need[i][j] = max_demand[i][j] - alloc[i][j]

    for k in range(n):
        for i in range(n):
            if f[i] == 0:
                flag = 0
                for j in range(r):
                    if need[i][j] > avail[j]:
                        flag = 1
                        break

                if flag == 0:
                    ans[ind] = i
                    ind += 1
                    for y in range(r):
                        avail[y] += alloc[i][y]
                    f[i] = 1

    print("The SAFE Sequence is as follows")
    for i in range(n - 1):
        print(f" P{ans[i]} ->", end="")
    print(f" P{ans[n - 1]}")
```
```JavaScript
function main() {
    const n = 5;
    const r = 3;

    const alloc = [
        [0, 0, 1],
        [3, 0, 0],
        [1, 0, 1],
        [2, 3, 2],
        [0, 0, 3]
    ];

    const max = [
        [7, 6, 3],
        [3, 2, 2],
        [8, 0, 2],
        [2, 1, 2],
        [5, 2, 3]
    ];

    const avail = [2, 3, 2];

    const f = new Array(n).fill(0);
    const ans = new Array(n);
    let ind = 0;
    const need = Array.from({ length: n }, () => new Array(r));

    for (let i = 0; i < n; i++) {
        for (let j = 0; j < r; j++) {
            need[i][j] = max[i][j] - alloc[i][j];
        }
    }

    for (let k = 0; k < n; k++) {
        for (let i = 0; i < n; i++) {
            if (f[i] === 0) {
                let flag = 0;
                for (let j = 0; j < r; j++) {
                    if (need[i][j] > avail[j]) {
                        flag = 1;
                        break;
                    }
                }

                if (flag === 0) {
                    ans[ind++] = i;
                    for (let y = 0; y < r; y++) {
                        avail[y] += alloc[i][y];
                    }
                    f[i] = 1;
                }
            }
        }
    }

    let out = "The SAFE Sequence is as follows\n";
    for (let i = 0; i < n - 1; i++) {
        out += " P" + ans[i] + " ->";
    }
    out += " P" + ans[n - 1];
    console.log(out);
}

main();
```

## Summary

The Banker's Algorithm is a core deadlock avoidance protocol that dynamically evaluates resource requests to guarantee system stability. By maintaining detailed data structures representing resource maximum limits, active allocations, and remaining requirements, it prevents systems from entering unsafe states. While computationally expensive due to the $O(n^2 \times m)$ safety checking loop, it serves as a critical mathematical model for safe resource allocation in concurrent execution environments.




