# Semaphores in Process Synchronization

A semaphore is a synchronization tool used in operating systems to manage access to shared resources in a multi-process or multi-threaded environment. It is an integer variable that controls process execution using atomic operations like `wait()` and `signal()`. Semaphores help prevent race conditions and ensure proper coordination between processes.

- **Resource Counter:** Maintains a counter representing available resources.
- **Mutual Exclusion:** Restricts concurrent entry to the critical section.
- **Process Coordination:** Coordinates order of execution and can block or wake up threads during execution.

## Core Concepts

### Working of Semaphores

A semaphore variable $S$ in an operating system uses two primary atomic, indivisible operations:

#### 1. wait(S) (Also known as P operation)

- Decrements the semaphore value: $S = S - 1$.
- If the value is less than 0, the calling process is blocked and added to the waiting queue until the resource becomes available.
- Used to acquire a resource.

#### 2. signal(S) (Also known as V operation)

- Increments the semaphore value: $S = S + 1$.
- If there are waiting processes in the queue, one is awakened and moved to the ready queue.
- Used to release a resource.

### Types of Semaphores

Semaphores are categorized based on their range of values:

#### 1. Binary Semaphore

- Range of values is strictly 0 and 1.
- Used primarily for mutual exclusion (acting similarly to a mutex lock) to protect a single critical section.
- Prevents multiple processes from accessing a shared resource simultaneously.

#### 2. Counting Semaphore

- Range of values spans from 0 to any positive integer $N$.
- Used to manage access to a resource pool with multiple identical instances (e.g., 5 printers, 3 database connections).
- Tracks how many instances are currently free.

### Limitations of Semaphores

- **Priority Inversion:** A low-priority process holding a semaphore can block a high-priority process.
- **Deadlock:** Multiple processes waiting on each other's semaphores in a cyclic dependency will block indefinitely.
- **Complex to Manage:** Hard to debug and verify; a missed `wait()` or `signal()` call can cause system-wide hang or data corruption.
- **Busy Waiting (Spinlock-like):** In basic implementations, processes spin checking variables, although advanced operating systems use sleeping/waiting queues.

## Implementations of Semaphores

Here are complete, multi-threaded implementations of a Counting Semaphore with 3 permits (allowing at most 3 threads to access the resource concurrently) in five programming languages:

