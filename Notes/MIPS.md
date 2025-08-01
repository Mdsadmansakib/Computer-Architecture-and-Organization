# Complete MIPS Assembly Reference Guide

## 1. Register Overview

MIPS has 32 general-purpose registers, each 32 bits wide. Here are the most commonly used ones:

| Register | Name | Purpose | Usage |
|----------|------|---------|-------|
| `$zero` | Zero | Always contains 0 | Used for comparisons and initialization |
| `$t0-$t9` | Temporaries | Caller-saved | Short-term storage, not preserved across function calls |
| `$s0-$s7` | Saved | Callee-saved | Long-term storage, preserved across function calls |
| `$a0-$a3` | Arguments | Function args | First 4 function arguments |
| `$v0-$v1` | Return values | Function returns | Function return values |
| `$ra` | Return address | Jump and link | Stores return address for function calls |
| `$sp` | Stack pointer | Stack management | Points to top of stack |
| `$gp` | Global pointer | Global data | Points to global data segment |
| `$fp` | Frame pointer | Stack frame | Points to current stack frame |
| `$at` | Assembler temp | Pseudoinstructions | Reserved for assembler use |

## 2. Instruction Categories with Examples

### Arithmetic Instructions

#### ADD - Addition (with overflow detection)
```mips
add $d, $s, $t    # $d = $s + $t (signed addition)
```
**Example:**
```mips
add $s1, $s2, $s3    # If $s2 = 5, $s3 = 7 → $s1 = 12
```
**Explanation:** Performs signed 32-bit addition. Traps on overflow (when result exceeds 32-bit signed range).

#### SUB - Subtraction
```mips
sub $d, $s, $t    # $d = $s - $t (signed subtraction)
```
**Example:**
```mips
sub $s1, $s2, $s3    # If $s2 = 10, $s3 = 4 → $s1 = 6
```
**Explanation:** Performs signed subtraction with overflow detection.

#### ADDI - Add Immediate
```mips
addi $t, $s, imm    # $t = $s + immediate (signed)
```
**Example:**
```mips
addi $t0, $t1, 20    # If $t1 = 100 → $t0 = 120
```
**Explanation:** Adds a 16-bit signed immediate value to a register. The immediate is sign-extended to 32 bits.

### Data Transfer Instructions

#### LW - Load Word
```mips
lw $t, offset($s)    # Load 32-bit word from memory
```
**Example:**
```mips
lw $t0, 20($s2)    # Load word from address ($s2 + 20) into $t0
```
**Explanation:** Loads a 32-bit word from memory. The effective address is calculated as base register + offset.

#### SW - Store Word
```mips
sw $t, offset($s)    # Store 32-bit word to memory
```
**Example:**
```mips
sw $t0, 20($s2)    # Store $t0 to memory address ($s2 + 20)
```
**Explanation:** Stores the contents of a register to memory at the calculated address.

#### LH - Load Halfword (signed)
```mips
lh $t, offset($s)    # Load signed 16-bit, sign-extend to 32 bits
```
**Example:**
```mips
lh $t1, 4($s3)    # Load halfword from ($s3 + 4), sign-extend
```
**Explanation:** Loads 16 bits and sign-extends to fill the 32-bit register.

#### LHU - Load Halfword Unsigned
```mips
lhu $t, offset($s)    # Load unsigned 16-bit, zero-extend
```
**Example:**
```mips
lhu $t1, 4($s3)    # Load halfword from ($s3 + 4), zero-extend
```
**Explanation:** Loads 16 bits and zero-extends (fills upper 16 bits with zeros).

#### SH - Store Halfword
```mips
sh $t, offset($s)    # Store lower 16 bits to memory
```
**Example:**
```mips
sh $t2, 8($s4)    # Store lower 16 bits of $t2 to ($s4 + 8)
```
**Explanation:** Stores only the lower 16 bits of the register to memory.

#### LB - Load Byte (signed)
```mips
lb $t, offset($s)    # Load signed byte, sign-extend
```
**Example:**
```mips
lb $t3, 0($s5)    # Load byte from $s5, sign-extend to 32 bits
```
**Explanation:** Loads 8 bits and sign-extends to fill the 32-bit register.

