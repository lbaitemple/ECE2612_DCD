---
layout: default
title: Assignment 5 - Binary Arithmetic
parent: Assignments
nav_order: 6
---

# Assignment 5: Binary Arithmetic and ALU Design
**Module 5 - Binary Arithmetic**

---

## Assignment Information

- **Due Date**: End of Week 6
- **Points**: 100
- **Submission**: Canvas (PDF + Verilog files)
- **Type**: Individual
- **Estimated Time**: 10-12 hours

---

## Learning Objectives

- Design adder and subtractor circuits
- Implement arithmetic operations in Verilog
- Understand carry propagation and optimization
- Build arithmetic logic units (ALUs)
- Analyze timing and critical paths

---

## Problems

### Problem 1: Adder Design (25 points)

**Part A: Full Adder Analysis (10 points)**

For a full adder:
1. Derive Sum and Carry equations from truth table
2. Draw gate-level implementation (minimum gates)
3. Implement in Verilog (gate-level and behavioral)
4. Calculate propagation delay assuming: AND=2ns, OR=2ns, XOR=3ns

**Part B: 4-Bit Ripple Carry Adder (15 points)**
1. Design using structural Verilog (instantiate 4 full adders)
2. Analyze worst-case delay
3. Create testbench with 10+ test cases
4. Implement on FPGA with switches and LEDs

---

### Problem 2: Subtractor and 2's Complement (20 points)

**Part A: Subtractor Design (10 points)**

Design 4-bit subtractor (A - B) using:
1. 2's complement method (invert B, add 1)
2. Shared adder/subtractor circuit (controlled by SUB signal)
3. Verilog implementation
4. Truth table for borrow detection

**Part B: Signed Arithmetic (10 points)**
1. Perform: `0110 - 1001` (6 - 9) in 4-bit two's complement
2. Detect overflow for: `0111 + 0001`, `1000 - 0001`
3. Implement overflow detection logic in Verilog

---

### Problem 3: Carry Lookahead Adder (30 points)

**Part A: Theory (15 points)**

For 4-bit carry lookahead:
1. Derive generate (G) and propagate (P) equations
2. Derive carry equations: C1, C2, C3, C4
3. Draw block diagram
4. Compare delay with ripple carry (show calculation)

**Part B: Verilog Implementation (15 points)**
1. Implement 4-bit CLA in Verilog
2. Create testbench comparing CLA vs ripple carry
3. Synthesize both, compare area and timing
4. Document results in table

---

### Problem 4: Barrel Shifter (25 points)

**Objective**: Design a 4-bit barrel shifter with shift and rotate modes.

**Specification**:
- **Inputs**: `DATA[3:0]`, `SHIFT_AMT[1:0]`, `DIR` (0=left, 1=right), `MODE` (0=shift, 1=rotate)
- **Output**: `RESULT[3:0]`

**Part A: Design (15 points)**
1. Truth table for all combinations
2. Verilog implementation (use case statement)
3. Handle logical shift (fill with 0) vs rotate

**Part B: FPGA Implementation (10 points)**
1. Implement on DE10-Lite
2. SW[3:0] = data, SW[5:4] = shift amount
3. SW[6] = direction, SW[7] = mode
4. Display: HEX0 = input, HEX1 = output
5. Demonstrate with photos/video

---

## Grading Rubric

### Problem 1 (25 points)
- Equations and gate diagram: 10 points
- Verilog full adder: 5 points
- 4-bit RCA: 7 points
- FPGA demo: 3 points

### Problem 2 (20 points)
- Subtractor design: 10 points
- Signed arithmetic: 7 points
- Verilog implementation: 3 points

### Problem 3 (30 points)
- CLA theory and equations: 15 points
- Verilog implementation: 10 points
- Comparison analysis: 5 points

### Problem 4 (25 points)
- Design and truth table: 10 points
- Verilog: 10 points
- FPGA demo: 5 points

---

## Resources
- Adder Design Tutorial
- Carry Lookahead Logic
- Barrel Shifter Examples
- Timing Analysis Guide

---

**Focus on understanding carry propagation—it's key to fast arithmetic!** ⚡
