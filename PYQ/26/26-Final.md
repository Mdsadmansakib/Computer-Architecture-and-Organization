# CSE 2204 Computer Architecture Exam Solutions

## Question 1a: Carry Save Adder

### Advantages of Carry Save Adder:
1. **Reduced propagation delay** - No carry propagation between stages
2. **Parallel operation** - All bit positions computed simultaneously
3. **Higher speed** - Constant time complexity O(1) for addition
4. **Suitable for multiple operand addition** - Efficient for adding 3+ numbers

### Carry Save Addition Example:
**Given:** W = 10011110, X = 10011011, Y = 11101101

**Step 1: Perform carry save addition**
```
Position: 76543210
W:        10011110
X:        10011011  
Y:        11101101
```

For each bit position, calculate Sum and Carry separately:
- Sum[i] = W[i] ⊕ X[i] ⊕ Y[i]
- Carry[i] = (W[i] & X[i]) | (W[i] & Y[i]) | (X[i] & Y[i])

**Calculations:**
```
Position 0: 0⊕1⊕1=0, Carry=(0&1)|(0&1)|(1&1)=1
Position 1: 1⊕1⊕0=0, Carry=(1&1)|(1&0)|(1&0)=1
Position 2: 1⊕0⊕1=0, Carry=(1&0)|(1&1)|(0&1)=1
Position 3: 1⊕1⊕1=1, Carry=(1&1)|(1&1)|(1&1)=1
Position 4: 1⊕0⊕0=1, Carry=(1&0)|(1&0)|(0&0)=0
Position 5: 0⊕1⊕1=0, Carry=(0&1)|(0&1)|(1&1)=1
Position 6: 0⊕0⊕1=1, Carry=(0&0)|(0&1)|(0&1)=0
Position 7: 1⊕1⊕1=1, Carry=(1&1)|(1&1)|(1&1)=1
```

**Results:**
- Sum = 11010001
- Carry = 10110110 (shifted left by 1 position = 101101100)

**Final Addition:** 11010001 + 101101100 = 1000111101

### Traditional Addition Comparison:
```
  10011110  (W = 158)
  10011011  (X = 155) 
+ 11101101  (Y = 237)
----------
 1000111101 (Result = 549)
```

**Advantage:** Carry save adder reduces the critical path delay from O(n) to O(log n).

---

## Question 1b: Booth's Multiplication Algorithm

### Advantages over Sequential Multiplication:
1. **Handles signed numbers** directly using 2's complement
2. **Reduces partial products** for consecutive 1s
3. **More efficient** for numbers with long strings of 1s
4. **Hardware simplification** - uses shift and add/subtract only

### Booth's Algorithm: 4 × 7

**Setup:**
- Multiplicand (M) = 4 = 0100
- Multiplier (Q) = 7 = 0111
- Q₋₁ = 0 (initially)
- Accumulator (A) = 0000
- Count = 4

**Steps:**

| Step | A    | Q    | Q₋₁ | Q₀Q₋₁ | Operation | New A | Shift A,Q,Q₋₁ |
|------|------|------|-----|-------|-----------|-------|----------------|
| 0    | 0000 | 0111 | 0   | 10    | A = A - M | 1100  | 1110 0011 1    |
| 1    | 1110 | 0011 | 1   | 11    | No op     | 1110  | 1111 0001 1    |
| 2    | 1111 | 0001 | 1   | 11    | No op     | 1111  | 1111 1000 1    |
| 3    | 1111 | 1000 | 1   | 01    | A = A + M | 0011  | 0001 1100 0    |

**Final Result:** A,Q = 00011100 = 28 (decimal)
**Verification:** 4 × 7 = 28 ✓

---

## Question 2: Floating Point Addition (0.5 + (-0.4375))

### Step 1: Convert to IEEE 754 32-bit format

**0.5 in IEEE 754:**
- Binary: 0.1₂ = 1.0 × 2⁻¹
- Sign: 0, Exponent: 126 (127-1), Mantissa: 00000000000000000000000
- IEEE 754: 0 01111110 00000000000000000000000

**-0.4375 in IEEE 754:**
- 0.4375 = 0.0111₂ = 1.11 × 2⁻²
- Sign: 1, Exponent: 125 (127-2), Mantissa: 11000000000000000000000
- IEEE 754: 1 01111101 11000000000000000000000

### Step 2: Align mantissas (shift smaller exponent)
- 0.5: 1.000... × 2⁻¹
- -0.4375: 0.111... × 2⁻¹ (shifted right by 1)

