# Operating System Interview Questions

1. What is the main purpose of an Operating System? Discuss different types.
- **Purpose:** Acts as an intermediary between the user/applications and computer hardware, managing hardware resources and providing a platform for software execution.
- **Types:** Batch OS, Time-Sharing OS, Distributed OS, Network OS, Real-Time OS (RTOS), and Mobile OS.

2. What is a socket, kernel, and monolithic kernel?
- **Socket:** An endpoint for communication between two machines over a network (combination of IP address and port).
- **Kernel:** The core central component of an operating system that manages system resources and hardware-software communication.
- **Monolithic Kernel:** An architecture where all OS services (file system, CPU scheduling, memory management) run in kernel space for high performance.

3. What is the difference between a process, program, and thread?
- **Program:** A passive set of instructions stored on disk (executable file).
- **Process:** An active, executing instance of a program with its own memory space and resources.
- **Thread:** The smallest unit of execution within a process; multiple threads share the same process memory.

4. What are the different types of processes?
- **Independent Process:** Execution does not affect or get affected by other processes.
- **Cooperating Process:** Can affect or be affected by other processes, requiring Inter-Process Communication (IPC).
- **Foreground / Background Process:** User-interactive vs. background system tasks.
- **CPU-bound / I/O-bound Process:** Spends more time computing vs. waiting for I/O operations.

5. Define virtual memory, thrashing, and threads.
- **Virtual Memory:** A memory management technique that gives an application the illusion of having a large, contiguous block of main memory by mapping it to secondary storage (disk space).
- **Thrashing:** A condition where the system spends more time paging (swapping pages in and out of memory) than executing actual application instructions, drastically slowing down performance.
- **Thread:** A lightweight sub-process that shares the parent process's resources to execute tasks concurrently.

6. What is RAID? Explain its different types.
RAID (Redundant Array of Independent Disks) is a technology that combines multiple physical hard disks/SSDs into one logical storage system.
- RAID 0 → Speed (Striping without redundancy)
- RAID 1 → Safety (Mirroring)
- RAID 5 → Speed + Safety (Striping with distributed parity, 1 disk failure)
- RAID 6 → More Safety (Dual distributed parity, 2 disk failures)
- RAID 10 → Speed + Safety (Combination of striping and mirroring)

7. What is a deadlock? What are the different conditions required to achieve a deadlock?
A deadlock is a situation in an Operating System where two or more processes are waiting for each other to release resources, so none of them can continue execution.
- M → Mutual Exclusion
- H → Hold and Wait
- N → No Preemption
- C → Circular Wait

8. What is fragmentation? Explain its types.
- **Fragmentation:** Inefficiency in memory allocation where free memory space is broken into small, non-contiguous pieces.
- **Internal Fragmentation:** Allocated memory blocks are slightly larger than requested memory, leaving unused space *inside* the block.
- **External Fragmentation:** Total free memory is enough to satisfy a request, but it is not contiguous, so it cannot be allocated.

9. What is spooling?
- **Spooling (Simultaneous Peripheral Operations On-Line):** A buffering technique where data is held in temporary storage (disk or memory buffer) so slower peripheral devices (like printers) can access data at their own pace without holding up the CPU.

10. What is a semaphore and mutex? What are the differences between them?
- **Semaphore:** A signaling mechanism using an integer variable to control access to multiple resources (can be binary or counting).
- **Mutex:** A locking mechanism used to ensure mutual exclusion, allowing only one thread to access a critical section at a time (owned by the thread that locks it).
- **Difference:** A mutex has ownership and can only be released by the thread that locked it, whereas a semaphore is a signaling flag that can be signaled/released by any thread.

11. What is a binary semaphore?
- A semaphore whose integer value can only range between 0 and 1, functioning similarly to a mutex (though it lacks ownership restrictions).

12. Explain Belady’s Anomaly.
- A phenomenon in page replacement algorithms (like FIFO) where increasing the number of allocated page frames results in an **increase** in the number of page faults rather than a decrease.

