# Lecture 05: Performance of a Computer

## 📌 Key Concepts

### 🕒 Response Time (Execution Time)
- Time between the **start and completion** of a task.
- Includes:
  - Disk accesses
  - Memory accesses
  - I/O activities
  - OS overhead
  - CPU execution time

### 📈 Throughput
- Total amount of **job done in a fixed time**.
- Decreasing response time often improves throughput.

---

## 🔁 Performance and Execution Time

- **PerformanceX = 1 / Execution TimeX**
- If `PerformanceX > PerformanceY`, then:
  - `Execution TimeY > Execution TimeX`

- If **X is n times faster than Y**:
  - `PerformanceX / PerformanceY = n`
  - or `Execution TimeY / Execution TimeX = n`

### 💡 Relative Performance Example
If A runs in **10s** and B in **15s**:
- `PerformanceA / PerformanceB = 15 / 10 = 1.5`
- So A is **1.5 times faster** than B.

---

## ⏲ Measuring Performance

- **Time** is the main performance metric.
- In shared systems, **throughput** may be optimized.
- **CPU Time**: Time CPU spends computing a task (not I/O or other programs)

### 🧠 CPU Time Breakdown
- **User CPU Time**: Time in user program.
- **System CPU Time**: Time in OS services (e.g., file handling).

### 🧮 Example
- User Time: 90.7s
- System Time: 12.9s
- Elapsed Time: 159s
- **CPU Utilization** = (90.7 + 12.9) / 159 ≈ **65.2%**

- **System Performance** = Elapsed time on **unloaded system**
- **CPU Performance** = User CPU time on **unloaded system**

---

## ⏰ Clock Cycles & Rates

- Computer events are synced using a **clock**.
- **Clock Period**: Time for 1 cycle.
- **Clock Rate** = 1 / Clock Period

---

## ⚙️ CPU Time Formulas

1. `CPU Time = CPU Cycles × Clock Cycle Time`
2. `CPU Time = CPU Cycles / Clock Rate`

### 🧮 CPI (Cycles per Instruction)
- `CPI = CPU Clock Cycles / Instruction Count (IC)`
- `IPC (Instructions per Clock) = 1 / CPI`

### 🔁 CPU Time Full Form
- `CPU Time = Instruction Count × CPI × Clock Cycle Time`
- Or, `T = N × CPI / f`  (Where `f` = Clock Rate)

---

## 🧩 CPU Cycles by Instruction Type

- `CPU Clock Cycles = Σ (CPIi × Ci)`
  - `Ci`: Count of instructions in class `i`
  - `CPIi`: Cycles per instruction of class `i`

---

## 🧪 Comparing Code Sequences

### Example:
**Sequence 1**: 5 instructions  
**Sequence 2**: 6 instructions

CPI Table:

| Class | CPI |
|-------|-----|
| A     | 1   |
| B     | 2   |
| C     | 3   |

Instruction count:

| Sequence | A | B | C |
|----------|---|---|---|
| 1        | 2 | 1 | 2 |
| 2        | 4 | 1 | 1 |

**CPU Cycles**:
- Seq1: 2×1 + 1×2 + 2×3 = 10
- Seq2: 4×1 + 1×2 + 1×3 = 9

**CPI**:
- Seq1: 10 / 5 = 2
- Seq2: 9 / 6 = 1.5 → **Faster**

---

## 🧠 Practice Problem

> A program runs in **10s** on computer A (2GHz).  
> We want computer B to run it in **6s**.  
> But B uses **1.2×** more clock cycles than A.

**Find the required clock rate for B**.

### Solution:

Let:
- `T_A = 10s`
- `f_A = 2 GHz`
- `T_B = 6s`
- `Cycles_B = 1.2 × Cycles_A`

From CPU time formula:  
- `T = C / f` ⇒ `C = T × f`

So:
- `C_A = 10 × 2GHz = 20G cycles`
- `C_B = 1.2 × 20G = 24G`

Required clock rate for B:
- `f_B = C_B / T_B = 24G / 6 = 4 GHz`

✅ **Target: 4 GHz**

---

## 🔍 Components Affecting Performance

| Component           | Affects              |
|---------------------|----------------------|
| Algorithm           | Instruction Count    |
| Programming Language| IC, CPI              |
| Compiler            | IC, CPI              |
| ISA                 | IC, Clock Rate, CPI  |

---

## 🚀 Speedup Techniques

| Feature               | Objective                                                  |
|------------------------|------------------------------------------------------------|
| **Cache Memory**       | Faster access to data/instructions                         |
| **Pipelined Processing** | Overlap instruction execution stages                       |
| **Superscalar Processing** | Parallel processing of multiple instructions              |

---

## 🔁 Sequential vs. Pipelined Processing

- **Sequential**: Instructions processed one at a time.
- **Pipelined**: Stages of multiple instructions processed in parallel.

---

## 📝 Exercises

### 1. Conceptual
a. Differentiate between **response time** and **throughput**.  
b. Define **CPU Time** and distinguish **User** vs **System** time.

### 2. Calculation
Given:
- A program runs in 20s on 3GHz CPU
- CPU B has 1.5× the clock rate but 1.2× the CPI

**Q: Which CPU is faster and by how much?**

---

### 3. Code Segment Analysis

Given:

| Class | CPI |
|-------|-----|
| A     | 1   |
| B     | 2   |
| C     | 4   |

| Code | A | B | C |
|------|---|---|---|
| X    | 3 | 1 | 2 |
| Y    | 5 | 2 | 1 |

Find:
- Total clock cycles for X and Y
- CPI for each
- Which is faster?

---

### 4. Practice Design
Suppose a designer can reduce CPI by 15% but clock rate drops by 10%.  
Will performance improve or degrade? Justify with formula.

---

### 5. Real-Life Interpretation
Explain with example how compiler choice can affect instruction count and CPI.

---

