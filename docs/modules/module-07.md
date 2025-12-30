---
layout: default
title: Module 7 - Sequential Design
parent: Course Modules
nav_order: 8
permalink: /docs/modules/module-07/
---

# Module 7: Sequential Circuit Design
**Weeks 8-9**

[View Full Module Content](../../../Module_07_Sequential_Design.md)

---

## Overview

Design and analyze synchronous sequential circuits using state machines and timing diagrams.

**Duration**: 2 weeks  
**Prerequisites**: Module 6 completed

---

## Learning Objectives

By the end of this module, you will be able to:
1. Analyze sequential circuits to determine behavior
2. Design synchronous state machines from specifications
3. Create state diagrams and state tables
4. Implement circuits using flip-flops and logic gates
5. Distinguish between Moore and Mealy machines
6. Perform state reduction and optimization

---

## Topics

### 1. Sequential Circuit Analysis
**Given circuit → determine behavior**

Process:
1. Write excitation equations (inputs to flip-flops)
2. Derive next-state equations
3. Create state table
4. Draw state diagram
5. Determine output equations

### 2. Sequential Circuit Synthesis
**Given specification → design circuit**

Process:
1. Create state diagram from word description
2. Assign binary codes to states (state encoding)
3. Create state table
4. Derive excitation tables for flip-flops
5. Simplify using K-maps
6. Implement using flip-flops and gates

### 3. State Machine Types

#### Moore Machine
- **Output depends only on current state**
- Outputs change synchronously with state transitions
- Generally requires more states
- More robust to input glitches

#### Mealy Machine
- **Output depends on current state AND inputs**
- Outputs can change asynchronously with inputs
- Generally requires fewer states
- Can respond faster to inputs

### 4. State Encoding Strategies
- **Binary**: Minimum number of flip-flops (log₂ N)
- **Gray Code**: Only one bit changes per transition
- **One-Hot**: One flip-flop per state (fast but costly)
- **Custom**: Optimized for specific design goals

### 5. State Reduction
- Identify and merge equivalent states
- Minimize number of states while preserving behavior
- Reduces hardware complexity

### 6. Design Verification
- State coverage testing
- Transition testing
- Timing simulation
- Hardware verification

---

## Assignment 7

**Due**: End of Week 9  
**Points**: 100

### Requirements

**Part 1**: Circuit Analysis (25 points)
Given sequential circuit schematic:
- Write excitation and next-state equations
- Create state table
- Draw state diagram
- Describe circuit behavior

**Part 2**: Sequence Detector Design (40 points)
Design detector for pattern "1011":
- **Moore version**: Create state diagram, implement
- **Mealy version**: Create state diagram, implement
- Compare: # states, # flip-flops, timing
- Implement both in Verilog with testbenches

**Part 3**: State Optimization (20 points)
Given state machine with redundant states:
- Identify equivalent states
- Perform state reduction
- Show before/after comparison
- Implement reduced version

**Part 4**: FPGA Implementation (15 points)
- Implement sequence detector on DE10-Lite
- Use switches for serial input
- Use button for clock
- Display state on LEDs
- Output on 7-segment display

[Download Assignment Template](../../assignments/assignment-07.md)

---

## Resources

### Lecture Materials
- [Module 7 Slides](../../resources/lectures/module07_slides.pdf)
- [State Machine Design Guide](../../resources/fsm_design_guide.pdf)
- [Moore vs Mealy Comparison](../../resources/moore_mealy.pdf)

