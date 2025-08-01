# Computer Architecture Solutions (Patterson Reference)

## Question 1a: Booth's Algorithm for 19 × 9 (8 marks)

**Booth's Algorithm Process:**

Booth's algorithm is more efficient than repeated addition as it reduces the number of operations by using bit patterns to determine add, subtract, or shift operations.

**Step-by-step multiplication of 19 × 9:**

Initial setup:
- Multiplicand (M): 19 = 010011 (6-bit)
- Multiplier (Q): 9 = 001001 (6-bit)  
- Q₋₁ = 0 (initially)
- A = 000000 (accumulator, 6-bit)

| Step | A | Q | Q₋₁ | Q₀Q₋₁ | Operation | Comments |
|------|---|---|-----|-------|-----------|----------|
| 0 | 000000 | 001001 | 0 | 10 | A = A - M | Q₀Q₋₁ = 10, subtract |
| 1 | 101101 | 001001 | 0 | - | Arithmetic shift right | |
| 1 | 110110 | 100100 | 1 | 01 | A = A + M | Q₀Q₋₁ = 01, add |
| 2 | 001001 | 100100 | 1 | - | Arithmetic shift right | |
| 2 | 000100 | 110010 | 0 | 00 | No operation | Q₀Q₋₁ = 00, shift only |
| 3 | 000010 | 011001 | 0 | 10 | A = A - M | Q₀Q₋₁ = 10, subtract |
| 4 | 101001 | 011001 | 0 | - | Arithmetic shift right | |
| 4 | 110100 | 101100 | 1 | 01 | A = A + M | Q₀Q₋₁ = 01, add |
| 5 | 001111 | 101100 | 1 | - | Arithmetic shift right | |
| 5 | 000111 | 110110 | 0 | 00 | No operation | Q₀Q₋₁ = 00, shift only |
| 6 | 000011 | 111011 | 0 | - | Final result | |

**Final Result:** A,Q = 000011111011 = 171 (decimal) ✓

**Why Booth's algorithm is more popular:**
- Reduces number of additions/subtractions
- Handles negative numbers naturally using 2's complement
- More efficient for sparse bit patterns
- Hardware implementation is straightforward

## Question 1b: IEEE-754 Single Precision Conversion of -9.375 (6 marks)

**Converting -9.375 to IEEE-754 single precision:**

**Step 1:** Convert to binary
- 9.375 = 1001.011₂
- Negative sign: Sign bit = 1

**Step 2:** Normalize
- 1001.011₂ = 1.001011 × 2³
- Mantissa: 001011 (implicit leading 1)
- Exponent: 3

**Step 3:** Calculate biased exponent
- Bias = 127 (for single precision)
- Biased exponent = 3 + 127 = 130 = 10000010₂

**Step 4:** IEEE-754 format (32-bit)
- Sign: 1
- Exponent: 10000010
- Mantissa: 00101100000000000000000 (23 bits)

**Final IEEE-754 representation:**
**11000001000101100000000000000000**

**8-bit fixed-point with 4 fractional bits:**
- Range: -8.0 to +7.9375
- Precision: 0.0625 (2⁻⁴)
- Cannot represent -9.375 (overflow)

## Question 2a: Floating Point Unit Design (5 marks)

**FPU for Addition and Subtraction Architecture:**

```
Input A (32-bit) ──┐
                   ├── Sign Logic ──┐
Input B (32-bit) ──┘                │
                                    │
Input A ──┐                         │
          ├── Exponent Compare ─────┼── Control Logic
Input B ──┘                         │
                                    │
Input A ──┐                         │
          ├── Mantissa Align ───────┼── Mantissa ALU
Input B ──┘                         │
                                    │
                                    └── Normalize & Round ── Output (32-bit)
```

