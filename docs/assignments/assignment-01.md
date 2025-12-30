---
layout: default
title: Assignment 1 - Logic Fundamentals
parent: Assignments
nav_order: 2
---

# Assignment 1: Digital Logic Fundamentals
**Module 1 - Logic Fundamentals**

---

## Assignment Information

- **Due Date**: End of Week 2
- **Points**: 100
- **Submission**: Canvas (PDF)
- **Type**: Individual
- **Estimated Time**: 8-10 hours

---

## Learning Objectives

By completing this assignment, you will:
- Master number system conversions
- Apply Boolean algebra laws to simplify expressions
- Design combinational circuits from truth tables
- Implement logic functions on FPGA
- Create professional technical documentation

---

## Assignment Problems

### Problem 1: Number System Conversions (20 points)

**Objective**: Demonstrate proficiency in converting between number systems.

**Part A: Binary to Decimal and Hexadecimal (7 points)**

Convert the following binary numbers. Show all work.

1. $10110111_2$ → Decimal and Hexadecimal
2. $11011010_2$ → Decimal and Hexadecimal
3. $10101100_2$ → Decimal and Hexadecimal

**Part B: Decimal to Binary and Hexadecimal (7 points)**

Convert the following decimal numbers. Show division/remainder method for binary.

1. $237_{10}$ → Binary and Hexadecimal
2. $156_{10}$ → Binary and Hexadecimal
3. $89_{10}$ → Binary and Hexadecimal

**Part C: Hexadecimal to Binary and Decimal (6 points)**

Convert the following hexadecimal numbers.

1. $0xA5F$ → Binary and Decimal
2. $0x2C8$ → Binary and Decimal
3. $0xF1B$ → Binary and Decimal

**Submission Requirements**:
- Show all intermediate steps
- Box or highlight final answers
- Use proper subscript notation

---

### Problem 2: Boolean Algebra Simplification (30 points)

**Objective**: Apply Boolean algebra laws to simplify complex expressions.

**Part A: Algebraic Simplification (12 points)**

Simplify the following expressions using Boolean algebra laws. Show each step and state which law you applied.

1. $F = A \cdot B + A \cdot \overline{B} \cdot C + \overline{A} \cdot B$

2. $F = (A + B) \cdot (A + \overline{B})$

3. $F = ABC + A\overline{B}C + \overline{A}BC + \overline{A}\overline{B}C$

**Part B: De Morgan's Theorem (10 points)**

Apply De Morgan's theorem to simplify:

1. $F = \overline{A + B \cdot C} + A \cdot \overline{B}$

2. $F = \overline{(A+B) \cdot (C+D)}$

3. $F = \overline{\overline{A} \cdot B + C \cdot \overline{D}}$

**Part C: Prove Equivalence (8 points)**

Prove that the following pairs are equivalent using Boolean algebra:

1. Prove: $AB + A\overline{B} = A$

2. Prove: $A + AB = A$

**Requirements**:
- Show step-by-step work
- State which law/theorem used at each step
- Verify final answer makes sense

---

### Problem 3: Truth Table to Logic Design (25 points)

**Objective**: Design logic circuits from specifications using truth tables.

Given the following truth table for function F:

| A | B | C | F |
|---|---|---|---|
| 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 1 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 0 |

**Part A: Sum of Products (SOP) (8 points)**

1. Write the canonical SOP expression (use minterms)
2. Simplify using Boolean algebra
3. Show your simplification steps

**Part B: Logic Circuit Diagram (10 points)**

1. Draw the logic circuit for your simplified expression
2. Use standard gate symbols (AND, OR, NOT)
3. Label all inputs and outputs
4. Show gate-level implementation (no nested expressions)

**Part C: Verilog Implementation (7 points)**

Implement the function in Verilog using:
- Continuous assignment (`assign` statement)
- Boolean operators (&, |, ~)

```verilog
module truth_table_logic (
    input  wire A, B, C,
    output wire F
);
    // Your code here
    
endmodule
```

---

### Problem 4: Logic Calculator - FPGA Implementation (25 points)

**Objective**: Design a multi-function logic calculator on FPGA.

