# CPU Fundamentals: Context Switching, Cores, Threads, Parallelism vs Concurrency

This README contains notes on essential CPU concepts — great for interviews and deep understanding of how programs run on hardware.

---

## 1. What is a CPU Core?

A **CPU core** is like a mini processor within the main CPU. Each core can handle **one task at a time**.

- **Single-core CPU** → Only one task at a time.
- **Multi-core CPU** → Multiple tasks can run **in parallel**.
- Modern CPUs usually have 2, 4, 6, or more cores.

Analogy:  
CPU = kitchen  
Core = chef  
More chefs → more dishes can be cooked simultaneously.

---

## 2. What is a Thread?

A **thread** is the smallest unit of execution inside a process.

- One process can have **multiple threads** doing different parts of a task.
- Threads in a program share memory but run independently.

Analogy:  
Process = full restaurant order  
Thread = each dish being prepared in parallel

---

## 3. What is Context Switching?

Context switching is when the CPU switches from one **thread/process** to another.

- It saves the current task’s state and loads the next.
- Happens super fast (thousands of times per second).
- Essential for multitasking on single-core CPUs.

Analogy:  
One chef (CPU) cooking different dishes (threads) by rapidly switching between them.

---

## 4. What is Hyper-Threading?

- Technology that allows **1 core to handle 2 threads**.
- Threads **share** the same physical core resources.
- Gives **pseudo-parallelism**, not as fast as true cores.

Example:  
A 4-core CPU with hyper-threading can handle **8 threads** (4 cores × 2 threads).

---

## 5. Concurrency vs Parallelism

| Feature         | Concurrency                             | Parallelism                            |
|----------------|------------------------------------------|----------------------------------------|
| Execution Style | Interleaved (one at a time)             | Simultaneous (true parallel)           |
| Requires        | Single or multi-core                    | Multi-core                             |
| Goal            | Responsiveness                          | Speed, performance                     |
| Analogy         | One chef switching between tasks        | Multiple chefs each doing one task     |
| Code Example    | Chat app switching users                | Video rendering using all cores        |

Key Quote:
> All parallel programs are concurrent,  
> but not all concurrent programs are parallel.

---

## 6. Example: Game Loading

When you launch a game:
- Main process starts
- Threads created:
  - Thread A → Graphics
  - Thread B → Sound
  - Thread C → Input
- On single-core CPU → context switch handles all
- On multi-core CPU → threads run in parallel → smoother gameplay

---

## Summary Points

- **Core** = physical unit of computation.
- **Thread** = unit of work inside a process.
- **Context Switching** = switching between tasks (enabled by OS).
- **Concurrency** = managing many tasks at once (not truly parallel).
- **Parallelism** = running multiple tasks at the exact same time.

