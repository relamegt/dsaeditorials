# Dekker's Algorithm in Process Synchronization

Dekker’s Algorithm was the first correct solution to the critical section problem for two processes. It is significant in the history of operating systems because: 

- **Avoids Strict Alternation:** It does not require processes to strictly take turns (naïve alternation).
- **Shared Memory Only:** It relies entirely on shared memory (Boolean flags and a single `turn` variable) without requiring hardware-level atomic instructions or OS-level semaphores.
- **Guarantees Core Synchronization Conditions:** It ensures mutual exclusion, progress, and bounded waiting.

A process participating in a synchronization protocol is generally structured as follows:

```C
do {
    // entry section
    critical section
    // exit section
    remainder section
} while (TRUE);
```

The solution to the critical section problem must satisfy three essential requirements:

1. **Mutual Exclusion:** If process $P_i$ is executing in its critical section, then no other processes can be executing in their critical sections.
2. **Progress:** If no process is executing in its critical section and there are some processes that wish to enter their critical section, then only those processes that are not executing in their remainder section can participate in deciding which process will enter its critical section next, and this selection cannot be postponed indefinitely.
3. **Bounded Waiting:** There must be a limit on the number of times that other processes are allowed to enter their critical sections after a process has made a request to enter its critical section and before that request is granted.

---

## The Dekker's Algorithm (Conceptual)

The algorithm uses a shared array of boolean flags to represent intent and a `turn` variable to resolve conflicts:

```Pascal
var flag: array [0..1] of boolean; // initialized to false
turn: 0..1;                        // initialized to 0 or 1

repeat
    flag[i] := true;
    while flag[j] do
    begin
        if turn = j then
        begin
            flag[i] := false;
            while turn = j do no-op; // busy wait
            flag[i] := true;
        end;
    end;
    
    // critical section
    
    turn := j;
    flag[i] := false;
    
    // remainder section
until false;
```

---

## Evolution of Dekker’s Algorithm

Dekker’s Algorithm was developed in five versions, with each iteration addressing a specific concurrency bug or limitation of the previous one.

### 1. First Version: Strict Alternation (Turn-taking)

The idea is to use a single shared variable `turn` to decide whose turn it is to enter the critical section.

- **Idea:** A process can enter only when `turn` matches its ID.
- **Problem:** Strict alternation. If Process 1 enters and exits, `turn` becomes 2. If Process 2 never wants to enter its critical section, Process 1 is blocked from entering again, even if the critical section is completely empty. This violates the **Progress** requirement.

