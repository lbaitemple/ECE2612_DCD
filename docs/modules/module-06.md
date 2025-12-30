---
layout: default
title: Module 6 - Latches & Flip-Flops
parent: Course Modules
nav_order: 7
permalink: /docs/modules/module-06/
---

# Module 6: Latches and Flip-Flops
**Weeks 7-8**

[View Full Module Content](../../../Module_06_Latches_Flipflops.md)

---

## Overview

Introduction to sequential logic: storage elements that form the foundation of all stateful digital systems.

**Duration**: 2 weeks  
**Prerequisites**: Modules 0-5 completed

---

## Learning Objectives

By the end of this module, you will be able to:
1. Understand the difference between latches and flip-flops
2. Design SR, D, JK, and T flip-flops
3. Analyze timing parameters (setup, hold, propagation delay)
4. Implement synchronous sequential circuits
5. Avoid common timing hazards

---

## Topics

### 1. Introduction to Sequential Logic
- Difference from combinational logic
- Concept of state and memory
- Feedback in digital circuits
- Synchronous vs asynchronous operation

### 2. SR Latch (Set-Reset)
- Basic bistable element
- Truth table and characteristic equation
- NAND and NOR implementations
- Invalid state problem

### 3. D Latch
- Eliminates SR latch invalid state
- Enable signal operation
- Transparent latch behavior
- Use cases

### 4. Edge-Triggered Flip-Flops

#### D Flip-Flop
- Positive and negative edge triggering
- Clock signal requirements
- Symbol and timing diagram

#### JK Flip-Flop
- No invalid state (toggles when J=K=1)
- Versatility for various functions
- Conversion to other flip-flop types

#### T Flip-Flop
- Toggle operation
- Use in counters and frequency dividers
- Implementation from JK or D

### 5. Timing Parameters
- **Setup Time (t_setup)**: Minimum time data must be stable before clock edge
- **Hold Time (t_hold)**: Minimum time data must be stable after clock edge
- **Propagation Delay (t_pd)**: Time from clock edge to output change
- **Clock-to-Q Delay**: Specific type of propagation delay
- Timing violations and metastability

### 6. Asynchronous Inputs
- Asynchronous reset and preset
- Synchronous vs asynchronous reset
- Reset priority and timing

---

## Assignment 6

**Due**: End of Week 8  
**Points**: 100

### Requirements

**Part 1**: Flip-Flop Conversions (25 points)
- Convert D flip-flop to JK flip-flop
- Convert JK flip-flop to T flip-flop
- Show excitation tables and logic
- Verify with truth tables

**Part 2**: Timing Analysis (25 points)
Given flip-flop datasheet:
- Calculate maximum clock frequency
- Identify timing violations
- Sketch timing diagrams
- Determine safe operation regions

**Part 3**: Register Design (30 points)
Design 8-bit register with:
- Parallel load
- Synchronous clear
- Clock enable
- Implement in Verilog
- Test with comprehensive testbench

**Part 4**: FPGA Implementation (20 points)
- Implement register on DE10-Lite
- Use switches for data input
- Use button for clock/load
- Display on LEDs
- Demo video

[Download Assignment Template](../../assignments/assignment-06.md)

---

## Resources

### Lecture Materials
- [Module 6 Slides](../../resources/lectures/module06_slides.pdf)
- [Flip-Flop Types Comparison](../../resources/flipflop_comparison.pdf)
- [Timing Parameters Guide](../../resources/timing_analysis.pdf)