13. What are starvation and aging in an Operating System?
- **Starvation:** A resource management problem where a low-priority process is indefinitely delayed because higher-priority processes keep taking the resources.
- **Aging:** A technique used to prevent starvation by gradually increasing the priority of waiting processes over time so they eventually get executed.

14. Why does thrashing occur?
- It occurs when the degree of multiprogramming is too high and the system lacks sufficient physical memory to hold the working sets of all active processes, causing excessive page-faulting.

15. What is paging and why do we need it?
- **Paging:** A memory management scheme that eliminates the need for contiguous physical memory allocation by dividing physical memory into fixed-size blocks called frames and logical memory into pages.
- **Need:** Eliminates external fragmentation and simplifies memory allocation.

16. Explain demand paging.
- A virtual memory management strategy where pages are only loaded into physical memory from secondary storage when they are actually referenced during execution (lazy loading).

17. Explain segmentation.
- A memory management scheme that supports the user's view of memory by dividing programs into variable-sized logical modules (like functions, arrays, stack, code) called segments.

18. What is a Real-Time Operating System (RTOS)? Explain its types.
- **RTOS:** An operating system designed to process data and events with strict, predictable time constraints (deadlines).
- **Types:** Hard RTOS (missing a deadline can cause total system failure) and Soft RTOS (missing a deadline degrades performance but doesn't cause catastrophic failure).

19. What is the difference between main memory and secondary memory?
- **Main Memory (RAM):** Volatile, faster, directly accessible by the CPU, smaller capacity.
- **Secondary Memory (HDD/SSD):** Non-volatile, slower, not directly accessed by the CPU, large storage capacity.

20. What is dynamic binding?
- A mechanism where function calls or data references are resolved at run-time rather than compile-time.

21. Explain FCFS (First Come First Serve) Scheduling.
- A non-preemptive CPU scheduling algorithm where processes are executed in the exact order they arrive in the ready queue.

22. Explain SJF (Shortest Job First) Scheduling.
- A scheduling algorithm that selects the waiting process with the smallest execution/burst time next (can be preemptive or non-preemptive).

23. Explain SRTF (Shortest Remaining Time First) Scheduling.
- The preemptive version of SJF, where the CPU is allocated to the process with the shortest remaining burst time, interrupting the current process if a shorter one arrives.

24. Explain LRTF (Longest Remaining Time First) Scheduling.
- The preemptive version of Longest Job First, where the process with the maximum remaining execution time is scheduled first.

25. Explain Priority Scheduling.
- A scheduling algorithm where each process is assigned a priority, and the CPU is allocated to the process with the highest priority (preemptive or non-preemptive).

26. Explain Round Robin Scheduling.
- A preemptive scheduling algorithm where each process is assigned a fixed time slice (quantum) in a cyclic order, ensuring fair CPU distribution.

27. Explain the Producer-Consumer Problem.
- A classic synchronization problem where two processes (Producer generating data and Consumer consuming data) share a fixed-size buffer, requiring synchronization to prevent race conditions (buffer overflow/underflow).

28. Explain Banker’s Algorithm.
- A deadlock avoidance and resource allocation algorithm that tests for safety by simulating the allocation of predetermined maximum possible amounts of all resources, checking for a safe state before deciding whether allocation can proceed.

29. What is Cache?
- A small, extremely fast volatile computer memory that sits close to the CPU, storing frequently used data and instructions to reduce access latency from main memory.

30. What is the difference between direct mapping and associative mapping?
- **Direct Mapping:** Each block of main memory maps to exactly one specific cache line slot, simple to implement but prone to high conflict misses.
- **Associative Mapping:** Any main memory block can be placed into any available cache line, eliminating conflict misses but requiring complex and costly hardware search logic.

31. What is the difference between multitasking and multiprocessing?
- **Multitasking:** Rapid switching of a single CPU core among multiple tasks/processes to give the illusion of simultaneous execution (Time-sharing).
- **Multiprocessing:** The use of two or more physical CPU cores within a single computer system to execute multiple processes simultaneously in parallel.
