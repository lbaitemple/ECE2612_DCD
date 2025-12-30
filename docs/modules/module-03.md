---
layout: default
title: Module 3 - Verilog HDL
parent: Course Modules
nav_order: 4
permalink: /docs/modules/module-03/
---

# Module 3: Verilog HDL Basics
**Week 4**

[View Full Module Content](../../../Module_03_Verilog_HDL.md)

---

## Overview

Learn Verilog Hardware Description Language for digital design. Master both behavioral and structural modeling styles.

**Duration**: 1 week  
**Prerequisites**: Modules 0-2 completed

---

## Learning Objectives

By the end of this module, you will be able to:
1. Write synthesizable Verilog code
2. Understand module structure and hierarchy
3. Use behavioral and dataflow modeling
4. Create effective testbenches
5. Debug designs using simulation

---

## Topics

### 1. Verilog Module Structure
- Module declaration and ports
- Input/output specifications
- Wire vs reg data types
- Continuous vs procedural assignments

### 2. Data Types and Operators
- Wire (continuous assignment)
- Reg (procedural assignment)
- Integer, parameter, localparam
- Arithmetic, logical, bitwise operators
- Reduction operators
- Concatenation and replication

### 3. Modeling Styles
- **Structural**: Gate-level instantiation
- **Dataflow**: Continuous assignments (assign)
- **Behavioral**: Always blocks
- Choosing the right style

### 4. Always Blocks
- Sensitivity lists
- Blocking (=) vs non-blocking (<=) assignments
- Combinational always blocks (@*)
- Sequential always blocks (@posedge/@negedge)

### 5. Conditional Statements
- if-else statements
- case statements
- Avoiding latches
- Priority vs parallel case

### 6. Testbench Development
- Testbench structure
- Clock generation
- Stimulus application
- Result checking
- $display, $monitor commands
- Simulation control

---

## Assignment 3

**Due**: End of Week 4  
**Points**: 100

### Requirements

**Part 1**: Modeling Styles (30 points)
Implement 4:1 MUX using three styles:
- Structural (gate-level)
- Dataflow (assign statements)
- Behavioral (always block with case)
- Compare and contrast

**Part 2**: Combinational Logic (25 points)
Design 3-bit priority encoder:
- Create truth table
- Write Verilog module
- Develop comprehensive testbench
- Show simulation waveforms

**Part 3**: Testbench Development (25 points)
Write testbench for provided full-adder:
- Test all input combinations
- Verify carry and sum outputs
- Use $display to show results
- Generate VCD waveform file

**Part 4**: Debugging Exercise (20 points)
Fix provided buggy Verilog code:
- Identify synthesis issues
- Correct latch inference
- Fix blocking/non-blocking errors
- Document all changes

[Download Assignment Template](../../assignments/assignment-03.md)

---

## Resources

### Lecture Materials
- [Module 3 Slides](../../resources/lectures/module03_slides.pdf)
- [Verilog Quick Reference](../../resources/verilog_reference.pdf)
- [Common Coding Mistakes](../../resources/verilog_pitfalls.pdf)

### Interactive Learning
- [HDLBits](https://hdlbits.01xz.net/) - Verilog practice problems
- [EDA Playground](https://edaplayground.com/) - Online simulator
- [ASIC World Verilog Tutorial](http://www.asic-world.com/verilog/index.html)

### Video Tutorials
- Verilog Syntax Fundamentals (25 min)
- Always Blocks Deep Dive (30 min)
- Testbench Best Practices (20 min)

### Books
- *Verilog HDL* by Samir Palnitkar
- *Digital Design and Computer Architecture* - Ch. 4

---

## Lab Exercise

### Lab 3: Verilog Design & Simulation
**Objectives**:
- Practice different modeling styles
- Create self-checking testbenches
- Debug using ModelSim waveforms

**Tasks**:
- Implement 8-bit ALU in Verilog
- Write comprehensive testbench
- Simulate and verify all operations
- Synthesize and test on FPGA

[View Full Lab Instructions](../../labs/combinational/lab03/)

---

## Key Syntax

### Module Template
```verilog
module module_name (
    input  wire [7:0] a, b,
    input  wire       sel,
    output reg  [7:0] result
);
    // Internal signals
    wire [7:0] temp;
    
    // Dataflow
    assign temp = a + b;
    
    // Behavioral
    always @(*) begin
        if (sel)
            result = temp;
        else
            result = a - b;
    end
endmodule
```

### Testbench Template
```verilog
`timescale 1ns/1ps

module tb_module_name;
    reg  [7:0] a, b;
    reg        sel;
    wire [7:0] result;
    
    // Instantiate DUT
    module_name dut (
        .a(a), .b(b), .sel(sel), .result(result)
    );
    
    // Test stimulus
    initial begin
        a = 0; b = 0; sel = 0;
        #10 a = 8'hAA; b = 8'h55;
        #10 sel = 1;
        #10 $finish;
    end
    
    // Monitor
    initial begin
        $monitor("Time=%0t a=%h b=%h sel=%b result=%h", 
                 $time, a, b, sel, result);
    end
endmodule
```

---

## Common Mistakes

❌ **Using reg for combinational outputs**
- Reg doesn't mean register!
- Use reg with always blocks, wire with assign

❌ **Incomplete sensitivity lists**
- Use @(*) for combinational logic
- Explicitly list signals for sequential

❌ **Mixing blocking/non-blocking**
- Use = for combinational always blocks
- Use <= for sequential always blocks

❌ **Inferring latches unintentionally**
- Always assign all outputs in all branches
- Include else clause or default case

✅ **Good Practice**
- Use meaningful signal names
- Comment complex logic
- Separate combinational and sequential logic
- Test thoroughly before synthesis

---

## Coding Guidelines

### Naming Conventions
- Lowercase for signals: `data_in`, `counter`
- Uppercase for parameters: `WIDTH`, `DEPTH`
- Suffix clocks with `_clk`: `sys_clk`
- Suffix resets with `_rst`: `async_rst_n` (active low)

### File Organization
```verilog
// Header comments
// Module description
// Author, date, version

// Module declaration
module example (...);

    // Parameters
    parameter WIDTH = 8;
    
    // Port declarations (already in module header)
    
    // Internal signals
    wire [WIDTH-1:0] internal_bus;
    reg  [3:0]       state;
    
    // Continuous assignments
    assign output1 = ...;
    
    // Always blocks
    always @(posedge clk) begin
        ...
    end
    
    // Module instantiations
    submodule inst1 (...);
    
endmodule
```

---

## Debugging Tips

1. **Start with simulation before hardware**
2. **Check synthesis warnings** - many bugs show up as warnings
3. **Use $display for debugging** - print intermediate values
4. **View waveforms** - visual debugging is powerful
5. **Test corner cases** - max/min values, zero, all-ones
6. **Verify timing** - check setup/hold violations

---

## Next Steps

After completing Module 3, proceed to:
- **[Module 4: Number Systems](module-04/)**
- Signed number representations
- BCD and magnitude comparators

---

[← Previous Module](module-02/) | [Back to All Modules](../) | [Next Module →](module-04/)
