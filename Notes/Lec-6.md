# 📘 Lecture 06 – Instruction Set Architecture & Addressing Modes

## 🔷 1. CISC vs RISC Architectures

### ✅ CISC (Complex Instruction Set Computer)
- **Large instruction set**: Many instructions, some of which perform complex tasks
- **Multiple addressing modes**: Supports a variety of ways to access data
- **Variable instruction size**: Some instructions are short, others are long
- **Multi-cycle execution**: Complex instructions may take several clock cycles
- **Examples**: Intel x86, VAX, Motorola 680X0

### ✅ RISC (Reduced Instruction Set Computer)
- **Small instruction set**: Simple instructions that perform basic tasks
- **Fixed instruction size**: All instructions are of the same length (typically one word)
- **Load/store architecture**: Only load and store instructions access memory; all other operations use registers
- **Single-cycle execution**: Most instructions execute in one clock cycle
- **Many registers**: RISC CPUs have a large set of general-purpose registers
- **Examples**: MIPS, ARM, SPARC, IBM 801

### 🔁 Comparison Table

| Feature | CISC | RISC |
|---------|------|------|
| Instruction Length | Variable | Fixed |
| Instruction Set | Large | Small |
| Addressing Modes | Many | Few |
| Execution Time | Multiple cycles | Mostly single cycle |
| Memory Access | Memory operands allowed | Only load/store access memory |
| Hardware Complexity | High | Simpler |

## 🔷 2. Instruction Format

### ✅ What is it?
An instruction tells the CPU:
- What operation to perform (opcode)
- Which operands to use (addresses/registers)

### ✅ Assembly Notation:
```
op X1, X2, ..., Xn
```
Where:
- `op` is the operation code
- `X1, X2, ..., Xn` are operands (registers or memory)

## 🔷 3. RISC Instruction Format

In RISC:
- Only load and store access memory
- Most instructions use registers as operands

### ✅ Format Example:
```
Rd := F(Rs, S2)
```
Where:
- `Rd` is destination register
- `Rs` is source register
- `S2` is either another register or an immediate value

## 🔷 4. Operand Extension

Sometimes operands in instructions are shorter than the CPU's standard word size. This causes a problem when extending these smaller values to the full size needed. There are two solutions:

### ✅ Sign Extension
- Used for signed numbers (two's complement)
- Copies the sign bit (leftmost bit) to extend
- Preserves the number's value

#### 🔹 Example:
```
Original (13-bit):     1010101010101  (negative)
Extended (32-bit): 1111111111111111101010101010101
```

### ✅ Zero Extension
- Used for unsigned numbers
- Pads with zeros to the left
- Used for addresses or constants

#### 🔹 Example:
```
Original:     1010101010101
Extended: 00000000000000001010101010101
```

## 🔷 5. Addressing Modes

### ✅ Purpose:
Addressing modes determine how an instruction identifies the location of its operand.

### 🔹 1. Immediate Addressing
- The operand is directly given in the instruction
- Fast but inflexible (value is fixed)
- **Example**: `LOADI 99`

### 🔹 2. Direct Addressing
- The operand is in memory at a specified address
- **Example**: `LOAD X` → load value at address X

### 🔹 3. Indirect Addressing
- The address field gives the location of another memory cell, which contains the real operand address
- Allows more flexibility
- **Example**: `LOADN W` → go to W, get address of X, then load X

### 🔁 Comparison Table

| Addressing Mode | Operand Location | Speed | Flexibility |
|----------------|------------------|-------|-------------|
| Immediate | Inside the instruction | Fast | Low |
| Direct | Memory location (address) | Medium | Medium |
| Indirect | Address points to another addr | Slowest | High |

## 🔷 6. Relative Addressing

- Only part of the address is given (offset)
- The rest (base address) is stored in a register
- **Effective Address = Base Register + Offset**
- Common in RISC systems

### ✅ Benefits:
- Shorter instructions
- Enables easy relocation of code blocks
- Can be used for indexed access (arrays)

## 🔷 7. Auto Indexing

### ✅ Concept:
- Used when data is accessed sequentially, like in loops or arrays
- Automatically increments or decrements an index register
- Two types:
  - **Pre-decrement**: address is changed before access
  - **Post-increment**: address is changed after access

### ✅ Example (ARM syntax):
- **Pre-increment**: `LDR R0, [R1, #4]!`
- **Post-increment**: `LDR R0, [R1], #4`

## 🔷 8. Register Addressing

### 🔹 Register Direct Addressing
- Operand is stored in a register
- Fastest type of access
- **Example**: `MOVE #99, D1` → move 99 to register D1

### 🔹 Register Indirect Addressing
- A register holds the address of the operand (not the operand itself)
- **Example**: `MOVE.B (A0), D1` → move byte from memory address in A0 to D1

### 🔹 Register Indirect with Offset
- Combines indirect addressing with an offset
- Common in load/store architectures like ARM
- **Example**: `SW Rt, OFFSET(Rs)` → store Rt to address Rs + OFFSET

## ✅ Summary of Addressing Modes

| Mode | Operand Location | Example |
|------|------------------|---------|
| Immediate | In the instruction itself | `LOADI 99` |
| Direct | At memory address specified | `LOAD X` |
| Indirect | At address found in memory location | `LOADN W` |
| Relative | Offset + base register | `LOAD D(R1)` |
| Register Direct | In register | `MOVE #99, D1` |
| Register Indirect | In memory, address in register | `MOVE.B (A0), D1` |
| Reg Indirect with Offset | Address = Register + Offset | `SW Rt, OFFSET(Rs)` |
| Auto Indexing | Register is auto-incremented/decremented | `LDR R0, [R1], #4` or `[R1, #4]!` |

---

## Exercises

### Q1. Differentiate between RISC and CISC with 3 points.

**Answer:**
- RISC uses fixed-length instructions; CISC uses variable-length
- RISC allows only load/store memory access; CISC supports memory operands in many instructions
- RISC generally executes instructions in one clock cycle; CISC may require multiple cycles

---

### Q2. Perform sign and zero extension for the binary number `1010101010101` (13-bit) to 32-bit.

**Sign Extension:**
- Leftmost bit = 1 → replicate 1
- **Result**: `11111111111111111010101010101`

**Zero Extension:**
- Pad with 0s to the left
- **Result**: `00000000000000001010101010101`

---

### Q3. What is the effective address for `STB Rs, Rd(S2)` when Rd = 0x1000 and S2 = 0x20?

**Answer:**
- Effective Address = Rd + S2 = 0x1000 + 0x20 = **0x1020**

---

### Q4. Identify the addressing mode used:

- `MOV A, #5` → **Immediate Addressing**
- `MOV A, B` → **Direct Addressing**
- `MOV A, [B]` → **Indirect Addressing**

---

### Q5. Why is relative addressing beneficial for loops or arrays?

**Answer:**
- Enables compact encoding
- Code can be relocated in memory
- Simplifies addressing with offsets for array elements
