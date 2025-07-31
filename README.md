# Computer Architecture and Organization - Complete Topics

## Lecture 01-02: Fixed-Point Arithmetic

### Addition and Subtraction
- Addition operations
- Subtraction operations

### Multiplication and Division
- Multiplication algorithms
- Division algorithms

### Half Adder
- Truth table and logic equations

### Full Adder
- Truth table and logic equations

### Serial Binary Adder
- Operation and characteristics

### Ripple Carry Adder
- Structure and limitations

### 2's Complement Adder-Subtracter
- Functionality and examples

### Overflow
- Detection and handling in unsigned and signed numbers

### Carry-Lookahead Adder
- Generate and propagate signals
- 4-bit implementation and expansion

### Carry-Save Adder
- Concept and application

## Lecture 03: Data Representation and Number Systems

### Basic Information Types
- Instruction
- Numbers
- Data
- Non-numerical data

### Word Length
- Bits
- Byte
- Halfword
- Word
- Double word

### Byte Storage
- Big-Endian methods
- Little-Endian methods

### Tags
- Purpose
- Advantages
- Disadvantages

### Error Detection and Correction
- Parity bit (even and odd parity)

### Fixed-Point Binary Numbers
- Unsigned representations
- Signed representations

### Signed Numbers
- Sign magnitude
- 1's complement
- 2's complement

### Decimal Codes
- BCD (Binary Coded Decimal)
- ASCII
- Excess-Three
- Two-out-of-Five

### Floating-Point Numbers
- Need for floating-point
- Basic format
- Representation
- Normalization
- IEEE 754 standard (32-bit and 64-bit formats)
- Biasing (excess-127 and excess-128)
- Conversion from decimal to binary floating-point
- Overflow and underflow

## Lecture 04: CPU Organization

### CPU Organization
- Instruction execution steps
- External communication (memory and I/O devices)
- Memory-mapped I/O vs. I/O-mapped I/O

### User and Supervisor Programs
- Roles and switching between them
- Interrupt handling

### CPU Operation
- Instruction cycle (fetch and execute steps)
- Micro operations and clock cycle time

### Accumulator-based CPU
- Structure and components (PCU, DPU, registers)
- Load and store operations
- Programming considerations (single-address instructions)

### Instruction Set
- Data transfer instructions
- Data processing instructions
- Program control instructions
- Example: Multiplication program

### Limitations of Accumulator-based CPU
- Register constraints
- Performance issues

## Lecture 05: Performance Analysis

### Performance Metrics
- Response time (execution time)
- Throughput
- Relative performance calculation

### Measuring Performance
- CPU time (user and system CPU time)
- CPU utilization

### Clock Cycles and CPU Time
- Clock period and rate
- CPI (cycles per instruction)
- IPC (instructions per cycle)
- CPU time equations

### Comparing Code Segments
- Instruction count
- CPI analysis
- Performance analysis

### Components Affecting CPU Performance
- Algorithm
- Programming language
- Compiler
- ISA (Instruction Set Architecture)

### Speedup Techniques
- Cache memory
- Pipelined processing
- Superscalar processing

### Sequential vs. Pipelined Processing
- Instruction fetch
- Decode
- Operand load
- Execution
- Operand store

## Lecture 06: Instruction Set Architecture

### Classifying Instruction Set
- CISC characteristics
- RISC characteristics

### Instruction Format
- Opcode fields
- Operand fields
- RISC1 instruction format

### Operand Extension
- Sign extension
- Zero extension

### Address Extension
- Base register
- Effective address

### Addressing Modes
- Immediate addressing
- Direct addressing
- Indirect addressing
- Relative addressing (advantages and drawbacks)
- Auto indexing (pre-decrementing and post-incrementing)
- Register direct addressing
- Register indirect addressing
- Register indirect with offset

## Lecture 07: Stack and Instruction Architecture

### Stack Control
- Push operations
- Pop operations
- Stack pointer (SP)

### Stack Control in Motorola 680X0
- Memory addressing modes for stack operations

### Number of Addresses in Instructions
- Three-address instructions
- Two-address instructions
- One-address instructions
- Examples for arithmetic operations

### Accumulator Architectures
- Pros and cons
- Example: AB - (A+BC)

### Zero Address Machine (Stack-Based Architecture)
- Implicit operand addressing
- Example: AB - (A+CB)

### Stack Architecture: Pros and Cons

### Requirements for Instruction Set
- Completeness
- Efficiency
- Regularity
- Compatibility

### Classification of Instructions
- Data transfer instructions
- Arithmetic instructions
- Logical instructions
- Program control instructions
- I/O instructions

