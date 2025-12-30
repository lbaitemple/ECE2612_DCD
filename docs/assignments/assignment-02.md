---
layout: default
title: Assignment 2 - Combinational Logic
parent: Assignments
nav_order: 3
---

# Assignment 2: Combinational Logic Design
**Module 2 - Combinational Logic**

---

## Assignment Information

- **Due Date**: End of Week 3
- **Points**: 100
- **Submission**: Canvas (PDF + Verilog files)
- **Type**: Individual
- **Estimated Time**: 10-12 hours

---

## Learning Objectives

By completing this assignment, you will:
- Master Karnaugh map minimization techniques
- Design and implement multiplexers and decoders
- Create complex combinational circuits
- Build a 4-bit ALU with status flags
- Implement 7-segment display drivers

---

## Assignment Problems

### Problem 1: Karnaugh Map Minimization (25 points)

**Objective**: Use K-maps to minimize Boolean functions efficiently.

**Part A: 3-Variable K-Map (8 points)**

Simplify the following function using a K-map:

$$F(A,B,C) = \Sigma m(0,1,2,5,6,7)$$

Requirements:
1. Draw the 3-variable K-map
2. Fill in 1s for given minterms
3. Show all possible groupings
4. Circle your chosen groups
5. Write the minimized SOP expression
6. Verify your answer covers all minterms

**Part B: 4-Variable K-Map (10 points)**

Simplify using a K-map:

$$F(W,X,Y,Z) = \Sigma m(0,2,5,7,8,10,13,15)$$

Requirements:
1. Draw the 4-variable K-map (use standard labeling)
2. Fill in 1s and 0s
3. Identify and circle all prime implicants
4. Show essential prime implicants
5. Write minimized SOP expression
6. Count total gates and gate inputs needed

**Part C: Don't Care Conditions (7 points)**

Simplify with don't cares:

$$F(A,B,C) = \Sigma m(1,3,7) + d(2,5)$$

where $d$ represents don't care conditions.

Requirements:
1. Draw K-map with 1s, 0s, and Xs
2. Show how don't cares help create larger groups
3. Write two possible simplified expressions
4. Choose the simpler one and justify

---

### Problem 2: Multiplexer and Decoder Design (30 points)

**Objective**: Design essential combinational building blocks.

**Part A: 8:1 Multiplexer from 2:1 MUX (12 points)**

Design an 8:1 multiplexer using only 2:1 multiplexers.

Requirements:
1. Draw block diagram showing how to connect seven 2:1 MUX to make 8:1 MUX
2. Label all inputs (D0-D7), select lines (S2,S1,S0), and output (Y)
3. Show the tree structure clearly
4. Explain how select lines control which input appears at output

**Part B: 3:8 Decoder with Enable (10 points)**

Design a 3:8 decoder with active-low enable in Verilog.

Specification:
- **Inputs**: A[2:0] (3-bit address), EN_N (active-low enable)
- **Outputs**: Y[7:0] (one-hot encoded, active-high)
- When EN_N=0: Exactly one output is 1 (based on address)
- When EN_N=1: All outputs are 0

```verilog
module decoder_3to8 (
    input  wire [2:0] A,
    input  wire       EN_N,
    output reg  [7:0] Y
);
    // Your code here
    
endmodule
```

Requirements:
- Truth table (8 rows with EN_N=0, 1 row with EN_N=1)
- Verilog implementation
- Brief explanation of decoder operation

**Part C: 8:3 Priority Encoder (8 points)**

Design an 8:3 priority encoder in Verilog.

Specification:
- **Inputs**: D[7:0] (request signals)
- **Outputs**: Y[2:0] (binary code), VALID (indicates any input active)
- Priority: D[7] has highest priority, D[0] has lowest
- Output encodes position of highest-priority active input

```verilog
module priority_encoder_8to3 (
    input  wire [7:0] D,
    output reg  [2:0] Y,
    output reg        VALID
);
    // Your code here
    
endmodule
```

Requirements:
- Truth table showing priority behavior
- Verilog using if-else or case statement
- Test with example: D=8'b00101100

---

### Problem 3: 7-Segment Display Decoder (20 points)

**Objective**: Create a BCD to 7-segment decoder for displaying digits.

**Specification**:

Design a decoder that converts 4-bit BCD (0-9) to 7-segment display control signals.

**Inputs**: BCD[3:0] (binary-coded decimal, 0000 to 1001)
**Outputs**: SEG[6:0] (segments a-g, active-low for common-anode display)

**7-Segment Layout**:
```
     a
    ___
 f |   | b
   |_g_|
 e |   | c
   |___|
     d
```

