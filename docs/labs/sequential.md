---
layout: default
title: Sequential Logic Labs
parent: Labs & Exercises
nav_order: 2
has_children: true
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

1. **Lab 5**: Flip-flops and registers
2. **Lab 5a**: Introduction to FSMs
3. **Lab 6**: Counters and timers
4. **Lab 7**: Finite state machine design
5. **Lab 8**: Memory systems and advanced topics

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
- ✅ Understand combinational logic
- ✅ Be proficient in Verilog/SystemVerilog
- ✅ Know how to use Quartus and ModelSim
- ✅ Be comfortable with FPGA programming
- ✅ Understand binary arithmetic

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

- [FSM Design Tutorial](../../resources#fsm-design)
- [Timing Analysis Guide](../../resources#timing)
- [Sequential Verilog Patterns](../../resources#verilog-patterns)
- [State Machine Coding Styles](../../resources#coding-styles)

---

**Start with [Lab 5: Flip-Flops and Registers](lab5) to begin sequential design!**
