---
layout: default
title: Assignment 6 - Sequential Logic Basics
parent: Assignments
nav_order: 7
---

# Assignment 6: Sequential Logic and Flip-Flops
**Module 6 - Sequential Logic Fundamentals**

---

## Assignment Information

- **Due Date**: End of Week 7
- **Points**: 100
- **Submission**: Canvas (PDF + Verilog files)
- **Type**: Individual
- **Estimated Time**: 10-12 hours

---

## Learning Objectives

- Understand flip-flop behavior and timing
- Analyze setup time, hold time, and clock-to-Q delays
- Design synchronous sequential circuits
- Implement registers and shift registers
- Understand metastability and clock domain crossing

---

## Problems

### Problem 1: Flip-Flop Timing Analysis (25 points)

**Given**: D flip-flop with:
- Setup time (Tsu) = 2ns
- Hold time (Th) = 1ns  
- Clock-to-Q delay (Tcq) = 3ns
- Combinational logic delay (Tlogic) = 10ns

**Part A: Maximum Frequency (10 points)**
1. Calculate minimum clock period
2. Calculate maximum clock frequency
3. Draw timing diagram showing critical path

**Part B: Timing Violations (8 points)**

For each scenario, determine if setup/hold violation occurs:
1. Data changes 1ns before clock edge
2. Data changes 0.5ns after clock edge
3. Data stable from 5ns before to 3ns after clock

**Part C: Verilog Timing Simulation (7 points)**

Write testbench demonstrating:
1. Successful data capture
2. Setup time violation
3. Hold time violation

Use `#delays` to create timing violations.

---

### Problem 2: Register Design (20 points)

**Part A: Parallel-Load Register (10 points)**

Design 8-bit register with:
- **Inputs**: `CLK`, `RST_N`, `LOAD`, `D[7:0]`
- **Output**: `Q[7:0]`
- Synchronous load (loads when LOAD=1)
- Asynchronous active-low reset

**Part B: Register with Enable (10 points)**

Design 8-bit register with:
- Load enable
- Clear (synchronous)
- Increment (adds 1 when INC=1)

Verilog implementation + testbench.

---

### Problem 3: Shift Register (30 points)

**Objective**: Design universal shift register.

**Specification**:
- 8-bit shift register
- **Modes** (MODE[1:0]):
  - `00`: Hold (no change)
  - `01`: Shift left
  - `10`: Shift right
  - `11`: Parallel load
- **Inputs**: `CLK`, `RST_N`, `MODE[1:0]`, `SI_L` (left serial in), `SI_R` (right serial in), `D[7:0]` (parallel data)
- **Outputs**: `Q[7:0]`, `SO_L` (left serial out), `SO_R` (right serial out)

**Part A: Design (15 points)**
1. Block diagram
2. Verilog implementation
3. Explain mode selection logic

**Part B: Testing (10 points)**
1. Testbench with all modes
2. Waveform showing:
   - Parallel load
   - Shift left sequence
   - Shift right sequence

**Part C: FPGA Demo (5 points)**
- Use switches for mode and parallel data
- Use KEY for clock (manual or slow clock)
- Display on LEDs

---

### Problem 4: Metastability and Synchronizers (25 points)

**Part A: Metastability Concept (10 points)**
1. Explain what metastability is
2. When does it occur?
3. Why is it dangerous in digital systems?
4. Draw timing diagram showing metastable state

**Part B: Two-Flip-Flop Synchronizer (10 points)**
1. Draw circuit diagram
2. Explain how it reduces metastability risk
3. Calculate MTBF (Mean Time Between Failures) given:
   - Clock frequency = 50 MHz
   - Input toggle rate = 1 kHz
   - τ (metastability time constant) = 0.5ns
   - T0 (metastability window) = 0.2ns

**Part C: Verilog Implementation (5 points)**

Implement 2-FF synchronizer:
```verilog
module synchronizer_2ff (
    input  wire CLK,
    input  wire ASYNC_IN,
    output reg  SYNC_OUT
);
    reg sync_stage1;
    
    always @(posedge CLK) begin
        sync_stage1 <= ASYNC_IN;
        SYNC_OUT <= sync_stage1;
    end
endmodule
```

Create testbench showing asynchronous input being synchronized.

---

## Grading Rubric

### Problem 1 (25 points)
- Timing calculations: 15 points
- Violation analysis: 7 points
- Simulation: 3 points

### Problem 2 (20 points)
- Parallel-load register: 10 points
- Enhanced register: 10 points

### Problem 3 (30 points)
- Design and Verilog: 20 points
- Testing: 7 points
- FPGA demo: 3 points

### Problem 4 (25 points)
- Metastability explanation: 10 points
- Synchronizer analysis: 10 points
- Verilog implementation: 5 points

---

## Resources
- Timing Analysis Tutorial
- Metastability White Paper
- Shift Register Patterns
- Synchronizer Design Guide

---

**Timing is everything in sequential logic. Analyze carefully!** ⏱️