#### LBU - Load Byte Unsigned
```mips
lbu $t, offset($s)    # Load unsigned byte, zero-extend
```
**Example:**
```mips
lbu $t3, 0($s5)    # Load byte from $s5, zero-extend to 32 bits
```
**Explanation:** Loads 8 bits and zero-extends to fill the register.

#### SB - Store Byte
```mips
sb $t, offset($s)    # Store low 8 bits to memory
```
**Example:**
```mips
sb $t4, 1($s6)    # Store lowest 8 bits of $t4 to ($s6 + 1)
```
**Explanation:** Stores only the lowest 8 bits of the register to memory.

#### LL - Load Linked
```mips
ll $t, offset($s)    # Load linked for atomic operations
```
**Example:**
```mips
ll $t0, 0($s7)    # Load word and set up for atomic operation
```
**Explanation:** Used in atomic read-modify-write sequences. Sets up a "reservation" on the memory location.

#### SC - Store Conditional
```mips
sc $t, offset($s)    # Store conditional (atomic)
```
**Example:**
```mips
sc $t1, 0($s7)    # Store if no intervening access, set $t1 = success/fail
```
**Explanation:** Stores only if no other processor has accessed the reserved location. Sets register to 1 on success, 0 on failure.

#### LUI - Load Upper Immediate
```mips
lui $t, imm    # Load immediate into upper 16 bits
```
**Example:**
```mips
lui $t0, 0x1234    # $t0 = 0x12340000 (lower 16 bits = 0)
```
**Explanation:** Loads 16-bit immediate into upper half of register, zeros lower half.

### Logical Instructions

#### AND - Bitwise AND
```mips
and $d, $s, $t    # $d = $s & $t (bitwise AND)
```
**Example:**
```mips
and $s1, $s2, $s3    # Each bit: result = bit_s2 AND bit_s3
```
**Explanation:** Performs bitwise AND operation on each bit position.

#### OR - Bitwise OR
```mips
or $d, $s, $t    # $d = $s | $t (bitwise OR)
```
**Example:**
```mips
or $s1, $s2, $s3    # Each bit: result = bit_s2 OR bit_s3
```
**Explanation:** Performs bitwise OR operation on each bit position.

#### NOR - Bitwise NOR
```mips
nor $d, $s, $t    # $d = ~($s | $t) (bitwise NOR)
```
**Example:**
```mips
nor $s1, $s2, $s3    # $s1 = ~($s2 | $s3)
```
**Explanation:** Performs bitwise NOR (NOT OR) - inverts the result of OR operation.

#### ANDI - AND Immediate
```mips
andi $t, $s, imm    # $t = $s & immediate (zero-extended)
```
**Example:**
```mips
andi $t0, $t1, 0xFF    # Mask to keep only lowest 8 bits
```
**Explanation:** Performs AND with zero-extended 16-bit immediate. Commonly used for masking.

#### ORI - OR Immediate
```mips
ori $t, $s, imm    # $t = $s | immediate
```
**Example:**
```mips
ori $t0, $t1, 0x100    # Set bit 8 (0x100 = 256 = 2^8)
```
**Explanation:** Performs OR with zero-extended immediate. Used to set specific bits.

#### SLL - Shift Left Logical
```mips
sll $d, $t, shamt    # $d = $t << shamt (shift left)
```
**Example:**
```mips
sll $t2, $t3, 2    # Shift left by 2 positions (multiply by 4)
```
**Explanation:** Shifts bits left, filling with zeros. Each left shift multiplies by 2.

#### SRL - Shift Right Logical
```mips
srl $d, $t, shamt    # $d = $t >> shamt (logical right shift)
```
**Example:**
```mips
srl $t2, $t3, 1    # Shift right by 1 (divide by 2, unsigned)
```
**Explanation:** Shifts bits right, filling with zeros. Used for unsigned division by powers of 2.

### Conditional Branch Instructions

#### BEQ - Branch if Equal
```mips
beq $s, $t, label    # if ($s == $t) goto label
```
**Example:**
```mips
beq $s1, $s2, equal_label    # Jump to equal_label if $s1 == $s2
```
**Explanation:** Compares two registers and branches if they contain the same value.

#### BNE - Branch if Not Equal
```mips
bne $s, $t, label    # if ($s != $t) goto label
```
**Example:**
```mips
bne $s1, $s2, notequal_label    # Jump if $s1 != $s2
```
**Explanation:** Branches when the two registers contain different values.