**Key Components:**
1. **Exponent Comparator:** Determines alignment shift
2. **Mantissa Shifter:** Aligns smaller operand
3. **Mantissa Adder/Subtractor:** Performs arithmetic
4. **Normalizer:** Adjusts result format
5. **Rounder:** Handles precision

## Question 2b: Finite State Machine (FSM) (4 marks)

**Finite State Machine (FSM):**

An FSM is a computational model consisting of:
- **States:** Discrete conditions or situations
- **Transitions:** Rules for moving between states
- **Inputs:** External signals that trigger transitions
- **Outputs:** Actions or signals produced

**Types:**
- **Moore Machine:** Output depends only on current state
- **Mealy Machine:** Output depends on current state and input

**Applications in Computer Architecture:**
- Control unit design
- Cache coherence protocols
- Memory controllers
- I/O controllers

## Question 2c: Digital Lock FSM with Moore and Mealy (5 marks)

**Sequence: CSEDU**

**Moore Machine State Diagram:**
```
[IDLE] --C--> [C] --S--> [CS] --E--> [CSE] --D--> [CSED] --U--> [UNLOCK]
  ↑                                                              │
  └─────────────────── Any wrong input ──────────────────────────┘
```

**Mealy Machine State Diagram:**
```
[S0] --C--> [S1] --S--> [S2] --E--> [S3] --D--> [S4] --U/UNLOCK--> [S0]
 ↑                                                                   │
 └─────────────── Any wrong input/LOCK ──────────────────────────────┘
```

**State Transition Table (Moore):**

| Current State | Input | Next State | Output |
|---------------|-------|------------|--------|
| IDLE | C | C | 0 |
| IDLE | Other | IDLE | 0 |
| C | S | CS | 0 |
| C | Other | IDLE | 0 |
| CS | E | CSE | 0 |
| CS | Other | IDLE | 0 |
| CSE | D | CSED | 0 |
| CSE | Other | IDLE | 0 |
| CSED | U | UNLOCK | 1 |
| CSED | Other | IDLE | 0 |

## Question 3a: RISC vs CISC Processors (4 marks)

**RISC (Reduced Instruction Set Computer):**
- Simple, uniform instructions
- Fixed instruction length
- Register-to-register operations
- Hardwired control
- **Example:** ARM Cortex-A series, MIPS

**CISC (Complex Instruction Set Computer):**
- Complex, variable-length instructions
- Memory-to-memory operations
- Microcoded control
- Rich addressing modes
- **Example:** Intel x86, IBM System/360

**Key Differences:**
- **Instruction Complexity:** RISC simple vs CISC complex
- **Execution Time:** RISC uniform vs CISC variable
- **Compiler Complexity:** RISC higher vs CISC lower
- **Hardware Complexity:** RISC simpler vs CISC complex

## Question 3b: Program Relocation Addressing Modes (5 marks)

**Addressing modes suitable for program relocation:**

1. **PC-Relative Addressing:**
   - Address = PC + displacement
   - Code remains position-independent
   - Used for branches and procedure calls

2. **Base Register Addressing:**
   - Address = Base register + displacement
   - Base register points to program start
   - All references relative to base

3. **Indexed Addressing:**
   - Address = Base + Index + displacement
   - Allows dynamic address calculation
   - Supports array and structure access

4. **Indirect Addressing:**
   - Address stored in memory location
   - Enables dynamic binding
   - Supports function pointers and virtual functions

**Why these modes help:**
- Programs can execute at any memory location
- No absolute addresses in code
- Runtime address binding possible

## Question 3c: Cache Memory Types (5 marks)

**Associate-Mapped Cache:**
- Any block can be placed in any cache line
- Requires full address comparison
- **Advantages:** No conflict misses, flexible placement
- **Disadvantages:** Complex hardware, expensive comparators

**Set-Associate Mapped Cache:**
- Combines direct and associate mapping
- Block can be placed in any line within a specific set
- Set = (Block address) mod (Number of sets)
- **Advantages:** Reduces conflict misses, reasonable complexity
- **Disadvantages:** Still some conflict misses possible

