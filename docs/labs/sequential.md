---
layout: default
title: Sequential Logic Labs
parent: Labs & Exercises
nav_order: 2
has_children: true
permalink: /docs/labs/sequential/
---

# Sequential Logic Labs

Advanced laboratory exercises focusing on sequential circuit design, state machines, counters, registers, and memory systems.

---

## Lab Overview

These labs cover sequential logic concepts:
- Flip-flops and latches
- Registers and shift registers
- Finite state machines (FSM)
- Counters and timers
- Memory systems (ROM, RAM, FIFO)
- Synchronous design principles
- Timing analysis

---

## Lab Sequence

| Lab | Title | Week | Topics |
|-----|-------|------|--------|
| [Lab 5a](lab5a) | Latches and Flip-flops | 8 | SR latch, D latch, D flip-flop, registers |
| [Lab 5](lab5) | Shift Logic | 9 | Logical/arithmetic shift, barrel shifter |
| [Lab 6](lab6) | Multiple Digit Display | 10 | Display multiplexing, refresh counters |
| [Lab 7](lab7) | Rotary Encoder | 11-12 | Quadrature decoding, FSM, debouncing |
| [Lab 8](lab8) | Memory Systems | 13 | Register file, multi-port memory |

---

## Learning Path

```
← Combinational Logic Labs (Complete first)
    ↓
Lab 5a: Latches & Flip-flops (Sequential fundamentals)
    ↓
Lab 5: Shift Logic (Combinational shifters)
    ↓
Lab 6: Multi-Digit Display (Counter + multiplexing)
    ↓
Lab 7: Rotary Encoder (FSM application)
    ↓
Lab 8: Memory Systems (Register file design)
    ↓
→ Final Project
```

---

## Lab Format

Each lab includes:
- **Learning Objectives**: Sequential design concepts
- **Prerequisites**: Combinational logic foundation
- **FSM Design**: State diagrams and transition tables
- **Timing Analysis**: Setup/hold time calculations
- **FPGA Implementation**: Hardware demonstration
- **Checkoff**: Required for all sequential labs

---

## Required Skills

Before starting sequential labs, you should:
- ✅ Complete all combinational logic labs (Labs 1-4)
- ✅ Be proficient in Verilog/SystemVerilog
- ✅ Know how to use Quartus and ModelSim
- ✅ Be comfortable with FPGA programming
- ✅ Understand seven-segment displays

---

## Key Concepts

### Synchronous Design
- All state changes on clock edges
- Proper reset methodology
- Clock domain considerations

### State Machines
- Moore vs Mealy FSMs
- State encoding (binary, one-hot, Gray)
- State diagram design
- Transition logic

### Timing
- Setup and hold time
- Clock-to-Q delay
- Maximum frequency calculation
- Critical path analysis

---

## Submission Guidelines

Sequential labs require:
1. **Verilog Code**: State machines, counters, registers
2. **State Diagrams**: Hand-drawn or digital
3. **Timing Analysis**: Calculations and explanations
4. **Waveforms**: Simulation screenshots
5. **FPGA Demo**: Video or in-person checkoff
6. **Lab Report**: Comprehensive documentation

---

## Common Challenges

### Timing Issues
- **Problem**: Violations in TimeQuest
- **Solution**: Review timing constraints, reduce logic depth

### Metastability
- **Problem**: Asynchronous inputs
- **Solution**: Use synchronizers (2-FF chains)

### State Machine Bugs
- **Problem**: Unreachable states, deadlock
- **Solution**: Complete state transition table, default cases

### Counter Overflow
- **Problem**: Counter doesn't wrap correctly
- **Solution**: Verify modulo logic, test edge cases

---

## Resources

- [Lab Resources](../../resources/lab-resources/)
- [AWS Cloud Setup](../../preparation/aws-setup/)
- [DE10-Lite Pin Assignments](../../resources/lab-resources/)

---

**Start with [Lab 5a: Latches and Flip-flops](lab5a) to begin sequential design!**