#### SLT - Set Less Than
```mips
slt $d, $s, $t    # $d = ($s < $t) ? 1 : 0 (signed comparison)
```
**Example:**
```mips
slt $t0, $s1, $s2    # $t0 = 1 if $s1 < $s2, else 0
```
**Explanation:** Sets destination to 1 if first operand is less than second (signed), else 0.

#### SLTU - Set Less Than Unsigned
```mips
sltu $d, $s, $t    # $d = ($s < $t) ? 1 : 0 (unsigned comparison)
```
**Example:**
```mips
sltu $t0, $s1, $s2    # Unsigned comparison
```
**Explanation:** Same as SLT but treats operands as unsigned values.

#### SLTI - Set Less Than Immediate
```mips
slti $t, $s, imm    # $t = ($s < immediate) ? 1 : 0 (signed)
```
**Example:**
```mips
slti $t1, $s3, 100    # $t1 = 1 if $s3 < 100, else 0
```
**Explanation:** Compares register with sign-extended immediate value.

#### SLTIU - Set Less Than Immediate Unsigned
```mips
sltiu $t, $s, imm    # $t = ($s < immediate) ? 1 : 0 (unsigned)
```
**Example:**
```mips
sltiu $t1, $s3, 100    # Unsigned comparison with immediate
```
**Explanation:** Unsigned comparison with zero-extended immediate.

### Unconditional Jump Instructions

#### J - Jump
```mips
j target    # Jump to target address
```
**Example:**
```mips
j 10000    # Jump to instruction at address 10000
```
**Explanation:** Unconditional jump to a 26-bit address (combined with upper bits of PC).

#### JR - Jump Register
```mips
jr $ra    # Jump to address in register
```
**Example:**
```mips
jr $ra    # Return from function (jump to return address)
```
**Explanation:** Jumps to the address stored in the specified register. Commonly used for function returns.

#### JAL - Jump and Link
```mips
jal target    # Jump to target, save return address in $ra
```
**Example:**
```mips
jal my_function    # Call function, save return address
```
**Explanation:** Saves the address of the next instruction in $ra, then jumps to target. Used for function calls.

## 3. C-to-MIPS Translation Examples

### Exercise 1: Simple Addition
**C Code:**
```c
int sum = a + b;
```
**MIPS:** (assume a in $s0, b in $s1, result in $s2)
```mips
add $s2, $s0, $s1    # sum = a + b
```
**Explanation:** Direct translation using three-register ADD instruction.

### Exercise 2: Add Constant
**C Code:**
```c
int x = y + 20;
```
**MIPS:** (y in $t1, result in $t0)
```mips
addi $t0, $t1, 20    # x = y + 20
```
**Explanation:** Uses ADD Immediate to add constant value efficiently.

### Exercise 3: Conditional Branch (if-else)
**C Code:**
```c
if (x == y) 
    z = 1;
else 
    z = 0;
```
**MIPS:** (x in $t0, y in $t1, z in $t2)
```mips
beq $t0, $t1, equal      # if x == y, go to equal
addi $t2, $zero, 0       # else: z = 0
j done                   # skip the equal case
equal:
    addi $t2, $zero, 1   # z = 1
done:
    # continue execution
```
**Explanation:** Uses conditional branch to implement if-else logic. Branch target handles the "true" case.

### Exercise 4: For Loop
**C Code:**
```c
for (i = 0; i < 10; i++) 
    sum += i;
```
**MIPS:** (i in $t0, sum in $t1)
```mips
addi $t0, $zero, 0       # i = 0
loop:
    slti $t2, $t0, 10    # $t2 = (i < 10) ? 1 : 0
    beq $t2, $zero, end  # if not (i < 10), exit loop
    add $t1, $t1, $t0    # sum += i
    addi $t0, $t0, 1     # i++
    j loop               # repeat loop
end:
    # loop finished
```
**Explanation:** Loop condition checking using SLT + BEQ pattern. Increment and jump back for iteration.

### Exercise 5: Array Access (Load)
**C Code:**
```c
int val = arr[3];
```
**MIPS:** (base of arr in $s3, result in $s4)
```mips
lw $s4, 12($s3)    # val = arr[3] (3 * 4 bytes = 12 offset)
```
**Explanation:** Array indexing: base address + (index × element size). Integers are 4 bytes each.

