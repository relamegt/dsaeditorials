# Deadlock Free Conditions in Operating Systems

A deadlock is a critical scheduling state where concurrent processes wait indefinitely for each other to release resources, halting system progress. To ensure smooth execution and high reliability, operating systems must enforce conditions that prevent deadlock states from ever forming.

## Mathematical Formulation for Deadlock Avoidance

In a system where P processes compete for R identical resources, we can mathematically calculate the minimum number of resource instances required to guarantee that a deadlock can never occur.

The condition for absolute deadlock avoidance is:

R &gt;= P * (N - 1) + 1

Where:

- **R:** The total available instances of the resource type.
- **P:** The number of competing processes.
- **N:** The maximum resource instances any single process can request.

### Rationale Behind the Formula

1. **Worst-Case Allocation State:** Imagine every process has successfully requested and holds N - 1 resources. In this state, every process is exactly 1 resource short of completing. The total resources currently held across the system is P * (N - 1).
2. **The Extra Resource (+1):** If the system has at least one additional resource instance available (+ 1), then at least one process can acquire its final needed resource, execute its critical section, and release all of its resources.
3. **Progress Guarantee:** Once that process completes and releases its resources, other waiting processes can acquire their needed resources sequentially, ensuring the system remains completely deadlock-free.

### Examples of Resource Calculation (Mohit's System Design Examples)

