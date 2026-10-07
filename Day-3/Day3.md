# DAY - 3 Digital Verilog with TL-Verilog and Makerchip

On day 3 we learn about the TL-Verilog ,makerchip platform ,digital designs and etc...

---

## Contents
- [1.What is Logic Design?](#1-what-is-Logic-Design?)
- [2. Mux Implementation and Introduction to Makerchip](#2-mux-implementation-and-introduction-to-makerchip)
- [3. Pipeline Logic](#3-pipeline-logic)
- [4. Introduction to validity](#4-introduction-to-validity)
- [5. Introduction to Hierarchy](#5-introduction-to-hierarchy)
- [6. Labs](#6-labs)
  - [Lab 1](#lab-1)
  - [Lab 2](#lab-2)
  - [Lab 3](#lab-3)
  - [Lab 4](#lab-4)
  - [Lab 5](#lab-5)
  - [Lab 6](#lab-6)
  - [Lab 7](#lab-7)

---

## 1.What is Logic Design?

Digital logic design builds electronic circuits and computer systems using fundamental building blocks called logic gates that process binary signals (1 for High/True, 0 for Low/False) based on Boolean algebra.


The Core Logic Gates

• AND Gate: Outputs High (1) only when all inputs are High (1). (X = A ⋅ B)

• OR Gate: Outputs High (1) if at least one input is High (1). (X = A + B)

• NOT Gate (Inverter): Reverses the input signal; 1 becomes 0, and 0 becomes 1. (Y = Ā)

• NAND Gate: An AND gate followed by a NOT gate; outputs Low (0) only when all inputs are High (1).

• NOR Gate: An OR gate followed by a NOT gate; outputs High (1) only when all inputs are Low (0).

• XOR Gate (Exclusive OR): Outputs High (1) when inputs are different from each other.

• XNOR Gate: Outputs High (1) when inputs are the same (both 1 or both 0).

<img width="1226" height="632" alt="logic design" src="https://github.com/user-attachments/assets/8b2a08e0-5fb3-468b-a9e7-03c987b728f2" />

# Verilog Syntax

The instructor explains that the syntax differs for:

- single-bit operations
- multi-bit operations

<img width="1057" height="631" alt="boolean operators" src="https://github.com/user-attachments/assets/375ab1e0-15e8-4952-9679-19b084a08620" />


## Combinational Logic:

A type of digital circuit where the output depends entirely on the current input values at any given time.

Key Characteristics

• Memoryless: These circuits have no internal memory, storage devices, or feedback loops.
• Instantaneous Response: Outputs change immediately as input signals change, subject only to small propagation delays through the gates.
• Building Blocks: They are constructed by combining basic logic gates like AND, OR, and NOT, plus universal gates like NAND and NOR.

Example: Full Adder

Inputs: A ,B , C

Each input is single-bit. The full adder adds three bits together. Possible output range:

```text
0 to 3
```
Therefore 2 output bits are required.

Outputs:

- S
- Cout

The  S is lower bit and Cout is upper bit.

Full adder circuit:

<img width="1200" height="642" alt="logic design combinational logic" src="https://github.com/user-attachments/assets/95666604-1ade-40a7-84a2-b0396aa33265" />

---

## 2. Mux Implementation and Introduction to Makerchip

Mux:

A multiplexer (MUX) is an electronic circuit that selects one of many input signals and forwards it to a single output line based on control or select signals.

## Basic MUX Operation

The lecture demonstrates 2 input values:

- x1
- x2

and one select signal s. 
output propagates one selected input.

<img width="1127" height="612" alt="mux design" src="https://github.com/user-attachments/assets/74de60ae-8ac0-45ca-a2e2-89df1bc75794" />

# Verilog Ternary Operator

The lecture introduces the Ternary Operator. MUX representation in Verilog:

```text
assign f = s ? x1 : x2;
```

<img width="1117" height="675" alt="ternary mux" src="https://github.com/user-attachments/assets/a631aaea-4c4c-42e2-8b5d-a0f30eeb2c6f" />


# Makerchip IDE

- Makerchip opens with TL-Verilog shell code
- Tutorials and examples can be loaded for an understanding of the platform

## Automatic Circuit Diagram Generation

Makerchip automatically generates circuit diagrams.
The platform:

- compiles TL-Verilog
- generates hardware diagrams
- simulates design
- produces waveforms

## Cloud-Based Simulation

Makerchip sends the design to the cloud.
The cloud:

- compiles design
- runs simulation
- returns results

## Waveform Window

The lecture demonstrates splitting windows to display waveform viewer below circuit diagram. The waveform shows signal behavior over time.

## Signal Highlighting

The lecture demonstrates that upon selecting a signal, the signal becomes highlighted:

- in waveform
- in circuit diagram
- in code view

This provides an interactive debug flow.
---

## 3. Pipeline Logic

CPU pipelining is a hardware technique that breaks instruction execution into sequential stages, allowing multiple instructions to be processed concurrently in an overlapping, assembly-line fashion.


How Pipelining Works

• Overlap: Instead of waiting for one instruction to completely finish before starting the next, the CPU starts a new instruction on every clock cycle.

• Classic 5-Stage Model: Standard RISC pipelines divide the process into Instruction Fetch (IF), Instruction Decode (ID), Execute (EX), Memory Access (MEM), and Write-Back (WB).

• Throughput vs. Latency: It increases overall instruction throughput (instructions per second), but individual instruction latency may slightly increase due to pipeline register overhead

The instructor compares non-pipelined logic
with pipelined logic. Shorter stage delays allow faster clocks.

As shown below:

<img width="1135" height="627" alt="pipeline" src="https://github.com/user-attachments/assets/1507f15c-60fb-4c2f-80bd-0d8154a087cf" />

---

## 4. Introduction to validity

# Validity

Validity is the notion of when values of signals are meaningful. This means that hardware signals may physically toggle, but not every value actually matters.

## Meaningful vs Meaningless Cycles

The calculator previously implemented was doing something meaningful every other cycle.
Meaning - alternate cycles contain useful computations, and remaining cycles contain:

- garbage values
- invalid values
- meaningless data

## Hardware Still Computes During Invalid Cycles

The gates are there, the gates are doing something,
but that value has no meaning. Even during invalid cycles:

- combinational logic still switches
- power is still consumed
- signals still propagate

Validity helps distinguish useful computation
from meaningless activity.

## Valid Signal

The valid signal indicates when computation is meaningful.

## Valid-When Condition

TL-Verilog introduces:
```text
?$valid
```
This is called valid-when condition. This condition applies to every stage of the pipeline.

## Pipeline-Wide Validity

A single validity condition propagates automatically through all pipeline stages. This is a major abstraction advantage of TL-Verilog.


### Clock Gating

Validity enables disabling clocks during meaningless cycles.

---

## 5. Introduction to Hierarchy

# Behavioral Hierarchy

Behavioral hierarchy means logic replicated behaviorally rather than manually instantiating modules repeatedly.

## Cell Neighborhood Logic

The next-state behavior depends on neighboring cells. The decision is all based on the nine cells in the cell's immediate neighborhood.
Meaning - 3×3 neighborhood considered.

# Conway’s Game of Life

The simulation contains a grid of cells where each cell is either alive or dead.

## Counting Alive Neighbors

The hardware first computes number of alive neighbors, including the cell itself total count includes:

- center cell
- surrounding neighbors

## Replicated Hierarchy

We create a replicated context for defining the logic of each cell.

# Lexical Re-Entrance

We can define logic in one context, leave that context, and then return back to that same context.
Meaning - hierarchy scopes can be re-entered later.

## Why Lexical Re-Entrance Matters

This allows:

- modular hardware construction
- distributed logic definition
- reusable libraries
- incremental hierarchy extension

---

## Labs

 ### Lab - 1

 The basic lab on understanding of the makerchip and TL-Verilog:
 
 <img width="1920" height="1080" alt="day3 exercise2" src="https://github.com/user-attachments/assets/54a92361-5f5f-478a-9b19-2bb72b05ca62" />
 

### Lab - 2

The lab on working of vectors:

<img width="1920" height="1080" alt="risc lab vectors" src="https://github.com/user-attachments/assets/3ecea42c-049d-4cf1-8173-0d5a61ca6b04" />

---

### Lab - 3

The lab on pythagoras thoerm:


<img width="1917" height="882" alt="pythogoras theroem hardware" src="https://github.com/user-attachments/assets/f9640a3a-8e84-4719-9be9-5c37e68f0808" />


---

### Lab - 4

The pipeline error fibonnacci series:


Everything in TL-Verilog is in a pipeline, even if not explicitly declared. Undeclared logic exists in:

- default pipeline
- stage zero.

<img width="1920" height="1080" alt="lab pipeline error" src="https://github.com/user-attachments/assets/32e89bb4-cadc-4af4-aeba-03967c78f083" />


---

### Lab - 5

The lab on mux:

<img width="1896" height="881" alt="risc lab mux" src="https://github.com/user-attachments/assets/47a2ceba-3227-4d2f-8269-9ba9cebc0dcb" />


---

### Lab - 6

The sequential calculator:

The code :
<img width="1252" height="402" alt="sequential code " src="https://github.com/user-attachments/assets/f2adce9e-9df2-433c-808e-6091ce1a8bc1" />


The output:
<img width="1317" height="297" alt="sequential waveform" src="https://github.com/user-attachments/assets/5100406c-a784-4522-b961-d7b40c9afe5b" />


---

### Lab - 7

The cycle calculator:

The code:

<img width="1310" height="685" alt="cycle calculator" src="https://github.com/user-attachments/assets/c1d139ce-ba26-4a9f-81c1-9ff2ab670e12" />


The output:

<img width="1311" height="322" alt="output" src="https://github.com/user-attachments/assets/a2d428af-891c-42f3-9e46-03952916513b" />


---

















