### Exercise 6: Array Store
**C Code:**
```c
arr[2] = x;
```
**MIPS:** (x in $t5, base arr in $s3)
```mips
sw $t5, 8($s3)    # arr[2] = x (2 * 4 = 8 byte offset)
```
**Explanation:** Stores value to calculated array position using base + offset addressing.

### Exercise 7: Function Call and Return
**C Code:**
```c
int foo(int a);
int result = foo(5);
```
**MIPS:**
```mips
addi $a0, $zero, 5       # Set argument a = 5
jal foo                  # Call function foo
move $s0, $v0            # result = return value from $v0

# Function foo should look like:
foo:
    # function body here
    # place return value in $v0
    jr $ra               # return to caller
```
**Explanation:** MIPS calling convention: arguments in $a0-$a3, return values in $v0-$v1, use JAL/JR for calls.

### Exercise 8: Compare and Set
**C Code:**
```c
if (a < b) 
    c = 1;
else 
    c = 0;
```
**MIPS:** (a in $s1, b in $s2, c in $s3)
```mips
slt $s3, $s1, $s2    # c = (a < b) ? 1 : 0
```
**Explanation:** SLT instruction directly implements the comparison and assignment in one step.

### Exercise 9: Bitwise Mask
**C Code:**
```c
x = x & 0xFF;
```
**MIPS:** (x in $t0)
```mips
andi $t0, $t0, 0xFF    # x = x & 0xFF (keep only low 8 bits)
```
**Explanation:** Uses AND immediate to mask bits, keeping only the lowest 8 bits (0-255).

### Exercise 10: Shift Left (Multiply by 16)
**C Code:**
```c
y = x * 16;
```
**MIPS:** (x in $t1, result in $t2)
```mips
sll $t2, $t1, 4    # y = x << 4 (multiply by 2^4 = 16)
```
**Explanation:** Left shift by 4 positions multiplies by 16. More efficient than multiplication instruction.

### Exercise 11: Unsigned Comparison
**C Code:**
```c
if ((unsigned)a < (unsigned)b) 
    flag = 1;
else 
    flag = 0;
```
**MIPS:** (a in $t3, b in $t4, flag in $t5)
```mips
sltu $t5, $t3, $t4    # flag = (unsigned a < unsigned b) ? 1 : 0
```
**Explanation:** SLTU treats operands as unsigned values, important for comparing large positive numbers.

### Exercise 12: Build 32-bit Constant
**C Code:**
```c
int big = 0x12345678;
```
**MIPS:**
```mips
lui $t0, 0x1234        # Load upper 16 bits: $t0 = 0x12340000
ori $t0, $t0, 0x5678   # OR in lower 16 bits: $t0 = 0x12345678
```
**Explanation:** MIPS can't load 32-bit constants directly. Use LUI + ORI pattern to build large constants.

## 4. Advanced Examples

### Exercise 13: Array Sum Function
**C Code:**
```c
int sum_array(int *arr, int n) {
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }
    return sum;
}
```
**MIPS:** (arr in $a0, n in $a1, return in $v0)
```mips
sum_array:
    addi $sp, $sp, -8      # Allocate stack space
    sw $ra, 4($sp)         # Save return address
    sw $s0, 0($sp)         # Save $s0 (callee-saved)

    move $s0, $a0          # $s0 = arr (save array pointer)
    move $t0, $zero        # i = 0
    move $v0, $zero        # sum = 0

loop_sum:
    beq $t0, $a1, done     # if i == n, exit loop
    sll $t1, $t0, 2        # $t1 = i * 4 (byte offset)
    add $t2, $s0, $t1      # $t2 = &arr[i]
    lw $t3, 0($t2)         # $t3 = arr[i]
    add $v0, $v0, $t3      # sum += arr[i]
    addi $t0, $t0, 1       # i++
    j loop_sum             # continue loop

done:
    lw $ra, 4($sp)         # Restore return address
    lw $s0, 0($sp)         # Restore $s0
    addi $sp, $sp, 8       # Deallocate stack space
    jr $ra                 # Return to caller
```
**Explanation:** Complete function with proper calling convention, stack management, and array traversal.

