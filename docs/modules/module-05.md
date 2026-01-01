---
layout: default
title: Module 5 - Binary Arithmetic
parent: Course Modules
nav_order: 6
permalink: /docs/modules/module-05/
---

# Module 5: Binary Arithmetic & ALU Design
**Week 6**

---

## Overview

Design arithmetic circuits including adders, subtractors, multipliers, and complete ALUs.

**Duration**: 1 week  
**Prerequisites**: Modules 0-4 completed

---

## Learning Objectives

By the end of this module, you will be able to:
1. Design binary adders and subtractors
2. Implement multiplication and division circuits
3. Handle overflow and carry flags
4. Create a complete ALU
5. Analyze and optimize arithmetic circuit performance

---

## Topics

### 1. Adders

#### Half-Adder
- Adds two 1-bit inputs
- Outputs: Sum, Carry
- Logic: Sum = A ⊕ B, Carry = A · B

#### Full-Adder
- Adds three 1-bit inputs (A, B, Cin)
- Outputs: Sum, Cout
- Can be cascaded for multi-bit addition

#### Ripple-Carry Adder
- Chain of full-adders
- Simple but slow
- Delay = n × t_FA (n = number of bits)

#### Carry-Lookahead Adder (CLA)
- Faster than ripple-carry
- Computes carries in parallel
- Generate (G) and Propagate (P) signals
- More complex hardware

### 2. Subtraction
- Using 2's complement: A - B = A + (~B) + 1
- Borrow vs carry
- Overflow detection

### 3. Multiplication

#### Shift-and-Add Algorithm
- Similar to long multiplication
- n iterations for n-bit multiplier
- Accumulator and partial products

#### Array Multiplier
- Parallel implementation
- Faster but more hardware
- Grid of AND gates and adders

#### Booth's Algorithm
- Handles signed multiplication
- Reduces number of additions
- More complex control logic

### 4. Division
- Restoring division algorithm
- Non-restoring division (faster)
- Quotient and remainder
- More complex than multiplication

### 5. ALU Design
Complete Arithmetic Logic Unit with:
- Arithmetic: ADD, SUB, INC, DEC
- Logic: AND, OR, XOR, NOT
- Shift: SHL, SHR, ROL, ROR
- Status flags: Zero, Carry, Overflow, Negative

---

## Assignment 5

**Due**: End of Week 6  
**Points**: 100

### Requirements

**Part 1**: Adder Analysis (25 points)
- Analyze 4-bit ripple-carry adder timing
- Design 4-bit carry-lookahead adder
- Compare delays and gate counts
- Explain speed vs complexity tradeoff

**Part 2**: 8-Bit ALU Design (40 points)
Design complete 8-bit ALU:
- Operations: ADD, SUB, AND, OR, XOR, NOT, SHL, SHR
- 3-bit operation select
- Status outputs: Z (zero), C (carry), V (overflow), N (negative)
- Implement in Verilog
- Comprehensive testbench

**Part 3**: Multiplier Implementation (20 points)
- Design 4×4 unsigned multiplier
- Use shift-and-add algorithm
- State machine or iterative approach
- Test all combinations

**Part 4**: FPGA Demo (15 points)
- Implement ALU on DE10-Lite
- Use switches for inputs and operation select
- Display results on 7-segment displays
- Demo video showing all operations

[Download Assignment Template](../assignments/assignment-05/)

---

## Resources

### Lecture Materials
- [Module 5 Slides](../../resources/lectures/module05_slides.pdf)