```Java
import java.lang.Thread;

public class ThreadExample {

    static boolean completed = false;
    static int threadNumber = 1;

    static void Thread1() {
        boolean doWhile = false;
        while (!completed || !doWhile) {
            doWhile = true;

            while (threadNumber == 2) {
                Thread.yield();
            }
            // critical section
            threadNumber = 2; // pass turn to Thread 2
        }
    }

    static void Thread2() {
        boolean doWhile = false;
        while (!completed || !doWhile) {
            doWhile = true;

            while (threadNumber == 1) {
                Thread.yield();
            }
            // critical section
            threadNumber = 1; // pass turn to Thread 1
        }
    }

    static void StartThreads() {
        Thread t1 = new Thread(ThreadExample::Thread1);
        Thread t2 = new Thread(ThreadExample::Thread2);
        t1.start();
        t2.start();
    }

    public static void main(String[] args) {
        threadNumber = 1;
        StartThreads();
    }
}
```
```C
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>
#include <stdbool.h>
#include <sched.h>

volatile int threadNumber = 1;
volatile bool completed = false;

void* Thread1(void* arg) {
    bool doWhile = false;
    while (!completed || !doWhile) {
        doWhile = true;
        while (threadNumber == 2) {
            sched_yield();
        }
        // critical section
        threadNumber = 2;
    }
    return NULL;
}

void* Thread2(void* arg) {
    bool doWhile = false;
    while (!completed || !doWhile) {
        doWhile = true;
        while (threadNumber == 1) {
            sched_yield();
        }
        // critical section
        threadNumber = 1;
    }
    return NULL;
}

int main() {
    pthread_t t1, t2;
    pthread_create(&t1, NULL, Thread1, NULL);
    pthread_create(&t2, NULL, Thread2, NULL);
    sleep(2);
    completed = true;
    pthread_join(t1, NULL);
    pthread_join(t2, NULL);
    return 0;
}
```
```Cpp
#include <iostream>
#include <thread>
#include <atomic>
#include <chrono>

std::atomic<int> threadNumber(1);
std::atomic<bool> completed(false);

void Thread1() {
    bool doWhile = false;
    while (!completed || !doWhile) {
        doWhile = true;
        while (threadNumber == 2) {
            std::this_thread::yield();
        }
        // critical section
        threadNumber = 2;
    }
}

void Thread2() {
    bool doWhile = false;
    while (!completed || !doWhile) {
        doWhile = true;
        while (threadNumber == 1) {
            std::this_thread::yield();
        }
        // critical section
        threadNumber = 1;
    }
}

int main() {
    std::thread t1(Thread1);
    std::thread t2(Thread2);
    std::this_thread::sleep_for(std::chrono::seconds(2));
    completed = true;
    t1.join();
    t2.join();
    return 0;
}
```
```Python
import threading
import time

thread_number = 1
completed = False

def thread1():
    global thread_number, completed
    do_while = False
    while not completed or not do_while:
        do_while = True
        while thread_number == 2:
            time.sleep(0.001)
        # critical section
        thread_number = 2

def thread2():
    global thread_number, completed
    do_while = False
    while not completed or not do_while:
        do_while = True
        while thread_number == 1:
            time.sleep(0.001)
        # critical section
        thread_number = 1

t1 = threading.Thread(target=thread1)
t2 = threading.Thread(target=thread2)
t1.start()
t2.start()
time.sleep(2)
completed = True
t1.join()
t2.join()
```
```JavaScript
const { Worker, isMainThread, workerData } = require('worker_threads');

if (isMainThread) {
    const sab = new SharedArrayBuffer(8);
    const sharedArray = new Int32Array(sab);
    sharedArray[0] = 1; // threadNumber = 1
    sharedArray[1] = 0; // completed = false

    new Worker(__filename, { workerData: { id: 1, sab } });
    new Worker(__filename, { workerData: { id: 2, sab } });

    setTimeout(() => {
        Atomics.store(sharedArray, 1, 1); // completed = true
    }, 2000);
} else {
    const { id, sab } = workerData;
    const sharedArray = new Int32Array(sab);

    const getThreadNum = () => Atomics.load(sharedArray, 0);
    const setThreadNum = (val) => Atomics.store(sharedArray, 0, val);
    const isCompleted = () => Atomics.load(sharedArray, 1) === 1;

    let doWhile = false;
    const waitNum = id === 1 ? 2 : 1;
    const nextNum = id === 1 ? 2 : 1;

    while (!isCompleted() || !doWhile) {
        doWhile = true;
        while (getThreadNum() === waitNum) {
            // Busy-wait
        }
        // critical section
        setThreadNum(nextNum);
    }
}
```

---

### 2. Second Version: Status Flags (After Entry check)

To remove the lockstep strict alternation, this version uses two flags to indicate the current state of each thread.

- **Idea:** Each process checks the other's flag, and if it's clear, sets its own flag and enters.
- **Problem:** If both threads check the flags at the same time and see they are `false`, they will both set their flags to `true` and enter the critical section simultaneously. This violates the **Mutual Exclusion** requirement.