**Segment Encoding** (active-low):
- Display '0': SEG = 7'b1000000 (segments a,b,c,d,e,f on; g off)
- Display '1': SEG = 7'b1111001 (segments b,c on)
- ... (complete for 0-9)

**Part A: Truth Table (8 points)**

Create complete truth table:

| BCD[3:0] | Digit | a | b | c | d | e | f | g | SEG[6:0] |
|----------|-------|---|---|---|---|---|---|---|----------|
| 0000 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 1000000 |
| 0001 | 1 | 1 | 0 | 0 | 1 | 1 | 1 | 1 | 1111001 |
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |
| 1001 | 9 | ? | ? | ? | ? | ? | ? | ? | ??????? |
| 1010-1111 | Invalid | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1111111 |

**Part B: Verilog Implementation (12 points)**

```verilog
module bcd_to_7seg (
    input  wire [3:0] BCD,
    output reg  [6:0] SEG
);
    // Your code here
    
endmodule
```

Requirements:
- Use case statement
- Handle all 10 valid digits (0-9)
- Display blank (all segments off) for invalid inputs (10-15)
- Include module header comment
- Well-formatted, readable code

---

### Problem 4: 4-Bit ALU Design (25 points)

**Objective**: Design a complete 4-bit Arithmetic Logic Unit.

**Specification**:

Design an ALU that performs four operations on 4-bit inputs.

**Inputs**:
- A[3:0]: First operand
- B[3:0]: Second operand
- OP[1:0]: Operation select

**Outputs**:
- RESULT[3:0]: Operation result
- CARRY: Carry out (for addition)
- ZERO: Result is zero
- SIGN: MSB of result (for signed operations)

**Operations**:

| OP[1:0] | Operation | Description |
|---------|-----------|-------------|
| 00 | AND | RESULT = A & B |
| 01 | OR | RESULT = A \| B |
| 10 | ADD | RESULT = A + B |
| 11 | XOR | RESULT = A ^ B |

**Part A: Verilog Implementation (15 points)**

```verilog
module alu_4bit (
    input  wire [3:0] A, B,
    input  wire [1:0] OP,
    output reg  [3:0] RESULT,
    output reg        CARRY, ZERO, SIGN
);
    // Your code here
    
endmodule
```

Requirements:
- Implement all 4 operations using case statement
- Compute CARRY only for ADD operation (0 for others)
- ZERO flag: RESULT == 0
- SIGN flag: RESULT[3] (MSB)
- Use intermediate 5-bit variable for addition to capture carry

**Part B: Test Plan (5 points)**

Create test cases covering:
1. Each operation (AND, OR, ADD, XOR)
2. Edge cases:
   - Addition with carry (e.g., 15 + 1)
   - Result equals zero
   - Signed result (MSB = 1)

Format as table:

| Test# | OP | A | B | Expected RESULT | Expected FLAGS (C,Z,S) |
|-------|----|----|---|-----------------|------------------------|
| 1 | 00 | 1010 | 1100 | ? | ?,?,? |
| 2 | 10 | 1111 | 0001 | ? | ?,?,? |
| ... | ... | ... | ... | ... | ... |

Minimum 8 test cases.

**Part C: FPGA Implementation (5 points)**

Implement on DE10-Lite:
- Use SW[3:0] for input A
- Use SW[7:4] for input B
- Use SW[9:8] for operation select
- Display RESULT on HEX0 (hex digits 0-F)
- Display FLAGS on LEDR[2:0] (Carry, Zero, Sign)

Provide:
- Pin assignment table
- Photos or simulation showing at least 3 different operations

---

## Grading Rubric

### Problem 1: K-Map Minimization (25 points)

| Criteria | Excellent (25pts) | Good (21pts) | Satisfactory (18pts) | Needs Improvement (13pts) | Incomplete (0pts) |
|----------|-------------------|--------------|----------------------|---------------------------|------------------|
| **K-Map Construction** | All K-maps perfect | Minor labeling errors | Some cell errors | Multiple errors | Missing or wrong |
| **Grouping** | Optimal groups, clearly marked | Good groups, minor issues | Sub-optimal groups | Poor grouping | No grouping |
| **Minimized Expression** | All expressions minimal | 1 expression not minimal | 2 expressions not minimal | Most not minimal | Incorrect |
| **Verification** | All work verified | Most verified | Some verification | Minimal verification | No verification |

**Point Distribution**:
- Part A (8 pts): K-map (3), Groups (2), Expression (2), Verification (1)
- Part B (10 pts): K-map (3), Groups (3), Expression (2), Gate count (2)
- Part C (7 pts): K-map with don't cares (3), Expressions (2), Justification (2)

