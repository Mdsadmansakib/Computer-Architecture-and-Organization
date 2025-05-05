# Basic Information Types and Number Representations

## 1. Basic Information Types

Information can be categorized into the following types:
- Instruction
- Data
- Nonnumerical data
- Numbers
  - Fixed-point (Binary and Decimal)
  - Floating-point (Binary and Decimal)

## 2. Word Length

Word length is defined in bits with specific naming conventions:

| Bits | Name | Description |
|------|------|-------------|
| 1 | Bit | Logic variable, flag |
| 8 | Byte | Smallest addressable memory item, Binary-coded decimal digit pair |
| 16 | Halfword | Short fixed-point number, Short address, Short instruction |
| 32 | Word | Fixed or floating point number, Memory address, Instruction |
| 64 | Double word | Long instruction, Double-precision floating point number |

## 3. Byte Storage

### Bit and Byte Indexing
```
Byte 0  Byte 1  Byte 2  Byte 3
0       7       15      23      31
^                               ^
Least significant bit           Most significant bit
```

### Big-Endian Storage Method
- Used by Motorola 680X0 processors
- The most significant byte (MSB) is stored at the lowest address
- Example word W₁ represented as B₁,₃ B₁,₂ B₁,₁ B₁,₀:

```
Memory Address | Content
---------------|--------
...000         | Byte 0,3 (MSB)
...001         | Byte 0,2
...002         | Byte 0,1
...003         | Byte 0,0 (LSB)
...004         | Byte 1,3 (MSB)
...005         | Byte 1,2
...006         | Byte 1,1
...007         | Byte 1,0 (LSB)
```

### Little-Endian Storage Method
- Used by Intel x86 processors
- The least significant byte (LSB) is stored at the lowest address
- Example word W₁ represented as B₁,₀ B₁,₁ B₁,₂ B₁,₃:

```
Memory Address | Content
---------------|--------
...000         | Byte 0,0 (LSB)
...001         | Byte 0,1
...002         | Byte 0,2
...003         | Byte 0,3 (MSB)
...004         | Byte 1,0 (LSB)
...005         | Byte 1,1
...006         | Byte 1,2
...007         | Byte 1,3 (MSB)
```

## 4. Tags

Tags are a group of bits associated with information words that identify the word's type.

### Format Example (B6500/7500 Series)
```
0       4       7       51
|-------|-------|-------|
   Tags   Parity   Information Bits
```

### Tag Interpretation Example
| Tag | Interpretation |
|-----|----------------|
| 000 | Single-precision number |
| 001 | Indirect reference word |
| 010 | Double-precision number |
| 011 | Segment descriptor |
| 100 | Step-index control word |
| 101 | Data descriptor |
| 110 | Uninitialized operand |
| 111 | Instruction |

### Advantages of Tags
- Simplifies instruction specifications
- Enables hardware to check for software errors

### Disadvantages of Tags
- Increases memory size
- Adds system hardware costs without improving computing performance

## 5. Error Detection and Correction

### Parity Bit
- Appended to an n-bit word to form an (n+1)-bit word
- For even parity: c₀ = x₀ ⊕ x₁ ⊕ ... ⊕ xₙ₋₁
- For odd parity: c₀' = x₀ ⊕ x₁ ⊕ ... ⊕ xₙ₋₁

### Error Detection Process
When a receiver B gets word X' = (x'₀, x'₁, ..., x'ₙ₋₁, c'₀):
1. Calculate c*₀ = x'₀ ⊕ x'₁ ⊕ ... ⊕ x'ₙ₋₁
2. If c'₀ ≠ c*₀, then an error has occurred
3. If c'₀ = c*₀, there is no single-bit error

## 6. Number Representation Selection Factors

When choosing a number representation format, consider:
- Types of numbers to represent (integers, real numbers)
- Required range of values (magnitude)
- Required precision (accuracy)
- Hardware cost for storage and processing

## 7. Fixed-Point Binary Numbers

### Unsigned Binary Format
- Form: bₙ...b₁b₀.b₋₁b₋₂...b₋ₘ (each bᵢ is 0 or 1)
- Represents: ∑bᵢ × 2ⁱ (where -M ≤ i ≤ N)
- Uses positional notation where each digit has a fixed weight

