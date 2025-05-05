
# Computer Architecture and Organization (CSE-2204) Exam Solutions
## Incourse Exam-2024, University of Dhaka

### Question 1
**Show the layers of abstraction in computer systems. What do abstraction layers provide? State its relative advantages over other representation of computer systems.**

#### Answer:
The layers of abstraction in computer systems include:

1. **Hardware Layer**: The physical components including processors, memory, I/O devices.
2. **Firmware Layer**: The basic software embedded in hardware (e.g., BIOS/UEFI).
3. **Machine Language Layer**: Binary instructions directly executable by the CPU.
4. **Assembly Language Layer**: Symbolic representation of machine instructions.
5. **Operating System Layer**: Provides resource management and services to applications.
6. **High-Level Language Layer**: Programming languages that are more human-readable.
7. **Application Layer**: End-user software applications.

Abstraction layers provide:
- **Simplification**: Each layer hides the complexity of the layer below it
- **Modularity**: Changes can be made to one layer without affecting others
- **Portability**: Software can run on different hardware implementations
- **Division of Labor**: Different specialists can work on different layers

Advantages over other representations:
- **Reduced Complexity**: Makes the system more understandable by compartmentalizing details
- **Easier Maintenance**: Problems can be isolated to specific layers
- **Faster Development**: Developers can focus on their specific layer without knowing all details
- **Reusability**: Components at each layer can be reused across different systems

### Question 2
**What do you understand by instruction, Instruction Set and Instruction Set Architecture of a CPU? List the steps, general purpose CPUs are designed to follow, in general, to process each Instruction. (Use suitable diagram for the later part).**

#### Answer:
**Instruction**: A single operation that a CPU can execute, represented by a binary code. Instructions are the fundamental units of execution and include operations like add, subtract, load, store, jump, etc.

**Instruction Set**: The complete collection of instructions that a processor can execute. It defines what the processor can do and forms the vocabulary of commands available to programmers.

**Instruction Set Architecture (ISA)**: The part of the computer architecture related to programming, including the instruction set, data types, registers, addressing modes, memory architecture, interrupt and exception handling, and external I/O. It is the interface between hardware and software.

**Steps a CPU follows to process instructions:**

1. **Fetch**: The CPU retrieves the instruction from memory at the location pointed to by the program counter (PC).
2. **Decode**: The CPU determines what operation the instruction represents and what operands are needed.
3. **Execute**: The CPU performs the operation specified by the instruction.
4. **Memory Access**: If needed, the CPU reads from or writes to memory.
5. **Write Back**: The CPU writes the results back to registers.

**Diagram of Instruction Execution Cycle:**

```
     ┌────────────┐
     │   START    │
     └─────┬──────┘
           │
           ▼
┌─────────────────────┐
│ FETCH INSTRUCTION   │◄───────┐
│ - Get instruction   │        │
│ - Increment PC      │        │
└────────┬────────────┘        │
         │                     │
         ▼                     │
┌─────────────────────┐        │
│ DECODE INSTRUCTION  │        │
│ - Interpret opcode  │        │
│ - Identify operands │        │
└────────┬────────────┘        │
         │                     │
         ▼                     │
┌─────────────────────┐        │
│ EXECUTE OPERATION   │        │
│ - ALU operations    │        │
│ - Address calc      │        │
└────────┬────────────┘        │
         │                     │
         ▼                     │
┌─────────────────────┐        │
│ MEMORY ACCESS       │        │
│ - Read/write memory │        │
│   (if needed)       │        │
└────────┬────────────┘        │
         │                     │
         ▼                     │
┌─────────────────────┐        │
│ WRITE BACK          │        │
│ - Update registers  │        │
└────────┬────────────┘        │
         │                     │
         └─────────────────────┘
```

### Question 3
**Show the hardware implementation of a floating point adder/subtractor and explain the steps.**

#### Answer:
A floating-point adder/subtractor performs addition or subtraction of numbers in IEEE 754 format. The hardware implementation involves the following components and steps:

**Hardware Implementation:**

