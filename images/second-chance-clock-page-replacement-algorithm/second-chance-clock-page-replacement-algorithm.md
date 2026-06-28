# Second Chance (Clock) Page Replacement Algorithm

The Second Chance Page Replacement Algorithm (often referred to as the Clock Page Replacement policy) is an optimization of the First-In, First-Out (FIFO) replacement scheme. It prevents the eviction of active, frequently accessed pages by introducing a single-bit reference flag for each physical page frame. When a page fault occurs, pages with an active reference bit are bypassed and given a "second chance," while pages with an inactive bit are selected for eviction.

## Mechanics of the Clock Pointer

The algorithm operates in a circular queue layout, conceptualized as a clock face with a rotating clock pointer:

- **Reference Bit (R):**
- `R = 1`: The page has been accessed since the last scan.
- `R = 0`: The page has not been accessed recently.
- **Allocation and Hit Heuristics:**

1. When a process references a page already in memory, the hardware set its reference bit to `1`.
2. When a page fault occurs and no frames are free, the clock pointer scans the circular queue:

- If the current page has `R = 0`, it is selected as the victim, replaced with the new page, and its reference bit is initialized to `0`. The pointer advances to the next slot.
- If the current page has `R = 1`, the bit is cleared to `0` (granting a second chance), the pointer advances to the next slot, and the evaluation repeats.

## Step-by-Step Translation Trace

Consider a system configured with **3 physical RAM frames** (initially empty) and the following page reference sequence:

```text
Reference String: 1, 5, 2, 5, 3, 5, 4, 5
```

The algorithm processes the stream as follows:

- **Pass 1 (Page 1):** Load page into Frame 0. Frames: `[1, -1, -1]`, Bits: `[0, 0, 0]`, Pointer: 0. (Fault 1)
- **Pass 2 (Page 5):** Load page into Frame 1. Frames: `[1, 5, -1]`, Bits: `[0, 0, 0]`, Pointer: 0. (Fault 2)
- **Pass 3 (Page 2):** Load page into Frame 2. Frames: `[1, 5, 2]`, Bits: `[0, 0, 0]`, Pointer: 0. (Fault 3)
- **Pass 4 (Page 5):** Already resident. Hit! Reference bit for 5 is set to 1. Frames: `[1, 5, 2]`, Bits: `[0, 1, 0]`, Pointer: 0.
- **Pass 5 (Page 3):** Fault. Pointer is at Frame 0 (page 1, bit 0). Evict 1. Frames: `[3, 5, 2]`, Bits: `[0, 1, 0]`, Pointer: 1. (Fault 4)
- **Pass 6 (Page 5):** Already resident. Hit! Reference bit for 5 remains 1. Frames: `[3, 5, 2]`, Bits: `[0, 1, 0]`, Pointer: 1.
- **Pass 7 (Page 4):** Fault. Pointer is at Frame 1 (page 5, bit 1). Reset bit to 0, advance pointer to Frame 2 (page 2, bit 0). Evict 2. Frames: `[3, 5, 4]`, Bits: `[0, 0, 0]`, Pointer: 0. (Fault 5)
- **Pass 8 (Page 5):** Already resident. Hit! Reference bit for 5 is set to 1. Frames: `[3, 5, 4]`, Bits: `[0, 1, 0]`, Pointer: 0.
- **Total Page Faults:** 5

## Implementations of Second Chance Algorithm

Below are the complete, compilation-ready implementations of the Second Chance (Clock) page replacement algorithm in five programming languages:

```Java
import java.util.Arrays;

public class Main {
    static boolean findAndUpdate(int x, int[] arr, boolean[] secondChance, int frames) {
        for (int i = 0; i < frames; i++) {
            if (arr[i] == x) {
                secondChance[i] = true;
                return true;
            }
        }
        return false;
    }

    static int replaceAndUpdate(int x, int[] arr, boolean[] secondChance, int frames, int pointer) {
        while (true) {
            if (!secondChance[pointer]) {
                arr[pointer] = x;
                return (pointer + 1) % frames;
            }
            secondChance[pointer] = false;
            pointer = (pointer + 1) % frames;
        }
    }

    static void printHitsAndFaults(String referenceString, int frames) {
        int pointer = 0, i, l, x, pf = 0;
        int[] arr = new int[frames];
        Arrays.fill(arr, -1);
        boolean[] secondChance = new boolean[frames];
        String[] str = referenceString.split(" ");
        l = str.length;
        for (i = 0; i < l; i++) {
            x = Integer.parseInt(str[i]);
            if (!findAndUpdate(x, arr, secondChance, frames)) {
                pointer = replaceAndUpdate(x, arr, secondChance, frames, pointer);
                pf++;
            }
        }
        System.out.println("Total page faults were " + pf);
    }

    public static void main(String[] args) {
        String referenceString = "1 5 2 5 3 5 4 5";
        int frames = 3;
        printHitsAndFaults(referenceString, frames);

        referenceString = "3 6 11 2 3 3 7 10 2 3 11 3 7 2 3 2 7 10 6 2";
        frames = 4;
        printHitsAndFaults(referenceString, frames);
    }
}
```
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>

bool findAndUpdate(int x, int arr[], bool secondChance[], int frames) {
    for (int i = 0; i < frames; i++) {
        if (arr[i] == x) {
            secondChance[i] = true;
            return true;
        }
    }
    return false;
}

int replaceAndUpdate(int x, int arr[], bool secondChance[], int frames, int pointer) {
    while (true) {
        if (!secondChance[pointer]) {
            arr[pointer] = x;
            return (pointer + 1) % frames;
        }
        secondChance[pointer] = false;
        pointer = (pointer + 1) % frames;
    }
}

void printHitsAndFaults(const char* referenceString, int frames) {
    int pointer = 0, pf = 0;
    int* arr = (int*)malloc(frames * sizeof(int));
    bool* secondChance = (bool*)malloc(frames * sizeof(bool));
    
    for (int i = 0; i < frames; i++) {
        arr[i] = -1;
        secondChance[i] = false;
    }

    char* refCopy = strdup(referenceString);
    char* token = strtok(refCopy, " ");
    while (token != NULL) {
        int x = atoi(token);
        if (!findAndUpdate(x, arr, secondChance, frames)) {
            pointer = replaceAndUpdate(x, arr, secondChance, frames, pointer);
            pf++;
        }
        token = strtok(NULL, " ");
    }

    printf("Total page faults were %d\n", pf);
    free(arr);
    free(secondChance);
    free(refCopy);
}

int main() {
    printHitsAndFaults("1 5 2 5 3 5 4 5", 3);
    printHitsAndFaults("3 6 11 2 3 3 7 10 2 3 11 3 7 2 3 2 7 10 6 2", 4);
    return 0;
}
```
```Cpp
#include <iostream>
#include <vector>
#include <string>
#include <sstream>

bool findAndUpdate(int x, std::vector<int>& arr, std::vector<bool>& secondChance, int frames) {
    for (int i = 0; i < frames; i++) {
        if (arr[i] == x) {
            secondChance[i] = true;
            return true;
        }
    }
    return false;
}

int replaceAndUpdate(int x, std::vector<int>& arr, std::vector<bool>& secondChance, int frames, int pointer) {
    while (true) {
        if (!secondChance[pointer]) {
            arr[pointer] = x;
            return (pointer + 1) % frames;
        }
        secondChance[pointer] = false;
        pointer = (pointer + 1) % frames;
    }
}

void printHitsAndFaults(const std::string& referenceString, int frames) {
    int pointer = 0, pf = 0;
    std::vector<int> arr(frames, -1);
    std::vector<bool> secondChance(frames, false);
    
    std::stringstream ss(referenceString);
    int x;
    while (ss >> x) {
        if (!findAndUpdate(x, arr, secondChance, frames)) {
            pointer = replaceAndUpdate(x, arr, secondChance, frames, pointer);
            pf++;
        }
    }
    std::cout << "Total page faults were " << pf << std::endl;
}

