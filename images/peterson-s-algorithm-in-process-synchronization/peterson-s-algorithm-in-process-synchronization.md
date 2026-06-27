# Peterson's Algorithm in Process Synchronization

Peterson's Algorithm is a classic **software-based solution** to the **critical section problem** in operating systems. It ensures **mutual exclusion** between **two processes**, allowing only one process to access the shared resource at a time and preventing race conditions.

It is one of the earliest synchronization algorithms and is mainly used for educational purposes to understand the concepts of process synchronization.

## Shared Variables Used

Peterson's Algorithm uses two shared variables:

- **flag[i]** – Indicates whether process *i* wants to enter the critical section.
- **turn** – Indicates whose turn it is to enter the critical section if both processes request access simultaneously.

## Peterson's Algorithm

### Process P&lt;sub&gt;i&lt;/sub&gt;

```text
do {
    flag[i] = true;          // Pi wants to enter
    turn = j;                // Give priority to Pj

    while(flag[j] && turn == j);

    // Critical Section

    flag[i] = false;

    // Remainder Section

} while(true);
```

### Process P&lt;sub&gt;j&lt;/sub&gt;

```text
do {
    flag[j] = true;          // Pj wants to enter
    turn = i;                // Give priority to Pi

    while(flag[i] && turn == i);

    // Critical Section

    flag[j] = false;

    // Remainder Section

} while(true);
```

## Step-by-Step Working

### 1. Intent to Enter

A process first sets its corresponding **flag** to **true**, indicating that it wants to enter the critical section.

### 2. Turn Assignment

The process assigns the **turn** variable to the other process.

If both processes request the critical section simultaneously, the **turn** variable decides which process gets priority.

### 3. Waiting Condition

A process waits only when:

- The other process also wants to enter the critical section.
- It is the other process's turn.

Otherwise, it immediately enters the critical section.

### 4. Critical Section

The selected process enters the critical section and accesses the shared resource.

Since only one process can satisfy the waiting condition, mutual exclusion is maintained.

### 5. Exit Section

After completing its work, the process sets its flag to **false**, allowing the waiting process to enter the critical section.

## Properties Guaranteed by Peterson's Algorithm

- **Mutual Exclusion:** Only one process enters the critical section at a time.
- **Progress:** If no process is inside the critical section, one of the waiting processes will eventually enter.
- **Bounded Waiting:** Every waiting process gets a chance to execute after a finite number of attempts.

## Example Use Cases

Although Peterson's Algorithm is rarely used in modern operating systems, it can theoretically be applied in:

- Accessing a shared printer.
- Reading or writing a shared file.
- Updating a shared variable.
- Accessing a shared database record.
- Controlling access to a shared hardware device.

**Note:** Modern operating systems generally use hardware-supported synchronization techniques such as mutexes, semaphores, monitors, or atomic instructions instead of Peterson's Algorithm.

# Peterson's Algorithm Programs