### Interactive Tools
- [State Machine Designer](https://madebyevan.com/fsm/)
- [Digital Logic Simulator](https://sebastian.itch.io/digital-logic-sim)
- [JK Flip-Flop Excitation Calculator](https://www.electronics-tutorials.ws/)

### Video Tutorials
- Sequential Circuit Analysis Walkthrough (30 min)
- State Machine Design Methodology (35 min)
- Moore vs Mealy State Machines (20 min)

### Practice Problems
- [State Diagram Exercises](../../practice/module07/state_diagrams.pdf)
- [Sequential Analysis Problems](../../practice/module07/analysis.pdf)
- [State Reduction Worksheet](../../practice/module07/reduction.pdf)

---

## Lab Exercise

### Lab 7: State Machine Controllers
**Objectives**:
- Design state machine from specification
- Implement Moore and Mealy versions
- Compare implementations
- Test thoroughly

**Tasks**:
- Traffic light controller
- Vending machine controller
- Elevator controller (choose one)

[View Full Lab Instructions](../../labs/sequential/lab07/)

---

## Design Methodology

### Complete Design Flow
```
1. Problem Specification
   ↓
2. State Diagram
   ↓
3. State Table
   ↓
4. State Assignment
   ↓
5. Excitation Tables
   ↓
6. K-Map Minimization
   ↓
7. Logic Implementation
   ↓
8. Verilog Coding
   ↓
9. Simulation & Verification
   ↓
10. FPGA Implementation
```

---

## Design Examples

### Moore Machine - Sequence Detector (1011)
```verilog
module seq_detector_moore (
    input  wire clk, reset, x,
    output reg  z
);
    // State encoding
    localparam S0 = 3'b000;  // Initial
    localparam S1 = 3'b001;  // Saw '1'
    localparam S2 = 3'b010;  // Saw '10'
    localparam S3 = 3'b011;  // Saw '101'
    localparam S4 = 3'b100;  // Saw '1011' - output 1
    
    reg [2:0] state, next_state;
    
    // State register
    always @(posedge clk or posedge reset) begin
        if (reset)
            state <= S0;
        else
            state <= next_state;
    end
    
    // Next state logic
    always @(*) begin
        case (state)
            S0: next_state = x ? S1 : S0;
            S1: next_state = x ? S1 : S2;
            S2: next_state = x ? S3 : S0;
            S3: next_state = x ? S4 : S2;
            S4: next_state = x ? S1 : S2;
            default: next_state = S0;
        endcase
    end
    
    // Output logic (Moore - depends only on state)
    always @(*) begin
        z = (state == S4);
    end
endmodule
```

### Mealy Machine - Sequence Detector (1011)
```verilog
module seq_detector_mealy (
    input  wire clk, reset, x,
    output reg  z
);
    // State encoding (needs fewer states)
    localparam S0 = 2'b00;  // Initial
    localparam S1 = 2'b01;  // Saw '1'
    localparam S2 = 2'b10;  // Saw '10'
    localparam S3 = 2'b11;  // Saw '101'
    
    reg [1:0] state, next_state;
    
    // State register
    always @(posedge clk or posedge reset) begin
        if (reset)
            state <= S0;
        else
            state <= next_state;
    end
    
    // Next state and output logic
    always @(*) begin
        z = 1'b0;  // Default output
        case (state)
            S0: begin
                next_state = x ? S1 : S0;
            end
            S1: begin
                next_state = x ? S1 : S2;
            end
            S2: begin
                next_state = x ? S3 : S0;
            end
            S3: begin
                if (x) begin
                    next_state = S1;
                    z = 1'b1;  // Output (Mealy)
                end else begin
                    next_state = S2;
                end
            end
            default: next_state = S0;
        endcase
    end
endmodule
```

---

## Common Mistakes

❌ **Incomplete state diagram**
- Missing transitions for all input combinations
- Undefined states or unreachable states

❌ **Incorrect state encoding**
- Not enough bits to encode all states
- Conflicting state assignments

❌ **Output logic errors**
- Moore: outputs depend on inputs (should be state-only)
- Mealy: forgetting to specify outputs for all transitions

❌ **Reset not included**
- Always include reset to known state
- Specify reset behavior clearly

✅ **Good Practice**
- Document state meanings clearly
- Test all state transitions
- Include reset in all designs
- Use descriptive state names
- Verify with comprehensive testbench

---

## State Encoding Comparison

### Example: 5-State Machine

**Binary Encoding** (3 bits needed):
```
S0: 000
S1: 001
S2: 010
S3: 011
S4: 100
```
- Minimum flip-flops (3)
- Complex next-state logic

**One-Hot Encoding** (5 bits):
```
S0: 00001
S1: 00010
S2: 00100
S3: 01000
S4: 10000
```
- More flip-flops (5)
- Simpler next-state logic
- Faster operation
- Easier to debug

---

## Next Steps

After completing Module 7, proceed to:
- **[Module 8: Counters & Registers](module-08/)**
- Specialized sequential circuits
- Timing and control applications

---

[← Previous Module](module-06/) | [Back to All Modules](../) | [Next Module →](module-08/)
