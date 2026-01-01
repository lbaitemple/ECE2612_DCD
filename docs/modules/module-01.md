---
layout: default
title: Module 1 - Digital Logic Fundamentals
parent: Course Modules
nav_order: 2
permalink: /docs/modules/module-01/
---

# Module 1: Digital Logic Fundamentals
**Weeks 1-2**

---

## Overview

Master the foundational concepts of digital logic including Boolean algebra, number systems, and basic logic gates.

**Duration**: 2 weeks  
**Prerequisites**: Module 0 completed

---

## Learning Objectives

By the end of this module, you will be able to:
1. Convert between decimal, binary, hexadecimal number systems
2. Apply Boolean algebra laws to simplify logic expressions
3. Design combinational circuits using basic logic gates
4. Create and interpret truth tables
5. Implement digital logic circuits on an FPGA

---

## Topics

### 1. Number Systems
- Binary (Base-2)
- Hexadecimal (Base-16)
- Conversion methods between bases
- Positional notation

### 2. Boolean Algebra
- Variables and constants (0, 1)
- Basic operations: AND, OR, NOT
- Boolean laws and theorems
- De Morgan's theorems

### 3. Logic Gates
- AND, OR, NOT gates
- NAND, NOR, XOR, XNOR gates
- Gate symbols and truth tables
- Multi-input gates

### 4. Boolean Simplification
- Algebraic manipulation
- Consensus theorem
- Absorption law
- Practical examples

### 5. Combinational Circuit Design
- From problem to truth table
- Truth table to Boolean expression
- Boolean expression to circuit
- Implementation on FPGA

---

## Assignment 1

**Due**: End of Week 2  
**Points**: 100

### Requirements

**Part 1**: Number System Conversions (20 points)
- Binary ↔ Decimal conversions
- Hexadecimal ↔ Binary conversions
- Show all work

**Part 2**: Boolean Algebra (25 points)
- Simplify expressions using laws
- Prove equivalence
- Apply De Morgan's theorems

**Part 3**: Truth Tables & Circuits (30 points)
Design circuits for given specifications:
- Create truth table
- Derive Boolean expression
- Draw logic circuit
- Simplify where possible

**Part 4**: FPGA Implementation (25 points)
Implement 3-input majority function:
- Write Verilog code
- Create testbench
- Test on DE10-Lite board
- Submit code, pin assignments, demo video

[Download Assignment Template](../../assignments/assignment-01.md)

---

## Resources

### Lecture Materials
- [Module 1 Slides](../../resources/lectures/module01_slides.pdf)
- [Boolean Algebra Reference](../../resources/boolean_algebra_ref.pdf)

### Video Tutorials
- Boolean Algebra Basics (15 min)
- De Morgan's Theorems Explained (12 min)
- Circuit Design Walkthrough (25 min)

### Helpful Links
- [Interactive Logic Gate Simulator](https://logic.ly/)
- [Boolean Algebra Calculator](https://www.boolean-algebra.com/)
- [Digital](https://github.com/hneemann/Digital) - Circuit simulator

---

## Key Formulas

### Boolean Laws
- **Identity**: A + 0 = A, A · 1 = A
- **Null**: A + 1 = 1, A · 0 = 0
- **Idempotent**: A + A = A, A · A = A
- **Inverse**: A + A' = 1, A · A' = 0
- **Commutative**: A + B = B + A, A · B = B · A
- **Associative**: (A + B) + C = A + (B + C)
- **Distributive**: A · (B + C) = A·B + A·C

### De Morgan's Theorems
- (A + B)' = A' · B'
- (A · B)' = A' + B'

---

## Common Mistakes

❌ **Confusing AND/OR operations**
- AND (·) requires ALL inputs true
- OR (+) requires ANY input true

❌ **Incorrect number conversions**
- Watch for off-by-one errors
- Remember positional values (powers of 2)

❌ **Not simplifying fully**
- Apply laws multiple times
- Check for further simplification

✅ **Good Practice**
- Show all conversion steps
- Verify truth tables have 2^n rows
- Test circuits before submission

---

## Next Steps

After completing Module 1, proceed to:
- **[Module 2: Combinational Logic](module-02/)**
- Learn K-maps for minimization
- Design multiplexers and decoders

---

[← Previous Module](module-00/) | [Back to All Modules](../) | [Next Module →](module-02/)