### Exercise 14: Sum of First N Integers (For Loop)
**C Code:**
```c
int sum_n(int n) {
    int sum = 0;
    for (int i = 1; i <= n; i++) {
        sum += i;
    }
    return sum;
}
```
**MIPS:** (n in $a0, return in $v0)
```mips
sum_n:
    addi $t0, $zero, 1     # i = 1
    addi $v0, $zero, 0     # sum = 0

loop_sum_n:
    slt $t1, $a0, $t0      # $t1 = (n < i) ? 1 : 0
    bne $t1, $zero, end_sum_n  # if n < i, exit loop
    add $v0, $v0, $t0      # sum += i
    addi $t0, $t0, 1       # i++
    j loop_sum_n           # continue loop

end_sum_n:
    jr $ra                 # return sum
```
**Explanation:** For loop with condition i <= n, implemented using SLT to check n < i for exit condition.

### Exercise 15: Find Maximum in Array
**C Code:**
```c
int max_in_array(int *arr, int len) {
    int max = arr[0];
    for (int i = 1; i < len; i++) {
        if (arr[i] > max) 
            max = arr[i];
    }
    return max;
}
```
**MIPS:** (arr in $a0, len in $a1, return in $v0)
```mips
max_in_array:
    lw $v0, 0($a0)          # max = arr[0]
    addi $t0, $zero, 1      # i = 1

loop_max:
    slt $t1, $t0, $a1       # $t1 = (i < len) ? 1 : 0
    beq $t1, $zero, done_max # if i >= len, done
    sll $t2, $t0, 2         # offset = i * 4
    add $t3, $a0, $t2       # address = &arr[i]
    lw $t4, 0($t3)          # $t4 = arr[i]
    slt $t5, $v0, $t4       # $t5 = (max < arr[i]) ? 1 : 0
    beq $t5, $zero, skip_update # if max >= arr[i], skip
    move $v0, $t4           # max = arr[i]
skip_update:
    addi $t0, $t0, 1        # i++
    j loop_max              # continue loop

done_max:
    jr $ra                  # return max
```
**Explanation:** Array traversal with conditional update of maximum value using comparison and branching.

### Exercise 16: Matrix Addition (2x2)
**C Code:**
```c
void add_mat2x2(int *A, int *B, int *C) {
    for (int i = 0; i < 4; i++) {
        C[i] = A[i] + B[i];
    }
}
```
**MIPS:** (A in $a0, B in $a1, C in $a2)
```mips
add_mat2x2:
    addi $t0, $zero, 0      # i = 0

loop_mat:
    slti $t1, $t0, 4        # $t1 = (i < 4) ? 1 : 0
    beq $t1, $zero, end_mat # if i >= 4, done
    sll $t2, $t0, 2         # offset = i * 4

    add $t3, $a0, $t2       # address of A[i]
    lw $t4, 0($t3)          # $t4 = A[i]

    add $t5, $a1, $t2       # address of B[i]
    lw $t6, 0($t5)          # $t6 = B[i]

    add $t7, $t4, $t6       # $t7 = A[i] + B[i]

    add $t8, $a2, $t2       # address of C[i]
    sw $t7, 0($t8)          # C[i] = A[i] + B[i]

    addi $t0, $t0, 1        # i++
    j loop_mat              # continue loop

end_mat:
    jr $ra                  # return
```
**Explanation:** Processes matrices as linear arrays, accessing corresponding elements with same offset.

### Exercise 17: Factorial (Recursive)
**C Code:**
```c
int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
```
**MIPS:** (n in $a0, return in $v0)
```mips
factorial:
    addi $sp, $sp, -8       # Allocate stack frame
    sw $ra, 4($sp)          # Save return address
    sw $a0, 0($sp)          # Save n

    slti $t0, $a0, 2        # $t0 = (n < 2) ? 1 : 0
    bne $t0, $zero, base_case # if n < 2, return 1

    addi $a0, $a0, -1       # argument = n - 1
    jal factorial           # recursive call factorial(n-1)
    lw $a0, 0($sp)          # restore original n
    mul $v0, $a0, $v0       # result = n * factorial(n-1)
    j finish_fact

base_case:
    addi $v0, $zero, 1      # return 1

finish_fact:
    lw $ra, 4($sp)          # restore return address
    addi $sp, $sp, 8        # deallocate stack frame
    jr $ra                  # return to caller
```
**Explanation:** Recursive function with proper stack management for preserving registers across calls.

