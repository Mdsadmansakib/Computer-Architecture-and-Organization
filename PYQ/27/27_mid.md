# University of Dhaka
## Department of Computer Science and Engineering
### CSE 2204: Computer Architecture and Organization
#### 2nd Year, 2nd Semester, 2023
**Total Mark: 30** | **Total Time: 1 Hour 30 Minutes**

## Solutions to Selected Questions

### Question 1
**What is the advantage of non-restoring division algorithm? Write down the steps needed to find the result of dividing 12 by 3. For each step you should mention the rule used.**

#### Solution:

**Advantages of Non-Restoring Division Algorithm:**
1. **More Efficient**: Eliminates the need for restoring steps when the remainder becomes negative
2. **Fewer Operations**: Requires fewer operations per iteration compared to restoring division
3. **Hardware Simplicity**: Simpler to implement in hardware
4. **Regular Pattern**: Operations follow a more consistent pattern

**Steps to divide 12 by 3 using Non-Restoring Division:**

Let's represent:
- Dividend (12) in binary: 1100
- Divisor (3) in binary: 0011

**Step 1: Initialization**
- A (Accumulator) = 0000
- Q (Quotient/Dividend) = 1100
- M (Divisor) = 0011
- n (number of bits) = 4

**Step 2: First Iteration**
- Shift A and Q left: A = 0000, Q = 1100 → A = 0001, Q = 1000
- Rule: A = A - M = 0001 - 0011 = 1110 (negative)
- Set rightmost bit of Q to 0: Q = 1000
- A = 1110

**Step 3: Second Iteration**
- Shift A and Q left: A = 1110, Q = 1000 → A = 1101, Q = 0000
- Since A is negative, Rule: A = A + M = 1101 + 0011 = 0000
- Set rightmost bit of Q to 1: Q = 0001
- A = 0000

**Step 4: Third Iteration**
- Shift A and Q left: A = 0000, Q = 0001 → A = 0000, Q = 0010
- Rule: A = A - M = 0000 - 0011 = 1101 (negative)
- Set rightmost bit of Q to 0: Q = 0010
- A = 1101

**Step 5: Fourth Iteration**
- Shift A and Q left: A = 1101, Q = 0010 → A = 1010, Q = 0100
- Since A is negative, Rule: A = A + M = 1010 + 0011 = 1101
- Set rightmost bit of Q to 1: Q = 0101
- A = 1101

**Step 6: Final Correction**
- Since A is negative, perform one more addition: A = A + M = 1101 + 0011 = 0000
- Final quotient is Q = 0100 (4 in decimal)
- Final remainder is A = 0000 (0 in decimal)

Result: 12 ÷ 3 = 4 with remainder 0, which is correct.

