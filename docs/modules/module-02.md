---
layout: default
title: Module 2 - Combinational Logic
parent: Course Modules
nav_order: 3
permalink: /docs/modules/module-02/
---

# Module 2: Combinational Logic Design
**Weeks 2-3**

---

## Overview

Explore standard combinational logic building blocks including multiplexers, decoders, encoders, and Karnaugh map optimization.

**Duration**: 2 weeks  
**Prerequisites**: Module 1 completed

---

## Learning Objectives

By the end of this module, you will be able to:
1. Design and implement multiplexers and demultiplexers
2. Create decoder and encoder circuits
3. Use Karnaugh maps for logic minimization
4. Design half-adders and full-adders
5. Implement combinational circuits in Verilog
6. Optimize digital circuits for size and speed

---

## Topics

### 1. Karnaugh Maps (K-Maps)
- 2-variable, 3-variable, 4-variable K-maps
- Grouping rules and strategies
- Handling don't care conditions
- Sum of Products (SOP) minimization
- Product of Sums (POS) minimization

### 2. Multiplexers (MUX)
- 2:1, 4:1, 8:1 multiplexers
- Cascading multiplexers
- Using MUX to implement Boolean functions
- Verilog implementation

### 3. Demultiplexers (DEMUX)
- 1:2, 1:4, 1:8 demultiplexers
- Applications in data routing
- Relationship to decoders

### 4. Decoders
- 2:4, 3:8 decoders
- BCD to 7-segment decoder
- Enable inputs
- Applications

### 5. Encoders
- Priority encoders
- 8:3 encoder
- Handling multiple active inputs

### 6. Adders
- Half-adder design
- Full-adder design
- Ripple-carry adder
- Carry propagation delay

---

## Assignment 2

**Due**: End of Week 3  
**Points**: 100

### Requirements

**Part 1**: K-Map Minimization (25 points)
Simplify Boolean functions using K-maps:
- 3-variable functions
- 4-variable functions with don't cares
- Derive minimized SOP expressions

**Part 2**: Multiplexer Design (25 points)
- Design 8:1 MUX using 2:1 MUX blocks
- Implement Boolean function using MUX
- Draw circuit diagram

**Part 3**: 7-Segment Decoder (30 points)
Design BCD to 7-segment decoder:
- Create truth table for all segments (a-g)
- Derive logic equations
- Implement in Verilog
- Test on DE10-Lite board

**Part 4**: 4-Bit Adder (20 points)
- Design using full-adders
- Calculate worst-case delay
- Implement and test in Verilog

[Download Assignment Template](../../assignments/assignment-02.md)

---

## Resources

### Lecture Materials
- [Module 2 Slides](../../resources/lectures/module02_slides.pdf)
- [K-Map Tutorial](../../resources/kmap_guide.pdf)
- [Combinational Building Blocks](../../resources/combinational_blocks.pdf)

### Interactive Tools
- [K-Map Solver](https://www.charlie-coleman.com/experiments/kmap/)
- [Logic Friday](http://www.sontrak.com/) - Logic minimization tool
- [Circuit Simulator](https://www.falstad.com/circuit/)

### Video Tutorials
- K-Map Minimization Master Class (30 min)
- Multiplexer Design Patterns (20 min)
- 7-Segment Display Decoder (25 min)

### Practice Problems
- [K-Map Practice Set](../../practice/module02/kmap_problems.pdf)
- [MUX/DEMUX Exercises](../../practice/module02/mux_demux.pdf)
- [Decoder Design Problems](../../practice/module02/decoders.pdf)

---

## Lab Exercise

### Lab 2: Multiplexers and Decoders
**Objectives**:
- Build 4:1 MUX from logic gates
- Implement 3:8 decoder
- Create 7-segment display driver

**Deliverables**:
- Verilog code for all components
- Testbench with comprehensive test vectors
- DE10-Lite demonstration
- Lab report with timing analysis

[View Full Lab Instructions](../../labs/combinational/lab02/)

---

## Key Concepts

### K-Map Grouping Rules
- Group sizes must be powers of 2 (1, 2, 4, 8)
- Make groups as large as possible
- Each group eliminates one variable
- Groups can overlap and wrap around

### Multiplexer Formula
For n select lines:
- 2^n data inputs
- 1 output
- Function: Y = D_i when S = i

### Decoder Formula
For n inputs:
- 2^n outputs
- Only one output active at a time
- Output i is active when input = i

---

## Common Mistakes

❌ **K-Map errors**
- Forgetting to group all 1s
- Making groups that aren't power-of-2 size
- Not using largest possible groups

❌ **MUX select line confusion**
- LSB vs MSB ordering
- Incorrect truth table mapping

❌ **7-segment display**
- Mixing up common-anode vs common-cathode
- Incorrect segment labeling

✅ **Good Practice**
- Always verify K-map grouping
- Draw truth tables before coding
- Test each segment individually
- Use systematic naming conventions

---

## Design Examples

### 4:1 Multiplexer Verilog
```verilog
module mux_4to1 (
    input  [3:0] d,
    input  [1:0] sel,
    output reg   y
);
    always @(*) begin
        case(sel)
            2'b00: y = d[0];
            2'b01: y = d[1];
            2'b10: y = d[2];
            2'b11: y = d[3];
        endcase
    end
endmodule
```

---

## Next Steps

After completing Module 2, proceed to:
- **[Module 3: Verilog HDL](module-03/)**
- Deep dive into Verilog syntax
- Learn testbench development

---

[← Previous Module](module-01/) | [Back to All Modules](../) | [Next Module →](module-03/)