### Interactive Tools
- [Flip-Flop Simulator](https://www.electronics-tutorials.ws/)
- [Timing Diagram Tool](https://wavedrom.com/)
- [Digital Circuit Simulator](https://simulator.io/board)

### Video Tutorials
- Latches vs Flip-Flops Explained (18 min)
- Timing Parameters Deep Dive (25 min)
- Metastability and Clock Domain Crossing (22 min)

### Practice Problems
- [Flip-Flop Conversion Exercises](../../practice/module06/conversions.pdf)
- [Timing Analysis Worksheets](../../practice/module06/timing.pdf)
- [Sequential Circuit Problems](../../practice/module06/sequential.pdf)

---

## Lab Exercise

### Lab 6: Flip-Flops and Registers
**Objectives**:
- Implement different flip-flop types
- Measure timing parameters
- Design parameterized register
- Test synchronous operation

**Deliverables**:
- D, JK, T flip-flop implementations
- 16-bit register with control signals
- Timing measurement report
- FPGA demonstration

[View Full Lab Instructions](../../labs/sequential/lab06/)

---

## Key Concepts

### Latch vs Flip-Flop
| Feature | Latch | Flip-Flop |
|---------|-------|-----------|
| Triggering | Level-sensitive | Edge-sensitive |
| Timing | Transparent when enabled | Changes only on clock edge |
| Behavior | Can cause timing issues | Synchronous, predictable |
| Usage | Rare in modern design | Standard building block |

### Flip-Flop Comparison
| Type | Inputs | Behavior | Applications |
|------|--------|----------|--------------|
| D | D | Q = D on clock edge | Registers, shift registers |
| JK | J, K | Set/Reset/Toggle/Hold | General purpose |
| T | T | Toggle if T=1 | Counters, frequency dividers |

---

## Design Examples

### D Flip-Flop with Async Reset
```verilog
module d_ff_async_reset (
    input  wire d, clk, reset_n,
    output reg  q
);
    always @(posedge clk or negedge reset_n) begin
        if (!reset_n)
            q <= 1'b0;
        else
            q <= d;
    end
endmodule
```

### 8-Bit Register with Enable
```verilog
module register_8bit (
    input  wire       clk, reset, enable,
    input  wire [7:0] d,
    output reg  [7:0] q
);
    always @(posedge clk or posedge reset) begin
        if (reset)
            q <= 8'b0;
        else if (enable)
            q <= d;
    end
endmodule
```

### JK Flip-Flop
```verilog
module jk_ff (
    input  wire j, k, clk, reset,
    output reg  q
);
    always @(posedge clk or posedge reset) begin
        if (reset)
            q <= 1'b0;
        else
            case ({j, k})
                2'b00: q <= q;      // Hold
                2'b01: q <= 1'b0;   // Reset
                2'b10: q <= 1'b1;   // Set
                2'b11: q <= ~q;     // Toggle
            endcase
    end
endmodule
```

---

## Common Mistakes

❌ **Using latches unintentionally**
- Incomplete if/case statements infer latches
- Always assign all outputs in combinational logic

❌ **Mixing blocking/non-blocking in sequential**
- Always use <= in clocked always blocks
- Use = only in combinational blocks

❌ **Timing violations**
- Violating setup/hold times causes metastability
- Ensure adequate timing margins

❌ **Asynchronous reset issues**
- Reset assertion is async, deassertion should be synchronous
- Consider reset synchronizers

✅ **Good Practice**
- Use D flip-flops for most designs
- Synchronize all asynchronous inputs
- Always specify reset behavior
- Use non-blocking assignments for sequential logic

---

## Timing Analysis

### Setup Time Constraint
```
T_clk ≥ t_pd(logic) + t_setup(FF)
```
Where:
- T_clk = clock period
- t_pd(logic) = combinational logic delay
- t_setup = flip-flop setup time

### Hold Time Constraint
```
t_pd(logic) ≥ t_hold(FF)
```

### Maximum Frequency
```
f_max = 1 / (t_pd(logic) + t_setup + t_clk-to-q)
```

---

## Real-World Applications

- **Registers**: CPUs, data storage
- **Counters**: Timers, frequency dividers
- **State Machines**: Controllers, protocols
- **Pipeline Stages**: High-performance processors
- **Synchronization**: Clock domain crossing

---

## Next Steps

After completing Module 6, proceed to:
- **[Module 7: Sequential Design](module-07/)**
- State machines
- Synchronous circuit design methodology

---

[← Previous Module](module-05/) | [Back to All Modules](../) | [Next Module →](module-07/)
