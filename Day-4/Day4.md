# DAY 4 : Basic RISC-V CPU Micro-Architecture
On the fourth day we were taught of CPU architecture, its cycles ,fetch, decode functions and etc...

---

## Contents.

- [1.Architecture for single cycle RISC-V CPU](#1-architecture-for-single-cycle-risc-v-cpu)
- [2. Concept of Array and register file details](#2-concept-of-array-and-register-file-details)
- [3. Labs](#3-labs)
  - [Lab 1](#lab-1)
  - [Lab 2](#lab-2)
  - [Lab 3](#lab-3)
  - [Lab 4](#lab-4)
  - [Lab 5](#lab-5)
  - [Lab 6](#lab-6)
  - [Lab 7](#lab-7)
  - [Lab 8](#lab-8)
  - [Lab 9](#lab-9)
 

 ---

## 1.Architecture for single cycle RISC-V CPU

A single-cycle RISC-V CPU executes an entire instruction—from fetching to writing back the result—within one single clock cycle.

An instruction passes through five conceptual stages sequentially inside the same clock pulse:

1. Fetch: The address in the PC points to the Instruction Memory, retrieving the 32-bit instruction while simultaneously computing PC + 4.

2. Decode: The instruction bits are parsed. Source registers (rs1, rs2) pull data from the Register File, and the Immediate Generator prepares offset values.
3. Execute (ALU):
	• For R-type instructions, the ALU operates on rs1 and rs2.
	• For I-type (arithmetic/loads) and S-type (stores), the ALU adds rs1 and the sign-extended immediate to calculate memory or target  addresses.
	• For B-type (branches), the ALU compares register values and evaluates branch conditions.

4. Memory Access: Data Memory is read (for lw) or written (for sw). Other instruction types bypass this stage.

5. Write-Back: The final result (from the ALU or Data Memory) is written back to the destination register (rd) in the Register File.

    
<img width="1017" height="585" alt="cpu" src="https://github.com/user-attachments/assets/3a6b2f95-a8d1-47bd-aa63-b6c96bcec6e8" />


---

## 2. Concept of Array and register file details

**Register File Entries**

Each register entry contains:

- storage flip-flops
- write selection logic
- recirculation logic


The CPU should be reading registers written by the previous instruction. If read and write happen in the same stage then an instruction could incorrectly read its own newly-written value. This is not desired CPU behavior. The correct behavior is that the previous instruction writes register file and the next instruction reads the updated value. Therefore instruction in stage 2 updates state and instruction in stage 1 reads updated state. This creates instruction-to-instruction dependency flow.


<img width="1042" height="592" alt="register file" src="https://github.com/user-attachments/assets/1272b0e0-e655-4e7a-8496-6c42db09f65f" />


---

## 3. Labs

 ### Lab - 1
 
The lab for PC:

The PC continuously feeds back through: 
 flip-flops, increment logic branch redirection logic forming the core execution loop of the processor.
 
<img width="1920" height="1080" alt="lab for pc" src="https://github.com/user-attachments/assets/52c29591-6c6b-4dbd-97a3-a4ff4637d839" />



 ---

 ## Lab - 2
The lab for pc with added instruction ,it is called the next_pc:

<img width="1920" height="1080" alt="lab next pc" src="https://github.com/user-attachments/assets/6005f30d-5001-41b4-9c9d-589f918b6168" />


 ---

 ## Lab - 3

The lab for instuction fetch logic:

# Instruction Fetch Path

The fetch datapath now becomes:
```text
PC -> IMEM Address -> Instruction Memory -> Instruction
```

<img width="1920" height="1080" alt="lab fetch logic" src="https://github.com/user-attachments/assets/49eed3d9-33ea-4736-ac87-fd68f54b06c8" />

 ---

 ## Lab - 4

The lab for instruction types:
they are IRSJBU:

 <img width="1920" height="1080" alt="instruction types" src="https://github.com/user-attachments/assets/95b0c7e2-a9bc-48fe-8f2a-51fa263afccb" />
 
 ---

 ## Lab - 5

This lab does instruction decode logic by implementing extraction of all remaining instruction fields for RV-ISBUJ instruction formats

The code:
<img width="1247" height="552" alt="next instuction code" src="https://github.com/user-attachments/assets/ef7cfef5-a902-4d06-955a-87530d8a518e" />

The output

<img width="1012" height="732" alt="instuction output" src="https://github.com/user-attachments/assets/13787d1b-e748-4c71-a0ed-d0a3f4effd8a" />


 ---

 ## Lab - 6

The lab for ALU operations such as addition:

<img width="1317" height="570" alt="ALU" src="https://github.com/user-attachments/assets/dcf47aeb-6bec-4cd1-bc49-e641dcb2c302" />


 ---

 ## Lab - 7
 
The lab for Register write File Instruction:


The register file already exists and now the CPU must:
- connect write control signals
- connect destination register index
- connect write data

<img width="1305" height="560" alt="rigister wirte" src="https://github.com/user-attachments/assets/f451684d-35eb-4369-a2a9-b16c03c26873" />


 ---

## Lab - 8

The lab for implementing and completing branch instuction:

The datapath now becomes:
```text
Instruction →
Decode →
Register Read →
Comparison →
Branch Decision
```

The implementation:

<img width="1302" height="550" alt="implementation" src="https://github.com/user-attachments/assets/00c53de8-b131-462a-b7a0-8667e73fcfda" />


The complention:

<img width="1272" height="690" alt="completion" src="https://github.com/user-attachments/assets/81e1e61c-e0b7-446e-867b-60466abf2735" />

---

## Lab -9 

The lab to create a simple testbench:

<img width="687" height="432" alt="test" src="https://github.com/user-attachments/assets/3b46a168-09df-4166-baab-3d47cc97e823" />



---

