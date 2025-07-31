# Booth's Multiplication Algorithm

## Introduction
An efficient algorithm for multiplying signed binary numbers in 2's complement representation. It optimizes processing by examining bit pairs to reduce operations.

## Key Advantages
- 🚀 **50% faster** than standard multiplication for certain bit patterns  
- 🔢 **Natively handles** positive/negative numbers  
- ⚡ **Hardware-friendly** design  
- 🔁 **Pipeline-compatible** structure  

## Flowchart

### Text Representation
```text
START
  │
  ▼
+---------------------+
| Initialize:         |
| A = 0, Q₋₁ = 0,    |
| M = Multiplicand,  |
| Q = Multiplier,    |
| Counter = n (bits) |
+---------------------+
  │
  ▼
+---------------------+
| Check LSB of Q (Q₀) |
| and Q₋₁:            |
| (Q₀, Q₋₁) = ?       |
+---------------------+
  │
  ├───────────┬───────────┐
  ▼           ▼           ▼
(0,0)      (0,1)      (1,0)      (1,1)
  │           │           │           │
  ▼           ▼           ▼           ▼
+-----+    +-----+    +-----+    +-----+
| ARS |    |A=A+M|  |A=A-M|   | ARS |
| (>>)|    +-----+    +-----+    | (>>)|
+-----+       │           │      +-----+
  │           ▼           ▼         │
  └─────────> ARS <───────┘         │
              (>>)                  │
                │                   │
                ▼                   ▼
           +---------------------+
           | Decrement Counter  |
           +---------------------+
                │
                ▼
           +-----------+
           | Counter=0?|
           +-----------+
                │
        No ┌────┘ └────┐ Yes
            ▼           ▼
+---------------------+     +---------------------+
| Update Q₋₁ = Q₀     |     |   Output:           |
| Shift AQQ₋₁ right   |     |   Result = AQ       |
| (Arithmetic Shift)  |     +---------------------+
+---------------------+               │
            │                         ▼
            └─────────────────────── STOP


```

##Visualization

![Booth's Algorithm Flowchart](https://github.com/Mdsadmansakib/Computer-Architecture-and-Organization/blob/main/Notes/Assets/booth_multiplication_demo.jpg) 