```Java
public class MutualExclusion {

    // flags to indicate if each thread is in its critical section
    volatile boolean thread1 = false;
    volatile boolean thread2 = false;
    static volatile boolean completed = false;

    public void startThreads() {
        new Thread(() -> thread1()).start();
        new Thread(() -> thread2()).start();
    }

    public void thread1() {
        do {
            // entry section
            // wait until thread2 is in its critical section
            while (thread2 == true) {
                Thread.yield();
            }

            // indicate thread1 entering its critical section
            thread1 = true;

            // critical section
            System.out.println("Thread 1 is in critical section");

            // exit section
            thread1 = false;

            // remainder section
        } while (!completed);
    }

    public void thread2() {
        do {
            // entry section
            // wait until thread1 is in its critical section
            while (thread1 == true) {
                Thread.yield();
            }

            // indicate thread2 entering its critical section
            thread2 = true;

            // critical section
            System.out.println("Thread 2 is in critical section");

            // exit section
            thread2 = false;

            // remainder section
        } while (!completed);
    }

    public static void main(String[] args) {
        MutualExclusion me = new MutualExclusion();
        me.startThreads();
    }
}
```
```C
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>
#include <stdbool.h>
#include <sched.h>

volatile bool thread1 = false;
volatile bool thread2 = false;
volatile bool completed = false;

void* Thread1(void* arg) {
    do {
        while (thread2 == true) {
            sched_yield();
        }
        thread1 = true;
        
        // Critical Section
        printf("Thread 1 is in critical section\n");
        fflush(stdout);

        thread1 = false;
        usleep(100000);
    } while (!completed);
    return NULL;
}

void* Thread2(void* arg) {
    do {
        while (thread1 == true) {
            sched_yield();
        }
        thread2 = true;
        
        // Critical Section
        printf("Thread 2 is in critical section\n");
        fflush(stdout);

        thread2 = false;
        usleep(100000);
    } while (!completed);
    return NULL;
}

int main() {
    pthread_t t1, t2;
    pthread_create(&t1, NULL, Thread1, NULL);
    pthread_create(&t2, NULL, Thread2, NULL);
    sleep(2);
    completed = true;
    pthread_join(t1, NULL);
    pthread_join(t2, NULL);
    return 0;
}
```
```Cpp
#include <iostream>
#include <thread>
#include <atomic>
#include <chrono>

std::atomic<bool> thread1(false);
std::atomic<bool> thread2(false);
std::atomic<bool> completed(false);

void Thread1() {
    do {
        while (thread2) {
            std::this_thread::yield();
        }
        thread1 = true;

        // Critical Section
        std::cout << "Thread 1 is in critical section\n";

        thread1 = false;
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    } while (!completed);
}

void Thread2() {
    do {
        while (thread1) {
            std::this_thread::yield();
        }
        thread2 = true;

        // Critical Section
        std::cout << "Thread 2 is in critical section\n";

        thread2 = false;
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    } while (!completed);
}

int main() {
    std::thread t1(Thread1);
    std::thread t2(Thread2);
    std::this_thread::sleep_for(std::chrono::seconds(2));
    completed = true;
    t1.join();
    t2.join();
    return 0;
}
```
```Python
import threading
import time

thread1_flag = False
thread2_flag = False
completed = False

def thread1():
    global thread1_flag, thread2_flag, completed
    while not completed:
        while thread2_flag:
            time.sleep(0.001)
        thread1_flag = True
        
        # Critical Section
        print("Thread 1 is in critical section")
        
        thread1_flag = False
        time.sleep(0.1)

def thread2():
    global thread1_flag, thread2_flag, completed
    while not completed:
        while thread1_flag:
            time.sleep(0.001)
        thread2_flag = True
        
        # Critical Section
        print("Thread 2 is in critical section")
        
        thread2_flag = False
        time.sleep(0.1)

t1 = threading.Thread(target=thread1)
t2 = threading.Thread(target=thread2)
t1.start()
t2.start()
time.sleep(2)
completed = True
t1.join()
t2.join()
```
```JavaScript
const { Worker, isMainThread, workerData } = require('worker_threads');

if (isMainThread) {
    const sab = new SharedArrayBuffer(12);
    const sharedArray = new Int32Array(sab);
    sharedArray[0] = 0; // thread1_flag = false
    sharedArray[1] = 0; // thread2_flag = false
    sharedArray[2] = 0; // completed = false

    new Worker(__filename, { workerData: { id: 1, sab } });
    new Worker(__filename, { workerData: { id: 2, sab } });

    setTimeout(() => {
        Atomics.store(sharedArray, 2, 1); // completed = true
    }, 2000);
} else {
    const { id, sab } = workerData;
    const sharedArray = new Int32Array(sab);

    const getFlag = (idx) => Atomics.load(sharedArray, idx);
    const setFlag = (idx, val) => Atomics.store(sharedArray, idx, val);
    const isCompleted = () => Atomics.load(sharedArray, 2) === 1;

    const myIdx = id - 1;
    const otherIdx = id === 1 ? 1 : 0;

    while (!isCompleted()) {
        while (getFlag(otherIdx) === 1) {
            // Busy-wait
        }
        setFlag(myIdx, 1);

        // Critical Section
        console.log(`Thread ${id} is in critical section`);

        setFlag(myIdx, 0);

        const start = Date.now();
        while (Date.now() - start < 100) {}
    }
}
```

---

### 3. Third Version: Flags Before Entry (Pre-state Declaration)

To guarantee mutual exclusion, the flags are set *before* the check loop.

- **Idea:** A process sets its flag to `true` before checking the other's flag.
- **Problem:** If both processes set their flags to `true` at the same time before entering the loop, both will find the other's flag is `true` and wait indefinitely. This leads to a **Deadlock**.

