# 1 - The Big Picture

## 1.1 - Layers of Abstraction in a Linux System
* System organization - 3 Layers
    * Hardware layer - CPU, RAM, disks, network ports
    * Kernel layer - system calls, process management, memory management, device drivers
    * User layer - GUI, server, shell, etc
* Kernel mode - unrestricted access to the processor and main memory (kernel space)
* User mode - restricts access to subset of memory and safe CPU operations (user space)

## 1.2 - Hardware
* Main memory - storage area for running processes

## 1.3.1 - Kernel: Processes
* Processes - kernel decides which can use the CPU
    * Process management - starting, pausing, resuming, scheduling, and terminating processes
    * Context switch - act of one process ceding control of the CPU to another process
        1. CPU interrupts current process and switches into Kernel mode
        2. Kernel records current state of the CPU and memory
        3. Kernel performs any tasks that might have come up during preceding time slice (such as IO ops)
        4. Kernel analyzes list of waiting processes and chooses one
        5. Kernel prepares memory and CPU
        6. Kernel tells CPU how long the next time slice will last
        7. Kernel switches CPU into user mode and hands control of CPU to the process
    * Time slice - time between context switches

## 1.3.2 - Kernel: Memory
* Memory - kernel keeps track of all memory, including what is allocated to a process, what might be shared between processes, and what is free
* Kernel memory management:
    * Kernel must have its own private area of memory
    * Each user process needs its own area of memory
    * One user process cannot access the private memory of another process
    * user processes can share memory
    * some memory in user processes can be read only
    * system can use more memory than is physically present by using disk space as auxiliary
* Memory management unit (MMU) - enables virtual memory
* Virtual memory - when the process accesses some memory, the MMU intercepts the access and uses a memory address map to translate the address from virtual to physical memory.
    * Kernel swaps the memory maps used by the MMU during context switch
* Page table - implementation of a memory address map

## 1.3.3 - Kernel: Device Drivers
* Device drivers - kernel acts as an interface between hardware and processes, its usually the kernel's job to operate the hardware
    * devices are typically only accessible in kernel mode
    * device drivers are traditionally part of the kernel to try and present a uniform interface to user processes

## 1.3.4 - Kernel: System Calls and Support
* System calls and support - processes use system calls to communicate with the kernel
* `fork()` - kernel creates a nearly identical copy of process
    * other than init all user processes on a Linux system start as a result of `fork()`
* `exec(<program>)` - kernel loads and starts `program`, replacing the current process
    * Entering `ls` into CLI:
        1. shell calls `fork()`
        2. new shell calls `exec(ls)`

## 1.4 - User Space

## 1.5 - Users
* User - entity that can run processes and own files
    * exist to support permissions and boundaries
    * every user space process has a user owner
    * a user can terminate or modify the behavior of its own processes, but it cannot do so to other users' processes
* `root` user - may terminate and alter another user's processes and acess any file on the local system.
* Groups - sets of users