### Interactive Tools
- [Logic Circuit Simulator](https://www.falstad.com/circuit/)
- [Digital Works](https://www.mechatronic.com/digital-works/) - Circuit design
- [Logisim Evolution](https://github.com/logisim-evolution/logisim-evolution)

### Video Tutorials
- Ripple-Carry vs Carry-Lookahead (22 min)
- Binary Multiplication Algorithms (28 min)
- Complete ALU Design Walkthrough (35 min)

---

## Lab Exercise

### Lab 5: ALU Implementation
**Objectives**:
- Design multi-function ALU
- Optimize critical paths
- Test arithmetic operations thoroughly

**Deliverables**:
- Verilog ALU module
- Self-checking testbench
- Timing analysis report
- FPGA demonstration

[View Full Lab Instructions](../../labs/combinational/lab05/)

---

## Key Formulas

### Ripple-Carry Adder Delay
$$t_{total} = n \times t_{FA}$$
where n = number of bits, t_FA = full-adder delay

### Carry-Lookahead
**Generate**: $G_i = A_i \cdot B_i$  
**Propagate**: $P_i = A_i \oplus B_i$  
**Carry**: $C_{i+1} = G_i + P_i \cdot C_i$

### Overflow Detection (Addition)
For signed numbers:
$$V = C_n \oplus C_{n-1}$$
where C_n = carry out, C_{n-1} = carry into MSB

---

## Design Examples

### Full-Adder
```verilog
module full_adder (
    input  a, b, cin,
    output sum, cout
);
    assign sum  = a ^ b ^ cin;
    assign cout = (a & b) | (b & cin) | (a & cin);
endmodule
```

### 8-Bit Ripple-Carry Adder
```verilog
module adder_8bit (
    input  [7:0] a, b,
    input        cin,
    output [7:0] sum,
    output       cout
);
    wire [7:0] carry;
    
    full_adder fa0 (.a(a[0]), .b(b[0]), .cin(cin), 
                    .sum(sum[0]), .cout(carry[0]));
    full_adder fa1 (.a(a[1]), .b(b[1]), .cin(carry[0]), 
                    .sum(sum[1]), .cout(carry[1]));
    // ... continue for all 8 bits
    assign cout = carry[7];
endmodule
```

### Simple ALU
```verilog
module alu_8bit (
    input  [7:0] a, b,
    input  [2:0] op,
    output reg [7:0] result,
    output reg zero, carry, overflow, negative
);
    reg [8:0] temp;  // 9-bit for carry
    
    always @(*) begin
        case (op)
            3'b000: temp = {1'b0, a & b};       // AND
            3'b001: temp = {1'b0, a | b};       // OR
            3'b010: temp = a + b;               // ADD
            3'b110: temp = a - b;               // SUB
            3'b111: temp = {1'b0, (a < b)};     // SLT
            default: temp = 9'b0;
        endcase
        
        result = temp[7:0];
        carry = temp[8];
        zero = (result == 8'b0);
        negative = result[7];
        overflow = (a[7] == b[7]) && (result[7] != a[7]);
    end
endmodule
```

---

## Common Mistakes

❌ **Confusing carry and overflow**
- Carry: unsigned arithmetic result > max value
- Overflow: signed arithmetic result out of range
- Both can occur independently

❌ **Incorrect status flag logic**
- Zero flag: check if result is all zeros
- Negative flag: check MSB for signed numbers
- Overflow: requires careful logic based on operation

❌ **Timing violations in ripple-carry**
- Ensure adequate propagation time
- Use carry-lookahead for faster operation

✅ **Good Practice**
- Test edge cases: 0, max, min values
- Verify all status flags
- Check both signed and unsigned operations
- Document timing assumptions

---

## Performance Optimization

### Speed Optimization
- Use carry-lookahead instead of ripple-carry
- Pipeline long arithmetic operations
- Consider carry-save adders for multiplication

### Area Optimization
- Reuse adder hardware for multiple operations
- Serial implementations for low-speed applications
- Share resources between functions

### Power Optimization
- Clock gating for unused operations
- Reduce switching activity
- Choose appropriate bit width

---

## Next Steps

After completing Module 5, proceed to:
- **[Module 6: Latches & Flip-Flops](module-06/)**
- Introduction to sequential logic
- Storage elements and timing

---

[← Previous Module](module-04/) | [Back to All Modules](../) | [Next Module →](module-06/)