### Signed Binary Format
- Form: xₙ₋₁xₙ₋₂...x₁x₀
- Using n-bit format can represent integers with magnitude |N| in range 0 ≤ |N| ≤ 2ⁿ⁻¹

### Signed Number Representations

#### Sign-Magnitude
- Uses a sign bit and magnitude bits
- Example: +75 = 01001011, -75 = 11001011

#### 1's Complement
- Invert all bits to negate
- Example: +75 = 01001011, -75 = 10110100

#### 2's Complement
- Invert all bits and add 1 to negate
- Example: +75 = 01001011, -75 = 10110101

#### Comparison Table
| Decimal | Sign-Magnitude | 1's Complement | 2's Complement |
|---------|----------------|----------------|----------------|
| +7      | 0111           | 0111           | 0111           |
| +6      | 0110           | 0110           | 0110           |
| +5      | 0101           | 0101           | 0101           |
| +4      | 0100           | 0100           | 0100           |
| +3      | 0011           | 0011           | 0011           |
| +2      | 0010           | 0010           | 0010           |
| +1      | 0001           | 0001           | 0001           |
| +0      | 0000           | 0000           | 0000           |
| -0      | 1000           | 1111           | 0000           |
| -1      | 1001           | 1110           | 1111           |
| -2      | 1010           | 1101           | 1110           |
| -3      | 1011           | 1100           | 1101           |
| -4      | 1100           | 1011           | 1100           |
| -5      | 1101           | 1010           | 1011           |
| -6      | 1110           | 1001           | 1010           |
| -7      | 1111           | 1000           | 1001           |

### Advantages of 2's Complement
- Subtraction can be performed by logical complementation and addition
- Addition and subtraction can be implemented by a simple adder for unsigned numbers
- No duplicate representation for zero

### Disadvantages of 2's Complement
- Multiplication and division are more difficult to implement

## 8. Decimal Codes

### BCD (Binary Coded Decimal)
- Each decimal digit dᵢ is represented by 4 bits (bᵢ,₃ bᵢ,₂ bᵢ,₁ bᵢ,₀)
- Weighted positional code where each bᵢ,ⱼ has weight 10ⁱ × 2ʲ

### ASCII
- 8-bit code where decimal digits use a 4-bit BCD field
- Remaining 4 bits have no numerical significance

### Excess-Three Code
- Formed by adding 0011₂ (3₁₀) to the corresponding BCD number
- Advantage: can be processed using the same logic as binary codes
- Disadvantage: non-weighted code, making some arithmetic operations difficult

Example of addition with excess-three:
```
1000 = 5 (excess-three)
+ 1100 = 9 (excess-three)
------
Carry 1 0100 (binary sum)
+ 0011 (correction)
------
0111 = 4 (excess-three sum)
```