int main() {
    printHitsAndFaults("1 5 2 5 3 5 4 5", 3);
    printHitsAndFaults("3 6 11 2 3 3 7 10 2 3 11 3 7 2 3 2 7 10 6 2", 4);
    return 0;
}
```
```Python
def find_and_update(x, arr, second_chance, frames):
    for i in range(frames):
        if arr[i] == x:
            second_chance[i] = True
            return True
    return False

def replace_and_update(x, arr, second_chance, frames, pointer):
    while True:
        if not second_chance[pointer]:
            arr[pointer] = x
            return (pointer + 1) % frames
        second_chance[pointer] = False
        pointer = (pointer + 1) % frames

def print_hits_and_faults(reference_string, frames):
    pointer = 0
    pf = 0
    arr = [-1] * frames
    second_chance = [False] * frames
    tokens = reference_string.split()
    for token in tokens:
        x = int(token)
        if not find_and_update(x, arr, second_chance, frames):
            pointer = replace_and_update(x, arr, second_chance, frames, pointer)
            pf += 1
    print(f"Total page faults were {pf}")

if __name__ == "__main__":
    print_hits_and_faults("1 5 2 5 3 5 4 5", 3)
    print_hits_and_faults("3 6 11 2 3 3 7 10 2 3 11 3 7 2 3 2 7 10 6 2", 4)
```
```JavaScript
function findAndUpdate(x, arr, secondChance, frames) {
    for (let i = 0; i < frames; i++) {
        if (arr[i] === x) {
            secondChance[i] = true;
            return true;
        }
    }
    return false;
}

function replaceAndUpdate(x, arr, secondChance, frames, pointer) {
    while (true) {
        if (!secondChance[pointer]) {
            arr[pointer] = x;
            return (pointer + 1) % frames;
        }
        secondChance[pointer] = false;
        pointer = (pointer + 1) % frames;
    }
}

function printHitsAndFaults(referenceString, frames) {
    let pointer = 0, pf = 0;
    const arr = new Array(frames).fill(-1);
    const secondChance = new Array(frames).fill(false);
    const tokens = referenceString.split(" ");
    
    for (let i = 0; i < tokens.length; i++) {
        const x = parseInt(tokens[i], 10);
        if (!findAndUpdate(x, arr, secondChance, frames)) {
            pointer = replaceAndUpdate(x, arr, secondChance, frames, pointer);
            pf++;
        }
    }
    console.log("Total page faults were " + pf);
}

printHitsAndFaults("1 5 2 5 3 5 4 5", 3);
printHitsAndFaults("3 6 11 2 3 3 7 10 2 3 11 3 7 2 3 2 7 10 6 2", 4);
```

## Output

Total page faults were 5
Total page faults were 11

## Advantages and Disadvantages

### Advantages

- **Optimizes FIFO Evictions:** Bypasses frequently accessed pages, preventing the thrashing associated with simple FIFO queue replacements.
- **Low Computational Overhead:** Does not require sorting pages by access times like LRU; it only requires a single-bit check per page, making it fast and easy to implement in hardware.
- **Similar Performance to LRU:** Under typical application workloads, the hit rate closely matches the performance of the more complex LRU algorithm.

### Disadvantages

- **Susceptible to Belady's Anomaly:** Because it is structurally a modification of the FIFO queue, it does not satisfy the stack property and remains vulnerable to Belady's Anomaly.
- **Pointer Traversal Overhead:** In the worst-case scenario (where all pages have their reference bits set to 1), the pointer must traverse the entire queue, resetting all bits to 0 before locating a page to evict, resulting in O(F) search latency.

> **Note:** The Second Chance (Clock) algorithm represents a compromise between FIFO simplicity and LRU performance. By using a single reference bit to bypass evicting active pages, it achieves low page fault rates with low CPU overhead.

## Summary

The Second Chance (Clock) algorithm is a page replacement strategy that updates FIFO queue mechanics with a reference bit tracking system. By using a rotating clock pointer to check page reference flags, it grants active pages a second chance, evicting only pages that have not been referenced recently. While the Clock algorithm is simple, fast, and performs similarly to LRU, it is still vulnerable to Belady's Anomaly. Modern operating systems implement this circular clock lookup to execute high-speed page evictions under heavy workloads.




