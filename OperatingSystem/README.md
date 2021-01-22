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

1. User program ing
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