```Java
class SharedData {
    static volatile boolean completed = false;
}

class Thread1 extends Thread {
    public static volatile boolean thread1wantstoenter = false;
    public static volatile boolean thread2wantstoenter = false;

    @Override
    public void run() {
        do {
            thread1wantstoenter = true;

            // Entry section
            // Wait until Thread2 wants to enter its critical section
            while (thread2wantstoenter) {
                Thread.yield();
            }

            // Critical section
            System.out.println("Thread 1 is in the critical section");

            // Exit section
            thread1wantstoenter = false;

            // Remainder section
        } while (!SharedData.completed);
    }
}

class Thread2 extends Thread {
    @Override
    public void run() {
        do {
            Thread1.thread2wantstoenter = true;

            // Entry section
            // Wait until Thread1 wants to enter its critical section
            while (Thread1.thread1wantstoenter) {
                Thread.yield();
            }

            // Critical section
            System.out.println("Thread 2 is in the critical section");

            // Exit section
            Thread1.thread2wantstoenter = false;

            // Remainder section
        } while (!SharedData.completed);
    }
}

public class Main {
    public static void main(String[] args) {
        SharedData.completed = false;

        Thread1 thread1 = new Thread1();
        Thread2 thread2 = new Thread2();

        thread1.start();
        thread2.start();

        try {
            Thread.sleep(5000); // Sleep for 5 seconds
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        SharedData.completed = true; // Stop the threads
    }
}
```
```C
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>
#include <stdbool.h>
#include <sched.h>

volatile bool thread1wantstoenter = false;
volatile bool thread2wantstoenter = false;
volatile bool completed = false;

void* Thread1(void* arg) {
    do {
        thread1wantstoenter = true;
        while (thread2wantstoenter) {
            sched_yield();
        }
        
        // Critical Section
        printf("Thread 1 is in the critical section\n");
        fflush(stdout);

        thread1wantstoenter = false;
        usleep(100000);
    } while (!completed);
    return NULL;
}

void* Thread2(void* arg) {
    do {
        thread2wantstoenter = true;
        while (thread1wantstoenter) {
            sched_yield();
        }
        
        // Critical Section
        printf("Thread 2 is in the critical section\n");
        fflush(stdout);

        thread2wantstoenter = false;
        usleep(100000);
    } while (!completed);
    return NULL;
}

int main() {
    pthread_t t1, t2;
    pthread_create(&t1, NULL, Thread1, NULL);
    pthread_create(&t2, NULL, Thread2, NULL);
    sleep(2);
    completed = true;
    pthread_join(t1, NULL);
    pthread_join(t2, NULL);
    return 0;
}
```
```Cpp
#include <iostream>
#include <thread>
#include <atomic>
#include <chrono>

std::atomic<bool> thread1wantstoenter(false);
std::atomic<bool> thread2wantstoenter(false);
std::atomic<bool> completed(false);

void Thread1() {
    do {
        thread1wantstoenter = true;
        while (thread2wantstoenter) {
            std::this_thread::yield();
        }

        // Critical Section
        std::cout << "Thread 1 is in the critical section\n";

        thread1wantstoenter = false;
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    } while (!completed);
}

void Thread2() {
    do {
        thread2wantstoenter = true;
        while (thread1wantstoenter) {
            std::this_thread::yield();
        }

        // Critical Section
        std::cout << "Thread 2 is in the critical section\n";

        thread2wantstoenter = false;
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    } while (!completed);
}

int main() {
    std::thread t1(Thread1);
    std::thread t2(Thread2);
    std::this_thread::sleep_for(std::chrono::seconds(2));
    completed = true;
    t1.join();
    t2.join();
    return 0;
}
```
```Python
import threading
import time

thread1wantstoenter = False
thread2wantstoenter = False
completed = False

def thread1():
    global thread1wantstoenter, thread2wantstoenter, completed
    while not completed:
        thread1wantstoenter = True
        while thread2wantstoenter:
            time.sleep(0.001)
        
        # Critical Section
        print("Thread 1 is in the critical section")
        
        thread1wantstoenter = False
        time.sleep(0.1)

def thread2():
    global thread1wantstoenter, thread2wantstoenter, completed
    while not completed:
        thread2wantstoenter = True
        while thread1wantstoenter:
            time.sleep(0.001)
        
        # Critical Section
        print("Thread 2 is in the critical section")
        
        thread2wantstoenter = False
        time.sleep(0.1)

t1 = threading.Thread(target=thread1)
t2 = threading.Thread(target=thread2)
t1.start()
t2.start()
time.sleep(2)
completed = True
t1.join()
t2.join()
```
```JavaScript
const { Worker, isMainThread, workerData } = require('worker_threads');

if (isMainThread) {
    const sab = new SharedArrayBuffer(12);
    const sharedArray = new Int32Array(sab);
    sharedArray[0] = 0; // thread1wantstoenter = false
    sharedArray[1] = 0; // thread2wantstoenter = false
    sharedArray[2] = 0; // completed = false

    new Worker(__filename, { workerData: { id: 1, sab } });
    new Worker(__filename, { workerData: { id: 2, sab } });

    setTimeout(() => {
        Atomics.store(sharedArray, 2, 1); // completed = true
    }, 2000);
} else {
    const { id, sab } = workerData;
    const sharedArray = new Int32Array(sab);

    const getWants = (idx) => Atomics.load(sharedArray, idx);
    const setWants = (idx, val) => Atomics.store(sharedArray, idx, val);
    const isCompleted = () => Atomics.load(sharedArray, 2) === 1;

    const myIdx = id - 1;
    const otherIdx = id === 1 ? 1 : 0;

    while (!isCompleted()) {
        setWants(myIdx, 1);
        while (getWants(otherIdx) === 1) {
            // Busy-wait
        }

        // Critical Section
        console.log(`Thread ${id} is in the critical section`);

        setWants(myIdx, 0);

        const start = Date.now();
        while (Date.now() - start < 100) {}
    }
}
```

