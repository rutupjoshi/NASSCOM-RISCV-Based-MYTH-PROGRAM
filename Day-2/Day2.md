# DAY - 2: Application binary Interface, Risc v registers, asm with c language

On the second day we learn about the ABI concepts ,the risc V registers ,its features and the each abi usage for each registers.

---

## Contents

- [Application Binary Interface](#application-binary-interface)
- [RISC V Registers](#risc-v-registers)
- [New Algorithm Sum 1 to N](#new-algorithm-sum-1-to-n)
  - [Lab 1](#lab-1)
  
---

## Application Binary Interface

An Application Binary Interface (ABI) is a low-level contract that defines how compiled application binary files interact with each other, with operating systems, or with hardware at the machine-code level.

The RISC-V Application Binary Interface (ABI), often documented as the RISC-V psABI (Processor-Specific ABI), provides the machine-level specifications necessary to link compiled code together, ensuring that different libraries, compilers, and operating systems can seamlessly interact on RISC-V hardware.

 Data Models
RISC-V defines specific base data models based on whether the architecture is 32-bit (RV32) or 64-bit (RV64). The letters represent the widths of integers, long integers, and pointers:
• ILP32: Used for 32-bit systems (RV32). int, long, and pointers are all 32 bits wide.
• LP64: Used for 64-bit systems (RV64). int remains 32 bits, while long and pointers are 64 bits wide.
Suffixes are appended to these names to denote hardware floating-point capabilities:
• Empty (e.g., lp64): Soft-float (floating-point arguments passed in integer registers).
• f (e.g., lp64f): Single-precision hardware float support.
• d (e.g., lp64d): Double-precision hardware float support (this is the default standard for desktop/server systems like RV64G).

**Memory Allocation**

Frame Pointer (s0 / fp)
• Using a frame pointer (s0) is optional in standard RISC-V code.
• If a function uses a frame pointer to anchor local variables or variable-length stack allocations (alloca), s0 is saved in the prologue, and sp is copied into s0. Like other s registers, s0 is callee-saved.

• Register Arguments: The first 8 integer/pointer arguments are passed in registers a0 through a7.
• Spilling to Stack: If a function receives more than 8 arguments (or large composite structures that do not fit in registers), the extra arguments are "spilled" onto the caller-allocated or callee-allocated stack frame.
• Return Values: Functions return data using a0 and a1 (for integer types) or fa0 and fa1 (for floating-point types). Larger aggregate return values are written to a memory location pointed to by an implicit pointer passed into the function.

• Downward Growth: The stack grows downward from higher memory addresses toward lower memory addresses.
• Stack Pointer (sp or x2): The stack pointer points to the current bottom-most valid address of the stack frame. To allocate space on the stack upon entering a function, you subtract the frame size from sp (e.g., addi sp, sp, -32).
• 16-Byte Alignment: The stack pointer (sp) must always be kept 16-byte aligned at all times throughout procedure execution.

# Positive 64-Bit Number

The lecture explains:

If the MSB is 0, the number is positive.

Therefore:

MSB determines sign in signed number representation

Memory allocation can be visually represented below:

<img width="1257" height="735" alt="memory allocatipon abi" src="https://github.com/user-attachments/assets/36905821-3bad-4117-827d-a12bcd32be95" />
The abi can have usage in registers of risc v this way.The RISC-V 32-integer register file assigns specific ABI names and responsibilities:

<img width="1180" height="701" alt="abi registers 12 names" src="https://github.com/user-attachments/assets/cd1b88e4-4991-4263-93e3-20f09c6b72c2" />
**Instructions of ABI :**

RISC-V uses separate instructions for arithmetic operations like addition and for moving data between memory and registers via a load-store architecture.
Some are,
**Addition Instructions:**

RISC-V provides register-to-register addition and register-to-immediate addition:
• add rd, rs1, rs2
	• Operation: Adds the values in source registers rs1 and rs2, then stores the result in destination register rd (rd = rs1 + rs2).
• addi rd, rs1, imm
	• Operation: Adds the value in source register rs1 to a 12-bit signed immediate (constant) value (imm), then stores the result in rd (rd = rs1 + imm)

 **Load Instructions**
 
Load instructions read data from a memory address into a general-purpose register. They use the format rd, offset(rs1), where the effective memory address is calculated as rs1 + offset (a 12-bit signed immediate).
• lb rd, offset(rs1) (Load Byte) — Fetches an 8-bit value and sign-extends it to fill the upper bits of rd.
• lbu rd, offset(rs1) (Load Byte Unsigned) — Fetches an 8-bit value and zero-fills the upper bits of rd.
• lh rd, offset(rs1) (Load Halfword) — Fetches a 16-bit value (2 bytes) and sign-extends it to rd.
• lhu rd, offset(rs1) (Load Halfword Unsigned) — Fetches a 16-bit value and zero-fills the upper bits of rd.
• lw rd, offset(rs1) (Load Word) — Fetches a 32-bit value (4 bytes) into rd.
• ld rd, offset(rs1) (Load Doubleword) — Fetches a 64-bit value into rd (RV64 only).
• lwu rd, offset(rs1) (Load Word Unsigned) — Fetches a 32-bit value and zero-fills the upper bits of rd (RV64 only)

**Store Instructions**

Store instructions write data from a register into memory. They use the format rs2, offset(rs1), where the value in rs2 is stored into the memory address calculated by rs1 + offset.
• sb rs2, offset(rs1) (Store Byte) — Writes the lowest 8 bits of rs2 to memory.
• sh rs2, offset(rs1) (Store Halfword) — Writes the lowest 16 bits of rs2 to memory.
• sw rs2, offset(rs1) (Store Word) — Writes the 32-bit value of rs2 to memory.
• sd rs2, offset(rs1) (Store Doubleword) — Writes the 64-bit value of rs2 to memory (RV64 only).

Visually it can be represented below

<img width="1117" height="661" alt="instuction set load add and store" src="https://github.com/user-attachments/assets/2dab6316-5c7b-4abb-b07a-6a6bba6c6bc0" />

---

## RISC V Registers

RISC-V architecture features 32 general-purpose integer registers (x0 through x31), alongside optional floating-point registers (f0 through f31).
Each register has an architectural number (x#) and an ABI (Application Binary Interface) name that defines its standard usage in software.

Key Register Categories

• Caller-saved (Volatile): Temporary (t0-t6) and argument (a0-a7) registers can be overwritten by a sub-routine; the caller must save them if needed after a call.
• Callee-saved (Preserved): Saved (s0-s11) registers must be retained/restored by the called function if it uses them.
• Specialized Convention: As noted in the RISC-V Register Conventions, procedures must avoid modifying global (gp) and thread (tp) pointers.

---

## New Algorithm Sum 1 to N


Before the new algorithum:

<img width="947" height="595" alt="new 1" src="https://github.com/user-attachments/assets/714a2dfc-bfae-4fcf-948d-6c2bb86b9007" />

# Algorithm Overview

The lecture develops the following algorithm.

## Step 1 — Pass Initial Values

From the main C program:
```text
pass:
0
10
```
through:
```text
a0
a1
```
This corresponds to summation from 0 to 9.

## Step 2 — Initialize Registers

The lecture initializes:
```text
a4 = 0
a3 = 0
```
The instructor specifically mentions x0/zero register for initialization.

Purpose:
```text
a4 → stores temporary summation
a3 → loop counter
```

## Step 3 — Store Final Count

The lecture stores final count from a1 into a2. The purpose is to preserve upper limit for comparison.

## Step 4 — Perform Addition

Core computation:
```text
a4 = a3 + a4
```
Initially:
| Register | Value |
| -------- | ----- |
| a3       | 0     |
| a4       | 0     |

Result:
```text
0 + 0 = 0
```
So:
```text
a4 = 0
```

## Step 5 — Increment Counter

The lecture then increments:
```text
a3 = a3 + 1
```
Now:
```text
a3 = 1
```

## Step 6 — Loop Comparison

Condition checked:
```text
a3 < a2
```
Initially:
| Register | Value |
| -------- | ----- |
| a3       | 1     |
| a2       | 10    |

Since:
```text
1 < 10
```
the loop continues.

## Loop Execution Example

The lecture walks through multiple iterations.

Iteration 1
| Register | Value |
| -------- | ----- |
| a3       | 1     |
| a4       | 0     |


Calculation:
```text
0 + 1 = 1
```
Updated:
```text
a4 = 1
```

Iteration 2
| Register | Value |
| -------- | ----- |
| a3       | 2     |
| a4       | 1     |

Calculation:
```text
1 + 2 = 3
```
Updated:
```text
a4 = 3
```

## Loop Exit Condition

The lecture explains that the loop continues as long as:
```text
a3 < a2
```
The moment:
```text
a3 = 10
```
the program exits the loop.

## Returning Final Result

Final summation exists in a4. But ABI convention requires that the return value be in a0. Therefore the result is  copied from a4 to a0.

The lecture specifically mentions:
```text
a4 + 0 → a0
```
to return the result.


<img width="955" height="666" alt="new 2" src="https://github.com/user-attachments/assets/f0c40b17-4e70-4b04-8952-f205543783d5" />


## Lab -1:

This lab introduces transition from simulations to actual RISC-V CPU execution flow, which includes testbench, hex file generation and the the final output.

<img width="1115" height="652" alt="lab risc" src="https://github.com/user-attachments/assets/5fdf94e9-4a20-47d0-b210-4cfb9282b7e1" />

The output:

<img width="1036" height="207" alt="lab output" src="https://github.com/user-attachments/assets/dd35de34-384c-4630-b5c5-29a8b1abd5cc" />

