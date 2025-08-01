# Computer Organization and Design Exam Solutions
*Based on Patterson & Hennessy: Computer Organization and Design*

## Question 1

### a) Carry Save Adder Advantages (2+3=5 marks)

**Advantages of Carry Save Adder:**
1. **Parallel Processing**: Multiple additions can be performed simultaneously without waiting for carry propagation
2. **Reduced Delay**: Fixed delay of 2 gate delays regardless of operand width
3. **Efficient for Multiple Operands**: Ideal when adding more than two numbers

**Carry Save Addition Example:**
- W = 10011110 (158 in decimal)
- X = 10011011 (155 in decimal)  
- Y = 11101101 (237 in decimal)

**Step 1**: Partial sum without carry propagation
```
  10011110 (W)
  10011011 (X)
+ 11101101 (Y)
-----------
Sum bits:   01111000
Carry bits: 11100111 (shifted left)
```

**Step 2**: Add sum and carry using conventional adder
```
  01111000
+ 111001110
-----------
 1000110110 (550 in decimal)
```

**Comparison with Traditional Addition:**
Traditional addition would require sequential carry propagation through each bit position, taking O(n) time. Carry save addition reduces this to constant time for the initial stage plus one final conventional addition.

### b) Booth's Multiplication Advantage (2+5=7 marks)

**Advantages of Booth's Algorithm:**
1. **Handles Signed Numbers**: Works directly with two's complement representation
2. **Reduces Partial Products**: Converts sequences of 1s into single subtract-add operations
3. **More Efficient**: Fewer operations for numbers with consecutive 1s or 0s

**Booth's Multiplication: 4 × 7**
- 4 = 0100, 7 = 0111
- Extend 7 with leading bit and trailing 0: 00111**0**

**Booth recoding (examining bit pairs from right):**
- Bits 10: +1 operation (add multiplicand)
- Bits 11: 0 operation (no change)
- Bits 11: 0 operation (no change)  
- Bits 01: -1 operation (subtract multiplicand)

**Step-by-step execution:**
```
Initial: 0000 0000
Step 1: Add 4    → 0000 0100
Step 2: Shift    → 0000 0010
Step 3: No op    → 0000 0010
Step 4: Shift    → 0000 0001
Step 5: No op    → 0000 0001
Step 6: Shift    → 0000 0000 (with carry)
Step 7: Sub 4    → 1111 1100
Final result: 00011100 = 28
```

### c) Non-Restoring Division Algorithm Advantages (2 marks)

**Advantages:**
1. **No Restoration Step**: Eliminates the need to restore the remainder after unsuccessful subtraction
2. **Faster Execution**: Reduces the number of operations per iteration
3. **Simplified Control**: Uses the sign of the remainder to determine next operation

## Question 2

### a) IEEE-754 Floating Point Addition: 0.5 + (-0.4375) (4+2=6 marks)

**Step 1: Convert to IEEE-754 32-bit format**
- 0.5 = 0.1₂ = 1.0 × 2⁻¹
  - Sign: 0, Exponent: 126 (127-1), Mantissa: 000...000
  - Binary: 00111111000000000000000000000000

- -0.4375 = -0.0111₂ = -1.11 × 2⁻²
  - Sign: 1, Exponent: 125 (127-2), Mantissa: 110...000
  - Binary: 10111110110000000000000000000000

**Step 2: Align exponents** (shift smaller to match larger)
- 0.5: 1.000 × 2⁻¹
- -0.4375: -0.111 × 2⁻¹ (shifted right)

**Step 3: Perform mantissa operation**
- 1.000 - 0.111 = 0.001₂

**Step 4: Normalize result**
- 0.001₂ = 1.0 × 2⁻⁴
- Result: 0.0625
- IEEE format: 00111101100000000000000000000000

### b) Spatial vs Temporal Expansion in ALU (4 marks)

**Spatial Expansion:**
- Physical replication of hardware units
- Multiple ALU units operating in parallel
- Higher area cost but better throughput
- Example: Multiple execution units in superscalar processors

**Temporal Expansion:**
- Time-multiplexed use of single hardware unit
- Sequential operations on same hardware
- Lower area cost but higher latency
- Example: Single ALU handling multiple operations in sequence

### c) 1-bit ALU Design for AND, NOR, NAND, Addition (4 marks)