**N-way Set-Associate:**
- Each set contains N blocks
- Common configurations: 2-way, 4-way, 8-way
- Trade-off between complexity and performance

## Question 4a: Pipelined Architecture (6 marks)

**Pipelined Architecture:**

A technique where multiple instructions are overlapped in execution, similar to an assembly line.

**5-Stage RISC Pipeline:**

```
Stage 1: IF (Instruction Fetch)
Stage 2: ID (Instruction Decode)
Stage 3: EX (Execute)
Stage 4: MEM (Memory Access)
Stage 5: WB (Write Back)
```

**Internal Architecture Diagram:**

```
IF Stage:    [PC] → [Instruction Memory] → [IF/ID Register]
                ↓
ID Stage:    [IF/ID] → [Register File] → [ID/EX Register]
                      [Control Unit]
                ↓
EX Stage:    [ID/EX] → [ALU] → [EX/MEM Register]
                ↓
MEM Stage:   [EX/MEM] → [Data Memory] → [MEM/WB Register]
                ↓
WB Stage:    [MEM/WB] → [Register File]
```

**Advantages over Non-pipelined:**
- **Higher Throughput:** One instruction completed per cycle (ideally)
- **Better Resource Utilization:** All stages work simultaneously
- **Improved Performance:** CPI approaches 1
- **Latency vs Throughput:** Individual instruction latency same, but overall throughput increases

## Question 4b: Pipeline Hazards (4 marks)

**True Data Dependency:**
- Instruction depends on result of previous instruction
- Example: ADD R1,R2,R3; SUB R4,R1,R5
- R1 written by ADD, read by SUB
- **Impact:** Pipeline stall or forwarding needed

**Resource Conflicts:**
- Multiple instructions need same hardware resource
- Example: Memory port conflict between IF and MEM stages
- **Impact:** Pipeline stall until resource available

## Question 4c: Data Forwarding in Pipeline (4 marks)

**Data Forwarding:**

Technique to reduce pipeline stalls by forwarding results from later pipeline stages to earlier stages before they're written to registers.

**Implementation:**
- **EX/MEM → EX:** Forward ALU result to next ALU operation
- **MEM/WB → EX:** Forward memory load result to ALU
- **MEM/WB → ID:** Forward result to instruction decode

**Benefits:**
- Eliminates many data hazard stalls
- Maintains pipeline efficiency
- Reduces overall execution time

## Question 5a: Multi-level Cache Memory System (6 marks)

**Given Specifications:**
- L1 I-cache miss rate: 3%
- L1 D-cache miss rate: 8%
- 40% instructions reference data
- L2 miss rate: 4%
- L2 time: 10 clock cycles
- Memory access time: 80 clock cycles
- Base CPI: 2
- CPU Clock rate: 4GHz

**i. Calculate average CPI:**

**Memory Access Analysis:**
- Instruction fetch: 100% of instructions
- Data access: 40% of instructions

**L1 Cache Penalties:**
- L1 I-cache penalty = 3% × 10 cycles = 0.3 cycles/instruction
- L1 D-cache penalty = 40% × 8% × 10 cycles = 0.32 cycles/instruction

**L2 Cache Penalties:**
- L2 I-miss penalty = 3% × 4% × 80 cycles = 0.096 cycles/instruction
- L2 D-miss penalty = 40% × 8% × 4% × 80 cycles = 0.1024 cycles/instruction

**Average CPI:**
CPI = Base CPI + L1 penalties + L2 penalties
CPI = 2 + 0.3 + 0.32 + 0.096 + 0.1024 = **2.8184**

**ii. Which modification will be better:**

**Option A: Faster L2 of 5 clock cycles**
- New L2 penalties = (0.096 + 0.1024) × (5/10) = 0.0992
- New L2 memory penalties = (0.096 + 0.1024) × (75/80) = 0.186
- New CPI = 2 + 0.62 + 0.0992 + 0.186 = 2.9052