## Lecture 08: ARM Architecture
- Reference to Patterson and Hennessy (4th Edition)

## Lecture 09: System Design and Hardware Description

### System Design
- Definition and components
- Function and representation (directed graph)

### Block Diagram
- Representation of components and connections

### Structure and Behavior
- Structural descriptions
- Behavioral descriptions
- Representation methods (truth table, equation, HDL)

### Hardware Description Language (HDL)
- Advantages
- Example (half adder)

### Design Process
- Goals (behavior, cost, performance)
- Iterative design process (flowchart)

### Computer-Aided Design (CAD)
- Editors
- Simulators
- Synthesizers

### Design Levels
- Processor level
- Register level
- Gate level (components, IC density, time units)

### System Hierarchy
- High-level components
- Low-level components
- Example: hierarchical system (XOR, NAND, half adder)

### Sequential Circuits
- Combinational circuit and flip-flops
- Internal state and clocked (synchronous) circuits

### Serial Adder
- State table
- Logic circuit
- 4-bit stream serial adder (structure and operation)

### 4-bit Magnitude Comparator
- Implementation using adders and inverters

## Lecture 10: Advanced Arithmetic Operations

### Combinational Array Multiplier
- Structure and components
- Mathematical representation (P = X × Y)
- Hardware requirements (AND gates, full adders)

### Multiplication Process
- Example: 1000 × 1001
- Rules for multiplicand placement
- Bit-length handling (n + m bits for product)

### Sequential Multiplication Algorithm
- Steps: Test multiplier bit → Shift → Decrement counter
- Hardware components (registers, ALU)

### Sequential Multiplication Example
- Iteration table (Multiplier, Multiplicand, Product)

### Refined Multiplication Hardware
- 32-bit ALU and 64-bit product register

### AND Array for 4×4-bit Multiplication
- Partial product generation

### Division Basics
- Example: 1001₁₀ ÷ 1000₁₀
- Hardware (Divisor, Remainder, Quotient registers)

### Division Algorithm
- Steps: Subtract → Test remainder → Shift
- Restoring vs. non-restoring

## Lecture 11: Advanced Multiplication and Floating-Point Operations

### Booth's Multiplication Algorithm
- Advantages: Uniform handling of signed numbers, efficiency
- Example: 0010 × 0110
- Bit-pair rules (01: add; 10: subtract)

### Booth's Algorithm Validity
- Mathematical proof for runs of 1s

### Array Implementation of Booth's Algorithm
- Multifunction cells (addition/subtraction)
- Control signals (H, D)

### Floating-Point Addition
- Steps: Align exponents → Add significands → Normalize → Round
- Example: 9.999 × 10¹ + 1.610 × 10⁻¹

### Floating-Point Multiplication
- Steps: Add exponents → Multiply significands → Normalize → Round
- Example: 1.110 × 10¹⁰ × 9.200 × 10⁻⁵

## Lecture 12: Pipeline Processing and Parallel Computing

### Pipeline Processing
- Definition and benefits (throughput improvement)

### Pipeline Processor Structure
- Stages (segments) and data flow

### Four-Stage Floating-Point Adder Pipeline
- Steps: Compare exponents → Align mantissas → Add → Normalize
- Speedup calculation (S ≈ 4 for large N)

### Pipeline Design Principles
- Balanced stage timing
- Buffer registers between stages

### Summation Using Feedback Pipelines
- Example: Summing N numbers

### Pipelined Multiplier
- Hardware (M cells, buffer registers)
- Limitations (carry propagation, cost)

### Carry-Save Addition
- Wallace Tree for multiplication
- Final carry-lookahead adder

### Systolic Arrays
- Matrix multiplication example
- Characteristics (parallelism, uniform cells)

## Lecture 13: Single-Cycle MIPS Datapath

### Single-Cycle MIPS Datapath
- Components: PC, ALU, registers, memory
- Control signals (RegWrite, ALUSrc, etc.)

### Instruction Execution Steps
- Fetch
- Decode
- Execute
- Memory
- Write-back

### Control Unit Design
- ALU control (ALUOp, funct field)
- Truth tables for control signals

### Datapath for R-type/Load/Branch Instructions
- Examples: add, lw, beq

### Jump Instruction Handling
- Address calculation (PC concatenation)

## Lecture 14: Multicycle Implementation

### Multicycle Datapath
- Temporary registers (IR, MDR, A, B, ALUOut)
- Shared functional units

### Multicycle Execution Steps
- 5 stages: Fetch → Decode → Execute → Memory → Write-back
- Example: lw, sw, R-type, branch