```Java
import java.util.concurrent.Semaphore;

public class Main {
    private static final int THREAD_COUNT = 6;
    private static final Semaphore semaphore = new Semaphore(3); // 3 permits
    private static volatile boolean completed = false;

    public static void main(String[] args) {
        Thread[] threads = new Thread[THREAD_COUNT];
        for (int i = 0; i < THREAD_COUNT; i++) {
            final int id = i;
            threads[i] = new Thread(() -> {
                while (!completed) {
                    try {
                        semaphore.acquire();
                        System.out.println("Thread " + id + " acquired a permit. Permits available: " + semaphore.availablePermits());
                        Thread.sleep(100); // Simulate resource usage
                        System.out.println("Thread " + id + " released a permit.");
                        semaphore.release();
                        Thread.sleep(150); // Remainder Section
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            });
            threads[i].start();
        }

        try {
            Thread.sleep(2000);
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
}
```
```C
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>
#include <stdbool.h>
#include <semaphore.h>

#define THREAD_COUNT 6

sem_t semaphore;
volatile bool completed = false;

void* worker(void* arg) {
    int id = *(int*)arg;
    while (!completed) {
        sem_wait(&semaphore);
        int val;
        sem_getvalue(&semaphore, &val);
        printf("Thread %d acquired a permit. Permits available: %d\n", id, val);
        fflush(stdout);
        usleep(100000); // simulate work (100ms)
        printf("Thread %d released a permit.\n", id);
        fflush(stdout);
        sem_post(&semaphore);
        usleep(150000); // remainder section
    }
    return NULL;
}

int main() {
    pthread_t threads[THREAD_COUNT];
    int ids[THREAD_COUNT];

    // Initialize semaphore with value 3
    sem_init(&semaphore, 0, 3);

    for (int i = 0; i < THREAD_COUNT; i++) {
        ids[i] = i;
        pthread_create(&threads[i], NULL, worker, &ids[i]);
    }

    sleep(2);
    completed = true;

    for (int i = 0; i < THREAD_COUNT; i++) {
        pthread_join(threads[i], NULL);
    }

    sem_destroy(&semaphore);
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

const int THREAD_COUNT = 6;
std::counting_semaphore<3> semaphore(3); // 3 permits
std::atomic<bool> completed(false);

void worker(int id) {
    while (!completed.load()) {
        semaphore.acquire();
        std::cout << "Thread " << id << " acquired a permit.\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(100)); // Simulate work
        std::cout << "Thread " << id << " released a permit.\n";
        semaphore.release();
        std::this_thread::sleep_for(std::chrono::milliseconds(150)); // Remainder Section
    }
}

int main() {
    std::vector<std::thread> threads;
    for (int i = 0; i < THREAD_COUNT; i++) {
        threads.emplace_back(worker, i);
    }

    std::this_thread::sleep_for(std::chrono::seconds(2));
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

THREAD_COUNT = 6
semaphore = threading.Semaphore(3) # 3 permits
completed = False

def worker(thread_id):
    global completed
    while not completed:
        semaphore.acquire()
        print(f"Thread {thread_id} acquired a permit.")
        time.sleep(0.1) # Simulate work
        print(f"Thread {thread_id} released a permit.")
        semaphore.release()
        time.sleep(0.15) # Remainder Section

if __name__ == "__main__":
    threads = []
    for i in range(THREAD_COUNT):
        t = threading.Thread(target=worker, args=(i,))
        threads.append(t)
        t.start()
        
    time.sleep(2)
    completed = True
    
    for t in threads:
        t.join()
```
```JavaScript
const { Worker, isMainThread, workerData } = require('worker_threads');

const THREAD_COUNT = 6;

if (isMainThread) {
    // Shared memory: 
    // - permits count at index 0 (initialized to 3)
    // - completed flag at index 1
    const sab = new SharedArrayBuffer(8);
    const sharedArray = new Int32Array(sab);
    sharedArray[0] = 3; 
    sharedArray[1] = 0; 

    const workers = [];
    for (let i = 0; i < THREAD_COUNT; i++) {
        workers.push(new Worker(__filename, { workerData: { id: i, sab } }));
    }

    setTimeout(() => {
        Atomics.store(sharedArray, 1, 1); // completed = true after 2s
        Atomics.notify(sharedArray, 0, THREAD_COUNT); // wake up any waiting threads to exit
    }, 2000);

} else {
    const { id, sab } = workerData;
    const sharedArray = new Int32Array(sab);

    const isCompleted = () => Atomics.load(sharedArray, 1) === 1;

    const wait = () => {
        while (true) {
            if (isCompleted()) return false;
            const current = Atomics.load(sharedArray, 0);
            if (current > 0) {
                if (Atomics.compareExchange(sharedArray, 0, current, current - 1) === current) {
                    return true;
                }
            } else {
                Atomics.wait(sharedArray, 0, 0, 100); // wait for 100ms
            }
        }
    };

    const signal = () => {
        while (true) {
            const current = Atomics.load(sharedArray, 0);
            if (Atomics.compareExchange(sharedArray, 0, current, current + 1) === current) {
                Atomics.notify(sharedArray, 0, 1);
                break;
            }
        }
    };

    while (!isCompleted()) {
        if (wait()) {
            console.log(`Thread ${id} acquired a permit. Permits available: ${Atomics.load(sharedArray, 0)}`);
            
            const start = Date.now();
            while (Date.now() - start < 100) {} // Simulate work
            
            console.log(`Thread ${id} released a permit.`);
            signal();

            const remainderStart = Date.now();
            while (Date.now() - remainderStart < 150) {}
        }
    }
}
```

## Example Output

When running the counting semaphore implementation with 3 available permits, you will see a maximum of 3 threads concurrent in the critical section, while others wait for release signals:

```text
Thread 0 acquired a permit.
Thread 1 acquired a permit.
Thread 2 acquired a permit.
Thread 0 released a permit.
Thread 3 acquired a permit.
Thread 1 released a permit.
Thread 4 acquired a permit.
Thread 2 released a permit.
Thread 5 acquired a permit.
```

## Summary

Semaphores are highly flexible OS-level abstractions for process synchronization, categorizable into binary semaphores (which enforce mutual exclusion) and counting semaphores (which govern access to a pool of multiple resources). Managed via atomic `wait()` and `signal()` operations, semaphores coordinate concurrent threads without requiring custom hardware loops. While incredibly versatile, their reliance on proper invocation order and OS-level queue checking can lead to complex issues such as deadlocks, starvation, and priority inversion if not carefully managed.