**Option B: Larger L2 with 2% miss rate**
- New L2 penalties = (0.096 + 0.1024) × (2/4) = 0.0992
- New memory penalties = (0.096 + 0.1024) × (2/4) × (80/80) = 0.0992
- New CPI = 2 + 0.62 + 0.0992 = 2.7192

**Answer:** Option B (larger L2 with 2% miss rate) is better.

## Question 5b: Direct Mapped Cache Problem (6 marks)

**Given Parameters:**
- Main memory: 4MB, Byte addressable
- Block size: 16 Bytes
- Cache capacity: 2KB, Direct mapped

**Memory accesses:** 49, 65, 97, 4144, 4160, 4192, 48, 65, 98
**Cache initially contains blocks 0 to 5**

**Cache Organization:**
- Cache lines = 2KB / 16B = 128 lines
- Block address = Byte address / 16
- Cache line = Block address mod 128

**Access Analysis:**

| Access | Byte Addr | Block Addr | Cache Line | Hit/Miss | Action |
|--------|-----------|------------|------------|----------|---------|
| 49 | 49 | 3 | 3 | Hit | Block 3 present |
| 65 | 65 | 4 | 4 | Hit | Block 4 present |
| 97 | 97 | 6 | 6 | Miss | Load block 6, replace block 6 |
| 4144 | 4144 | 259 | 3 | Miss | Load block 259, replace block 3 |
| 4160 | 4160 | 260 | 4 | Miss | Load block 260, replace block 4 |
| 4192 | 4192 | 262 | 6 | Miss | Load block 262, replace block 6 |
| 48 | 48 | 3 | 3 | Miss | Load block 3, replace block 259 |
| 65 | 65 | 4 | 4 | Miss | Load block 4, replace block 260 |
| 98 | 98 | 6 | 6 | Miss | Load block 6, replace block 262 |

**(i) Hit ratio:** 2/9 = 22.22%

**(ii) Final cache state:**
- Line 0: Block 0
- Line 1: Block 1  
- Line 2: Block 2
- Line 3: Block 3
- Line 4: Block 4
- Line 5: Block 5
- Line 6: Block 6

**(iii) Blocks replaced:** 6 blocks (original block 6, blocks 259, 260, 262, and reloaded blocks 3, 4)

## Question 5c: Cache Coherence (2 marks)

**Cache Coherence:**

The property that ensures all processors in a multiprocessor system have a consistent view of memory. When one processor modifies a memory location, all other processors must see the same updated value.

**Key Requirements:**
- **Write Propagation:** Writes must be visible to all processors
- **Write Ordering:** All processors must see writes in the same order

**Common Protocols:** MESI, MOESI, Directory-based protocols

## Question 6a: Control Unit Functions and Implementation (8 marks)

**Functions of Control Unit:**

1. **Instruction Fetch:** Generates addresses for instruction memory
2. **Instruction Decode:** Interprets instruction format and generates control signals
3. **Execution Control:** Coordinates ALU operations and data paths
4. **Memory Access Control:** Manages data memory read/write operations
5. **Register File Control:** Controls register read/write operations
6. **Exception Handling:** Manages interrupts and exceptions

**Microprogrammed Control Unit Implementation:**

```
[Instruction] → [Instruction Decoder] → [Microprogram Counter]
                                             ↓
[Control Store (ROM)] ← [Microprogram Counter]
                                             ↓
[Microinstruction Register] → [Control Signal Generator]
                                             ↓
                              [Control Signals to Datapath]
```

**Components:**
- **Control Store:** ROM containing microinstructions
- **Microprogram Counter:** Points to current microinstruction
- **Microinstruction Register:** Holds current microinstruction
- **Sequencing Logic:** Determines next microinstruction address