**Specification**:

Design a "Logic Calculator" that implements four different logic functions selectable by mode.

**Inputs**:
- `SW[2:0]`: Three input switches (A, B, C)
- `SW[4:3]`: Mode select (2 bits)
- `KEY[0]`: Reset (optional, not graded)

**Outputs**:
- `LEDR[0]`: Function result
- `HEX0`: Display current mode (0, 1, 2, or 3)

**Functions by Mode**:

| Mode[1:0] | Function | Description |
|-----------|----------|-------------|
| 00 | F = A & B & C | Three-input AND |
| 01 | F = A \| B \| C | Three-input OR |
| 02 | F = (A & B) \| (B & C) \| (A & C) | Majority function |
| 03 | F = A ^ B ^ C | Three-input XOR (parity) |

**Part A: Verilog Design (12 points)**

Create a complete Verilog module:

```verilog
module logic_calculator (
    input  wire [2:0] SW,      // A, B, C
    input  wire [1:0] MODE,    // Function select
    output reg        RESULT,  // Function output
    output reg  [6:0] HEX0     // 7-segment display for mode
);
    // Your code here
    
endmodule
```

Requirements:
- Use `case` statement for mode selection
- Implement 7-segment decoder for mode display
- Include module header comments

**Part B: Testing (8 points)**

Create a test plan and verify your design:

1. Create truth table for majority function (8 rows)
2. Test all 4 modes with at least 3 input combinations each
3. Document test results with:
   - Photos showing switch settings and LED output, OR
   - Simulation waveforms showing all test cases

**Part C: Pin Assignments (5 points)**

Document your pin assignments for DE10-Lite:

| Signal | Pin | Description |
|--------|-----|-------------|
| SW[0] | PIN_C10 | Input A |
| SW[1] | PIN_C11 | Input B |
| SW[2] | PIN_D12 | Input C |
| SW[3] | PIN_C12 | Mode bit 0 |
| SW[4] | PIN_A12 | Mode bit 1 |
| LEDR[0] | PIN_A8 | Result output |
| HEX0[0] | PIN_C14 | Segment A |
| ... | ... | (complete table) |

---

## Grading Rubric

### Problem 1: Number Conversions (20 points)

| Criteria | Excellent (20pts) | Good (17pts) | Satisfactory (14pts) | Needs Improvement (10pts) | Incomplete (0pts) |
|----------|-------------------|--------------|----------------------|---------------------------|------------------|
| **Accuracy** | All conversions correct | 1-2 minor errors | 3-4 errors | 5-6 errors | >6 errors or not attempted |
| **Work Shown** | All steps clearly shown | Most steps shown | Some steps missing | Minimal work shown | No work shown |
| **Format** | Perfect notation, organized | Minor formatting issues | Some notation errors | Poor organization | Unreadable |

**Partial Credit Breakdown**:
- Part A: 7 points (2.33 per conversion)
- Part B: 7 points (2.33 per conversion)
- Part C: 6 points (2 per conversion)

**Common Errors to Avoid**:
- Forgetting to show division steps for decimal→binary
- Incorrect hexadecimal digit values (A=10, F=15)
- Missing subscripts on final answers

---

### Problem 2: Boolean Algebra (30 points)

| Criteria | Excellent (30pts) | Good (25pts) | Satisfactory (21pts) | Needs Improvement (15pts) | Incomplete (0pts) |
|----------|-------------------|--------------|----------------------|---------------------------|------------------|
| **Simplification** | All expressions correctly simplified | 1-2 minor errors | Several errors but shows understanding | Many errors | Incorrect or missing |
| **Law Application** | All laws correctly identified | Most laws correct | Some laws incorrect | Many laws wrong | No laws stated |
| **Steps Shown** | All intermediate steps clear | Most steps shown | Some steps missing | Minimal steps | No steps |
| **Final Answer** | All final forms minimal | 1-2 not fully simplified | Several not minimal | Most not simplified | Incorrect |

**Point Distribution**:
- Part A (12 pts): 4 points each expression
- Part B (10 pts): 3.33 points each
- Part C (8 pts): 4 points each proof