```
┌─────────────┐     ┌─────────────┐
│ Input A     │     │ Input B     │
│ (IEEE 754)  │     │ (IEEE 754)  │
└──────┬──────┘     └──────┬──────┘
       │                   │
       ▼                   ▼
┌──────────┬───────────────┬──────────┐
│ Sign A   │ Exponent A    │ Mantissa A│
└────┬─────┴───────┬───────┴────┬─────┘
     │             │            │
     │             │            │
┌────▼─────┬───────▼───────┬────▼─────┐
│ Sign B   │ Exponent B    │ Mantissa B│
└────┬─────┴───────┬───────┴────┬─────┘
     │             │            │
     │             │            │
     ▼             ▼            ▼
┌────────────┐ ┌───────────┐ ┌─────────────────┐
│ Sign Logic │ │ Compare   │ │ Mantissa        │
│            │ │ Exponents │ │ Preparation     │
└──────┬─────┘ └─────┬─────┘ └────────┬────────┘
       │             │                │
       │             │                │
       │             ▼                │
       │      ┌────────────┐          │
       │      │ Alignment  │          │
       │      │ Shifter    │          │
       │      └──────┬─────┘          │
       │             │                │
       │             │                │
       ▼             ▼                ▼
┌─────────────────────────────────────────┐
│ Addition/Subtraction Unit               │
└───────────────────────┬─────────────────┘
                        │
                        ▼
┌───────────────────────────────────────┐
│ Normalization & Rounding              │
└───────────────────────┬───────────────┘
                        │
                        ▼
┌───────────────────────────────────────┐
│ Output (IEEE 754 Format)              │
└───────────────────────────────────────┘
```

**Steps:**

1. **Unpacking**: Extract the sign, exponent, and mantissa from both inputs.

2. **Exponent Comparison**: Compare exponents to determine which number is larger.

3. **Mantissa Alignment**: Shift the mantissa of the smaller number right by the difference in exponents to align decimal points.

4. **Operation Selection**: Determine whether to add or subtract based on the signs:
   - If signs are the same, perform addition
   - If signs are different, perform subtraction (larger magnitude - smaller magnitude)

5. **Mantissa Operation**: Add or subtract the aligned mantissas.

6. **Normalization**: Shift the result mantissa to ensure a leading 1 in the normalized form (for binary floating-point), adjusting the exponent accordingly.

7. **Rounding**: Apply the appropriate rounding mode (typically round-to-nearest).

8. **Overflow/Underflow Check**: Check if the result exponent exceeds the representable range.

9. **Special Cases Handling**: Handle special cases like NaN, infinity, zero, denormalized numbers.

10. **Packaging**: Combine the resulting sign, exponent, and mantissa into the IEEE 754 format.

### Question 4
**Explain Booth's algorithm for multiplication of signed binary numbers. Show its implementation. How does Booth's algorithm save computations compared to conventional binary multiplication technique?**

#### Answer:
**Booth's Algorithm** is an efficient method for multiplying signed binary numbers in two's complement notation. It reduces the number of additions needed in the multiplication process.

#### Explanation:

Booth's algorithm works by identifying consecutive 0s and 1s in the multiplier and performing operations based on the pattern:
- When transitioning from 0 to 1: Add the multiplicand
- When transitioning from 1 to 0: Subtract the multiplicand
- When consecutive 1s or 0s: No operation needed

This approach takes advantage of the fact that a sequence like "1111" can be computed as "10000 - 1" (i.e., 2^4 - 2^0), requiring just one addition and one subtraction rather than four additions.

#### Implementation:

1. Initialize:
   - A = 0 (accumulator)
   - Q = Multiplier
   - M = Multiplicand
   - Q₋₁ = 0 (an extra bit to the right of the multiplier)
   - Count = n (number of bits in the multiplier)

2. For each bit position, examine Q₀ (least significant bit of Q) and Q₋₁:
   - If Q₀Q₋₁ = 01: A = A + M (add multiplicand to accumulator)
   - If Q₀Q₋₁ = 10: A = A - M (subtract multiplicand from accumulator)
   - If Q₀Q₋₁ = 00 or 11: No arithmetic operation

3. Shift right arithmetically: A, Q, Q₋₁

4. Decrement Count. If Count > 0, go to step 2

5. The final result is in A and Q

#### Example:
Let's multiply 3 × (-4) using Booth's algorithm.

3 in binary is 0011 and -4 in 2's complement is 1100.

Initial values:
- A = 0000
- Q = 1100 (multiplier, -4)
- M = 0011 (multiplicand, 3)
- Q₋₁ = 0

Steps:
1. Q₀Q₋₁ = 00: No operation
   Shift: A = 0000, Q = 0110, Q₋₁ = 0
2. Q₀Q₋₁ = 00: No operation
   Shift: A = 0000, Q = 0011, Q₋₁ = 0
3. Q₀Q₋₁ = 10: A = A - M = 0000 - 0011 = 1101
   Shift: A = 1110, Q = 1001, Q₋₁ = 1