### Control Signals
- RegDst
- MemtoReg
- IorD
- etc.

### Handling Jumps
- Additional multiplexer for jump address

## Lecture 15: ALU Control and Single-Cycle Control

### ALU Control
- Multi-level decoding (ALUOp + funct field)
- Truth table for ALU operations

### Single-Cycle Control
- Signal settings for R-type, lw, sw, beq

### Datapath Operation Examples
- R-type: ALU operation → Write-back
- lw: Address calculation → Memory read → Write-back

## Lecture 16: Pipelining Implementation

### Multicycle Implementation
- Advantages: Shared hardware, reduced latency

### Pipeline Hazards
- Structural: Resource conflicts
- Data: Dependencies (solved via forwarding/stalling)
- Control: Branches (solved via prediction/flushing)

### Pipeline Scheduling
- Reordering instructions to avoid stalls

### Pipelined Datapath
- IF/ID registers
- ID/EX registers
- EX/MEM registers
- MEM/WB registers
- Example: lw pipeline flow

## Lecture 17: Pipelining Fundamentals

### Pipelining Basics
- Laundry analogy
- Speedup calculation (S = stages for large N)

### MIPS Pipeline Stages
- Fetch
- Decode
- Execute
- Memory
- Write-back

### Hazard Resolution
- Forwarding for data hazards
- Branch prediction for control hazards

### Pipeline Diagrams
- Single-clock-cycle views
- Multiple-clock-cycle views

## Lecture 18: Control Signals and Data Hazards in Pipelining

### Control Signals in Pipelined Datapath
- Control Signal Table: ALUOp, ALU control input for different instructions (LW, SW, Branch equal, R-type operations)
- Signal Effects: RegDst, RegWrite, ALUSrc, PCSrc, MemRead, MemWrite, MemtoReg (asserted vs. deasserted)
- Stage-wise Control Lines: Execution/address calculation, memory access, write-back stages for R-format, LW, SW, and beq instructions
- Control Signals Generation: WB, M, EX stages and their connections (RegDst, ALUOp, ALUSrc, Branch, MemRead, MemWrite, MemtoReg, RegWrite)

### Pipelined Datapath Example
- Example Instructions: Sequential execution of LW, SUB, AND, OR, ADD
- Pipeline Stages: Breakdown of IF, ID, EX, MEM, WB stages for each instruction
- Block Diagrams: Datapath components (instruction memory, registers, ALU, data memory, pipeline registers)

### Data Hazards
- Definition: Dependencies between instructions (e.g., SUB followed by AND using the same register)
- Hazard Example: Code segment with SUB, AND, OR, ADD, SW depending on SUB's result
- Partial Resolution: Register file design (write in first half of clock cycle, read in second half)

### Fixing Data Hazards with Forwarding
- Forwarding Concept: Passing results from EX/MEM or MEM/WB registers to ALU inputs
- Multiplexor Setup:
  - 00: Normal input (ID/EX)
  - 10: Forward from EX/MEM
  - 01: Forward from MEM/WB
- Hazard Conditions:
  - EX/MEM Hazard: Forward if EX/MEM.RegisterRd matches ID/EX.RegisterRs or Rt
  - MEM/WB Hazard: Forward if MEM/WB.RegisterRd matches ID/EX.RegisterRs or Rt (with additional checks for RegWrite and non-zero registers)
- Datapath with Forwarding Hardware: Integration of forwarding unit into pipeline stages

### Complications and Stalls
- Conflict Scenarios: When WB and MEM stages both need to forward (prioritize recent result)
- Stall Conditions:
  - Load-Use Hazard: Detection during ID stage if LW is followed by an instruction needing its result
  - Stall Logic: Preserving PC and IF/ID registers, inserting NOPs in EX, MEM, WB by deasserting control signals
- Hazard Detection Unit: Checks for ID/EX.MemRead and register conflicts (ID/EX.RegisterRt vs. IF/ID.RegisterRs/Rt)

### Diagrams and Hardware
- Pipelined Datapath Diagrams: With control signals and forwarding hardware
- Forwarding Unit: Integration with ALU inputs and pipeline registers (EX/MEM, MEM/WB)

## Lecture 19-20: Memory Hierarchy and Cache Systems

### Memory Hierarchy
- Definition: Levels of memory with varying speeds, sizes, and costs
- Technologies:
  - SRAM (Cache): Fastest, smallest, highest cost
  - DRAM (Main memory): Moderate speed/size/cost
  - Magnetic Disk: Slowest, largest, lowest cost
