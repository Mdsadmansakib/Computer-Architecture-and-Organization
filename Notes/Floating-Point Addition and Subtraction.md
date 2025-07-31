# Floating-Point Addition and Subtraction - Complete Guide

## Introduction

Floating-point addition and subtraction are fundamental arithmetic operations in computer systems. Unlike integer arithmetic, floating-point operations require careful handling of the exponent and mantissa components to maintain precision and proper normalization.

## Floating-Point Number Representation

### IEEE 754 Standard Format (32-bit)
```
Sign | Exponent (8 bits) | Mantissa/Fraction (23 bits)
  S  |    E₇E₆...E₀      |      M₂₂M₂₁...M₀
```

- **Sign bit (S)**: 0 = positive, 1 = negative
- **Exponent (E)**: Biased by 127 (actual exponent = E - 127)
- **Mantissa (M)**: Fractional part with implicit leading 1

### Normalized Form
A normalized floating-point number has the form:
```
(-1)ˢ × 1.M × 2^(E-127)
```



![Visual](https://github.com/Mdsadmansakib/Computer-Architecture-and-Organization/blob/main/Notes/Assets/floating_point_pipeline_interactive.jpg) 
## Algorithm for Floating-Point Addition/Subtraction

### Step-by-Step Process

#### Step 1: Exponent Comparison
```
Compare the exponents of the two operands
Determine which number has the larger exponent
Calculate the difference: |E₁ - E₂|
```

**Example:**
- A = 1.9505 × 2¹³ (exponent = 13)
- B = 0.8100 × 2¹² (exponent = 12)
- Difference = 13 - 12 = 1

#### Step 2: Mantissa Alignment
```
Shift the mantissa of the smaller number right
by the exponent difference
Pad with zeros on the right
```

**Example:**
- A mantissa: 0.9505 (no shift needed)
- B mantissa: 0.8100 → 0.4050 (shifted right by 1)

#### Step 3: Addition/Subtraction of Mantissas
```
If signs are same: Add the aligned mantissas
If signs are different: Subtract the aligned mantissas
Handle the sign of the result
```

**Addition Example:**
```
  0.9505
+ 0.4050
---------
  1.3555
```

**Subtraction Example:**
```
  0.9505
- 0.4050
---------
  0.5455
```

#### Step 4: Normalization
```
If result ≥ 2.0: Shift mantissa right, increment exponent
If result < 1.0: Shift mantissa left, decrement exponent
Round to fit precision requirements
```

**Addition Normalization:**
```
1.3555 × 2¹³ → 0.6777 × 2¹⁴
(shift right by 1, increment exponent)
```

## Pipelined Implementation

### 4-Stage Pipeline Architecture

```
Stage 1: Exponent Comparison    |  Stage 1: Mantissa Buffering
   ↓                           |     ↓
Stage 2: Exponent Selection    |  Stage 2: Mantissa Alignment
   ↓                           |     ↓
Stage 3: Exponent Buffering    |  Stage 3: Mantissa Add/Sub
   ↓                           |     ↓
Stage 4: Exponent Adjustment   |  Stage 4: Result Normalization
```

### Pipeline Registers
- **R1**: Input buffer for both operands
- **R2**: Stores exponent difference and aligned mantissas
- **R3**: Stores preliminary results
- **R4**: Final result buffer

### Pipeline Benefits
- **Throughput**: One result per clock cycle (after initial latency)
- **Latency**: 4 clock cycles for single operation
- **Efficiency**: Multiple operations processed simultaneously

## Detailed Example Walkthrough

### Example: 1.9505 × 2¹³ + 0.8100 × 2¹²

#### Initial Values
```
A: Sign=0, Exponent=13+127=140, Mantissa=0.9505
B: Sign=0, Exponent=12+127=139, Mantissa=0.8100
```

#### Stage 1: Exponent Comparison
```
Compare: 140 vs 139
Difference: 140 - 139 = 1
Larger exponent: 140 (from A)
```

#### Stage 2: Mantissa Alignment
```
A mantissa: 0.9505 (no change)
B mantissa: 0.8100 → 0.4050 (shift right by 1)
Selected exponent: 140
```

#### Stage 3: Mantissa Addition
```
Operation: 0.9505 + 0.4050 = 1.3555
Result exponent: 140
```

#### Stage 4: Normalization
```
Check: 1.3555 ≥ 1.0 but < 2.0
Since 1.3555 > 1.0, need to normalize:
1.3555 → 0.6777 (shift right by 1)
Exponent: 140 + 1 = 141
Final: 0.6777 × 2^(141-127) = 0.6777 × 2¹⁴
```

## Special Cases

### Zero Operands
```
A + 0 = A
0 + B = B
0 + 0 = 0
```

### Infinity and NaN
```
A + ∞ = ∞
∞ + ∞ = ∞
∞ - ∞ = NaN (Not a Number)
```

### Underflow and Overflow
- **Overflow**: Result exponent > 255 → ±∞
- **Underflow**: Result exponent < 0 → ±0 or denormalized

## Hardware Implementation Considerations

### Critical Components

#### Exponent Unit
- **Comparator**: Determines larger exponent
- **Subtractor**: Calculates difference
- **Incrementer/Decrementer**: Adjusts final exponent

#### Mantissa Unit
- **Shifter**: Aligns mantissas (barrel shifter)
- **Adder/Subtractor**: Performs arithmetic
- **Leading Zero Detector**: For normalization
- **Normalizer**: Shifts result mantissa

### Performance Optimizations

#### Parallel Processing
```
Exponent comparison || Mantissa preparation
Alignment || Exponent selection
Addition || Exponent adjustment
Normalization || Result formatting
```

#### Early Termination
- Detect zero operands early
- Skip unnecessary operations
- Handle special cases efficiently

## Timing Analysis

### Non-Pipelined Implementation
- **Latency**: 4T (where T = clock period)
- **Throughput**: 1/(4T)
- **N operations**: N × 4T time

### Pipelined Implementation
- **Latency**: 4T (same as non-pipelined)
- **Throughput**: 1/T (4× improvement)
- **N operations**: (N + 3)T time
- **Speedup**: S = 4N/(N+3) ≈ 4 for large N

## Error Handling and Precision

### Rounding Modes
1. **Round to Nearest**: Default IEEE 754 mode
2. **Round toward Zero**: Truncation
3. **Round toward +∞**: Ceiling
4. **Round toward -∞**: Floor

### Guard, Round, and Sticky Bits
```
Mantissa | Guard | Round | Sticky
   23b   |   1b  |   1b  |   1b
```

Used for accurate rounding in normalization step.

## Applications

### Digital Signal Processing
- **FIR/IIR Filters**: Coefficient multiplication and accumulation
- **FFT Operations**: Complex number arithmetic
- **Image Processing**: Pixel value calculations

### Scientific Computing
- **Matrix Operations**: Linear algebra computations
- **Numerical Integration**: Iterative algorithms
- **Simulation**: Physical system modeling

### Graphics Processing
- **3D Transformations**: Vertex calculations
- **Lighting Models**: Color computations
- **Texture Mapping**: Coordinate transformations

## Comparison: Addition vs Subtraction

| Aspect | Addition | Subtraction |
|--------|----------|-------------|
| **Mantissa Operation** | Simple addition | May require complement |
| **Result Sign** | Based on larger operand | Depends on magnitude difference |
| **Normalization** | May need right shift | May need left shift |
| **Complexity** | Lower | Higher (sign handling) |

## Summary

Floating-point addition and subtraction are complex operations requiring:

1. **Careful exponent handling** for proper alignment
2. **Precise mantissa arithmetic** with proper rounding
3. **Result normalization** to maintain IEEE 754 compliance
4. **Pipeline optimization** for high-performance implementations

The 4-stage pipeline provides an excellent balance between hardware complexity and performance, achieving nearly 4× speedup for sustained operations while maintaining IEEE 754 accuracy standards.

---

*Key Takeaway: Floating-point arithmetic is fundamentally different from integer arithmetic due to the need for alignment, normalization, and precision management, making pipelined implementations essential for high-performance computing systems.*