**K-Map Drawing Standards**:
- Proper Gray code labeling
- Clear cell boundaries
- 1s, 0s (and Xs for don't cares) clearly marked
- Groups circled with different colors or line styles
- Adjacent cells follow K-map rules (wrap-around)

---

### Problem 2: MUX and Decoder (30 points)

| Criteria | Part A (12pts) | Part B (10pts) | Part C (8pts) |
|----------|----------------|----------------|---------------|
| **Excellent** | Perfect 8:1 MUX design, clear diagram, correct connections | Working decoder with truth table, good code | Working priority encoder, correct priority |
| **Good** | Minor diagram errors | Code works, minor truth table issues | Works but minor priority issues |
| **Satisfactory** | Design correct but unclear | Missing truth table or code has bugs | Partial priority implementation |
| **Needs Improvement** | Significant design errors | Major code errors | Priority not working |
| **Incomplete** | Missing or wrong | Not attempted | Not attempted |

**Part A Grading Details**:
- Block diagram: 6 points
- Correct 2:1 MUX connections: 4 points
- Explanation: 2 points

**Part B Grading Details**:
- Truth table: 3 points
- Verilog correctness: 5 points
- Explanation: 2 points

**Part C Grading Details**:
- Truth table: 2 points
- Verilog implementation: 5 points
- Test example: 1 point

---

### Problem 3: 7-Segment Decoder (20 points)

| Criteria | Points | Excellent | Good | Satisfactory | Poor |
|----------|--------|-----------|------|--------------|------|
| **Truth Table** | 8 | Complete, all digits correct | 1-2 digits wrong | 3-4 digits wrong | Many errors |
| **Verilog Code** | 10 | Perfect, compiles, all digits | Minor errors, mostly works | Several bugs | Doesn't work |
| **Code Quality** | 2 | Excellent style, comments | Good style | Poor style | Unreadable |

**Truth Table Requirements**:
- All 10 digits (0-9) with correct segment patterns
- Invalid inputs (10-15) handled
- Clear formatting
- Segment mapping documented

**Verilog Requirements**:
- ✅ Uses case statement
- ✅ All 10 digits implemented correctly
- ✅ Invalid inputs produce blank display
- ✅ Active-low outputs (for common-anode)
- ✅ Compiles without errors
- ✅ Well-commented

**Common 7-Segment Patterns** (active-low):
```
0: 1000000  5: 0100100
1: 1111001  6: 0100000
2: 0100100  7: 1111000
3: 0110000  8: 0000000
4: 0011001  9: 0010000
```

---

### Problem 4: 4-Bit ALU (25 points)

| Criteria | Points | Excellent | Good | Satisfactory | Needs Improvement |
|----------|--------|-----------|------|--------------|-------------------|
| **ALU Logic** | 15 | All ops correct, flags perfect | Minor flag errors | Some ops wrong | Major errors |
| **Test Plan** | 5 | Comprehensive, edge cases | Good coverage | Basic tests | Minimal |
| **FPGA Demo** | 5 | Works perfectly, well-documented | Works, minor doc issues | Partially works | Doesn't work |

**ALU Grading Details (15 points)**:
- AND operation: 2 points
- OR operation: 2 points
- ADD operation: 4 points (including carry)
- XOR operation: 2 points
- ZERO flag logic: 2 points
- CARRY flag logic: 2 points
- SIGN flag logic: 1 point

**Test Plan Grading (5 points)**:
- Minimum 8 test cases: 2 points
- Coverage of all operations: 2 points
- Edge case testing: 1 point

**FPGA Demo Grading (5 points)**:
- Pin assignments documented: 2 points
- Demonstration evidence: 3 points

---

## Submission Requirements

### Required Files

**PDF Document** (`LastName_FirstName_Assignment2.pdf`):
1. Cover page with your information
2. Problem 1: All K-maps, work, and expressions
3. Problem 2: Block diagrams, truth tables, Verilog code
4. Problem 3: Truth table and Verilog code
5. Problem 4: Verilog code, test plan, FPGA documentation

**Verilog Source Files**:
- `decoder_3to8.v`
- `priority_encoder_8to3.v`
- `bcd_to_7seg.v`
- `alu_4bit.v`
- Optional: testbench files

### Formatting Requirements

**K-Maps**: 
- Can be hand-drawn (scanned clearly) or digital
- Use proper Gray code ordering
- Circle groups with different colors/styles
- Label all variables

**Block Diagrams**:
- Use standard symbols or clear boxes
- Label all signals
- Show data flow direction
- Neat and professional

**Verilog Code in PDF**:
- Format as text (use monospace font)
- Include syntax highlighting if possible
- Proper indentation (2-4 spaces)
- Include all required modules

**Truth Tables**:
- Aligned columns
- Binary values clearly marked
- Headers for all columns
- Complete (no missing rows)

---

## Common Issues & Solutions

### K-Map Problems

**❌ Issue**: Groups overlap incorrectly
**✅ Solution**: Remember groups can overlap, but each must be power of 2 size

**❌ Issue**: Missed wrap-around groups
**✅ Solution**: Top/bottom and left/right edges are adjacent in K-maps

**❌ Issue**: Expression not minimal
**✅ Solution**: Make groups as large as possible, minimize number of groups

### Verilog Problems

**❌ Issue**: "Inferred latch" warning in decoder
**✅ Solution**: Ensure all outputs assigned in all cases, use default case

**❌ Issue**: Priority encoder gives wrong priority
**✅ Solution**: Use if-else with highest priority first, not case statement

**❌ Issue**: ALU carry flag always wrong
**✅ Solution**: Use {CARRY, RESULT} = A + B to capture carry

**❌ Issue**: 7-segment display shows wrong digits
**✅ Solution**: Verify common-anode (active-low) vs common-cathode (active-high)

### Testing Problems

**❌ Issue**: Don't know how to test on FPGA without 7-segment
**✅ Solution**: Use LEDs to display binary result, verify with calculator

**❌ Issue**: Simulation doesn't match expected results
**✅ Solution**: Hand-trace your logic, verify truth table, check for off-by-one errors

---

## Resources

### K-Map Tools
- [K-Map Solver](https://www.charlie-coleman.com/experiments/kmap/)
- [Interactive K-Map](https://www.32x8.com/var_3.html)
- [K-Map Tutorial](https://www.electronics-tutorials.ws/boolean/karnaugh-maps.html)

### Verilog References
- [Verilog Case Statement](http://www.asic-world.com/verilog/verilog_one_day4.html)
- [Priority Encoder Example](https://www.nandland.com/verilog/examples/example-priority-encoder.html)
- [7-Segment Tutorial](https://www.fpga4student.com/2017/09/seven-segment-led-display-controller-basys3-fpga.html)

### Video Tutorials
- K-Map Minimization Master Class (30 min)
- Multiplexer Design Patterns (20 min)
- Building an ALU from Scratch (35 min)
- 7-Segment Display Interfacing (15 min)

### Practice
- Module 2 Practice Problems (Canvas)
- K-Map Worksheets
- Combinational Logic Exercises

---

## Tips for Success

### K-Map Strategy
1. Fill in K-map carefully (double-check minterm positions)
2. Look for largest possible groups first (8, then 4, then 2, then 1)
3. Remember wrap-around is allowed
4. Verify expression includes all 1s and excludes all 0s
5. Count gates to verify you're truly minimized

### Verilog Debugging
1. **Compile often**: Don't write all code then compile
2. **Test incrementally**: Test one module before moving to next
3. **Use testbenches**: Create simple testbench to verify logic
4. **Check synthesis**: Look at RTL viewer to see what hardware was generated
5. **Read warnings**: Latches and multiple drivers usually indicate bugs

### Time Management
- **Days 1-2**: Complete Problem 1 (K-maps)
- **Days 3-4**: Complete Problem 2 (MUX/Decoder)
- **Day 5**: Complete Problem 3 (7-segment)
- **Days 6-7**: Complete Problem 4 (ALU)
- **Day 8**: Test on FPGA, finalize PDF

### Testing Approach
1. **Desk check**: Verify logic by hand first
2. **Simulation**: Use ModelSim for functional verification
3. **Synthesis check**: Compile in Quartus, check for warnings
4. **Hardware test**: Program FPGA and verify with switches/LEDs
5. **Edge cases**: Test boundary conditions (all 0s, all 1s, etc.)

---

## Academic Integrity

This is an **individual assignment**.

**Collaboration Policy**:
- ✅ Discuss K-map techniques
- ✅ Explain Verilog syntax
- ✅ Help debug general errors
- ❌ Share K-map solutions
- ❌ Share Verilog code
- ❌ Copy from online sources without understanding

**Citing Sources**:
If you reference online tutorials or examples, cite them:
```
// Reference: www.example.com/mux-design
// Modified for 4-bit inputs
```

---

**This assignment builds critical combinational design skills. Start early and test thoroughly!** ⚡