---

### 4. Fourth Version: Flags with Backoff (Politeness)

This version resolves the deadlock problem by making a process back off (unset its flag) if it detects a conflict, waiting for a brief period before retrying.

- **Idea:** If a conflict occurs, a process sets its flag to `false` to let the other go, then sets it back to `true` to retry.
- **Problem:** If both processes run in perfect synchronization, they might continuously set their flags, detect a conflict, back off, and retry simultaneously. This leads to **Livelock** / **Starvation** (indefinite postponement).

```Java
import java.util.Random;

public class TwoThreadMutex {

    private static volatile boolean thread1wantstoenter = false;
    private static volatile boolean thread2wantstoenter = false;
    private static volatile boolean completed = false;

    public static void main(String[] args) {
        startThreads();
    }

    private static void startThreads() {
        Thread t1 = new Thread(TwoThreadMutex::Thread1);
        Thread t2 = new Thread(TwoThreadMutex::Thread2);

        t1.start();
        t2.start();

        try {
            Thread.sleep(5000);
            completed = true;
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    private static void Thread1() {
        Random rand = new Random();
        do {
            thread1wantstoenter = true;

            while (thread2wantstoenter) {
                thread1wantstoenter = false;
                try {
                    // random backoff to break potential synchronization loops
                    Thread.sleep(rand.nextInt(10));
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                thread1wantstoenter = true;
            }

            // Critical section
            System.out.println("Thread 1 is in critical section");

            // Exit section
            thread1wantstoenter = false;

            // Remainder section
        } while (!completed);
    }

    private static void Thread2() {
        Random rand = new Random();
        do {
            thread2wantstoenter = true;

            while (thread1wantstoenter) {
                thread2wantstoenter = false;
                try {
                    // random backoff
                    Thread.sleep(rand.nextInt(10));
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                thread2wantstoenter = true;
            }

            // Critical section
            System.out.println("Thread 2 is in critical section");

            // Exit section
            thread2wantstoenter = false;

            // Remainder section
        } while (!completed);
    }
}
```
```C
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>
#include <stdbool.h>
#include <stdlib.h>
#include <sched.h>

volatile bool thread1wantstoenter = false;
volatile bool thread2wantstoenter = false;
volatile bool completed = false;

void* Thread1(void* arg) {
    do {
        thread1wantstoenter = true;
        while (thread2wantstoenter) {
            thread1wantstoenter = false;
            usleep((rand() % 10) * 1000); // random delay
            thread1wantstoenter = true;
        }

        // Critical Section
        printf("Thread 1 is in critical section\n");
        fflush(stdout);

        thread1wantstoenter = false;
        usleep(100000);
    } while (!completed);
    return NULL;
}

void* Thread2(void* arg) {
    do {
        thread2wantstoenter = true;
        while (thread1wantstoenter) {
            thread2wantstoenter = false;
            usleep((rand() % 10) * 1000); // random delay
            thread2wantstoenter = true;
        }

        // Critical Section
        printf("Thread 2 is in critical section\n");
        fflush(stdout);

        thread2wantstoenter = false;
        usleep(100000);
    } while (!completed);
    return NULL;
}

int main() {
    pthread_t t1, t2;
    pthread_create(&t1, NULL, Thread1, NULL);
    pthread_create(&t2, NULL, Thread2, NULL);
    sleep(2);
    completed = true;
    pthread_join(t1, NULL);
    pthread_join(t2, NULL);
    return 0;
}
```
```Cpp
#include <iostream>
#include <thread>
#include <atomic>
#include <chrono>
#include <random>

std::atomic<bool> thread1wantstoenter(false);
std::atomic<bool> thread2wantstoenter(false);
std::atomic<bool> completed(false);

void Thread1() {
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_int_distribution<> dis(1, 10);

    do {
        thread1wantstoenter = true;
        while (thread2wantstoenter) {
            thread1wantstoenter = false;
            std::this_thread::sleep_for(std::chrono::milliseconds(dis(gen)));
            thread1wantstoenter = true;
        }

        // Critical Section
        std::cout << "Thread 1 is in critical section\n";

        thread1wantstoenter = false;
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    } while (!completed);
}

void Thread2() {
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_int_distribution<> dis(1, 10);

    do {
        thread2wantstoenter = true;
        while (thread1wantstoenter) {
            thread2wantstoenter = false;
            std::this_thread::sleep_for(std::chrono::milliseconds(dis(gen)));
            thread2wantstoenter = true;
        }

        // Critical Section
        std::cout << "Thread 2 is in critical section\n";

        thread2wantstoenter = false;
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    } while (!completed);
}

int main() {
    std::thread t1(Thread1);
    std::thread t2(Thread2);
    std::this_thread::sleep_for(std::chrono::seconds(2));
    completed = true;
    t1.join();
    t2.join();
    return 0;
}
```
```Python
import threading
import time
import random

thread1wantstoenter = False
thread2wantstoenter = False
completed = False

def thread1():
    global thread1wantstoenter, thread2wantstoenter, completed
    while not completed:
        thread1wantstoenter = True
        while thread2wantstoenter:
            thread1wantstoenter = False
            time.sleep(random.uniform(0.001, 0.01))
            thread1wantstoenter = True
        
        # Critical Section
        print("Thread 1 is in critical section")
        
        thread1wantstoenter = False
        time.sleep(0.1)

def thread2():
    global thread1wantstoenter, thread2wantstoenter, completed
    while not completed:
        thread2wantstoenter = True
        while thread1wantstoenter:
            thread2wantstoenter = False
            time.sleep(random.uniform(0.001, 0.01))
            thread2wantstoenter = True
        
        # Critical Section
        print("Thread 2 is in critical section")
        
        thread2wantstoenter = False
        time.sleep(0.1)

t1 = threading.Thread(target=thread1)
t2 = threading.Thread(target=thread2)
t1.start()
t2.start()
time.sleep(2)
completed = True
t1.join()
t2.join()
```
```JavaScript
const { Worker, isMainThread, workerData } = require('worker_threads');

if (isMainThread) {
    const sab = new SharedArrayBuffer(12);
    const sharedArray = new Int32Array(sab);
    sharedArray[0] = 0; // thread1wantstoenter = false
    sharedArray[1] = 0; // thread2wantstoenter = false
    sharedArray[2] = 0; // completed = false

    new Worker(__filename, { workerData: { id: 1, sab } });
    new Worker(__filename, { workerData: { id: 2, sab } });

    setTimeout(() => {
        Atomics.store(sharedArray, 2, 1); // completed = true
    }, 2000);
} else {
    const { id, sab } = workerData;
    const sharedArray = new Int32Array(sab);

    const getWants = (idx) => Atomics.load(sharedArray, idx);
    const setWants = (idx, val) => Atomics.store(sharedArray, idx, val);
    const isCompleted = () => Atomics.load(sharedArray, 2) === 1;

    const myIdx = id - 1;
    const otherIdx = id === 1 ? 1 : 0;

    while (!isCompleted()) {
        setWants(myIdx, 1);
        while (getWants(otherIdx) === 1) {
            setWants(myIdx, 0);
            // Random backoff wait (e.g. 1 to 10 ms)
            const waitTime = Math.floor(Math.random() * 10) + 1;
            const start = Date.now();
            while (Date.now() - start < waitTime) {}
            setWants(myIdx, 1);
        }

        // Critical Section
        console.log(`Thread ${id} is in critical section`);

        setWants(myIdx, 0);

        const start = Date.now();
        while (Date.now() - start < 100) {}
    }
}
```