4. Q₀Q₋₁ = 11: No operation
   Shift: A = 1111, Q = 0100, Q₋₁ = 1

Result: A:Q = 11110100 = -12 (correct: 3 × (-4) = -12)

#### Advantages over Conventional Multiplication:

1. **Reduced Operations**: Multiple consecutive 1s are treated as a block, reducing the number of additions.

2. **Handling of Signed Numbers**: Directly works with two's complement numbers without needing separate sign handling.

3. **Reduced Hardware**: Needs only a single register for addition/subtraction.

4. **Efficiency for Sparse Bit Patterns**: Particularly efficient when multiplier has long runs of 1s or 0s.

5. **Computational Savings**: For n-bit multipliers with many bit transitions, conventional multiplication might require up to n additions, while Booth's algorithm requires only the number of transitions from 0 to 1 and 1 to 0.

### Question 5
**Construct a finite-state machine for entering a security code into an automatic teller machine (ATM) that implements the following rules:**
**A user enters a string of four digits, one digit at a time.**
**If the user enters the correct four digits of the password, the ATM displays a welcome screen.**
**When the user enters an incorrect string of four digits, the ATM displays a screen that informs the user that an incorrect password was entered.**
**If a user enters the incorrect password two times, the ATM displays a screen that informs the user that the account is locked.**

#### Answer:
To design a finite-state machine (FSM) for the ATM security code system, I'll define the states, inputs, transitions, and outputs.

Let's assume the correct password is "1234" for this example.

**States:**
- S0: Initial state
- S1: After entering first correct digit (1)
- S2: After entering second correct digit (2)
- S3: After entering third correct digit (3)
- S4: After entering fourth correct digit (4)
- W: Welcome screen (successful authentication)
- E1: First error state (after first incorrect password)
- E2: Second error state (account locked)

**Inputs:**
- Digits 0-9
- For simplicity, we'll use "C" to represent a correct digit and "I" for an incorrect digit in the diagram

**State Transition Diagram:**

```
                ┌───┐
          I     │   │     I
     ┌─────────►│ E1├──────────┐
     │          │   │          │
     │          └───┘          │
     │                         ▼
┌────┴───┐                  ┌─────┐
│        │      4 digits    │     │
│   S0   ├─────────────────►│  E2 │
│        │    completed     │     │
└────┬───┘    (incorrect)   └─────┘
     │                      (Locked)
     │
     │   "1"
     ▼
┌────────┐  "2"   ┌────────┐  "3"   ┌────────┐  "4"   ┌────────┐
│        ├───────►│        ├───────►│        ├───────►│        │
│   S1   │        │   S2   │        │   S3   │        │   S4   │
│        │        │        │        │        │        │        │
└────┬───┘        └───┬────┘        └───┬────┘        └───┬────┘
     │                │                 │                 │
     │   Wrong        │   Wrong         │   Wrong         │   Wrong
     │   digit        │   digit         │   digit         │   digit
     ▼                ▼                 ▼                 ▼
  Back to S0      Back to S0        Back to S0        Back to S0
     │                                                    │
     │                                                    │
     │                 4 digits completed (correct)       │
     └────────────────────────────────────────────────────┘
                               │
                               ▼
                            ┌─────┐
                            │     │
                            │  W  │
                            │     │
                            └─────┘
                           (Welcome)
```

**Formal Specification:**

Let's define the transition function δ and output function λ:

1. For the correct password sequence:
   - δ(S0, 1) = S1
   - δ(S1, 2) = S2
   - δ(S2, 3) = S3
   - δ(S3, 4) = W
   - λ(W) = "Welcome screen"

2. For incorrect digits during entry:
   - δ(S0, d≠1) = S0
   - δ(S1, d≠2) = S0
   - δ(S2, d≠3) = S0
   - δ(S3, d≠4) = S0

3. For incorrect password completion:
   - When 4 digits have been entered and state is not W:
     - If current state is S0 and no previous incorrect attempt: δ = E1
     - If current state is S0 and one previous incorrect attempt (E1): δ = E2
     - λ(E1) = "Incorrect password was entered"
     - λ(E2) = "Account is locked"

The FSM keeps track of the number of digits entered and moves to the error states once four digits have been processed. After the first incorrect attempt, it moves to E1, and after the second incorrect attempt, it moves to E2 (locked state).

This FSM successfully implements the specified ATM security code requirements, properly handling correct password entry, incorrect password notification, and account locking after two failed attempts.