**Control Signals:**
- Op[1:0]: Operation select (00=AND, 01=NOR, 10=NAND, 11=ADD)
- CarryIn: Input carry for addition

**Circuit Components:**
```
Inputs: A, B, CarryIn, Op[1:0]
Outputs: Result, CarryOut

AND gate: A & B
NOR gate: ~(A | B)  
NAND gate: ~(A & B)
Full Adder: Sum = A ⊕ B ⊕ CarryIn, CarryOut = AB + CarryIn(A⊕B)

4:1 MUX selects output based on Op[1:0]
```

## Question 3

### a) MIPS Instruction Formats and Decimal Representation (4+3=7 marks)

**(1) sub $t1, $s3, $s5 [opcode = 0, funct = 34]**
- Type: R-format
- op(6) | rs(5) | rt(5) | rd(5) | shamt(5) | funct(6)
- 000000 | 10011 | 10101 | 01001 | 00000 | 100010
- Decimal: 0x02954822 = 43345954

**(2) lw $t1, 150($t0) [opcode = 35]**
- Type: I-format  
- op(6) | rs(5) | rt(5) | immediate(16)
- 100011 | 01000 | 01001 | 0000000010010110
- Addressing mode: Base + displacement
- Decimal: 0x8D090096 = 2365783958

**(3) beq $s3, $s4, 200 [opcode = 4]**
- Type: I-format
- op(6) | rs(5) | rt(5) | immediate(16) 
- 000100 | 10011 | 10100 | 0000000011001000
- Addressing mode: PC-relative
- Decimal: 0x127400C8 = 309067976

### b) Single Cycle Processor Circuit for lw and beq Instructions (3+4=7 marks)

**Key Components:**
1. **Instruction Memory**: Fetches instruction using PC
2. **Register File**: Reads source registers, writes destination
3. **ALU**: Computes addresses and comparisons
4. **Data Memory**: Accessed for load/store operations
5. **Control Unit**: Generates control signals

**Control Signals for lw:**
- RegWrite = 1, MemRead = 1, MemtoReg = 1, ALUSrc = 1
- Jump = 0, Branch = 0, RegDst = 0

**Control Signals for beq:**
- Branch = 1, ALUSrc = 0, ALUOp = 01 (subtraction)
- RegWrite = 0, MemRead = 0, MemWrite = 0

## Question 4

### a) ARM Assembly Code (5 marks)

```arm
    ; Variables a and b assigned to registers r1 and r2
    
loop:
    CMP r1, #0        ; Compare a with 0
    BEQ end_loop      ; Branch if a == 0
    
    CMP r1, r2        ; Compare a with b  
    BGT else_part     ; Branch if a > b
    
    SUB r1, r1, r2    ; a = a - b
    B loop            ; Branch back to loop
    
else_part:
    ADD r2, r2, r1    ; b = a + b
    B loop            ; Branch back to loop
    
end_loop:
    ; End of while loop
```

### b) RISC vs CISC Processors (4 marks)

**RISC (Reduced Instruction Set Computer):**
- Simple, uniform instruction format
- Load/store architecture
- Large register file
- Fixed instruction length
- Hardwired control
- Examples: ARM, MIPS

**CISC (Complex Instruction Set Computer):**
- Complex, variable instruction format  
- Memory-to-memory operations
- Smaller register file
- Variable instruction length
- Microcoded control
- Examples: x86, VAX

### c) Carry Look-ahead Adder (5 marks)

**Working Principle:**
Generates carry signals in parallel rather than sequentially using:
- Generate: Gi = Ai · Bi
- Propagate: Pi = Ai ⊕ Bi  
- Carry: Ci+1 = Gi + Pi · Ci

**Disadvantages:**
1. **Hardware Complexity**: Exponential increase in gate complexity with width
2. **Fan-in Limitations**: High fan-in requirements for wide adders
3. **Routing Complexity**: Complex interconnections for carry signals
4. **Power Consumption**: Higher power due to increased gate count

## Question 5

### a) Delayed Branching Strategies (2+3=5 marks)

**Delayed Branching:**
A technique where the instruction following a branch is always executed regardless of branch outcome, eliminating pipeline stalls.

**Implementation Strategies:**
1. **Compiler Optimization**: Move useful instruction into delay slot
2. **NOP Insertion**: Insert no-operation if no suitable instruction found
3. **Branch Prediction**: Predict likely path and fill delay slot accordingly