**Operation:**
1. Instruction opcode maps to microprogram starting address
2. Microprogram counter sequences through microinstructions
3. Each microinstruction generates control signals
4. Branch microinstructions handle conditional operations

## Question 6b: Hardwired vs Microprogrammed Control (2 marks)

**Hardwired Implementation:**
- Control logic implemented using combinational circuits
- Faster execution, fixed control logic
- Difficult to modify, less flexible

**Microprogrammed Implementation:**
- Control logic stored as microinstructions in ROM
- Slower execution, programmable control logic
- Easy to modify and extend, more flexible

## Question 6c: Processor Specifications and Microinstruction Format (4 marks)

**Given:**
- 16 registers (32-bit each)
- ALU: 16 logic + 16 arithmetic functions
- 8 operations, connected by internal bus
- 3 operand fields for addressing

**Microinstruction Format:**

**Horizontal Format:**
```
| ALU Func | Src1 | Src2 | Dest | Memory | Branch | Condition | Next Address |
|  5 bits  |4 bits|4 bits|4 bits| 3 bits | 2 bits |  3 bits   |   12 bits    |
```

**Vertical Format:**
```
| Operation Code | Operand 1 | Operand 2 | Operand 3 | Next Address |
|    8 bits      |  8 bits   |  8 bits   |  8 bits   |   8 bits     |
```

**Field Encoding:**
- ALU Function: 5 bits (32 functions)
- Register Address: 4 bits (16 registers)
- Memory Operations: 3 bits (8 operations)
- Branch Control: 2 bits (4 types)
- Condition Codes: 3 bits (8 conditions)

## Question 7a: I/O Module Block Diagram (2+6 marks)

**I/O Module Block Diagram:**

```
    CPU Bus Interface
           ↓
    [Address Decoder] → [Control Logic]
           ↓                    ↓
    [Data Register] ← → [Status Register]
           ↓                    ↓
    [I/O Interface Logic]
           ↓
    External Device Interface
```

**Input Block Data Techniques:**

1. **Programmed I/O:**
   - CPU directly controls I/O operations
   - Polling method to check device status
   - Simple but inefficient for large data blocks

2. **Interrupt-Driven I/O:**
   - Device interrupts CPU when ready
   - CPU responds to interrupt and transfers data
   - More efficient than polling

3. **Direct Memory Access (DMA):**
   - DMA controller handles data transfer
   - CPU initiates transfer, DMA completes it
   - Most efficient for large blocks

## Question 7b: DMA Controller Interface with CPU (2 marks)

**DMA-CPU Interface:**

```
CPU ←→ [System Bus] ←→ [DMA Controller] ←→ [I/O Device]
 ↓                           ↓
[Memory]                [DMA Registers]
```

**Control Signals:**
- **DREQ:** DMA Request from device
- **DACK:** DMA Acknowledge to device  
- **HRQ:** Hold Request to CPU
- **HLDA:** Hold Acknowledge from CPU

## Question 7c: Priority Interrupt Controller (2 marks)

**Priority Interrupt Controller Interface:**

```
[Interrupt Sources] → [Priority Encoder] → [Interrupt Controller] → [CPU]
                           ↓
                    [Interrupt Vector Table]
```

**Operation:**
- Multiple interrupt sources connected
- Priority encoder determines highest priority
- Controller sends interrupt vector to CPU
- CPU uses vector to jump to service routine

## Question 7d: DMA and Interrupt Breakpoints (2 marks)

**DMA Breakpoints:**
- Occur between instruction cycles
- CPU relinquishes bus control to DMA controller
- Memory access cycles stolen from CPU
- Transparent to instruction execution

**Interrupt Breakpoints:**
- Occur at instruction completion
- CPU saves context and jumps to interrupt handler
- Normal instruction flow disrupted
- Requires context save/restore operations

**Key Difference:** DMA breakpoints are transparent cycle-stealing, while interrupt breakpoints involve explicit program flow changes.
