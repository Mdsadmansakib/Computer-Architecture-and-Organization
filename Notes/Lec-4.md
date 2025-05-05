# CPU Organization and Architecture

## 1. Primary Function of CPU

The CPU executes sequences of instructions stored in memory through a three-step process:

1. **Transfer** - CPU fetches instructions and operands from main memory to CPU registers
2. **Execute** - CPU executes instructions in stored sequence (except when altered by branch instructions)
3. **Store Results** - CPU transfers results from registers back to main memory when necessary

## 2. External Communication

### Memory Communication

The CPU communicates with memory in two primary configurations:

#### Without Cache
```
CPU <---> Main Memory (MM)
         Instructions
         Data
```

#### With Cache
```
CPU <---> Cache Memory (CM) <---> Main Memory (MM)
         Instructions               Instructions
         Data                       Data
```

**Key Performance Difference:**
- CPU can perform memory load/store operations from cache in a single clock cycle
- The same operations take many clock cycles when performed from main memory
- CPU considers cache and main memory as a single, seamless memory space of 2^m addressable locations M(0), M(1), …, M(2^m-1)

## 3. Communication with I/O Devices

- CPU communicates with I/O devices similar to external memory
- I/O devices are associated with addressable registers called **I/O ports**
- CPU can store to or load from these ports

### I/O Communication Approaches:

1. **Memory-mapped I/O**
   - Memory locations and I/O ports share the same address space
   - An address assigned to memory cannot be assigned to an I/O port, and vice versa

2. **I/O-mapped I/O**
   - Uses distinct I/O instructions separate from memory-referencing instructions
   - These instructions produce control signals to which only I/O ports respond

## 4. User and Supervisor Programs

- **User/Application Programs**: Handle specific applications
- **Supervisor Programs**: Manage routine system aspects (part of the operating system)

### CPU Operation Mode Switching

- CPU continuously switches between user and supervisor programs
- Requests for supervisor services from secondary memory and I/O devices are called **interrupts**
- Upon interrupt, CPU suspends current program execution and transfers to an interrupt handling program
- CPU frequently checks for interrupt requests

### CPU Operation Flow

```
Begin
  ↓
Fetch next instruction
  ↓
Execute instruction
  ↓
Are there interrupts waiting? → Yes → Transfer to interrupt handling program
  ↓ No                             ↓
Are there instructions waiting? → No → End
  ↓ Yes
  ↑ (Return to fetch)
```

## 5. CPU Instruction Cycle

- The sequence of operations performed to process an instruction constitutes an **instruction cycle**
- Each instruction generally requires two steps:
  1. **Fetch step**: A new instruction is read from external memory
  2. **Execute step**: Operations specified by the instruction are executed

### Micro Operations

- CPU actions during an instruction cycle are defined by a sequence of **micro operations**
- Each micro operation involves a register transfer operation
- **CPU cycle time** (or **clock period** Tclock): Time required for the shortest well-defined CPU micro operation
- Number of CPU cycles required to process an instruction varies by instruction type

## 6. Accumulator-based CPU

### Architecture Components

```
                               System Bus
                                   ↕
                   +---------------------------+
                   |     Instruction           |
                   |     Decoder               |
                   +---------------------------+
                   |                           |
     ┌───────┐     |     ┌───┐ ┌──┐ ┌──┐      |  To M and I/O devices
     │Control│     |     │IR │ │AR│ │PC│      |
     │Signal │     |     └───┘ └──┘ └──┘      |
     └───────┘     |                          |
                   |     ┌──┐ ┌──┐            |
                   |     │DR│ │AC│            |
                   |     └──┘ └──┘            |
                   |     Arithmetic-Logic     |
                   |     Unit                 |
                   |                          |
                   +---------------------------+
                         PCU       DPU
```

# Key CPU Components and Their Roles

These terms are key components of a CPU (Central Processing Unit) architecture, primarily related to instruction execution and data handling. Here's a concise breakdown:

---

## 1. Program Control Unit (PCU)

- **Role**: Manages the fetch-decode-execute cycle of instructions.
- **Function**: Coordinates operations between CPU registers, memory, and the Data Processing Unit (DPU).

---

## 2. Registers in the CPU

### (A) Address Register (AR)

- **Purpose**: Stores the memory address from which data will be read or written.
- **Example**: If the CPU needs to fetch data from memory location `0x1000`, AR holds `0x1000`.

### (B) Instruction Register (IR)

- **Purpose**: Holds the current instruction being decoded/executed.
- **Example**: For the instruction `ADD R1, R2`, IR stores the binary opcode of `ADD`.

### (C) Program Counter (PC)

- **Purpose**: Stores the address of the next instruction to execute.
- **Behavior**: Increments automatically after each fetch or jumps for branches.

### (D) Accumulator (AC)

- **Purpose**: Temporarily stores intermediate results of arithmetic/logic operations.
- **Example**: After `ADD R1, R2`, the sum is held in AC before being stored elsewhere.

### (E) Data Register (DR)

- **Purpose**: Temporarily holds data read from memory or to be written to memory.
- **Example**: When loading data from AR’s address, DR holds the retrieved value.

---

## 3. Data Processing Unit (DPU)

- **Role**: Performs arithmetic/logic operations (e.g., `ADD`, `AND`).
- **Components**: Includes the ALU (Arithmetic Logic Unit) and registers like AC.

---

## How They Work Together

### **Fetch**
- PC sends the next instruction address to memory → Fetched instruction stored in IR.

### **Decode**
- PCU decodes the instruction in IR.

