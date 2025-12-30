---
layout: default
title: Assignment 4 - Number Systems
parent: Assignments
nav_order: 5
---

# Assignment 4: Number Systems and Representation
**Module 4 - Number Systems**

---

## Assignment Information

- **Due Date**: End of Week 5
- **Points**: 100
- **Submission**: Canvas (PDF)
- **Type**: Individual
- **Estimated Time**: 8-10 hours

---

## Learning Objectives

- Convert between binary, decimal, octal, and hexadecimal
- Understand signed number representations
- Perform binary arithmetic operations
- Represent fixed-point and floating-point numbers
- Design BCD arithmetic circuits

---

## Problems

### Problem 1: Number System Conversions (20 points)

Perform the following conversions showing all work:

**Part A: Binary ↔ Decimal (6 points)**
1. `10110101₂` → decimal
2. `237₁₀` → binary
3. `11111111₂` → decimal

**Part B: Hexadecimal ↔ Binary (6 points)**
1. `0x3F7A` → binary
2. `101101100011₂` → hexadecimal
3. `0xDEADBEEF` → binary (show grouping)

**Part C: Octal Conversions (4 points)**
1. `753₈` → binary → decimal
2. `1023₁₀` → binary → octal

**Part D: Multi-base (4 points)**
1. `0x1A3` → octal
2. `2748₈` → hexadecimal

---

### Problem 2: Signed Number Representations (25 points)

**Part A: Two's Complement (10 points)**

For 8-bit two's complement representation:
1. Represent: +42, -42, +127, -128
2. What is the range? (minimum and maximum values)
3. Convert: `11001010₂` → decimal
4. Find: `-75₁₀` → binary (8-bit)

**Part B: Sign-Magnitude and One's Complement (8 points)**

For the value -45 in 8-bit:
1. Sign-magnitude representation
2. One's complement representation
3. Two's complement representation
4. Which is best for arithmetic? Why?

**Part C: Overflow Detection (7 points)**

For each 8-bit two's complement addition, determine if overflow occurs:
1. `01111111` + `00000001`
2. `10000000` + `11111111`
3. `01000000` + `01000000`

Explain the overflow detection rule.

---

### Problem 3: Binary Arithmetic (20 points)

**Part A: Addition (8 points)**

Perform 8-bit unsigned binary addition:
1. `10110011` + `01001101`
2. `11111111` + `00000001`

Show carries and check with decimal.

**Part B: Subtraction (12 points)**

Perform 8-bit two's complement subtraction using addition:
1. `42 - 17` (show conversion to two's complement, perform addition)
2. `25 - 67` (result should be negative)
3. Verify both results in decimal

---

### Problem 4: BCD Representation (15 points)

**Part A: BCD Encoding (7 points)**
1. Encode `3947₁₀` in BCD
2. How many bits required?
3. What is the range for 16-bit BCD?

**Part B: BCD Addition (8 points)**

Add the following BCD numbers:
1. `0011 0101` + `0010 0111` (35 + 27)
2. `0111 1000` + `0100 0101` (78 + 45)

Show correction when digit exceeds 9.

---

### Problem 5: Fixed and Floating Point (20 points)

**Part A: Fixed-Point (10 points)**

Using 8-bit fixed-point with 4 integer bits and 4 fractional bits (Q4.4):
1. Represent: 5.75, -3.25
2. What is the range?
3. What is the resolution (smallest increment)?
4. Add: `0101.1000` + `0010.0100`

**Part B: IEEE 754 Single Precision (10 points)**

For the value 12.375:
1. Convert to binary
2. Normalize to scientific notation (1.xxx × 2^exp)
3. Find: Sign bit, Exponent (biased), Mantissa
4. Show final 32-bit representation (sign, exponent, mantissa)

---

## Grading Rubric

### Problem 1 (20 points)
- Each conversion: 1-2 points
- Must show work
- Binary grouping for hex/octal

### Problem 2 (25 points)
- Correct representations: 15 points
- Understanding of ranges: 5 points
- Overflow explanation: 5 points

### Problem 3 (20 points)
- Correct arithmetic: 15 points
- Showing carries/borrows: 3 points
- Decimal verification: 2 points

### Problem 4 (15 points)
- BCD encoding: 7 points
- BCD addition with correction: 8 points

### Problem 5 (20 points)
- Fixed-point: 10 points
- Floating-point: 10 points

---

## Resources
- Number Systems Reference Sheet
- Binary Arithmetic Tutorial
- IEEE 754 Calculator
- Two's Complement Visualizer

---

**Show all your work! Partial credit available.** 🔢
