# DAY 1 :Introduction to RISC-V Instuction Set Architecture(ISA)
Today we learn about Risc v architecture ,conversion from software to hardware and some industry oriented examples...

---

## Contents

- [Introduction to RISC-V](#introduction-to-risc-v)
- [From Software to Hardware](#from-software-to-hardware)
- [Labs on Risc v](#labs-on-risc-v)
  - [Lab 1](#lab-1)
  - [Lab 2](#lab-2)
  - [Lab 3](#lab-3)
- [Bit Number System](#bit-number-system)
  - [Unsigned Numbers](#unsigned-numbers)
  - [Signed Numbers](#signed-numbers)
- [Lab on Signed and Unsigned numbers](#lab-on-signed-and-unsigned-numbers)

---

## 1. Introduction to RISC-V

-The RISC-V (pronounced "risk-five") architecture is a free and open-source instruction set architecture (ISA) based on 
established reduced instruction set computer (RISC) principles.

-Managed by RISC-V International, the architecture represents the fifth generation of RISC processor designs originating from the University of California, Berkeley. Unlike proprietary alternatives like x86 or ARM, RISC-V is royalty-free and open to modification, allowing any individual or
enterprise to design, manufacture, and distribute custom silicon without paying licensing fees.

The base integer instruction set, also known as the "RV32I" or "RV64I" instruction set, depending on the address space size, 
provides the core functionality required for general-purpose computing. It includes instructions for arithmetic, logical, and control operations, as well as memory access and manipulation. The base integer instruction set is designed to be minimal and efficient, adhering to the principles of reduced instruction set computing (RISC).

RISC-V instructions are encoded using a fixed-length 32-bit format, which simplifies decoding and execution. 
The instruction formats are categorized into six types: R, I, S, B, U, and J. Each format serves a specific purpose and has a unique encoding structure:

R-type instructions: Used for register-to-register operations, such as arithmetic and logical operations.
They include three register operands: two source registers and one destination register. Eg:- add (Add 2 registers and store results in another)\

I-type instructions: Used for immediate operations, such as arithmetic and logical operations with an immediate value.
They include two register operands and a 12-bit immediate value. Eg:- li (Load immediate value)

S-type instructions: Used for store operations, which store data from a register to memory.
They include two register operands and a 12-bit immediate value for the memory address offset. Eg:- sw (store the value in register)

B-type instructions: Used for conditional branch operations, which transfer control to a different instruction based on a condition. 
They include two register operands and a 12-bit immediate value for the branch target address. Eg:- beq (compare and label)

U-type instructions: Used for operations with a 20-bit immediate value, such as loading a 20-bit constant into a register or setting the upper 20 bits of a register. 
Eg:- lui (load upper immediate value)

J-type instructions: Used for unconditional jump operations, which transfer control to a different instruction unconditionally.
They include one register operand and a 20-bit immediate value for the jump target address. Eg:- J (jump)

---

### 2. From Software to Hardware

The execution flow discussed in the lecture is:

```text
Applications  >  Operating System   >  Compiler  >  Assembly Language  >  Instruction Set Architecture (ISA)  >  Hardware
```
---

<img width="1322" height="740" alt="software to hardware" src="https://github.com/user-attachments/assets/2cdc7f56-fedf-419b-8dcb-43d628bf9383" />


### Applications
Applications are programs written using high-level programming languages such as:

- C
- C++
- Python

Examples:

- Browser applications
- Games

These programs can be understood by humans directly.

---

### Operating System (OS)

The Operating System acts as an interface between: application software and hardware 

Responsibilities of the OS include:

- handle I/O operations
- allocate memory
- low level systems
- software to assembler


---

### Compiler

A compiler converts high-level language programs into lower-level instructions.

Example:

The GCC compiler:

 - optimizes code
 - generates assembly instructions
 - targets a specific ISA

Example flow:

image

### Assembly Language

Assembly language is a human-readable representation of machine instructions.

Characteristics:

- ISA-specific
- low-level
- closely related to hardware operations

Example RISC-V instruction:
```text
MOV ro,#12
```

---

 ## Labs on Risc v
  - Lab 1
we here compute a C program for sum 1 to N:

The program:

<img width="1202" height="427" alt="sum1ton pgm" src="https://github.com/user-attachments/assets/c14c0bbd-1c76-4df8-b8d1-54d4a46981dc" />

The output:

```shell
sum  of numbers from 1 to 5 is 15
```


-Lab 2

This lab demonstrates the RISC V GCC Complier.


Compiler used:
```text
riscv64-unknown-elf-gcc
```

The output:

<img width="1207" height="702" alt="gcc compiler" src="https://github.com/user-attachments/assets/ce5c4690-8ba5-40d2-b687-e2fdefb83bfc" />

 - Lab 3

The spike simulator:

# What is Spike?

Spike is the official RISC-V ISA simulator.

It is used to:
- execute RISC-V binaries
- simulate processor behavior
- debug instructions
- inspect registers and memory

Spike helps learners understand how instructions execute internally inside a RISC-V processor.

---

## Bit Number System

RISC-V uses a binary number system with scalable register and data widths defined by
-XLEN (the register width in bits)
-supporting 32-bit (RV32)
-64-bit (RV64)
-128-bit (RV128) architectures

**Unsigned Numbers:**

RISC-V treats integer registers as plain bit patterns (XLEN bits wide, such as 32 bits in RV32 or 64 bits in RV64), and 
handles unsigned numbers through dedicated instructions that interpret these bit patterns without sign extension.


**Signed Numbers**
RISC-V represents signed numbers using two's complement representation in integer registers.

---

## Lab on Signed and Unsigned numbers:

Sometimes overflow occurs in signed and unsigned numbers . We correct it through some steps.

# Overflow in Unsigned Numbers

Overflow occurs when arithmetic result exceeds representable range.

<img width="1226" height="417" alt="unsigned overflow" src="https://github.com/user-attachments/assets/1bc2e3fd-c8a7-49b8-8e95-3c27c25b4995" />
---

# Overflow in Signed Numbers

Signed overflow occurs when result exceeds signed representable range.

<img width="1222" height="547" alt="signed overflow" src="https://github.com/user-attachments/assets/6e92a619-4232-4310-ae6d-016d6f578343" />
---

Corrected Version


<img width="1207" height="167" alt="Corected version" src="https://github.com/user-attachments/assets/52ebb6fc-ccac-426d-806b-d3b0baaf0b43" />