**Must Show**:
- Initial expression
- Each transformation step
- Law/theorem applied
- Final simplified form

**Example**:
```
F = AB + AB'
  = A(B + B')      [Distributive law]
  = A(1)           [Inverse law: B + B' = 1]
  = A              [Identity law: A·1 = A]
```

---

### Problem 3: Truth Table Design (25 points)

| Criteria | Points | Excellent | Good | Needs Improvement |
|----------|--------|-----------|------|-------------------|
| **SOP Expression** | 8 | Correct canonical and simplified forms | Minor errors in simplification | Incorrect SOP |
| **Circuit Diagram** | 10 | Clear, correct, well-labeled | Minor drawing or labeling errors | Significant errors |
| **Verilog Code** | 7 | Correct, compiles, good style | Works but style issues | Syntax errors |

**Circuit Diagram Requirements**:
- ✅ Use standard IEEE gate symbols
- ✅ Draw inputs on left, outputs on right
- ✅ Label all signals
- ✅ Show proper connections
- ✅ No crossing wires (use dots for connections)

**Verilog Requirements**:
- ✅ Compiles without errors
- ✅ Uses continuous assignment (`assign`)
- ✅ Correct Boolean operators
- ✅ Module header comment
- ✅ Proper indentation

---

### Problem 4: Logic Calculator (25 points)

| Criteria | Points | Excellent | Good | Satisfactory | Poor |
|----------|--------|-----------|------|--------------|------|
| **Verilog Implementation** | 12 | All modes work, clean code, good comments | Minor bugs or style issues | Works partially | Major errors |
| **Testing & Verification** | 8 | Complete test coverage, well-documented | Minor testing gaps | Incomplete testing | Minimal testing |
| **Pin Assignments** | 5 | Complete, correct, documented | Minor errors | Incomplete | Missing |

**Verilog Grading Details (12 points)**:
- Mode selection logic: 4 points
- All 4 functions correct: 4 points
- 7-segment decoder: 2 points
- Code quality & comments: 2 points

**Testing Grading Details (8 points)**:
- Majority truth table: 2 points
- Test all 4 modes: 4 points (1 per mode)
- Documentation (photos/waveforms): 2 points

**Pin Assignment Grading (5 points)**:
- All required pins listed: 3 points
- Correct pin numbers: 1 point
- Clear formatting: 1 point

---

## Submission Requirements

### Required Contents

Your PDF must include:

1. **Cover Page**:
   - Name, Student ID
   - Course and Section
   - Assignment 1
   - Date

2. **Problem 1**: 
   - All conversions with work shown
   - Organized by part (A, B, C)
   - Final answers clearly marked

3. **Problem 2**:
   - All simplifications with steps
   - Laws/theorems identified
   - Proofs clearly formatted

4. **Problem 3**:
   - Truth table analysis
   - Circuit diagram (hand-drawn or digital)
   - Verilog code (text, not screenshot)

5. **Problem 4**:
   - Complete Verilog code
   - Test results (photos or waveforms)
   - Pin assignment table
   - Brief description of testing

6. **Optional Appendix**:
   - Compilation reports
   - Additional test cases
   - Reflection notes

### File Submission

**PDF File**:
- Name: `LastName_FirstName_Assignment1.pdf`
- Max size: 10 MB
- Include all problems

**Verilog Files**:
- `truth_table_logic.v` (Problem 3)
- `logic_calculator.v` (Problem 4)
- Optional: testbench files

### Formatting Guidelines

**Equations**: Use clear mathematical notation
- Can be handwritten (neat) or typed
- Use proper subscripts and symbols
- Box final answers

**Diagrams**: 
- Can be hand-drawn (scanned) or digital
- Must be clear and legible
- Label all components
- Use standard symbols

**Code**:
- Format as text (not screenshot)
- Use monospace font
- Include syntax highlighting if possible
- Proper indentation

---

## Common Issues & Solutions

### Problem 1 Issues

**❌ Error**: Decimal→Binary conversion wrong
**✅ Solution**: Use division-by-2 method, read remainders bottom-to-top