### Two-out-of-Five Code
- Each decimal digit uses 5 bits containing exactly two 1s and three 0s
- Single-error detecting (changing any bit results in an invalid code)
- Uses 5 bits per digit (more than BCD's 4 bits)

### Decimal Code Comparison Table
| Decimal Digit | BCD    | ASCII     | Excess-three | Two-out-of-five |
|---------------|--------|-----------|--------------|-----------------|
| 0             | 0000   | 00110000  | 0011         | 11000           |
| 1             | 0001   | 00110001  | 0100         | 00011           |
| 2             | 0010   | 00110010  | 0101         | 00101           |
| 3             | 0011   | 00110011  | 0110         | 00110           |
| 4             | 0100   | 00110101  | 0111         | 01001           |
| 5             | 0101   | 00110101  | 1000         | 01010           |
| 6             | 0110   | 00110110  | 1001         | 01100           |
| 7             | 0111   | 00110111  | 1010         | 10001           |
| 8             | 1000   | 00111000  | 1011         | 10010           |
| 9             | 1001   | 00111001  | 1100         | 10100           |

### Hexadecimal Numbers
- Base-16 system using digits 0-9 and A-F (A=10, B=11, C=12, D=13, E=14, F=15)
- Useful for compact representation of binary numbers
- Each hexadecimal digit represents 4 binary digits

## 9. Floating-Point Numbers

### Need for Floating-Point
- Fixed-point has insufficient range for many applications
- Scientific notation allows representation of very large and very small numbers
- Example: 1.0 × 10¹⁸ is more compact than 1,000,000,000,000,000,000

### Basic Format
- Three components: mantissa (M), exponent (E), and base (B)
- Real number represented as M × Bᴱ
- Example: 1.0 × 10¹⁸ (M=1.0, B=10, E=18)

### Representation in Memory
- Stored as a word (M,E) with two signed fixed-point numbers
- Base B is constant and built into the processing circuits
- Precision determined by number of digits in M
- Range determined by B and E

### Example of 6-bit Floating-Point Format
With M and E both as 3-bit sign-magnitude numbers, B=2:
- Smallest positive number: (001, 111) = 1 × 2⁻³ = 0.125
- Smallest negative number: (111, 111) = -3 × 2⁻³ = -0.375
- Largest positive number: (011, 011) = 3 × 2³ = 24
- Largest negative number: (111, 011) = -3 × 2³ = -24

### Approximation in Floating-Point
- Most real numbers are only approximated
- Example: 1.25 might be approximated by 1.5 or 1.0
- Most calculations yield approximate results
- Guard digits can be used to reduce approximation errors

### Normalization
- Creates a unique form for each representable number
- Binary normalization typically has one non-zero digit to the left of the decimal point
- IEEE 754 uses normalized form 1.M
- Process: shift mantissa and adjust exponent to achieve normalized form

#### Advantages of Normalization
- Simplifies data exchange
- Simplifies floating-point arithmetic algorithms
- Increases accuracy by replacing leading zeros with significant digits

## 10. IEEE 754 Standard

### 32-bit Single-Precision Format
```
1 bit     8 bits    23 bits
| Sign | Exponent | Mantissa |
```
- Sign (S): 1 bit for sign representation
- Exponent (E): 8-bit excess-127 format (actual exponent = E-127)
- Mantissa (M): 23-bit fraction part with hidden leading 1
- Real number N = (-1)ˢ × 2ᴱ⁻¹²⁷ × (1.M) where 0 < E < 255

### 64-bit Double-Precision Format
```
1 bit     11 bits    52 bits
| Sign | Exponent | Mantissa |
```
- Sign (S): 1 bit
- Exponent (E): 11-bit excess-1023 format (actual exponent = E-1023)
- Mantissa (M): 52-bit fraction
- Real number N = (-1)ˢ × 2ᴱ⁻¹⁰²³ × (1.M) where 0 < E < 2047

### Biased Exponent
- Makes comparison of floating-point numbers easier
- Exponents encoded in excess-K code where E = actual_exponent + K
- Example with excess-127:
  - Exponent -1: -1+127=126=01111110₂
  - Exponent +1: +1+127=128=10000000₂

#### Biased Exponent Table (8-bit)
| Exponent E | Unsigned value | Bias 127 | Bias 128 |
|------------|----------------|----------|----------|
| 11111111   | 255           | +128     | +127     |
| 11111110   | 254           | +127     | +126     |
| ...        | ...           | ...      | ...      |
| 10000001   | 129           | +2       | +1       |
| 10000000   | 128           | +1       | 0        |
| 01111111   | 127           | 0        | -1       |
| 01111110   | 126           | -1       | -2       |
| ...        | ...           | ...      | ...      |
| 00000001   | 1             | -126     | -127     |
| 00000000   | 0             | -127     | -128     |

## 11. Converting Decimal to Binary Floating-Point

### Example: Convert -12.25₁₀ to IEEE 754 Single-Precision

Step 1: Convert to binary
-12.25₁₀ = -1100.01₂

Step 2: Normalize
-1100.01₂ = -1.10001₂ × 2³

Step 3: Determine components
- Sign (S) = 1 (negative)
- Exponent (E) = 3 + 127 = 130 = 10000010₂
- Mantissa (M) = 10001000000000000000000₂

Step 4: Combine
Final representation = 11000001010001000000000000000000₂

## 12. Special Cases

### Overflow
- Occurs when a positive exponent becomes too large to fit in the exponent field

### Underflow
- Occurs when a negative exponent becomes too large (in magnitude) to fit in the exponent field

## 13. Key Takeaways

- **Fixed-point numbers**: Simple but with limited range and precision
- **Floating-point numbers**: Flexible range and precision but more complex arithmetic
- **Standards like IEEE 754**: Ensure compatibility across different systems
- **Trade-offs**: Hardware cost vs. performance vs. accuracy
