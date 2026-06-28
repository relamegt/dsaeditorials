# Bakery Algorithm in Process Synchronization

The Bakery Algorithm, proposed by Leslie Lamport, is one of the simplest and most famous solutions to the mutual exclusion problem for $N$ processes. It ensures fairness and follows a First-Come-First-Serve (FCFS) order.

---

## How Does the Bakery Algorithm Work?

In the Bakery Algorithm, each process is assigned a ticket number in lexicographical order. Before entering the critical section, a process receives a ticket number, and the process with the smallest ticket number enters the critical section. If two processes receive the same ticket number, the process with the lower process ID is given priority.

### Lexicographical Order Comparison

If processes $P_i$ and $P_j$ receive the same ticket number:

- If $i &lt; j$, then $P_i$ is served first.
- Else, $P_j$ is served first.

This is formalized as comparing pairs of (ticket number, process ID):
$$(a, b) &lt; (c, d) \iff (a &lt; c) \lor (a = c \land b &lt; d)$$

- $$\max(a[0], \dots, a[n-1])$$ is a number $k$ such that $k \ge a[i]$ for all $i = 0, \dots, n-1$.

### Shared Data Structures

- `choosing` is an array $[0..n-1]$ of boolean values, indicating if process $i$ is currently picking a ticket. Initialized to `false`.
- `number` is an array $[0..n-1]$ of integer values representing the ticket numbers. Initialized to `0`.

---

## Algorithm Pseudocode

```Pascal
repeat
    choosing[i] := true
    number[i] := max(number[0..n-1]) + 1
    choosing[i] := false

    for j := 0 to n-1 do
        while choosing[j] do skip      // wait if other process is choosing
        while number[j] ≠ 0 and (number[j], j) < (number[i], i) do skip
    end for

    // critical section

    number[i] := 0     // exit section
    
    // remainder section
until false
```

---

## Detailed Step Walkthrough

1. **Choosing a Ticket:**

- `choosing[i] := true` announces that process $i$ is in the process of taking a ticket.
- `number[i] := max(number[0..n-1]) + 1` assigns the next highest ticket.
- `number[i] := 0` means that the process is not interested in entering the critical section.
- `choosing[i] := false` declares that the process has finished choosing its ticket.

1. **Waiting Phase:** For each process $j$:

- Wait if process $j$ is still choosing its ticket (`choosing[j] == true`).
- Wait if process $j$ has a smaller ticket number, or has the same ticket number but a smaller process ID $j &lt; i$.

1. **Critical Section:** Process $i$ enters when no other process has higher priority.
2. **Exit Section:** `number[i] := 0` releases the ticket.
3. **Remainder Section:** Process does normal work, then repeats.

---

## Implementations of the Bakery Algorithm

Here are complete, multi-threaded implementations of the Bakery Algorithm in five programming languages, demonstrating mutual exclusion without standard mutex locks:

