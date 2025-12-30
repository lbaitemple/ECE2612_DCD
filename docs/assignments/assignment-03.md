---
layout: default
title: Assignment 3 - Verilog HDL
parent: Assignments
nav_order: 4
---

# Assignment 3: Verilog HDL Programming
**Module 3 - Verilog HDL**

---

## Assignment Information

- **Due Date**: End of Week 4
- **Points**: 100
- **Submission**: Canvas (PDF + Verilog files)
- **Type**: Individual
- **Estimated Time**: 10-12 hours

---

## Learning Objectives

- Master Verilog modeling styles (dataflow, behavioral, structural)
- Design and instantiate hierarchical modules
- Write comprehensive testbenches
- Debug Verilog code using simulation
- Implement arithmetic circuits in HDL

---

## Problems

### Problem 1: Verilog Modeling Styles (25 points)

Design a 4:1 multiplexer using three different Verilog modeling styles.

**Specification**:
- **Inputs**: `D[3:0]` (data), `SEL[1:0]` (select)
- **Output**: `Y` (selected input)

**Part A: Gate-Level/Structural (8 points)**
```verilog
module mux4to1_structural (
    input  wire [3:0] D,
    input  wire [1:0] SEL,
    output wire       Y
);
    // Implement using primitive gates (and, or, not)
endmodule
```

**Part B: Dataflow (8 points)**
```verilog
module mux4to1_dataflow (
    input  wire [3:0] D,
    input  wire [1:0] SEL,
    output wire       Y
);
    // Implement using conditional operator or boolean expressions
endmodule
```

**Part C: Behavioral (9 points)**
```verilog
module mux4to1_behavioral (
    input  wire [3:0] D,
    input  wire [1:0] SEL,
    output reg        Y
);
    // Implement using always block with case statement
endmodule
```

Include testbench that verifies all three produce identical results.

---

### Problem 2: Combinational Logic with Testbench (30 points)

Design a 4-bit comparator with comprehensive testbench.

**Specification**:
- **Inputs**: `A[3:0]`, `B[3:0]`
- **Outputs**: `A_GT_B`, `A_EQ_B`, `A_LT_B` (exactly one high)

**Part A: Design (15 points)**
Implement using:
1. Behavioral Verilog
2. Proper output logic (mutual exclusion)
3. Comments explaining operation

**Part B: Testbench (15 points)**
Write testbench that:
1. Tests all equal cases (A = B)
2. Tests boundary cases (0, 15)
3. Tests random comparisons
4. Uses `$display` to show results
5. Automatically checks correctness

Requirements:
- Minimum 20 test vectors
- Self-checking (displays PASS/FAIL)
- Simulation waveform screenshot

---

### Problem 3: Hierarchical Design (20 points)

Design a 4-bit ripple carry adder using structural instantiation.

Create:
1. **Full Adder Module** (10 points)
   - Inputs: `A`, `B`, `CIN`
   - Outputs: `SUM`, `COUT`
   - Use dataflow or behavioral

2. **4-Bit Adder Module** (10 points)
   - Instantiate 4 full adders
   - Connect carry chain
   - Inputs: `A[3:0]`, `B[3:0]`, `CIN`
   - Outputs: `SUM[3:0]`, `COUT`

Include block diagram showing connections.

---

### Problem 4: FPGA Calculator Enhancement (25 points)

Extend the Assignment 1 calculator to support subtraction and display on 7-segment.

**Features**:
- Operations: AND, OR, ADD, SUB (4 operations)
- Inputs: SW[3:0] = A, SW[7:4] = B, SW[9:8] = OP
- Outputs: HEX0 = result (hexadecimal), LEDR[4] = overflow/borrow

**Requirements**:
- Top-level module with pin assignments
- Testbench simulation
- Hardware demonstration (photos/video)
- Brief documentation

---

## Grading Rubric

### Problem 1 (25 points)
- Each modeling style: 8-9 points
- Code correctness: 60%
- Code quality: 20%
- Testbench: 20%

### Problem 2 (30 points)
- Design correctness: 15 points
- Testbench quality: 10 points
- Self-checking: 3 points
- Documentation: 2 points

### Problem 3 (20 points)
- Full adder: 10 points
- 4-bit adder structure: 7 points
- Block diagram: 3 points

### Problem 4 (25 points)
- Verilog implementation: 15 points
- FPGA demonstration: 7 points
- Documentation: 3 points

---

## Resources
- Verilog HDL Quick Reference
- ModelSim Tutorial
- Testbench Writing Guide
- Module 3 lecture notes

---

**Start early! Verilog debugging takes time.** 💻