### Step 3: Add mantissas
```
  1.000000000000000000000000
- 0.111000000000000000000000
= 0.001000000000000000000000
```

### Step 4: Normalize result
- 0.001₂ × 2⁻¹ = 1.0 × 2⁻⁴
- Result: 0.0625

### Step 5: IEEE 754 representation of 0.0625
- Sign: 0, Exponent: 123 (127-4), Mantissa: 00000000000000000000000
- **Final:** 0 01111011 00000000000000000000000

---

## Question 3: 1-bit ALU Design

### Circuit Components:
1. **AND Gate** - for A AND B
2. **NOR Gate** - for A NOR B  
3. **NAND Gate** - for A NAND B
4. **Full Adder** - for A + B + Cin

### Control Signals:
- **S1, S0**: Operation select (2-bit)
  - 00: AND
  - 01: NOR
  - 10: NAND
  - 11: ADD

### 1-bit ALU Logic:
```
Inputs: A, B, Cin, S1, S0
Outputs: Result, Cout

Operation Logic:
- AND_out = A & B
- NOR_out = ~(A | B)
- NAND_out = ~(A & B)
- ADD_out, Cout = Full_Adder(A, B, Cin)

Result = MUX4x1(AND_out, NOR_out, NAND_out, ADD_out, {S1,S0})
```

---

## Question 4a: MIPS Instruction Formats

### (1) sub $t1, $s3, $s5 (R-type)
```
opcode | rs   | rt   | rd   | shamt | funct
000000 | 10011| 10101| 01001| 00000 | 100010
6 bits | 5    | 5    | 5    | 5     | 6 bits
```
**Decimal:** 0x02754822

### (2) lw $t1, 150($t0) (I-type)
```
opcode | rs   | rt   | immediate
100011 | 01000| 01001| 0000000010010110
6 bits | 5    | 5    | 16 bits
```
**Decimal:** 0x8D090096
**Addressing Mode:** Base + Displacement
**Address Calculation:** Reg[$t0] + 150

### (3) beq $s3, $s4, 200 (I-type)
```
opcode | rs   | rt   | immediate
000100 | 10011| 10100| 0000000011001000
6 bits | 5    | 5    | 16 bits
```
**Decimal:** 0x126800C8
**Addressing Mode:** PC-relative
**Address Calculation:** PC + 4 + (200 << 2)

---

## Question 5: ARM Code Implementation

### While Loop in ARM Assembly:
```arm
loop:
    CMP r1, r2          ; Compare a and b
    BEQ end             ; Branch if a == b
    
    BGT else            ; Branch if a > b
    ADD r2, r1, r2      ; b = a + b
    B loop              ; Branch back to loop
    
else:
    SUB r1, r1, r2      ; a = a - b
    B loop              ; Branch back to loop
    
end:
    ; End of program
```

### RISC vs CISC Differences:

| Aspect | RISC | CISC |
|--------|------|------|
| Instruction Set | Simple, fixed-length | Complex, variable-length |
| Addressing Modes | Few, simple | Many, complex |
| Execution | Single cycle | Multiple cycles |
| Hardware | Simple | Complex |
| Compiler | Complex optimization | Simple compilation |
| Examples | ARM, MIPS | x86, VAX |

---

## Question 6: Cache Write Operations

### Write Policies:

**1. Write-Through**
- **Pros:** Data consistency, simple recovery
- **Cons:** Higher memory traffic, slower writes

**2. Write-Back**  
- **Pros:** Reduced memory traffic, faster writes
- **Cons:** Complex consistency, dirty bit overhead

**3. Write-Around**
- **Pros:** Avoids cache pollution for sequential writes
- **Cons:** Read misses for recently written data

**4. Write-Allocate vs No-Write-Allocate**
- **Write-Allocate:** Loads block on write miss
- **No-Write-Allocate:** Writes directly to memory on miss

---

## Question 7: I/O and Memory Access

### Programmed I/O vs Interrupt-Driven I/O:

| Aspect | Programmed I/O | Interrupt-Driven I/O |
|--------|----------------|---------------------|
| CPU Usage | Continuous polling, wasteful | Efficient, event-driven |
| Response Time | Immediate | Slightly delayed |
| Complexity | Simple | More complex |
| Multitasking | Poor support | Good support |
| Power Consumption | High | Lower |

### DMA Controller Operation:
1. **Setup:** CPU programs DMA with source, destination, count
2. **Transfer:** DMA takes bus control, transfers data directly
3. **Completion:** DMA interrupts CPU when done
4. **Advantage:** Frees CPU for other tasks during transfer