### Question 2
**What are the advantages of using a carry save adder? Discuss the concept of carry save addition using W = 10101010, X = 1100(1010 and Y = 1111 0101. Compare it with the traditional addition using the same example.**

#### Solution:

**Advantages of Carry Save Adder (CSA):**
1. **Speed**: Significantly faster for adding multiple numbers as it eliminates carry propagation delays
2. **Parallelism**: Processes multiple bits simultaneously
3. **Reduced Latency**: Critical path is shorter compared to ripple carry adders
4. **Efficiency in Multi-Operand Addition**: Especially efficient when adding more than two numbers
5. **Hardware Implementation**: Used in high-speed multipliers and ALU designs

**Concept of Carry Save Addition:**
A carry save adder adds three binary numbers simultaneously, producing two outputs:
1. Sum bits (S)
2. Carry bits (C)

These two outputs must then be added using a conventional adder to get the final result.

**Example with W = 10101010, X = 11001010, Y = 11110101:**

Step 1: Perform carry save addition:
```
  W: 1 0 1 0 1 0 1 0
  X: 1 1 0 0 1 0 1 0
  Y: 1 1 1 1 0 1 0 1
  -----------------
  S: 1 0 0 1 0 1 1 1 (Sum bits)
  C: 1 1 1 0 1 0 1 0 (Carry bits, shifted left)
```

Step 2: Add S and C using conventional addition:
```
    C: 1 1 1 0 1 0 1 0 0
    S: 0 1 0 0 1 0 1 1 1
    ---------------------
Final: 1 0 0 1 1 1 0 0 1
```

**Traditional Addition:**
Adding W + X first, then adding Y:
```
    W: 1 0 1 0 1 0 1 0
    X: 1 1 0 0 1 0 1 0
    ---------------------
 W+X: 1 0 1 1 0 1 0 0
    Y: 1 1 1 1 0 1 0 1
    ---------------------
Final: 1 0 0 1 1 1 0 0 1
```

**Comparison:**
- Traditional addition requires sequential carry propagation through each bit position
- In our example, sequential addition requires two full propagations of carries
- Carry save addition performs the operation with only one carry propagation at the final stage
- For large numbers or multiple operands, CSA significantly reduces the delay time
- Especially efficient in hardware implementations like multipliers where multiple additions are needed

### Question 3
**Write down the steps needed to compute 5 × 6 using Booth's multiplication algorithm. For each step you should mention the rule used.**

#### Solution:

Booth's algorithm multiplies two signed binary numbers efficiently by encoding the multiplier.

For 5 × 6:
- Multiplicand (M): 5₁₀ = 0101₂
- Multiplier (Q): 6₁₀ = 0110₂

**Step 1: Initialization**
- A (Accumulator) = 0000
- Q (Multiplier) = 0110
- M (Multiplicand) = 0101
- Q₋₁ (Extra bit) = 0
- Count = 4

**Step 2: First Iteration**
- Examine Q₀Q₋₁ = 00
- Rule: No operation (00 pattern)
- Arithmetic right shift: A, Q, Q₋₁ = 0000, 0110, 0 → 0000, 0011, 0
- Count = 3

**Step 3: Second Iteration**
- Examine Q₀Q₋₁ = 10
- Rule: A = A - M (10 pattern indicates -M)
- A = A - M = 0000 - 0101 = 1011
- Arithmetic right shift: A, Q, Q₋₁ = 1011, 0011, 0 → 1101, 1001, 1
- Count = 2

**Step 4: Third Iteration**
- Examine Q₀Q₋₁ = 11
- Rule: No operation (11 pattern)
- Arithmetic right shift: A, Q, Q₋₁ = 1101, 1001, 1 → 1110, 1100, 1
- Count = 1

**Step 5: Fourth Iteration**
- Examine Q₀Q₋₁ = 01
- Rule: A = A + M (01 pattern indicates +M)
- A = A + M = 1110 + 0101 = 0011
- Arithmetic right shift: A, Q, Q₋₁ = 0011, 1100, 0 → 0001, 1110, 0
- Count = 0

**Step 6: Final Result**
- The product is in A:Q = 0001 1110 = 30₁₀

Result: 5 × 6 = 30, which is correct.

**Rules used in Booth's algorithm:**
- Q₀Q₋₁ = 00 or 11: No operation (consecutive same digits)
- Q₀Q₋₁ = 01: Add multiplicand to accumulator (transition from 0 to 1)
- Q₀Q₋₁ = 10: Subtract multiplicand from accumulator (transition from 1 to 0)
- After each operation, perform arithmetic right shift on A, Q, Q₋₁

### Question 4
**Discuss the concept of organization of an ALU. Draw a 1-bit ALU supporting AND, OR, NOR, Addition, Subtraction and set on less than instruction. Finally draw the 32-bit ALU supporting the above mentioned operations. Discuss how each operation is implemented with the explanation of control input.**

#### Solution:

**Concept of ALU Organization:**

An Arithmetic Logic Unit (ALU) is a fundamental building block of the CPU that performs arithmetic and logical operations. The ALU organization consists of:

1. **Input Registers**: Hold the operands for operations
2. **Control Unit**: Decodes operation codes and generates control signals
3. **Arithmetic Unit**: Performs arithmetic operations (add, subtract, etc.)
4. **Logic Unit**: Performs logical operations (AND, OR, NOT, etc.)
5. **Status Flags**: Store information about the result (zero, carry, overflow, etc.)
6. **Output Register**: Holds the result of the operation

**1-bit ALU Design:**

```
                  ┌─────────┐
                  │ Control │
                  │ Logic   │
                  └────┬────┘
                       │
                       ▼ Control signals
         A ────┬───────┬───────┬───────┐
               │       │       │       │
               ▼       ▼       ▼       ▼
         B ───►AND    OR     NOR     Adder◄── Cin
               │       │       │       │
               │       │       │       │
               └───┐   └───┐   └───┐   │
                   │       │       │   │ Cout
                   │       │       │   │
                   ▼       ▼       ▼   ▼
                  ┌─────────────────────┐
                  │     MUX (4:1)       │
                  └──────────┬──────────┘
                             │
                             ▼
                           Result
```

**32-bit ALU Design:**

A 32-bit ALU is constructed by connecting 32 1-bit ALUs with appropriate carry propagation. The control signals are shared across all bit positions.

```
  A[31:0] ─────┬─────────┬─────────┬─────────┐
               │         │         │         │
               ▼         ▼         ▼         ▼
  B[31:0] ────►1-bit    1-bit    1-bit     1-bit
               ALU[31]   ALU[30]  ALU[1]    ALU[0]
               │         │         │         │
               └─────────┴────┬────┴─────────┘
                             │
                             ▼
                        Result[31:0]
```

**Operation Implementation with Control Inputs:**

For a 32-bit ALU, we need at least 3 control lines to select between 6 operations:

| Operation    | Control[2:0] | Implementation Details |
|--------------|--------------|------------------------|
| AND          | 000          | Bitwise AND of A and B |
| OR           | 001          | Bitwise OR of A and B |
| NOR          | 010          | Bitwise NOR of A and B |
| Addition     | 011          | A + B with carry propagation |
| Subtraction  | 100          | A - B (implemented as A + ~B + 1) |
| Set-on-less  | 101          | Sets result to 1 if A < B, otherwise 0 |

**Implementation Details:**
1. **AND/OR/NOR**: Direct implementation using logic gates
2. **Addition**: Uses full adders with carry propagation
3. **Subtraction**: Inverts B and adds 1 (two's complement)
4. **Set-on-less-than (SLT)**: 
   - Subtracts B from A
   - Examines the most significant bit of the result (sign bit)
   - Sets output to 1 if the sign bit is 1 (A < B), otherwise 0
   - Only the least significant bit of the result is meaningful

The control inputs determine which operation's result is selected by the multiplexer at each bit position. Additional control may be needed for operations like shifting or rotating.

### Question 5
**Write on PC-relative and pseudo-direct addressing.**

#### Solution:

### PC-Relative Addressing

**Definition:**
PC-relative addressing is an addressing mode where the effective address is determined by adding an offset (displacement) to the current Program Counter (PC) value. The offset is typically provided in the instruction.

**Format:**
```
Effective Address = PC + Offset
```

**Characteristics:**
1. **Position Independence**: Code can be loaded and executed at any memory location without modification
2. **Compact Code**: Requires less bits to represent addresses since only the offset is stored
3. **Commonly Used For**: Branch and jump instructions, accessing local data
4. **Range Limitation**: Limited by the size of the offset field in the instruction

**Advantages:**
1. **Relocatable Code**: Supports position-independent code
2. **Efficient Memory Usage**: Smaller instruction size
3. **Simplified Linking**: Easy to link modules without address translation
4. **Cache Efficiency**: Promotes code locality

**Disadvantages:**
1. **Limited Range**: Can only address locations within offset range
2. **Additional Computation**: Requires addition to calculate effective address

**Example:**
If PC = 0x1000 and a branch instruction has an offset of +20 (0x14), the target address would be 0x1014.

### Pseudo-Direct Addressing

**Definition:**
Pseudo-direct addressing is a hybrid addressing mode where part of an absolute address is specified in the instruction, and the remaining high-order bits are taken from the PC. This allows for larger address spaces than pure PC-relative addressing.

**Format:**
```
Effective Address = (PC & HIGH_BITS_MASK) | (Offset << 2)
```
Where HIGH_BITS_MASK preserves the high-order bits of the PC, and the offset is shifted left to accommodate word or byte alignment.

**Characteristics:**
1. **Extended Range**: Can address locations in a larger region around the current PC
2. **Common in RISC**: Used in architectures like MIPS for jump instructions
3. **Semi-Position Independence**: Code can be relocated within the same memory segment

**Advantages:**
1. **Larger Addressable Range**: Than pure PC-relative addressing
2. **Compact Representation**: More efficient than full absolute addressing
3. **Simplified Hardware**: Easier implementation than full 32-bit addressing

**Disadvantages:**
1. **Limited to Current Segment**: Cannot jump between distant memory segments
2. **Not Fully Position Independent**: May require relocation if moved to a different segment

**Example in MIPS:**
In MIPS architecture, the j (jump) instruction uses pseudo-direct addressing:
- 26-bit address field is shifted left by 2 bits (for word alignment)
- The upper 4 bits are taken from the PC
- This creates a 32-bit address within the same 256MB segment

**Comparison:**
- PC-relative addressing is more position-independent but has a smaller range
- Pseudo-direct addressing offers a larger range but is constrained to the current memory segment
- Both are more compact than absolute addressing, which would require the full address to be encoded in the instruction

### Question 6
**Write the MIPS instructions for the following code segment:**
```
i=0;
k=3;
while(i<4) {
  save[i] = k*save[i];
  i++;
  k=5;
}
```

#### Solution:

Assuming:
- `i` is in register `$s0`
- `k` is in register `$s1`
- Base address of array `save` is in register `$s2`

MIPS Instructions:
```assembly
# Initialize variables
li    $s0, 0         # i = 0
li    $s1, 3         # k = 3

loop:
# Check loop condition (i < 4)
slti  $t0, $s0, 4    # $t0 = (i < 4) ? 1 : 0
beq   $t0, $zero, exit  # if not (i < 4), exit loop

# Calculate address of save[i]
sll   $t1, $s0, 2    # $t1 = i * 4 (multiply by 4 for word offset)
add   $t1, $t1, $s2  # $t1 = address of save[i]

# Load save[i]
lw    $t2, 0($t1)    # $t2 = save[i]

# Multiply by k
mul   $t2, $t2, $s1  # $t2 = k * save[i]

# Store result back to save[i]
sw    $t2, 0($t1)    # save[i] = k * save[i]

# Increment i
addi  $s0, $s0, 1    # i++

# Set k = 5
li    $s1, 5         # k = 5

# Jump back to start of loop
j     loop

exit:
# End of program
```

### Question 7
**Show the MIPS instruction format for each of the following instruction and then derive the decimal representation:**

**(1) add $s1, $s2, $s3    [opcode = 0 and funct = 32]**
**(2) sw $t0, 300($t1)     [opcode = 43]**
**(3) bne $s1, $s2, 100    [opcode = 5]**

#### Solution:

**MIPS Instruction Format Types:**
- R-format: For register operations (op, rs, rt, rd, shamt, funct)
- I-format: For immediate and memory operations (op, rs, rt, immediate)
- J-format: For jump operations (op, address)

**(1) add $s1, $s2, $s3    [opcode = 0 and funct = 32]**

This is an R-format instruction:
- opcode = 0 (6 bits): 000000
- rs = $s2 = 18 (5 bits): 10010
- rt = $s3 = 19 (5 bits): 10011
- rd = $s1 = 17 (5 bits): 10001
- shamt = 0 (5 bits): 00000
- funct = 32 (6 bits): 100000

Instruction format: `000000 10010 10011 10001 00000 100000`

Binary: 00000010010100111000100000100000
Hexadecimal: 0x02538020
Decimal: 38797344

**(2) sw $t0, 300($t1)     [opcode = 43]**

This is an I-format instruction:
- opcode = 43 (6 bits): 101011
- rs = $t1 = 9 (5 bits): 01001
- rt = $t0 = 8 (5 bits): 01000
- immediate = 300 (16 bits): 0000000100101100

Instruction format: `101011 01001 01000 0000000100101100`

Binary: 10101101001010000000000100101100
Hexadecimal: 0xAD28012C
Decimal: 2906087724

**(3) bne $s1, $s2, 100    [opcode = 5]**

This is an I-format instruction. For branch instructions, the immediate value is the offset in words (so we need to divide by 4), and it's relative to the PC+4 location:
- opcode = 5 (6 bits): 000101
- rs = $s1 = 17 (5 bits): 10001
- rt = $s2 = 18 (5 bits): 10010
- immediate = 100/4 = 25 (16 bits): 0000000000011001

Instruction format: `000101 10001 10010 0000000000011001`

Binary: 00010110001100100000000000011001
Hexadecimal: 0x16320019
Decimal: 372244505

**For (2) and (3) mention how memory address is calculated:**

**(2) sw $t0, 300($t1)**
The memory address is calculated as:
Memory address = Content of $t1 + 300

**(3) bne $s1, $s2, 100**
The branch target address is calculated as:
Target address = PC + 4 + (100 * 4)
(where PC is the address of the branch instruction itself, 4 is added to get to the next instruction, and the immediate value is multiplied by 4 since MIPS addresses are byte addresses but the offset is in words)

### Question 8
**Discuss the necessity of normalization and bias in floating point representation. Find the normalized binary representation of the following number using IEEE-754 32 bit floating point format.**

**-23.875**

#### Solution:

**Necessity of Normalization in Floating Point:**

1. **Unique Representation**: Normalization ensures every number has a unique representation, avoiding ambiguity
2. **Maximizing Precision**: By shifting the binary point to have exactly one non-zero digit before it, we maximize the number of significant digits that can be stored
3. **Simplified Comparison**: Makes comparing numbers easier as they follow a standard format
4. **Efficient Hardware**: Simplifies hardware implementation for arithmetic operations

**Necessity of Bias in Floating Point:**

1. **Representation of Negative Exponents**: Allows both negative and positive exponents to be represented using unsigned integers
2. **Simplified Comparison**: Makes comparison of floating-point numbers simpler (as unsigned integers)
3. **Avoiding Signed Zero in Exponent**: Prevents complications with signed zeros in the exponent field
4. **Hardware Efficiency**: Makes hardware implementation more straightforward by using unsigned arithmetic

**IEEE-754 32-bit Format:**
- 1 bit for sign
- 8 bits for exponent (with bias of 127)
- 23 bits for mantissa (with implied leading 1)

**Converting -23.875 to IEEE-754 32-bit Format:**

**Step 1: Determine the sign bit**
- The number is negative, so sign bit = 1

**Step 2: Convert the absolute value to binary**
- |23.875| = 23.875
- Integer part: 23₁₀ = 10111₂
- Fractional part: 0.875₁₀
  - 0.875 × 2 = 1.75 → 1
  - 0.75 × 2 = 1.5 → 1
  - 0.5 × 2 = 1.0 → 1
  - So 0.875₁₀ = 0.111₂
- Combined: 23.875₁₀ = 10111.111₂

**Step 3: Normalize the binary representation**
- Move the binary point to have one digit before it: 1.0111111₂ × 2⁴
- Exponent: 4

**Step 4: Calculate the biased exponent**
- Biased exponent = actual exponent + bias = 4 + 127 = 131₁₀ = 10000011₂

**Step 5: Determine the mantissa**
- The mantissa is the fractional part after normalization (without the leading 1):
- 0111111₂ (padded with zeros to 23 bits): 01111110000000000000000₂

**Step 6: Combine the parts**
- Sign bit: 1
- Biased exponent: 10000011
- Mantissa: 01111110000000000000000

**IEEE-754 32-bit representation of -23.875:**
1 10000011 01111110000000000000000

In hexadecimal: 0xC1BF0000