### b) Combinational Array Multiplier for X × Y (4 marks)

For X = x₃x₂x₁x₀ and Y = y₃y₂y₁y₀:

**Circuit Structure:**
- Array of AND gates for partial product generation
- Array of full adders for partial product summation
- Each row handles one bit of multiplier
- Carries propagate diagonally downward and rightward

**Necessary Components:**
- 16 AND gates (4×4 partial products)
- 9 full adders for summation
- Appropriate interconnections for carry propagation

### c) Cache Memory Write Operations (4 marks)

**Write-Through:**
- **Pros**: Data consistency, simple recovery from failures
- **Cons**: Higher memory traffic, slower write operations

**Write-Back:**  
- **Pros**: Reduced memory traffic, faster write operations
- **Cons**: Complex coherency, risk of data loss

**Write-Around:**
- **Pros**: No cache pollution for non-temporal writes
- **Cons**: Subsequent reads miss in cache

## Question 6

### a) Machine Code Equivalent (4 marks)

For (A*B+C)/(A-B*C):

**Assuming stack-based architecture:**
```
LOAD A      ; Push A
LOAD B      ; Push B  
MUL         ; A*B
LOAD C      ; Push C
ADD         ; A*B+C
LOAD A      ; Push A
LOAD B      ; Push B
LOAD C      ; Push C
MUL         ; B*C
SUB         ; A-B*C
DIV         ; (A*B+C)/(A-B*C)
```

### b) Single Cycle Processor Datapath for STORE (5 marks)

**Key Datapath Components Highlighted:**
1. **Instruction Memory** → **Control Unit**
2. **Register File** → **ALU** (for address calculation)
3. **ALU** → **Data Memory** (address input)
4. **Register File** → **Data Memory** (write data input)
5. **Control signals**: MemWrite, ALUSrc, RegWrite=0

**Control Signal Values:**
- MemWrite = 1, MemRead = 0, RegWrite = 0
- ALUSrc = 1 (immediate for offset)

### c) Load Hazard Avoidance Code (5 marks)

**Original Code:**
```
a = b - c;
d = e - f;
```

**Optimized Assembly (avoiding load hazards):**
```mips
lw   $t1, b      ; Load b
lw   $t2, c      ; Load c  
lw   $t3, e      ; Load e (fill delay slot)
lw   $t4, f      ; Load f (fill delay slot)
sub  $t0, $t1, $t2    ; a = b - c (no stall)
sub  $t5, $t3, $t4    ; d = e - f (no stall)
sw   $t0, a      ; Store a
sw   $t5, d      ; Store d
```

## Question 7

### a) Programmed I/O vs Interrupt Driven I/O (5 marks)

**Programmed I/O:**
- CPU continuously polls device status
- Simple implementation
- Wastes CPU cycles during I/O operations
- Synchronous operation
- Lower overhead per transfer

**Interrupt Driven I/O:**
- Device interrupts CPU when ready
- CPU can perform other tasks while waiting
- Higher overhead per transfer due to context switching
- Asynchronous operation  
- Better CPU utilization

### b) MIMD Architecture Models (3 marks)

**Shared Memory MIMD:**
- Multiple processors share common memory space
- Communication through shared variables
- Examples: SMP, NUMA systems
- Simpler programming model but scalability limits

**Distributed Memory MIMD:**
- Each processor has private memory
- Communication through message passing
- Examples: Cluster systems, MPP machines
- Better scalability but complex programming

### c) Direct Memory Access (DMA) (2+4=6 marks)

**Direct Memory Access:**
Allows I/O devices to transfer data directly to/from memory without CPU intervention.

**DMA Controller Operation with Processor/Memory/I/O:**

```
[Processor] ←→ [System Bus] ←→ [Memory]
     ↑              ↑
     ↓              ↓  
[DMA Controller] ←→ [I/O Device]
```

**Operation Steps:**
1. **Setup**: CPU programs DMA controller with source, destination, and count
2. **Transfer**: DMA controller takes control of bus and transfers data
3. **Completion**: DMA controller interrupts CPU when transfer complete
4. **Bus Arbitration**: DMA controller and CPU share bus access through arbitration

**Advantages:**
- Reduced CPU overhead
- Higher throughput for bulk transfers
- Concurrent CPU and I/O operations