- **Scenario A (Mohit's Allocation Setup):** Consider three processes—Mohit, Process B, and Process C—competing for resources. If P = 3 and each process requires a maximum of 4 resources (N = 4), the minimum resources required to prevent deadlock is:

  R &gt;= 3 * (4 - 1) + 1 = 10 resources.

- **Scenario B (Mohit's Multi-Task Setup):** If 7 processes (P = 7) each require a maximum of 2 resources (N = 2), the minimum resources required to prevent deadlock is:

  R &gt;= 7 * (2 - 1) + 1 = 8 resources.

## Example of Deadlock-Free Implementation

Below are the complete, compilation-ready implementations of a deadlock-free system check using semaphores in five programming languages.

To prevent the classic circular-wait deadlock (where every process picks up its left resource and waits indefinitely for its right), the solution enforces an asymmetric pickup protocol. While threads `Mohit 0` through `Mohit 3` pick up their left resource first and then their right, thread `Mohit 4` picks up its right resource first. This breaks the circular wait condition.

```Java
import java.util.concurrent.Semaphore;

public class Main {
    private static final int MOHIT_COUNT = 5;
    private static final Semaphore[] resources = new Semaphore[MOHIT_COUNT];
    private static volatile boolean running = true;

    public static void main(String[] args) {
        for (int i = 0; i < MOHIT_COUNT; i++) {
            resources[i] = new Semaphore(1);
        }

        Thread[] threads = new Thread[MOHIT_COUNT];
        for (int i = 0; i < MOHIT_COUNT; i++) {
            final int id = i;
            threads[i] = new Thread(() -> {
                int left = id;
                int right = (id + 1) % MOHIT_COUNT;

                // Enforce asymmetric pick-up for the last thread to avoid deadlock
                if (id == MOHIT_COUNT - 1) {
                    int temp = left;
                    left = right;
                    right = temp;
                }

                while (running) {
                    try {
                        resources[left].acquire();
                        resources[right].acquire();

                        System.out.println("Mohit " + id + " is executing");
                        Thread.sleep(100); // Simulate execution

                        resources[left].release();
                        resources[right].release();

                        System.out.println("Mohit " + id + " is resting");
                        Thread.sleep(100); // Simulate resting
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            });
            threads[i].start();
        }

        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        running = false;

        for (Thread t : threads) {
            try {
                t.join();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```
```C
#include <pthread.h>
#include <semaphore.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <stdbool.h>

#define MOHIT_COUNT 5

sem_t resources[MOHIT_COUNT];
volatile bool running = true;

void* worker(void* arg) {
    int id = *(int*)arg;
    int left = id;
    int right = (id + 1) % MOHIT_COUNT;

    // Asymmetric pickup order for the last thread
    if (id == MOHIT_COUNT - 1) {
        int temp = left;
        left = right;
        right = temp;
    }

    while (running) {
        sem_wait(&resources[left]);
        sem_wait(&resources[right]);

        printf("Mohit %d is executing\n", id);
        fflush(stdout);
        usleep(100000); // 100ms

        sem_post(&resources[left]);
        sem_post(&resources[right]);

        printf("Mohit %d is resting\n", id);
        fflush(stdout);
        usleep(100000); // 100ms
    }
    free(arg);
    return NULL;
}

int main() {
    pthread_t threads[MOHIT_COUNT];

    for (int i = 0; i < MOHIT_COUNT; i++) {
        sem_init(&resources[i], 0, 1);
    }

    for (int i = 0; i < MOHIT_COUNT; i++) {
        int* id = malloc(sizeof(int));
        *id = i;
        pthread_create(&threads[i], NULL, worker, id);
    }

    sleep(1);
    running = false;

    for (int i = 0; i < MOHIT_COUNT; i++) {
        pthread_join(threads[i], NULL);
    }

    for (int i = 0; i < MOHIT_COUNT; i++) {
        sem_destroy(&resources[i]);
    }

    return 0;
}
```
```Cpp
#include <iostream>
#include <thread>
#include <semaphore>
#include <vector>
#include <chrono>
#include <atomic>

const int MOHIT_COUNT = 5;
std::binary_semaphore resources[MOHIT_COUNT]{
    std::binary_semaphore{1}, std::binary_semaphore{1},
    std::binary_semaphore{1}, std::binary_semaphore{1},
    std::binary_semaphore{1}
};
std::atomic<bool> running(true);

void worker(int id) {
    int left = id;
    int right = (id + 1) % MOHIT_COUNT;

    // Asymmetric pickup order for the last thread
    if (id == MOHIT_COUNT - 1) {
        int temp = left;
        left = right;
        right = temp;
    }

    while (running.load()) {
        resources[left].acquire();
        resources[right].acquire();

        std::cout << "Mohit " << id << " is executing\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(100));

        resources[left].release();
        resources[right].release();

        std::cout << "Mohit " << id << " is resting\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    }
}

int main() {
    std::vector<std::thread> threads;
    for (int i = 0; i < MOHIT_COUNT; i++) {
        threads.emplace_back(worker, i);
    }

    std::this_thread::sleep_for(std::chrono::seconds(1));
    running.store(false);

    for (auto& t : threads) {
        t.join();
    }

    return 0;
}
```
```Python
import threading
import time

MOHIT_COUNT = 5
resources = [threading.Semaphore(1) for _ in range(MOHIT_COUNT)]
running = True

def worker(worker_id):
    global running
    left = worker_id
    right = (worker_id + 1) % MOHIT_COUNT

    # Asymmetric pickup order for the last thread
    if worker_id == MOHIT_COUNT - 1:
        left, right = right, left

    while running:
        resources[left].acquire()
        resources[right].acquire()

        print(f"Mohit {worker_id} is executing")
        time.sleep(0.1)

        resources[left].release()
        resources[right].release()

        print(f"Mohit {worker_id} is resting")
        time.sleep(0.1)

if __name__ == "__main__":
    threads = []
    for i in range(MOHIT_COUNT):
        t = threading.Thread(target=worker, args=(i,))
        threads.append(t)
        t.start()

    time.sleep(1)
    running = False

    for t in threads:
        t.join()
```
```JavaScript
const { Worker, isMainThread, workerData } = require('worker_threads');

const MOHIT_COUNT = 5;

if (isMainThread) {
    // Shared memory: 
    // - indices 0 to 4: resources semaphores (0 = taken, 1 = free)
    // - index 5: running status (1 = running, 0 = stop)
    const sab = new SharedArrayBuffer(24);
    const sharedArray = new Int32Array(sab);
    for (let i = 0; i < MOHIT_COUNT; i++) {
        sharedArray[i] = 1; // All resources initially free
    }
    sharedArray[5] = 1; // running = true

    const workers = [];
    for (let i = 0; i < MOHIT_COUNT; i++) {
        workers.push(new Worker(__filename, { workerData: { id: i, sab } }));
    }

    setTimeout(() => {
        Atomics.store(sharedArray, 5, 0); // running = false after 1s
        for (let i = 0; i < MOHIT_COUNT; i++) {
            Atomics.notify(sharedArray, i, MOHIT_COUNT); // notify any waiting workers
        }
    }, 1000);

} else {
    const { id, sab } = workerData;
    const sharedArray = new Int32Array(sab);

    let left = id;
    let right = (id + 1) % MOHIT_COUNT;

    // Asymmetric pickup order for the last thread
    if (id === MOHIT_COUNT - 1) {
        const temp = left;
        left = right;
        right = temp;
    }

    const acquireResource = (resourceId) => {
        while (true) {
            if (Atomics.load(sharedArray, 5) === 0) return false;
            // Try to acquire (set from 1 to 0)
            if (Atomics.compareExchange(sharedArray, resourceId, 1, 0) === 1) {
                return true;
            }
            // Wait on the resource index
            Atomics.wait(sharedArray, resourceId, 0, 50);
        }
    };

    const releaseResource = (resourceId) => {
        Atomics.store(sharedArray, resourceId, 1);
        Atomics.notify(sharedArray, resourceId, 1);
    };

    while (Atomics.load(sharedArray, 5) === 1) {
        if (acquireResource(left)) {
            if (acquireResource(right)) {
                console.log(`Mohit ${id} is executing`);
                
                const start = Date.now();
                while (Date.now() - start < 100) {} // Simulate execution
                
                releaseResource(right);
                releaseResource(left);

                console.log(`Mohit ${id} is resting`);
                const thinkStart = Date.now();
                while (Date.now() - thinkStart < 100) {} // Simulate resting
            } else {
                releaseResource(left);
            }
        }
    }
}
```

## Example Output

When running the thread execution, you will see a continuous trace of threads safely alternating between executing and resting without deadlocking:

```text
Mohit 0 is executing
Mohit 2 is executing
Mohit 0 is resting
Mohit 4 is executing
Mohit 2 is resting
Mohit 1 is executing
Mohit 1 is resting
Mohit 4 is resting
Mohit 0 is executing
Mohit 3 is executing
```

## Summary

Deadlock-free execution inside concurrent computing platforms requires enforcing mathematical resource boundaries or implementing asymmetric coordination protocols. The relation R &gt;= P * (N - 1) + 1 establishes the hardware limits required to prevent starvation or blocking under worst-case hold-and-wait requests. Concurrently, software algorithms (such as the asymmetric pickup order implemented by the Mohit threads) break the circular-wait condition, ensuring that execution cycles remain productive. By matching hardware allocations with smart resource contention designs, operating systems guarantee high performance and reliable concurrency.




