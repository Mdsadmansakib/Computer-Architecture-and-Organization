# ARM & MIPS Architectures (RISC-Based)

## 🔹 ARM Architecture
- **Type**: RISC (Reduced Instruction Set Computer)
- **Developed by**: ARM Holdings (Acorn RISC Machine)
- **Key Features**:
  - Load-store architecture (only load/store instructions access memory)
  - Fixed-length 32-bit instructions (Thumb mode uses 16-bit)
  - Large register file (16-32 general-purpose registers)
  - Conditional execution (most instructions can be conditional)
  - Multiple addressing modes (including auto-indexing)
  - Pipelined execution (typically 3-5 stages)

- **Common Uses**:
  - Mobile devices (95% of smartphones)
  - Embedded systems
  - IoT devices
  - Recent Apple Silicon (M1/M2 chips)

## 🔹 MIPS Architecture
- **Type**: RISC (Like ARM)
- **Developed by**: MIPS Technologies (Stanford team)
- **Key Features**:
  - Fixed-length 32-bit instructions
  - 32 general-purpose registers
  - Pure load-store architecture
  - 5-stage pipeline (classic design)
  - Delayed branching (in early versions)
  - Simple addressing modes

- **Common Uses**:
  - Early workstations (SGI)
  - Network routers (Cisco)
  - Game consoles (PlayStation 1/2, Nintendo 64)
  - Automotive systems
  - Some embedded devices

## 🔁 ARM vs MIPS Comparison
| Feature        | ARM                          | MIPS                         |
|---------------|-----------------------------|-----------------------------|
| **Registers** | 16 (32 in ARMv8)            | 32                          |
| **ISA**       | ARM/Thumb (mixed 16/32-bit) | Pure 32-bit                 |
| **Market**    | Dominates mobile            | Declining in general use    |
| **Licensing** | IP-core licensing model     | Was open-sourced (RISC-V replaced it)|
| **Pipeline**  | Variable (3-13 stages)      | Classic 5-stage             |

## ✅ Why They're Both "RISC"
1. Fixed instruction length
2. Load-store architecture
3. Large register sets
4. Simple addressing modes
5. Pipelined execution (1 instruction/cycle ideal)

> **Note**: While ARM dominates mobile, MIPS has largely been replaced by RISC-V in new designs. Both demonstrate classic RISC principles.




# MIPS Instruction Set Reference

## Arithmetic Instructions
| Mnemonic | Example | Meaning | Notes |
|----------|---------|---------|-------|
| add | `add $s1,$s2,$s3` | `$s1 = $s2 + $s3` | Three register operands |
| sub | `sub $s1,$s2,$s3` | `$s1 = $s2 - $s3` | Three register operands |
| addi | `addi $s1,$s2,20` | `$s1 = $s2 + 20` | Immediate addition |
| mul | `mul $s1,$s2,$s3` | `$s1 = $s2 * $s3` | Multiplication (32-bit result) |
| div | `div $s1,$s2,$s3` | `$s1 = $s2 / $s3` | Division |

## Data Transfer Instructions
| Mnemonic | Example | Meaning | Notes |
|----------|---------|---------|-------|
| lw | `lw $s1,20($s2)` | `$s1 = Memory[$s2 + 20]` | Load word (32-bit) |
| sw | `sw $s1,20($s2)` | `Memory[$s2 + 20] = $s1` | Store word |
| lh | `lh $s1,20($s2)` | `$s1 = Memory[$s2 + 20]` | Load halfword (sign-extended) |
| lhu | `lhu $s1,20($s2)` | `$s1 = Memory[$s2 + 20]` | Load halfword (zero-extended) |
| sh | `sh $s1,20($s2)` | `Memory[$s2 + 20] = $s1` | Store halfword |
| lb | `lb $s1,20($s2)` | `$s1 = Memory[$s2 + 20]` | Load byte (sign-extended) |
| lbu | `lbu $s1,20($s2)` | `$s1 = Memory[$s2 + 20]` | Load byte (zero-extended) |
| sb | `sb $s1,20($s2)` | `Memory[$s2 + 20] = $s1` | Store byte |
| lui | `lui $s1,20` | `$s1 = 20 << 16` | Load upper immediate |
| mfhi | `mfhi $s1` | `$s1 = HI` | Move from HI register |
| mflo | `mflo $s1` | `$s1 = LO` | Move from LO register |

## Logical Instructions
| Mnemonic | Example | Meaning | Notes |
|----------|---------|---------|-------|
| and | `and $s1,$s2,$s3` | `$s1 = $s2 & $s3` | Bitwise AND |
| or | `or $s1,$s2,$s3` | `$s1 = $s2 | $s3` | Bitwise OR |
| nor | `nor $s1,$s2,$s3` | `$s1 = ~($s2 | $s3)` | Bitwise NOR |
| xor | `xor $s1,$s2,$s3` | `$s1 = $s2 ^ $s3` | Bitwise XOR |
| andi | `andi $s1,$s2,20` | `$s1 = $s2 & 20` | AND with immediate |
| ori | `ori $s1,$s2,20` | `$s1 = $s2 | 20` | OR with immediate |
| xori | `xori $s1,$s2,20` | `$s1 = $s2 ^ 20` | XOR with immediate |
| sll | `sll $s1,$s2,10` | `$s1 = $s2 << 10` | Shift left logical |
| srl | `srl $s1,$s2,10` | `$s1 = $s2 >> 10` | Shift right logical |
| sra | `sra $s1,$s2,10` | `$s1 = $s2 >> 10` | Shift right arithmetic |

## Control Flow Instructions
| Mnemonic | Example | Meaning | Notes |
|----------|---------|---------|-------|
| beq | `beq $s1,$s2,25` | `if ($s1 == $s2) PC += 4 + (25<<2)` | Branch equal |
| bne | `bne $s1,$s2,25` | `if ($s1 != $s2) PC += 4 + (25<<2)` | Branch not equal |
| slt | `slt $s1,$s2,$s3` | `$s1 = ($s2 < $s3) ? 1 : 0` | Set less than (signed) |
| sltu | `sltu $s1,$s2,$s3` | `$s1 = ($s2 < $s3) ? 1 : 0` | Set less than (unsigned) |
| slti | `slti $s1,$s2,20` | `$s1 = ($s2 < 20) ? 1 : 0` | Set less than immediate |
| sltiu | `sltiu $s1,$s2,20` | `$s1 = ($s2 < 20) ? 1 : 0` | Set less than unsigned immediate |
| j | `j 2500` | `PC = 2500<<2` | Jump |
| jr | `jr $ra` | `PC = $ra` | Jump register |
| jal | `jal 2500` | `$ra = PC+4; PC = 2500<<2` | Jump and link |

## Special Instructions
| Mnemonic | Example | Meaning | Notes |
|----------|---------|---------|-------|
| syscall | `syscall` | Invoke OS service | Service number in $v0 |
| break | `break` | Breakpoint trap | For debuggers |
| nop | `nop` | No operation | `sll $0,$0,0` |

## Pseudo-Instructions
| Mnemonic | Actual Implementation | Meaning |
|----------|----------------------|---------|
| move | `add $d,$s,$zero` | Copy register |
| li | `ori $d,$0,imm` or `lui+ori` | Load immediate |
| la | `lui+ori` | Load address |
| b | `beq $0,$0,label` | Unconditional branch |

**Notes:**
1. Immediate values are sign-extended unless specified as unsigned
2. Branch offsets are in words (PC = PC + 4 + offset<<2)
3. Jump targets are absolute word addresses (PC = target<<2)
4. Memory operations use base+offset addressing
