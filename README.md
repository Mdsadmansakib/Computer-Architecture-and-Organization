# Computer-Architecture-and-Organization

Topics:

**** Lecture 01-02


Fixed-Point Arithmetic

Addition

Subtraction

Multiplication

Division

Half Adder

Truth table and logic equations.

Full Adder

Truth table and logic equations.

Serial Binary Adder

Operation and characteristics.

Ripple Carry Adder

Structure and limitations.

2's Complement Adder-Subtracter

Functionality and examples.

Overflow

Detection and handling in unsigned and signed numbers.

Carry-Lookahead Adder

Generate and propagate signals.

4-bit implementation and expansion.

Carry-Save Adder

Concept and application.

**** Lecture 03


Basic Information Types

Instruction, numbers, data, nonnumerical data.

Word Length

Bits, byte, halfword, word, double word.

Byte Storage

Big-Endian and Little-Endian methods.

Tags

Purpose, advantages, and disadvantages.

Error Detection and Correction

Parity bit (even and odd parity).

Fixed-Point Binary Numbers

Unsigned and signed representations.

Signed Numbers

Sign magnitude, 1's complement, 2's complement.

Decimal Codes

BCD, ASCII, Excess-Three, Two-out-of-Five.

Floating-Point Numbers

Need, basic format, representation.

Normalization, IEEE 754 standard (32-bit and 64-bit formats).

Biasing (excess-127 and excess-128).

Conversion from decimal to binary floating-point.

Overflow and underflow.



**** Lecture 04


CPU Organization

Instruction execution steps.

External communication (memory and I/O devices).

Memory-mapped I/O vs. I/O-mapped I/O.

User and Supervisor Programs

Roles and switching between them.

Interrupt handling.

CPU Operation

Instruction cycle (fetch and execute steps).

Micro operations and clock cycle time.

Accumulator-based CPU

Structure and components (PCU, DPU, registers).

Load and store operations.

Programming considerations (single-address instructions).

Instruction Set

Data transfer, data processing, program control instructions.

Example: Multiplication program.

Limitations of Accumulator-based CPU

Register constraints and performance issues.



****  Lecture 05


Performance Metrics

Response time (execution time) and throughput.

Relative performance calculation.

Measuring Performance

CPU time (user and system CPU time).

CPU utilization.

Clock Cycles and CPU Time

Clock period and rate.

CPI (cycles per instruction) and IPC (instructions per cycle).

CPU time equations.

Comparing Code Segments

Instruction count, CPI, and performance analysis.

Components Affecting CPU Performance

Algorithm, programming language, compiler, ISA.

Speedup Techniques

Cache memory, pipelined processing, superscalar processing.

Sequential vs. Pipelined Processing

Instruction fetch, decode, operand load, execution, operand store.



**** Lecture 06


Classifying Instruction Set

CISC vs. RISC characteristics.

Instruction Format

Opcode and operand fields.

RISC1 instruction format.

Operand Extension

Sign extension and zero extension.

Address Extension

Base register and effective address.

Addressing Modes

Immediate, direct, indirect addressing.

Relative addressing (advantages and drawbacks).

Auto indexing (pre-decrementing and post-incrementing).

Register direct and indirect addressing.

Register indirect with offset.



****  Lecture 07


Stack Control

Push and pop operations.

Stack pointer (SP).

Stack Control in Motorola 680X0

Memory addressing modes for stack operations.

Number of Addresses in Instructions

Three-address, two-address, one-address instructions.

Examples for arithmetic operations.

Accumulator Architectures

Pros and cons.

Example: AB - (A+BC).

Zero Address Machine (Stack-Based Architecture)

Implicit operand addressing.

Example: AB - (A+CB).

Stack Architecture: Pros and Cons

Requirements for Instruction Set

Completeness, efficiency, regularity, compatibility.

Classification of Instructions

Data transfer, arithmetic, logical, program control, I/O instructions.



**** Lecture 08
ARM Architecture



Reference to Patterson and Hennessy (4th Edition).

**** Lecture 09


System Design

Definition and components.

Function and representation (directed graph).

Block Diagram

Representation of components and connections.

Structure and Behavior

Structural vs. behavioral descriptions.

Representation methods (truth table, equation, HDL).

Hardware Description Language (HDL)

Advantages and example (half adder).

Design Process

Goals (behavior, cost, performance).

Iterative design process (flowchart).

Computer-Aided Design (CAD)

Editors, simulators, synthesizers.

Design Levels

Processor, register, gate levels (components, IC density, time units).

System Hierarchy

High-level vs. low-level components.

Example: hierarchical system (XOR, NAND, half adder).

Sequential Circuits

Combinational circuit and flip-flops.

Internal state and clocked (synchronous) circuits.

Serial Adder

State table and logic circuit.

4-bit stream serial adder (structure and operation).

4-bit Magnitude Comparator

Implementation using adders and inverters.
