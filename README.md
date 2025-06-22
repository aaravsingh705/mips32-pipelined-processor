# MIPS-32 Pipelined Processor (Verilog)

This repository contains the Verilog implementation of a 5-stage pipelined MIPS-32 processor. It includes support for basic R-type, I-type, memory, and branch instructions. A testbench is provided to demonstrate functionality by computing the factorial of 7 using a loop and storing the result in memory.

Features

- 5-stage pipeline: **IF → ID → EX → MEM → WB**
- Instruction set includes:
  - Arithmetic (ADD, SUB, MUL, ADDI, SUBI)
  - Logical (AND, OR, SLT)
  - Memory operations (LW, SW)
  - Branches (BEQZ, BNEQZ)
  - HALT instruction
- Data forwarding and basic branch handling
- Fully synthesizable Verilog code

Testbench: `test_mips32.v`

 Example :Simulates the factorial of 7 using this instruction sequence:

```assembly
ADDI R10, R0, 200   ; R10 = 200 (memory address)
ADDI R2, R0, 1      ; R2 = 1 (accumulator)
LW   R3, 0(R10)     ; R3 = Mem[200] = 7
Loop:
MUL  R2, R2, R3     ; R2 *= R3
SUBI R3, R3, 1      ; R3 -= 1
BNEQZ R3, Loop      ; Repeat until R3 == 0
SW   R2, -2(R10)    ; Store result in Mem[198]
HLT                 ; Halt processor