### **Execute**
- **For memory access**: AR holds the target address; DR holds data.
- **For calculations**: DPU uses AC for results.

### **Update**
- PC increments or jumps to the next instruction.


### Characteristics

- Accumulator architecture always stores intermediate calculation results in the accumulator
- Called a "1-operand machine"
- Instructions that reference memory data contain:
  - An opcode (op)
  - A memory address (adr)
  - Expressed as: I = op.adr
- Instruction cycle begins with fetch: IR.AR = M(PC), where IR=op and AR=adr
- Instructions not referencing memory don't use AR
- After placing opcode in IR, CPU decodes and executes it, then increments PC

## 7. Load and Store Operations

- **Load instruction**: Transfers word from memory location with address adr to accumulator
  - AC := M(adr)
  
- **Store instruction**: Transfers word from AC to memory
  - M(adr) := AC

## 8. Programming Considerations

- Data processing operations normally require up to 3 operands (e.g., Z := X + Y)
- Accumulator-based CPU supports only single-address instructions

### Example: Implementing Z := X + Y

**Using separate load/store operations:**

| HDL format | Assembly language | Comment |
|------------|-------------------|---------|
| AC := M(X) | LD X | Load X from M into AC |
| DR := AC | MOV DR, AC | Move contents of AC to DR |
| AC := M(Y) | LD Y | Load Y into AC |
| AC := AC + DR | ADD | Add DR to AC |
| M(Z) := AC | ST Z | Store contents of AC in M |

**Using optimized instruction set:**

| HDL format | Assembly language | Comment |
|------------|-------------------|---------|
| AC := M(X) | LD X | Load X from M to AC |
| AC := AC + M(Y) | ADD Y | Load Y into DR and add to AC |
| M(Z) := AC | ST Z | Store contents of AC in M |

## 9. Instruction Set

The instruction set of an accumulator-based CPU typically includes:

| Type | Instruction | HDL format | Assembly format |
|------|------------|------------|----------------|
| Data Transfer | Load | AC := M(X) | LD X |
| | Store | M(X) := AC | ST X |
| | Move Register | DR := AC | MOV DR, AC |
| Data Processing | Add | AC := AC + DR | ADD |
| | Subtract | AC := AC - DR | SUB |
| | And | AC := AC and DR | AND |
| | Not | AC := not AC | NOT |
| Program Control | Branch | PC := M(adr) | BRA adr |
| | Branch zero | if AC = 0 then PC := M(adr) | BZ adr |

### Example: Arithmetic Negation

| HDL format | Assembly language | Comment |
|------------|-------------------|---------|
| DR := AC | MOV DR, AC | Copy contents X of AC to DR |
| AC := AC - DR | SUB | Compute AC = X - X = 0 |
| AC := AC - DR | SUB | Compute AC = 0 - X = -X |

## 10. Multiplication Program Example

**Objective**: Implement AC := AC × N
- Multiplicand is initial content of AC
- Multiplier N is a variable stored in memory

**Implementation**:
- Perform AC + AC + ... + AC (N times)
- Memory location storing N acts as a count register
- After each add operation, decrement N by 1 until it reaches 0
- Use BZ instruction to test for N = 0

**Memory Locations**:
- `one` - stores constant 1
- `mult` - stores N
- `ac` - stores Y (multiplicand)
- `prod` - stores partial product

**Assembly Program**:

| Line | Location | Instruction/Data | Assembly format | HDL format |
|------|----------|-----------------|----------------|------------|
| 0 | one | 00...01 | | |
| 1 | mult | N | | |
| 2 | ac | 00...00 | | |
| 3 | prod | 00...00 | | |
| 4 | | | ST ac | M(ac) := AC |
| 5 | Loop | | LD mult | AC := M(mult) |
| 6 | | | BZ exit | If AC = 0 then exit |
| 7 | | | LD one | AC := M(one) |
| 8 | | | MOV DR, AC | DR := AC |
| 9 | | | LD mult | AC := M(mult) |
| 10 | | | SUB | AC := AC - DR |
| 11 | | | ST mult | M(mult) := AC |
| 12 | | | LD ac | AC := M(ac) |
| 13 | | | MOV DR, AC | DR := AC |
| 14 | | | LD prod | AC := M(prod) |
| 15 | | | ADD | AC := AC + DR |
| 16 | | | ST prod | M(prod) := AC |
| 17 | | | BRA Loop | PC := Loop |
| 18 | exit | | | |

## 11. Limitations of Accumulator-based CPU

- Few data registers in CPU leads to excessive data transfers between CPU and memory
- Program execution would be faster if quantities like constants, counters, and intermediate values could be stored in dedicated CPU registers

## Exercises

### Exercise 1: Implement Division Operation
Write an assembly program for an accumulator-based CPU to implement integer division AC := N / D, where:
- N is the dividend stored in memory location `dividend`
- D is the divisor stored in memory location `divisor`
- The result should be stored in memory location `quotient`
- Assume memory location `result` is available for intermediate calculations

### Exercise 2: Compare Memory Architectures
Given a simple calculation Z = (A + B) * (C - D):
1. Write the assembly code for an accumulator-based CPU
2. Count the number of memory accesses required
3. Explain how the performance would improve with:
   a) A CPU with multiple general-purpose registers
   b) A cache memory system

### Exercise 3: Analyze the Multiplication Program
For the multiplication program shown in section 10:
1. How many memory accesses are required to multiply by N = 5?
2. Modify the program to be more efficient by reducing memory accesses
3. Calculate the performance improvement in terms of clock cycles