### Exercise 18: Fibonacci (Recursive)
**C Code:**
```c
int fib(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    return fib(n - 1) + fib(n - 2);
}
```
**MIPS:** (n in $a0, return in $v0)
```mips
fib:
    addi $sp, $sp, -12      # Stack frame for 3 values
    sw $ra, 8($sp)          # Save return address
    sw $a0, 4($sp)          # Save n
    sw $s0, 0($sp)          # Save $s0 for temp storage

    beq $a0, $zero, fib_zero # if n == 0, return 0
    addi $t0, $zero, 1
    beq $a0, $t0, fib_one   # if n == 1, return 1

    # Compute fib(n-1)
    addi $a0, $a0, -1       # argument = n - 1
    jal fib                 # call fib(n-1)
    move $s0, $v0           # save fib(n-1) in $s0

    # Compute fib(n-2)
    lw $a0, 4($sp)          # restore original n
    addi $a0, $a0, -2       # argument = n - 2
    jal fib                 # call fib(n-2)
    add $v0, $v0, $s0       # result = fib(n-1) + fib(n-2)
    j fib_done

fib_zero:
    addi $v0, $zero, 0      # return 0
    j fib_done

fib_one:
    addi $v0, $zero, 1      # return 1

fib_done:
    lw $ra, 8($sp)          # restore return address
    lw $a0, 4($sp)          # restore n (if needed)
    lw $s0, 0($sp)          # restore $s0
    addi $sp, $sp, 12       # deallocate stack frame
    jr $ra                  # return
```
**Explanation:** Double recursion requires careful stack management to preserve values across multiple function calls.

### Exercise 19: Recursive Array Sum
**C Code:**
```c
int sum_array_rec(int *arr, int n) {
    if (n == 0) return 0;
    return arr[0] + sum_array_rec(arr + 1, n - 1);
}
```
**MIPS:** (arr in $a0, n in $a1, return in $v0)
```mips
sum_array_rec:
    addi $sp, $sp, -8       # Stack frame
    sw $ra, 4($sp)          # Save return address
    sw $a1, 0($sp)          # Save n

    beq $a1, $zero, base_sum # if n == 0, return 0
    lw $t0, 0($a0)          # $t0 = arr[0]
    addi $a0, $a0, 4        # arr = arr + 1 (next element)
    addi $a1, $a1, -1       # n = n - 1
    jal sum_array_rec       # recursive call
    add $v0, $v0, $t0       # result = arr[0] + recursive_sum
    j done_sum_rec

base_sum:
    addi $v0, $zero, 0      # return 0

done_sum_rec:
    lw $ra, 4($sp)          # restore return address
    lw $a1, 0($sp)          # restore n (if needed)
    addi $sp, $sp, 8        # deallocate stack
    jr $ra                  # return
```
**Explanation:** Recursion with pointer arithmetic - moves array pointer forward and decreases count.
## C to MIPS Assembly Exercises

### Exercise : GCD using Euclidean Algorithm
**C Code:**
```c
int gcd(int a, int b) {
    if (b == 0) return a;
    return gcd(b, a % b);
}
```
**MIPS:** (`a` in `$a0`, `b` in `$a1`, return in `$v0`)
```mips
gcd:
    beq $a1, $zero, gcd_base    # if b == 0
    div $a0, $a1                # divide a by b
    mfhi $t0                    # t0 = a % b
    move $a0, $a1               # new a = b
    move $a1, $t0               # new b = a % b
    jal gcd
    jr $ra
gcd_base:
    move $v0, $a0               # return a
    jr $ra
```

### Exercise 20: Factorial (For Loop)
**C Code:**
```c
int factorial_for(int n) {
    int fact = 1;
    for (int i = 1; i <= n; i++) {
        fact *= i;
    }
    return fact;
}
```
**MIPS:** (`n` in `$a0`, return value in `$v0`)
```mips
factorial_for:
    addi $v0, $zero, 1          # fact = 1
    addi $t0, $zero, 1          # i = 1
loop_fact:
    bgt $t0, $a0, end_fact      # if i > n, exit loop
    mul $v0, $v0, $t0           # fact *= i
    addi $t0, $t0, 1            # i++
    j loop_fact
end_fact:
    jr $ra                      # return fact
```
**Explanation:** Iterative factorial using a for-loop structure with initialization, condition check, and increment.