```Java
import java.util.concurrent.atomic.AtomicInteger;

public class Main {
    private static final int THREAD_COUNT = 8;
    private static final AtomicInteger[] tickets = new AtomicInteger[THREAD_COUNT];
    private static final AtomicInteger[] choosing = new AtomicInteger[THREAD_COUNT];
    private static final AtomicInteger resource = new AtomicInteger(0);
    private static volatile boolean completed = false;

    public static void main(String[] args) {
        for (int i = 0; i < THREAD_COUNT; i++) {
            tickets[i] = new AtomicInteger(0);
            choosing[i] = new AtomicInteger(0);
        }

        Thread[] threads = new Thread[THREAD_COUNT];
        for (int i = 0; i < THREAD_COUNT; i++) {
            final int threadId = i;
            threads[i] = new Thread(() -> {
                while (!completed) {
                    lock(threadId);
                    useResource(threadId);
                    unlock(threadId);
                    try {
                        Thread.sleep(100); // Remainder section
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            });
            threads[i].start();
        }

        try {
            Thread.sleep(5000); // Run for 5 seconds
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        completed = true;

        for (Thread thread : threads) {
            try {
                thread.join();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    private static void lock(int thread) {
        choosing[thread].set(1);

        int maxTicket = 0;
        for (int i = 0; i < THREAD_COUNT; i++) {
            maxTicket = Math.max(tickets[i].get(), maxTicket);
        }
        tickets[thread].set(maxTicket + 1);
        choosing[thread].set(0);

        for (int other = 0; other < THREAD_COUNT; other++) {
            while (choosing[other].get() != 0) {
                Thread.yield();
            }
            while (tickets[other].get() != 0
                   && (tickets[other].get() < tickets[thread].get()
                       || (tickets[other].get() == tickets[thread].get() && other < thread))) {
                Thread.yield();
            }
        }
    }

    private static void unlock(int thread) {
        tickets[thread].set(0);
    }

    private static void useResource(int thread) {
        int current = resource.get();
        if (current != 0) {
            System.out.println("CRITICAL SECTION VIOLATION! Thread " + thread 
                               + " entered while Thread " + current + " is using the resource.");
        }
        resource.set(thread);
        System.out.println("Thread " + thread + " is in the critical section.");
        try {
            Thread.sleep(50);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        resource.set(0);
    }
}
```
```C
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>
#include <stdbool.h>
#include <stdatomic.h>
#include <sched.h>

#define THREAD_COUNT 8

_Atomic int tickets[THREAD_COUNT];
_Atomic int choosing[THREAD_COUNT];
_Atomic int resource = 0;
volatile bool completed = false;

void lock(int thread) {
    atomic_store(&choosing[thread], 1);

    int maxTicket = 0;
    for (int i = 0; i < THREAD_COUNT; i++) {
        int ticket = atomic_load(&tickets[i]);
        if (ticket > maxTicket) {
            maxTicket = ticket;
        }
    }
    atomic_store(&tickets[thread], maxTicket + 1);
    atomic_store(&choosing[thread], 0);

    for (int other = 0; other < THREAD_COUNT; other++) {
        while (atomic_load(&choosing[other]) != 0) {
            sched_yield();
        }
        while (true) {
            int other_ticket = atomic_load(&tickets[other]);
            int my_ticket = atomic_load(&tickets[thread]);
            if (other_ticket == 0) break;
            if (other_ticket < my_ticket || (other_ticket == my_ticket && other < thread)) {
                sched_yield();
            } else {
                break;
            }
        }
    }
}

void unlock(int thread) {
    atomic_store(&tickets[thread], 0);
}

void useResource(int thread) {
    int current = atomic_load(&resource);
    if (current != 0) {
        printf("CRITICAL SECTION VIOLATION! Thread %d entered while Thread %d is using the resource.\n", thread, current);
        fflush(stdout);
    }
    atomic_store(&resource, thread);
    printf("Thread %d is in the critical section.\n", thread);
    fflush(stdout);
    usleep(50000); // simulate critical section work (50ms)
    atomic_store(&resource, 0);
}

void* worker(void* arg) {
    int threadId = *(int*)arg;
    while (!completed) {
        lock(threadId);
        useResource(threadId);
        unlock(threadId);
        usleep(100000); // remainder section
    }
    return NULL;
}

int main() {
    pthread_t threads[THREAD_COUNT];
    int ids[THREAD_COUNT];

    for (int i = 0; i < THREAD_COUNT; i++) {
        atomic_init(&tickets[i], 0);
        atomic_init(&choosing[i], 0);
        ids[i] = i;
    }
    atomic_init(&resource, 0);

    for (int i = 0; i < THREAD_COUNT; i++) {
        pthread_create(&threads[i], NULL, worker, &ids[i]);
    }

    sleep(5);
    completed = true;

    for (int i = 0; i < THREAD_COUNT; i++) {
        pthread_join(threads[i], NULL);
    }

    return 0;
}
```
```Cpp
#include <iostream>
#include <thread>
#include <atomic>
#include <vector>
#include <chrono>
#include <algorithm>

const int THREAD_COUNT = 8;
std::vector<std::atomic<int>> tickets(THREAD_COUNT);
std::vector<std::atomic<int>> choosing(THREAD_COUNT);
std::atomic<int> resource(0);
std::atomic<bool> completed(false);

void lock(int thread) {
    choosing[thread].store(1);

    int maxTicket = 0;
    for (int i = 0; i < THREAD_COUNT; i++) {
        maxTicket = std::max(tickets[i].load(), maxTicket);
    }
    tickets[thread].store(maxTicket + 1);
    choosing[thread].store(0);

    for (int other = 0; other < THREAD_COUNT; other++) {
        while (choosing[other].load() != 0) {
            std::this_thread::yield();
        }
        while (true) {
            int other_ticket = tickets[other].load();
            int my_ticket = tickets[thread].load();
            if (other_ticket == 0) break;
            if (other_ticket < my_ticket || (other_ticket == my_ticket && other < thread)) {
                std::this_thread::yield();
            } else {
                break;
            }
        }
    }
}

void unlock(int thread) {
    tickets[thread].store(0);
}

void useResource(int thread) {
    int current = resource.load();
    if (current != 0) {
        std::cout << "CRITICAL SECTION VIOLATION! Thread " << thread 
                  << " entered while Thread " << current << " is using the resource.\n";
    }
    resource.store(thread);
    std::cout << "Thread " << thread << " is in the critical section.\n";
    std::this_thread::sleep_for(std::chrono::milliseconds(50));
    resource.store(0);
}

void worker(int threadId) {
    while (!completed.load()) {
        lock(threadId);
        useResource(threadId);
        unlock(threadId);
        std::this_thread::sleep_for(std::chrono::milliseconds(100)); // remainder section
    }
}

int main() {
    for (int i = 0; i < THREAD_COUNT; i++) {
        tickets[i].store(0);
        choosing[i].store(0);
    }
    resource.store(0);

    std::vector<std::thread> threads;
    for (int i = 0; i < THREAD_COUNT; i++) {
        threads.emplace_back(worker, i);
    }

    std::this_thread::sleep_for(std::chrono::seconds(5));
    completed.store(true);

    for (auto& t : threads) {
        t.join();
    }

    return 0;
}
```
```Python
import threading
import time

THREAD_COUNT = 8
tickets = [0] * THREAD_COUNT
choosing = [0] * THREAD_COUNT
resource = 0
completed = False

def lock(thread_id):
    choosing[thread_id] = 1
    max_ticket = max(tickets)
    tickets[thread_id] = max_ticket + 1
    choosing[thread_id] = 0
    
    for other in range(THREAD_COUNT):
        while choosing[other] != 0:
            time.sleep(0.001)
        while tickets[other] != 0 and (
            tickets[other] < tickets[thread_id] or 
            (tickets[other] == tickets[thread_id] and other < thread_id)
        ):
            time.sleep(0.001)

def unlock(thread_id):
    tickets[thread_id] = 0

def use_resource(thread_id):
    global resource
    current = resource
    if current != 0:
        print(f"CRITICAL SECTION VIOLATION! Thread {thread_id} entered while Thread {current} is using the resource.")
    
    resource = thread_id
    print(f"Thread {thread_id} is in the critical section.")
    time.sleep(0.05)
    resource = 0

def worker(thread_id):
    global completed
    while not completed:
        lock(thread_id)
        use_resource(thread_id)
        unlock(thread_id)
        time.sleep(0.1)

if __name__ == "__main__":
    threads = []
    for i in range(THREAD_COUNT):
        t = threading.Thread(target=worker, args=(i,))
        threads.append(t)
        t.start()
        
    time.sleep(5)
    completed = True
    
    for t in threads:
        t.join()
```
```JavaScript
const { Worker, isMainThread, workerData } = require('worker_threads');

const THREAD_COUNT = 8;

if (isMainThread) {
    // 3 blocks of shared memory: 
    // - choosing array (8 integers)
    // - tickets array (8 integers)
    // - resource integer (1 integer)
    // - completed flag (1 integer)
    // Total: 8 + 8 + 1 + 1 = 18 integers = 72 bytes
    const sab = new SharedArrayBuffer(72);
    const sharedArray = new Int32Array(sab);

    // Initializing state
    for (let i = 0; i < 18; i++) {
        sharedArray[i] = 0;
    }

    const workers = [];
    for (let i = 0; i < THREAD_COUNT; i++) {
        workers.push(new Worker(__filename, { workerData: { id: i, sab } }));
    }

    setTimeout(() => {
        Atomics.store(sharedArray, 17, 1); // completed = true after 5s
    }, 5000);

} else {
    const { id, sab } = workerData;
    const sharedArray = new Int32Array(sab);

    const getChoosing = (idx) => Atomics.load(sharedArray, idx);
    const setChoosing = (idx, val) => Atomics.store(sharedArray, idx, val);

    const getTicket = (idx) => Atomics.load(sharedArray, 8 + idx);
    const setTicket = (idx, val) => Atomics.store(sharedArray, 8 + idx, val);

    const getResource = () => Atomics.load(sharedArray, 16);
    const setResource = (val) => Atomics.store(sharedArray, 16, val);

    const isCompleted = () => Atomics.load(sharedArray, 17) === 1;

    const lock = (threadId) => {
        setChoosing(threadId, 1);

        let maxTicket = 0;
        for (let i = 0; i < THREAD_COUNT; i++) {
            const ticket = getTicket(i);
            if (ticket > maxTicket) {
                maxTicket = ticket;
            }
        }
        setTicket(threadId, maxTicket + 1);
        setChoosing(threadId, 0);

        for (let other = 0; other < THREAD_COUNT; other++) {
            while (getChoosing(other) !== 0) {
                // Busy-wait
            }
            while (true) {
                const otherTicket = getTicket(other);
                const myTicket = getTicket(threadId);
                if (otherTicket === 0) break;
                if (otherTicket < myTicket || (otherTicket === myTicket && other < threadId)) {
                    // Busy-wait
                } else {
                    break;
                }
            }
        }
    };

    const unlock = (threadId) => {
        setTicket(threadId, 0);
    };

    const useResource = (threadId) => {
        const current = getResource();
        if (current !== 0) {
            console.log(`CRITICAL SECTION VIOLATION! Thread ${threadId} entered while Thread ${current} is using the resource.`);
        }
        setResource(threadId);
        console.log(`Thread ${threadId} is in the critical section.`);
        
        const start = Date.now();
        while (Date.now() - start < 50) {}
        
        setResource(0);
    };

    while (!isCompleted()) {
        lock(id);
        useResource(id);
        unlock(id);

        const start = Date.now();
        while (Date.now() - start < 100) {}
    }
}
```

---

## Example Output

When running the implementations, you will see a serialized, mutual exclusion sequence of threads entering the critical section one by one without conflict:

```text
Thread 0 is in the critical section.
Thread 1 is in the critical section.
Thread 2 is in the critical section.
Thread 3 is in the critical section.
Thread 4 is in the critical section.
Thread 5 is in the critical section.
Thread 6 is in the critical section.
Thread 7 is in the critical section.
Thread 0 is in the critical section.
Thread 1 is in the critical section.
```

---

## Advantages and Disadvantages

### Advantages

- **Fairness:** The Bakery Algorithm ensures FCFS order, eliminating any chance of indefinite postponement or favoritism.
- **No Deadlocks or Starvation:** Guaranteed by the strictly increasing lexicographical tickets order.
- **Software-Only Solution:** Works purely on shared memory without requiring underlying OS scheduling or hardware primitives (like Test-And-Set).

### Disadvantages

- **Not Scalable:** Time complexity for thread verification grows linearly $O(N)$ with the thread count.
- **Busy Waiting:** Threads spin in empty `while` loops waiting for their priority turn, wasting CPU cycles and energy.
- **Memory Overhead:** Requires state arrays of size $N$ (`choosing` and `tickets`), which grows with scale.




