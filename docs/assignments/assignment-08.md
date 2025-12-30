---
layout: default
title: Assignment 8 - Counters and Registers
parent: Assignments
nav_order: 9
---

# Assignment 8: Advanced Counters and Registers
**Module 8 - Counters and Registers**

---

## Assignment Information

- **Due Date**: End of Week 9
- **Points**: 100
- **Submission**: Canvas (PDF + Verilog files)
- **Type**: Group (2-3 students)
- **Check-off Required**: Yes (30% penalty if not completed)
- **Estimated Time**: 12-15 hours

---

## Learning Objectives

- Design complex counter circuits
- Implement shift register applications
- Build digital clock systems
- Create frequency dividers
- Understand cascaded counter architectures

---

## Problems

### Problem 1: Johnson Counter and Ring Counter (20 points)

**Part A: Ring Counter (10 points)**

Design 4-bit ring counter:
- **Outputs**: `Q[3:0]` (only one bit high at a time)
- **Pattern**: 0001 → 0010 → 0100 → 1000 → repeat
- Verilog implementation
- Self-correcting logic (handles illegal states)

**Part B: Johnson Counter (10 points)**

Design 4-bit Johnson counter:
- **Pattern**: 0000 → 1000 → 1100 → 1110 → 1111 → 0111 → 0011 → 0001 → repeat
- Verilog implementation
- Compare with ring counter (states, decoding complexity)

Include testbenches and waveforms for both.

---

### Problem 2: Programmable Frequency Divider (25 points)

**Objective**: Design frequency divider with programmable division ratio.

**Specification**:
- **Input**: 50 MHz clock
- **Control**: `DIV_RATIO[7:0]` (division ratio: 1-255)
- **Output**: `CLK_OUT` (divided clock)
- Formula: `f_out = f_in / DIV_RATIO`

**Part A: Design (10 points)**
1. Architecture (counter-based approach)
2. Calculate output frequencies for:
   - DIV_RATIO = 1 (50 MHz)
   - DIV_RATIO = 50 (1 MHz)
   - DIV_RATIO = 250 (200 kHz)
3. Explain 50% duty cycle generation

**Part B: Verilog Implementation (10 points)**
```verilog
module frequency_divider (
    input  wire       CLK_IN,     // 50 MHz
    input  wire       RST_N,
    input  wire [7:0] DIV_RATIO,
    output reg        CLK_OUT
);
    // Your code
endmodule
```

Requirements:
- Handle DIV_RATIO = 0 (pass-through)
- 50% duty cycle when possible
- Glitch-free output

**Part C: Testing (5 points)**
- Testbench with multiple division ratios
- Calculate actual output frequencies
- Measure duty cycle

---

### Problem 3: LFSR and Pseudo-Random Sequence (25 points)

**Objective**: Design Linear Feedback Shift Register for random number generation.

**Specification**: 8-bit maximal-length LFSR
- **Taps**: positions 8, 6, 5, 4 (x^8 + x^6 + x^5 + x^4 + 1)
- **Period**: 255 (all states except 0000_0000)
- **Output**: 8-bit pseudo-random value

**Part A: Theory (8 points)**
1. Explain LFSR operation
2. Draw block diagram with XOR feedback
3. Why is all-zero state excluded?
4. Calculate sequence period

**Part B: Verilog Implementation (12 points)**
```verilog
module lfsr_8bit (
    input  wire       CLK,
    input  wire       RST_N,
    input  wire       ENABLE,
    input  wire [7:0] SEED,     // Initial value (non-zero)
    output reg  [7:0] RANDOM
);
    // Implement LFSR with taps at [8,6,5,4]
endmodule
```

**Part C: Verification (5 points)**
- Testbench running for 300 clocks
- Verify no repeated value (until period completes)
- Plot histogram (if time permits)

---

### Problem 4: Digital Clock Display (30 points)

**Objective**: Design complete digital clock (HH:MM:SS, 24-hour format).

**Specification**:
- **Display**: 6 digits (HH:MM:SS)
- **Controls**: 
  - `SET_HOURS`, `SET_MINS`, `SET_SECS` (buttons to set time)
  - `RUN_STOP` (toggle)
- **Clock**: 1 Hz (generated from 50 MHz)
- **Range**: 00:00:00 to 23:59:59 (then rollover)

**Part A: Architecture (10 points)**
1. Block diagram showing:
   - Clock divider (50MHz → 1Hz)
   - Cascaded BCD counters (seconds, minutes, hours)
   - Control logic for setting time
   - 7-segment display driver
2. Counter cascade (carry propagation)

**Part B: Verilog Implementation (15 points)**

Modular design:
- Clock divider module
- BCD counter module (with load capability)
- Control FSM (RUN, SET_H, SET_M, SET_S states)
- 7-segment decoder (reuse from Assignment 2)
- Top-level integration

**Part C: FPGA Demo (5 points)**
- Program DE10-Lite
- KEY0 = RUN/STOP
- KEY1 = Mode (select what to set)
- KEY2 = Increment selected field
- HEX[5:0] = time display
- Demonstrate setting time and running

---

## Grading Rubric

### Problem 1 (20 points)
- Ring counter: 10 points
- Johnson counter: 10 points
- (Verilog, waveforms, comparison)

### Problem 2 (25 points)
- Design and calculations: 10 points
- Verilog: 10 points
- Testing: 5 points

### Problem 3 (25 points)
- Theory: 8 points
- Implementation: 12 points
- Verification: 5 points

### Problem 4 (30 points)
- Architecture: 10 points
- Verilog modules: 15 points
- FPGA demo: 5 points

---

## Check-off Requirements

Demonstrate:
1. **Frequency Divider**: Show different division ratios
2. **LFSR**: Verify pseudo-random sequence
3. **Digital Clock**: Set time and demonstrate counting

---

## Resources
- Counter Architectures Guide
- LFSR Theory and Applications
- Clock Divider Techniques
- BCD Counter Cascading

---

**Timing and synchronization are critical for counters. Test thoroughly!** ⏰