```javascript
let flag = [false, false];
let turn = 0;

async function process(id) {

    let other = 1 - id;

    for (let i = 0; i < 5; i++) {

        // Entry Section
        flag[id] = true;
        turn = other;

        while (flag[other] && turn === other) {
            await new Promise(resolve => setTimeout(resolve, 1));
        }

        // Critical Section
        console.log(
            `AlphaKnowledge: Process ${id} entered Critical Section`
        );

        // Exit Section
        flag[id] = false;

        // Remainder Section
        console.log(
            `Process ${id} entered Remainder Section`
        );
    }
}

(async () => {
    process(0);
    process(1);
})();
```
```c
#include <stdio.h>
#include <pthread.h>
#include <stdbool.h>

bool flag[2] = {false, false};
int turn;

void* process(void *arg)
{
    int id = *(int*)arg;
    int other = 1 - id;

    for(int i = 0; i < 5; i++)
    {
        // Entry Section
        flag[id] = true;
        turn = other;

        while(flag[other] && turn == other);

        // Critical Section
        printf("AlphaKnowledge: Process %d entered Critical Section\n", id);

        // Exit Section
        flag[id] = false;

        // Remainder Section
        printf("Process %d entered Remainder Section\n", id);
    }

    return NULL;
}

int main()
{
    pthread_t t1, t2;
    int p0 = 0, p1 = 1;

    pthread_create(&t1, NULL, process, &p0);
    pthread_create(&t2, NULL, process, &p1);

    pthread_join(t1, NULL);
    pthread_join(t2, NULL);

    return 0;
}
```
```cpp
#include <iostream>
#include <thread>
#include <atomic>

std::atomic<bool> flag[2];
std::atomic<int> turn;

void process(int id)
{
    int other = 1 - id;

    for(int i = 0; i < 5; i++)
    {
        // Entry Section
        flag[id] = true;
        turn = other;

        while(flag[other] && turn == other);

        // Critical Section
        std::cout << "AlphaKnowledge: Process "
                  << id
                  << " entered Critical Section\n";

        // Exit Section
        flag[id] = false;

        // Remainder Section
        std::cout << "Process "
                  << id
                  << " entered Remainder Section\n";
    }
}

int main()
{
    flag[0] = false;
    flag[1] = false;
    turn = 0;

    std::thread t1(process,0);
    std::thread t2(process,1);

    t1.join();
    t2.join();

    return 0;
}
```
```java
class Peterson {

    static volatile boolean[] flag = new boolean[2];
    static volatile int turn;

    static class Process extends Thread {

        int id;

        Process(int id) {
            this.id = id;
        }

        public void run() {

            int other = 1 - id;

            for(int i = 0; i < 5; i++) {

                // Entry Section
                flag[id] = true;
                turn = other;

                while(flag[other] && turn == other);

                // Critical Section
                System.out.println(
                    "AlphaKnowledge: Process " + id +
                    " entered Critical Section");

                // Exit Section
                flag[id] = false;

                // Remainder Section
                System.out.println(
                    "Process " + id +
                    " entered Remainder Section");
            }
        }
    }

    public static void main(String[] args) {

        flag[0] = false;
        flag[1] = false;
        turn = 0;

        Process p0 = new Process(0);
        Process p1 = new Process(1);

        p0.start();
        p1.start();
    }
}
```
```python
import threading

flag = [False, False]
turn = 0

def process(pid):
    global turn

    other = 1 - pid

    for _ in range(5):

        # Entry Section
        flag[pid] = True
        turn = other

        while flag[other] and turn == other:
            pass

        # Critical Section
        print(f"AlphaKnowledge: Process {pid} entered Critical Section")

        # Exit Section
        flag[pid] = False

        # Remainder Section
        print(f"Process {pid} entered Remainder Section")

t1 = threading.Thread(target=process, args=(0,))
t2 = threading.Thread(target=process, args=(1,))

t1.start()
t2.start()

t1.join()
t2.join()
```

### Output
Process 0 entered Critical Section

Process 0 entered Remainder Section

Process 1 entered Critical Section

Process 1 entered Remainder Section

...

## Explanation of the Programs

- `flag[id] = true` indicates that the process wants to enter the critical section.
- `turn = other` gives priority to the other process when both request access simultaneously.
- The `while` loop makes the process wait if the other process also wants to enter and it is the other process's turn.
- Only one process enters the critical section at a time, ensuring mutual exclusion.
- After completing its work, the process resets its flag to **false**, allowing the waiting process to enter.
- The same synchronization logic is demonstrated in **C, C++, Java, Python, and JavaScript**.

## Advantages

- Simple and easy to understand.
- Guarantees mutual exclusion.
- Prevents race conditions.
- Ensures progress.
- Prevents indefinite waiting (bounded waiting).
- Does not require special hardware instructions.

## Limitations

- Works only for **two processes**.
- Uses busy waiting, which wastes CPU time.
- Not suitable for modern multicore processors.
- Rarely used in real operating systems because hardware-supported synchronization techniques are more efficient.

## Summary

Peterson's Algorithm is a software-based synchronization algorithm that solves the critical section problem for two processes using two shared variables, **flag** and **turn**. It guarantees mutual exclusion, progress, and bounded waiting without requiring hardware support. Although modern operating systems rely on mutexes, semaphores, monitors, and atomic instructions, Peterson's Algorithm remains an important concept for understanding the fundamentals of process synchronization.




