# DAY 5 : Complete pipelined RISC-V CPU micro-architecture
On the fifth day we learn about pipelining the CPU, control flow hazard and read after write hazard etc...

---

## Contents

- [1.Introduction to control flow hazard and read after write hazard](#1-introduction-to-control-flow-hazard-and-read-after-write-hazard)
- [2.Introduction_To_Load_Store_Instructions](#2-introduction-to-load-store-instructions)
- [3. Labs](#6-labs)
  - [Lab 1](#lab-1)
  - [Lab 2](#lab-2)
  - [Lab 3](#lab-3)
  - [Lab 4](#lab-4)
  - [Lab 5](#lab-5)
  - [Lab 6](#lab-6)
  - [Lab 7](#lab-7)
  
---

## Introduction to control flow hazard and read after write hazard

A Control Hazard happens when a branch or jump instruction changes the program counter, causing the RISC-V pipeline to fetch the wrong instructions. A Read-After-Write (RAW) hazard happens when a later instruction tries to read a register before an earlier instruction has finished writing the new value to it.


1. Read-After-Write (RAW) Hazard

• What it is: Also called a true dependency or flow dependency. Instruction I₂ needs data produced by instruction I₁.

• Example in RISC-V:

assembly

```shell
add x10, x1, x2   # Instruction 1: writes result to x10
sub x11, x10, x3  # Instruction 2: reads x10
```

• Why it happens in a 5-stage pipeline:

	• The standard RISC-V 5 stages are: IF (Fetch), ID (Decode), EX (Execute), MEM (Memory), and WB (Writeback).
  
	• add writes the new value of x10 during the WB stage.
  
	• sub reads x10 during the ID stage.
  
	• Without intervention, sub reads the old, stale value of x10 before add reaches WB.
  
• How RISC-V fixes it:

	• Forwarding (Bypassing): Hardware routes the computed result directly from the output of the EX or MEM stage to the input of the EX stage, bypassing the register file.
  
	• Stalling (Load-Use Hazard): If add is replaced by a load instruction (ld), data isn't ready until after the MEM stage. Forwarding alone cannot go backward in time, so the pipeline must stall (insert a bubble/NOP) for 1 cycle.

The valid signal:

The valid pulse effectively behaves like periodic pipeline enable generator. We can see this in waveform below;

<img width="1315" height="92" alt="valid signal" src="https://github.com/user-attachments/assets/8b2564f2-3469-4cff-8042-798060629ced" />


  After write hazard you get these registers

 <img width="746" height="460" alt="after write hazard" src="https://github.com/user-attachments/assets/cf37657e-6cfb-4fad-80fc-1730075eb88f" />
 
---

## Introduction_To_Load_Store_Instructions

Load-store architecture, meaning that main memory can only be accessed using dedicated load and store instructions. All arithmetic, logical, and shift operations in RISC-V operate strictly on CPU registers rather than directly on memory addresses.

• Load (load): Reads data from a memory address and writes it into a destination register (rd).

• Store (store): Writes data from a source register (rs2) into a memory address.

• Effective Address: Calculated by adding a 12-bit signed immediate offset to a base address held in a source register (rs1)

• Offset Range: The 12-bit signed immediate allows a reach of -2048 to +2047 bytes from the base address

# PC Redirection For Loads

After detecting a load:

- the PC is redirected
- the next correct instruction is replayed
- invalid shadow instructions are squashed

The redirected PC becomes:
```text
PC(load) + 4
```
which is the next sequential instruction after the load.

---

<img width="1312" height="487" alt="load" src="https://github.com/user-attachments/assets/cf73017a-dbc6-471e-9b37-62e57628ff59" />


---

## Labs

  ### Lab - 1:
  
  This lab upgrades the RISC-V CPU from an artificially spaced 3-cycle execution model into a near continuous pipelined processor.
  
  The result:
  
  <img width="677" height="477" alt="op11" src="https://github.com/user-attachments/assets/732a22f2-b7e6-47c8-bdfe-6332c4b36ce6" />
  


---

## Lab - 2

This lab completes the remaining instruction decode logic for the RV32I base instruction set.

The result:

<img width="622" height="527" alt="lab 22" src="https://github.com/user-attachments/assets/7c5ab67f-a8ab-4015-8f0e-555aa7b778cf" />



---

## Lab - 3

This lab completes ALU functionality for concerned instructions

That is:

<img width="1247" height="495" alt="lab 3" src="https://github.com/user-attachments/assets/688c0085-ef73-405a-9446-6a5173bc5997" />


---

## Lab - 4

This lab does the delayed load writeback into register file;

which is:

<img width="491" height="552" alt="lab 4" src="https://github.com/user-attachments/assets/0ee64fca-fe1f-4035-b4a4-8b74700ca5b5" />

---

## Lab - 5

This lab puts actual memory into pipeline:

<img width="632" height="576" alt="lab5" src="https://github.com/user-attachments/assets/d2abfd1e-0231-431b-8a7d-0dc20004170a" />

---

## Lab - 6

We verify the correctness of previous lab:

<img width="726" height="477" alt="lab 6" src="https://github.com/user-attachments/assets/d836b60a-f07d-496a-84ae-6c4de6e0fb9a" />


---

## Lab - 7

In this lab we add jump instructions where the final output is:

<img width="1047" height="575" alt="lab 7" src="https://github.com/user-attachments/assets/1187923a-5d8b-4ab0-8913-02a7eb7082e2" />


---
