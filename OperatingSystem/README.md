## Instruction cycle

Instruction cycle (also called fetch–decode–execute cycle, or fetch-execute cycle) 

Three main stages: fetch, decode, and execute

1. Copied the address in PC to MAR
2. PC "point" to the memory address of the next instruction to be executed. 
3. Copied instruction at the memory address described by the MAR to MDR(or call MBR)
4. CU decode instruction to IR
5. Execute

Reference: https://en.wikipedia.org/wiki/Instruction_cycle 

## Program Counter (PC)

sometimes called instruction pointer(IP) or instruction address register(IAR)

PC hold the memory address of the next instruction

## Instruction register (IR)

IR holds the instruction currently being executed or decoded

Fetched instruction load into Instruction Register 

## Accumulator (AC)

Intermediate arithmetic and logic results are stored

Execution result stored in Accumulator temporarily 

## Program Status Word (PSW)

contains execution status information

performs the function of a status register and program counter

## Interrupt

1. Running User program
2. Interrupt
3. Store all information to control stack
4. Store user program address to stack pointer
5. PC point to interrupt service program
6. Run interrupt service program
7. Interrupt service program run finish
8. Resume all information in control stack
9. PC point to stack pointer(user program before)

## Spatial Locality

If a particular storage location is referenced at a particular time, then it is likely that nearby memory locations will be referenced in the near future.

## Temporal Locality

If at one point a particular memory location is referenced, then it is likely that the same location will be referenced again in the near future

## Direct memory access (DMA)

Allows hardware subsystems to access main system memory independent of CPU

Without DMA, when the CPU is using programmed input/output, it is typically fully occupied for the entire duration of the read or write operation, and is thus unavailable to perform other work. 

With DMA, the CPU first initiates the transfer, then it does other operations while the transfer is in progress, and it finally receives an interrupt from the DMA controller (DMAC) when the operation is done

## Process
Instance of program running

Execution of a sequence of instructions, state, and associated set of system resource

Much more than just running program

## Process Element
- Program (code) (which may shared with other process that executing same program)
- Data (even running same program, but may different set of user data)
- Context (contain all information OS need to manage process)

## Process Management requirement of OS
- Interleave execution of multiple processes
- Allocate resources to processes and protect 
- Share and exchange information between processes
- Synchronization among processes

## Interleave execution of processes
Dispatcher is one of function of Operating system

Dispatcher switch processor from one process to other

Dispatcher generate Clock interrupts (also called timeout), and switch processor

All in memory

## Create Process in UNIX
Parent process can create child process by system call - fork()

After create child process, all following routine are possible

- Stay in parent process
- Transfer control to child process
- Transfer control to another process

fork() will return pid,  if pid equal 0, this is child process

Example:
```cpp
#include <iostream>
#include <unistd.h>

using namespace std;

int main(){
    int pid = fork();
    cout << "(1)" << endl;
    if(pid == 0){
        cout << "(2)" << endl;
    }
    cout << "(3)"  << endl; 
}
```
`(1)` and `(3)`  execute both child and parent, only child process execute `(2)`

Variable value between child and parent process will not share 

State and value of variable will copy when process create

## Other
Application corresponds to one or more process

You can download Process Explorer to find more information of process

## Two-State Process Model
- Running (Pause to Not Running state)
- Not Running (Dispatch to Running state)

Process not running will keep on Queue, store all waiting process

Waiting for dispatcher to dispatch first process to processor for execution

After timeout then go back to the end of the queue

## Five-State Process Model
Not Running state can divide to Ready and Blocked (my be waiting for I/O operation)
- New (Admit to Ready)
- Ready (Dispatch to Running)
- Running (Timeout to Ready, Event wait to Blocked, Release to Exit)
- Blocked (Event occurs to Ready)
- Exit

Use Two Queues, Ready Queue and Blocked Queue

Ready Queue store process that ready for execution

Blocked Queue store blocked process that waiting for event occur

There could be many different events, it not efficient if simply put all the blocked process into singe queue

Better way is Multiple Blocked Queue for each type of event

When event occur, we can simply dequeue the first process

## Suspended Processes
If all processes in main memory waiting for I/O operation, then processor becomes idle

To solve this problem, swap blocked process out to disk

So that memory space can release for new process

Blocked state become Suspend state when process swapped to disk

- Blocked (suspend to Suspend State)
- Suspend (Activate to Ready)

But One Process is no enough, we need to distinguish some suspend state already occur event and ready for execution

Other the other hand, release memory is reason of swap process , not only blocked process swap, Running Process may require to suspend

So we divide to Block/Suspend and Ready/Suspend State

## Two Suspend States

Two addition state of Five State Model

- Blocked/Suspend (Event occurs to Ready/Suspend)
- Ready/Suspend (Activate to Ready)

 There are total Seven State:

- New (Admit to Ready, Admit to Ready/Suspend)
- Ready (Dispatch to Running, Suspend to Ready/Suspend)
- Running (Timeout to Ready, Event wait to Blocked, Suspend to Ready/Suspend, Release to Exit)
- Blocked (Event occurs to Ready, Suspend to Blocked/Suspend)
- Blocked/Suspend (Event occurs to Ready/Suspend, Activate to Blocked)
- Ready/Suspend (Activate to Ready)
- Exit

## Reason of Process Suspend 

- Swap (Release main memory to bring in new process)
- Interactive User Request (User suspend for debugging)
- Timing (Execute periodically)
- Parent Process Request

## OS Control Table

- Memory Tables
- I/O Tables
- File Tables
- Primary Process Table (and it point to Process Image)

A lot of information need to store about each process, so we require another data structure called Process Image

## Memory Table

