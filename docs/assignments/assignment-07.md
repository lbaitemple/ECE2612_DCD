---
layout: default
title: Assignment 7 - Sequential Circuit Design
parent: Assignments
nav_order: 8
---

# Assignment 7: Sequential Circuit Design
**Module 7 - Sequential Design**

---

## Assignment Information

- **Due Date**: End of Week 8
- **Points**: 100
- **Submission**: Canvas (PDF + Verilog files)
- **Type**: Group (2-3 students)
- **Check-off Required**: Yes (30% penalty if not completed)
- **Estimated Time**: 12-15 hours

---

## Learning Objectives

- Design synchronous sequential circuits from specifications
- Create state machines for control logic
- Implement counters with various moduli
- Build practical sequential systems
- Analyze sequential circuit timing

---

## Problems

### Problem 1: Synchronous Counter Design (25 points)

**Objective**: Design a mod-12 up/down counter.

**Specification**:
- **Inputs**: `CLK`, `RST_N`, `UP_DOWN` (1=up, 0=down), `ENABLE`
- **Outputs**: `COUNT[3:0]`, `TC` (terminal count)
- Counts: 0→11 (up) or 11→0 (down)
- TC pulses when reaching limit (11 for up, 0 for down)
- Enable controls counting (hold when ENABLE=0)

**Part A: Design (10 points)**
1. State diagram or transition table
2. Explain wrap-around behavior
3. Block diagram

**Part B: Verilog (10 points)**
```verilog
module counter_mod12 (
    input  wire       CLK,
    input  wire       RST_N,
    input  wire       UP_DOWN,
    input  wire       ENABLE,
    output reg  [3:0] COUNT,
    output reg        TC
);
    // Your code
endmodule
```

**Part C: Testing (5 points)**
- Testbench with full up count, full down count
- Waveform screenshot

---

### Problem 2: Sequence Generator (25 points)

**Objective**: Design FSM that generates repeating sequence: 0, 3, 7, 10, 14, repeat.

**Specification**:
- **Outputs**: `OUT[3:0]` (generates sequence on consecutive clocks)
- **Control**: `START` (begin sequence), `STOP` (pause)
- When stopped, holds current value

**Part A: FSM Design (10 points)**
1. State diagram with 5 states
2. Output encoding for each state
3. Transition conditions

**Part B: Verilog (10 points)**
- Implement as Moore machine
- Include START/STOP control

**Part C: Verification (5 points)**
- Testbench showing multiple sequence cycles
- Demonstrate start/stop behavior

---

### Problem 3: Digital Stopwatch (30 points)

**Objective**: Design a stopwatch with minutes:seconds.tenths display.

**Specification**:
- **Range**: 00:00.0 to 59:59.9
- **Controls**: `START`, `STOP`, `RESET`
- **Clock**: 10 Hz (100ms period)
- **Outputs**: 
  - `MIN_TENS[3:0]`, `MIN_ONES[3:0]` (minutes)
  - `SEC_TENS[3:0]`, `SEC_ONES[3:0]` (seconds)
  - `TENTH[3:0]` (tenths of second)

**Part A: Architecture (10 points)**
1. Block diagram showing counter chain
2. Clock divider (if needed from 50MHz to 10Hz)
3. Carry/rollover logic between digits

**Part B: Verilog Implementation (15 points)**

Create modular design:
- BCD counter module (0-9 with rollover)
- Stopwatch control FSM
- Top-level integration

**Part C: FPGA Demo (5 points)**
- KEY0 = START/STOP toggle
- KEY1 = RESET
- HEX displays show time
- Demonstrate counting and reset

---

### Problem 4: Button Debouncer (20 points)

**Objective**: Design robust button debouncer for FPGA.

**Specification**:
- Eliminates mechanical bounce
- Generates clean single pulse per press
- Typical bounce duration: ~10ms

**Part A: Theory (7 points)**
1. Explain button bouncing problem (with diagram)
2. Compare debouncing methods:
   - Counter-based
   - Shift register-based
3. Choose method and justify

**Part B: Verilog Implementation (10 points)**

Counter-based debouncer example:
```verilog
module debouncer (
    input  wire CLK,        // 50 MHz
    input  wire BTN_IN,     // Raw button
    output reg  BTN_OUT     // Debounced pulse
);
    parameter DEBOUNCE_TIME = 500000; // 10ms at 50MHz
    
    // Your implementation
    
endmodule
```

Requirements:
- Configurable debounce time
- Generates single pulse on press
- Works with active-low buttons (DE10-Lite KEY)

**Part C: Integration (3 points)**
- Integrate with stopwatch or counter
- Demonstrate button debouncing works

---

## Grading Rubric

### Problem 1 (25 points)
- Design: 10 points
- Verilog: 10 points
- Testing: 5 points

### Problem 2 (25 points)
- FSM design: 10 points
- Verilog: 10 points
- Verification: 5 points

### Problem 3 (30 points)
- Architecture: 10 points
- Verilog: 15 points
- FPGA demo: 5 points

### Problem 4 (20 points)
- Theory: 7 points
- Implementation: 10 points
- Integration: 3 points

---

## Check-off Requirements

Demonstrate to instructor/TA:
1. **Mod-12 Counter**: Show up/down counting, terminal count
2. **Stopwatch**: Start, stop, reset, verify timing
3. **Debouncer**: Show clean button operation

---

## Resources
- Counter Design Patterns
- FSM for Sequential Control
- Clock Divider Techniques
- Debouncing Guide

---

**Sequential design requires careful state management. Plan before coding!** 🔄