**❌ Error**: Binary→Hex grouping incorrect  
**✅ Solution**: Group from right to left in groups of 4 bits, pad left with zeros

### Problem 2 Issues

**❌ Error**: Can't simplify further
**✅ Solution**: Try different law combinations, look for common factors

**❌ Error**: De Morgan's application unclear
**✅ Solution**: Remember: Break the bar, change the operation (AND↔OR)

### Problem 3 Issues

**❌ Error**: Too many gates in circuit
**✅ Solution**: Simplify Boolean expression first before drawing

**❌ Error**: Verilog doesn't compile
**✅ Solution**: Check semicolons, parentheses, endmodule statement

### Problem 4 Issues

**❌ Error**: Mode selection not working
**✅ Solution**: Check case statement syntax, ensure all cases covered

**❌ Error**: 7-segment display wrong
**✅ Solution**: Verify you're using common-anode (active-low) encoding

---

## Resources

### Reference Materials

**Number Systems**:
- [Binary Tutorial](https://www.electronics-tutorials.ws/binary/bin_2.html)
- [Hexadecimal Guide](https://www.mathsisfun.com/hexadecimals.html)
- [Number Converter Tool](https://www.rapidtables.com/convert/number/)

**Boolean Algebra**:
- [Laws and Theorems](https://www.electrical4u.com/boolean-algebra/)
- [Boolean Calculator](https://www.dcode.fr/boolean-expressions-calculator)
- [De Morgan's Explained](https://www.allaboutcircuits.com/textbook/digital/chpt-7/demorgans-theorems/)

**Verilog**:
- [Verilog Operators](http://www.asic-world.com/verilog/operators1.html)
- [Continuous Assignment](http://www.asic-world.com/verilog/verilog_one_day3.html)
- [Case Statement Guide](http://www.asic-world.com/verilog/verilog_one_day4.html)

### Video Tutorials

- Boolean Algebra Fundamentals (25 min)
- Number System Conversions (18 min)  
- De Morgan's Theorem Examples (15 min)
- Verilog Basics for Combinational Logic (30 min)

### Practice Problems

- Module 1 Practice Problems (PDF on Canvas)
- Boolean Algebra Worksheet
- Truth Table Exercises

---

## Tips for Success

### Time Management
1. **Day 1-2**: Complete Problems 1 & 2 (conversions, Boolean algebra)
2. **Day 3-4**: Complete Problem 3 (truth table design)
3. **Day 5-6**: Complete Problem 4 (FPGA implementation & testing)
4. **Day 7**: Review, format PDF, final checks

### Problem-Solving Strategies

**For Boolean Algebra**:
- Write out all steps, don't skip
- Double-check each law application
- Verify with truth table if unsure

**For Circuit Design**:
- Simplify expression first
- Draw rough sketch before final diagram
- Trace through with example inputs

**For Verilog**:
- Start with simple test case
- Compile frequently
- Test one function at a time
- Add comments as you code

### Debugging Tips

1. **Syntax errors**: Read error message carefully, check line number
2. **Logic errors**: Test with truth table, trace by hand
3. **FPGA not working**: Verify pin assignments, check compilation successful
4. **Simulation issues**: Check testbench, verify timing

---

## Academic Integrity

This is an **individual assignment**. 

**Allowed**:
- Course materials and textbook
- Online references (with citation)
- Asking TA/instructor conceptual questions
- Discussing problem approach with classmates

**Not Allowed**:
- Sharing solution files
- Copying code from others
- Using previous semester solutions
- Having someone else do the work

---

## Regrade Policy

Regrade requests must be submitted within **1 week** of grade posting.

**Valid reasons**:
- Grading error (points miscalculated)
- Solution not properly reviewed
- Rubric not followed correctly

**Invalid reasons**:
- "I think I deserve more points"
- "I worked really hard"
- After 1-week deadline

**How to request**:
1. Write clear explanation of issue
2. Reference specific rubric criteria
3. Submit via Canvas message
4. Include original submission

---

**Start early and test thoroughly! This assignment builds the foundation for everything else in the course.** 🎯