---

### 5. Dekker's Algorithm: Final and Completed Solution

The final version combines the use of flags (intent) and a `turn` (priority) variable. If both processes want to enter, the `turn` variable decides who goes. After exiting the critical section, the process hands the turn over to the other.

- **Idea:** Flags represent intent; `turn` decides priority during conflict.
- **Solution:** Ensures Mutual Exclusion, Progress, and Bounded Waiting.

```Java
public class Main {
    static volatile int favouredThread = 1;
    static volatile boolean thread1WantsToEnter = false;
    static volatile boolean thread2WantsToEnter = false;
    static volatile boolean completed = false;

    public static void main(String[] args) {
        startThreads();
    }

    static void startThreads() {
        Thread thread1 = new Thread(Main::Thread1);
        Thread thread2 = new Thread(Main::Thread2);

        thread1.start();
        thread2.start();

        try {
            Thread.sleep(5000);
            completed = true;
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    static void Thread1() {
        do {
            thread1WantsToEnter = true;
            while (thread2WantsToEnter) {
                if (favouredThread == 2) {
                    thread1WantsToEnter = false;
                    while (favouredThread == 2) {
                        Thread.yield(); // Wait until it's our turn
                    }
                    thread1WantsToEnter = true;
                }
            }
            
            // Critical Section
            System.out.println("Thread 1 is in the critical section");
            
            favouredThread = 2;
            thread1WantsToEnter = false;
            
            // Remainder Section
        } while (!completed);
    }

    static void Thread2() {
        do {
            thread2WantsToEnter = true;
            while (thread1WantsToEnter) {
                if (favouredThread == 1) {
                    thread2WantsToEnter = false;
                    while (favouredThread == 1) {
                        Thread.yield(); // Wait until it's our turn
                    }
                    thread2WantsToEnter = true;
                }
            }
            
            // Critical Section
            System.out.println("Thread 2 is in the critical section");
            
            favouredThread = 1;
            thread2WantsToEnter = false;
            
            // Remainder Section
        } while (!completed);
    }
}
```
```C
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>
#include <stdbool.h>
#include <sched.h>

volatile int favouredThread = 1;
volatile bool thread1WantsToEnter = false;
volatile bool thread2WantsToEnter = false;
volatile bool completed = false;

void* Thread1(void* arg) {
    do {
        thread1WantsToEnter = true;
        while (thread2WantsToEnter) {
            if (favouredThread == 2) {
                thread1WantsToEnter = false;
                while (favouredThread == 2) {
                    sched_yield(); // Wait until it's our turn
                }
                thread1WantsToEnter = true;
            }
        }

        // Critical Section
        printf("Thread 1 is in the critical section\n");
        fflush(stdout);

        favouredThread = 2;
        thread1WantsToEnter = false;

        // Remainder Section
        usleep(100000); // 100ms delay
    } while (!completed);
    return NULL;
}

void* Thread2(void* arg) {
    do {
        thread2WantsToEnter = true;
        while (thread1WantsToEnter) {
            if (favouredThread == 1) {
                thread2WantsToEnter = false;
                while (favouredThread == 1) {
                    sched_yield(); // Wait until it's our turn
                }
                thread2WantsToEnter = true;
            }
        }

        // Critical Section
        printf("Thread 2 is in the critical section\n");
        fflush(stdout);

        favouredThread = 1;
        thread2WantsToEnter = false;

        // Remainder Section
        usleep(100000); // 100ms delay
    } while (!completed);
    return NULL;
}

int main() {
    pthread_t t1, t2;

    pthread_create(&t1, NULL, Thread1, NULL);
    pthread_create(&t2, NULL, Thread2, NULL);

    sleep(5); // Run for 5 seconds
    completed = true;

    pthread_join(t1, NULL);
    pthread_join(t2, NULL);

    return 0;
}
```
```Cpp
#include <iostream>
#include <thread>
#include <atomic>
#include <chrono>

std::atomic<int> favouredThread(1);
std::atomic<bool> thread1WantsToEnter(false);
std::atomic<bool> thread2WantsToEnter(false);
std::atomic<bool> completed(false);

void Thread1() {
    do {
        thread1WantsToEnter = true;
        while (thread2WantsToEnter) {
            if (favouredThread == 2) {
                thread1WantsToEnter = false;
                while (favouredThread == 2) {
                    std::this_thread::yield(); // Wait until it's our turn
                }
                thread1WantsToEnter = true;
            }
        }

        // Critical Section
        std::cout << "Thread 1 is in the critical section\n";

        favouredThread = 2;
        thread1WantsToEnter = false;

        // Remainder Section
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    } while (!completed);
}

void Thread2() {
    do {
        thread2WantsToEnter = true;
        while (thread1WantsToEnter) {
            if (favouredThread == 1) {
                thread2WantsToEnter = false;
                while (favouredThread == 1) {
                    std::this_thread::yield(); // Wait until it's our turn
                }
                thread2WantsToEnter = true;
            }
        }

        // Critical Section
        std::cout << "Thread 2 is in the critical section\n";

        favouredThread = 1;
        thread2WantsToEnter = false;

        // Remainder Section
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    } while (!completed);
}

int main() {
    std::thread t1(Thread1);
    std::thread t2(Thread2);

    std::this_thread::sleep_for(std::chrono::seconds(5));
    completed = true;

    t1.join();
    t2.join();

    return 0;
}
```
```Python
import threading
import time

favoured_thread = 1
thread1_wants_to_enter = False
thread2_wants_to_enter = False
completed = False

def thread1():
    global favoured_thread, thread1_wants_to_enter, thread2_wants_to_enter, completed
    while not completed:
        thread1_wants_to_enter = True
        while thread2_wants_to_enter:
            if favoured_thread == 2:
                thread1_wants_to_enter = False
                while favoured_thread == 2:
                    time.sleep(0.001)  # Wait until it's our turn
                thread1_wants_to_enter = True
        
        # Critical Section
        print("Thread 1 is in the critical section")
        
        favoured_thread = 2
        thread1_wants_to_enter = False
        
        # Remainder Section
        time.sleep(0.1)

def thread2():
    global favoured_thread, thread1_wants_to_enter, thread2_wants_to_enter, completed
    while not completed:
        thread2_wants_to_enter = True
        while thread1_wants_to_enter:
            if favoured_thread == 1:
                thread2_wants_to_enter = False
                while favoured_thread == 1:
                    time.sleep(0.001)  # Wait until it's our turn
                thread2_wants_to_enter = True
        
        # Critical Section
        print("Thread 2 is in the critical section")
        
        favoured_thread = 1
        thread2_wants_to_enter = False
        
        # Remainder Section
        time.sleep(0.1)

if __name__ == "__main__":
    t1 = threading.Thread(target=thread1)
    t2 = threading.Thread(target=thread2)
    
    t1.start()
    t2.start()
    
    time.sleep(5)
    completed = True
    
    t1.join()
    t2.join()
```
```JavaScript
const { Worker, isMainThread, workerData } = require('worker_threads');

if (isMainThread) {
    // Allocate 16 bytes for 4 Shared 32-bit Integers
    const sab = new SharedArrayBuffer(16);
    const sharedArray = new Int32Array(sab);
    
    // Initializing state
    sharedArray[0] = 1; // favouredThread = 1
    sharedArray[1] = 0; // thread1WantsToEnter = false
    sharedArray[2] = 0; // thread2WantsToEnter = false
    sharedArray[3] = 0; // completed = false

    const w1 = new Worker(__filename, { workerData: { id: 1, sab } });
    const w2 = new Worker(__filename, { workerData: { id: 2, sab } });

    setTimeout(() => {
        Atomics.store(sharedArray, 3, 1); // Set completed to true after 5s
    }, 5000);

} else {
    const { id, sab } = workerData;
    const sharedArray = new Int32Array(sab);

    const getFavoured = () => Atomics.load(sharedArray, 0);
    const setFavoured = (val) => Atomics.store(sharedArray, 0, val);
    
    const wantsToEnter = (threadId) => Atomics.load(sharedArray, threadId);
    const setWantsToEnter = (threadId, val) => Atomics.store(sharedArray, threadId, val);
    
    const isCompleted = () => Atomics.load(sharedArray, 3) === 1;

    const myId = id;              // 1 or 2
    const otherId = id === 1 ? 2 : 1;

    while (!isCompleted()) {
        setWantsToEnter(myId, 1);
        
        while (wantsToEnter(otherId) === 1) {
            if (getFavoured() === otherId) {
                setWantsToEnter(myId, 0);
                while (getFavoured() === otherId) {
                    // Busy-wait loop
                }
                setWantsToEnter(myId, 1);
            }
        }

        // Critical Section
        console.log(`Thread ${myId} is in the critical section`);

        setFavoured(otherId);
        setWantsToEnter(myId, 0);

        // Remainder Section
        const start = Date.now();
        while (Date.now() - start < 100) {} // Wait 100ms
    }
}
```

---

## Summary of Versions

| Version | Mechanism | Problem / Limitation |
| --- | --- | --- |
| **1. Turn variable only** | Strict alternation | No progress if one process exits permanently |
| **2. Flags (after entry)** | Mutual exclusion attempt | Both may enter simultaneously (violates Mutual Exclusion) |
| **3. Flags (before entry)** | Pre-state declaration | Deadlock possible |
| **4. Flags + random backoff** | Politeness backoff | Starvation / Livelock (indefinite postponement) |
| **5. Final Dekker’s Algorithm** | Flags + turn variable | **Correct solution** (ensures Mutual Exclusion, Progress, and Bounded Waiting) |