- Goal: Balance cost and speed by leveraging hierarchy

### Cache Basics
- Terminology:
  - Block: Minimum transfer unit between hierarchy levels
  - Hit/Miss: Data presence in upper level (cache)
  - Hit Rate/Miss Rate: Fraction of accesses found/not found in cache
  - Hit Time: Time to access cache + determine hit/miss
  - Miss Penalty: Time to fetch block from lower level
- Principle of Locality:
  - Temporal Locality: Repeated access to same data
  - Spatial Locality: Access to nearby data

### Cache Organization
- Direct Mapped Cache:
  - Each memory block maps to one cache location (Block address mod Cache blocks)
  - Tag/Valid Bit: Identifies block and validates data
- Cache Access Example:
  - Steps for handling hits/misses (e.g., address 10110 mapped to block 110)
- Cache Size Calculation:
  - Formula: Total bits = (Data bits + Tag bits + Valid bit) × Cache entries

### Cache Performance Optimization
- Block Size Trade-offs:
  - Larger blocks reduce miss rate (spatial locality) but increase miss penalty
- Techniques:
  - Early Restart: Execute once requested word arrives
  - Critical Word First: Deliver requested word before full block

### Handling Cache Misses & Writes
- Cache Miss Steps:
  - Send PC to memory
  - Read memory
  - Update cache (tag, data, valid bit)
  - Restart instruction
- Write Policies:
  - Write-Through: Update cache and memory (slow, uses write buffer)
  - Write-Back: Update cache only; write to memory on replacement (faster, complex)

### Memory System Design
- Bandwidth Optimization:
  - One-Word-Wide: High miss penalty (e.g., 65 cycles for 4-word block)
  - Wide/Interleaved Memory: Reduces miss penalty (e.g., 20 cycles for 4-word block)

### Cache Associativity
- Fully Associative:
  - Block can be placed anywhere (high hardware cost)
- Set-Associative:
  - Block maps to a set (e.g., 2-way, 4-way). Combines direct mapping and full associativity
  - Trade-off: Higher associativity reduces conflict misses but increases hit time
- Examples:
  - Direct-mapped vs. set-associative vs. fully associative miss rates

### Cache Miss Classification
- Compulsory Misses: First access to a block
- Capacity Misses: Cache too small to hold needed blocks
- Conflict Misses: Blocks compete for same set (direct/set-associative)

### Advanced Cache Topics
- Tag Size Calculation:
  - Varies with associativity (direct: 16 bits, 2-way: 17 bits, fully associative: 28 bits)
- Block Replacement Policies:
  - Random or LRU (Least Recently Used)
- Performance Trade-offs:
  - Increasing cache size/associativity/block size impacts miss rate/access time/miss penalty

## Lecture 21: Communication and I/O Systems

### Communication Methods
- Intrasystem Communication:
  - Occurs within a single computer system
  - Implemented via bus with parallel transmission
- Intersystem Communication:
  - Involves long-distance communication
  - Uses serial transmission over physical media (e.g., cables, wireless)

### Buses
- Definition: Shared pathway for communication between components
- Bus Arbitration: Mechanism to resolve conflicts when multiple devices request bus access
- Schemes:
  - Daisy Chaining:
    - Advantages: Simple, minimal control lines
    - Disadvantages: Fixed priority, potential lockout, propagation issues
  - Polling:
    - Advantages: Programmable priority, fault isolation
    - Disadvantages: More control lines, limited by addressing
  - Independent Requesting:
    - Advantages: Rapid response, programmable priority
    - Disadvantages: High wiring complexity (n request/grant lines)

### I/O Control Methods
- Programmed I/O:
  - CPU directly controls all I/O operations
  - Advantages: Simple, no extra hardware
  - Disadvantages: CPU overhead limits transfer speed
- Memory-Mapped I/O: I/O devices mapped to memory address space
- Direct Memory Access (DMA):
  - I/O devices access memory directly without CPU intervention
  - Uses DMA controller; CPU grants bus control
  - Interrupts: Signal completion of DMA transfers
- Interrupts:
  - Process:
    - Identify interrupt source
    - Fetch interrupt handler address
    - Save CPU state (PC, registers)
    - Execute handler; return via RET instruction
  - Trigger: Between instruction cycles

### Key Diagrams & Concepts
- Daisy Chaining: Bus grant/request signals propagate sequentially
- Polling: Bus controller queries devices via poll count
- Independent Requesting: Dedicated request/grant lines per device
- Memory-Mapped I/O vs. I/O-Mapped I/O: Address space integration
