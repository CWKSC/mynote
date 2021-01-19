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

___

1. User program ing
2. Interrupt
3. Store all information to control stack
4. Store user program address to stack pointer
5. PC point to interrupt service program
6. Run interrupt service program
7. Interrupt service program run finish
8. Resume all information in control stack
9. PC point to stack pointer(user program before)

Spatial Locality, Temporal Locality