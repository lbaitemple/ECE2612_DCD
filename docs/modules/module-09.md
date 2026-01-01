---
layout: default
title: Module 9 - Finite State Machines
parent: Course Modules
nav_order: 10
permalink: /docs/modules/module-09/
---

# Module 9: Finite State Machines (FSM)
**Weeks 11-12**

---

## Overview

Master FSM design - the key abstraction for controlling complex digital systems. Learn to design robust controllers for real-world applications.

**Duration**: 2 weeks  
**Prerequisites**: Modules 6-8 completed

---

## Learning Objectives

By the end of this module, you will be able to:
1. Design Moore and Mealy state machines from specifications
2. Implement FSM controllers in Verilog using standard templates
3. Create datapath + control architectures
4. Optimize state encoding for speed and area
5. Debug state machines using simulation and hardware
6. Apply FSM design to real-world control problems

---

## Topics

### 1. FSM Design Methodology

**Complete Design Process**:
1. Understand specification thoroughly
2. Draw state diagram (bubble diagram)
3. Create state table
4. Choose state encoding strategy
5. Derive next-state logic equations
6. Derive output logic equations
7. Implement in Verilog
8. Verify with comprehensive testbench
9. Synthesize and test on hardware

### 2. State Encoding Strategies

#### Binary Encoding
- **Bits needed**: ⌈log₂(N)⌉ for N states
- **Pros**: Minimum flip-flops
- **Cons**: Complex next-state logic
- **Use when**: Area-constrained designs

#### One-Hot Encoding
- **Bits needed**: N for N states
- **Pros**: Simple logic, fast, easy to debug
- **Cons**: More flip-flops
- **Use when**: Speed-critical, FPGA designs

#### Gray Code
- **Bits needed**: ⌈log₂(N)⌉ for N states
- **Pros**: Only one bit changes per transition
- **Cons**: Encoding can be tricky
- **Use when**: Minimizing switching noise

### 3. FSM Coding Styles in Verilog

#### One Always Block
- Combines state register, next-state, and output logic
- Compact but harder to debug

#### Two Always Blocks
- Separate state register from logic
- Commonly used

#### Three Always Blocks (Recommended)
- State register
- Next-state combinational logic
- Output logic
- Most readable and maintainable

### 4. Moore vs Mealy Revisited

**Moore Machine**:
- Outputs = f(current_state)
- Synchronous outputs (glitch-free)
- May need more states
- Preferred for most designs

**Mealy Machine**:
- Outputs = f(current_state, inputs)
- Can respond faster (1 cycle less)
- Fewer states possible
- Outputs can glitch

### 5. Datapath + Control Architecture

**Datapath**: Performs data operations (ALU, registers, muxes)  
**Control**: FSM that orchestrates datapath operations

**Benefits**:
- Separation of concerns
- Easier verification
- Scalable design

### 6. Advanced FSM Topics
- Hierarchical state machines
- Concurrent state machines
- FSM with datapath (FSMD)
- Safe state machines (error recovery)

---

## Assignment 9

**Due**: End of Week 12  
**Points**: 100

### Requirements

**Part 1**: Traffic Light Controller (35 points)
Design 4-way intersection controller:
- States: Green, Yellow, Red for each direction
- Minimum green time: 20 seconds
- Yellow time: 5 seconds
- Sensor input for traffic detection
- Pedestrian crossing request
- Draw state diagram
- Implement Moore version in Verilog
- Testbench with various scenarios

**Part 2**: Vending Machine (35 points)
Design controller for vending machine:
- Item cost: 25 cents
- Accepts: nickels (5¢), dimes (10¢), quarters (25¢)
- Outputs: Dispense item, Return change
- Handle exact change, overpayment
- Reset after transaction
- Implement both Moore and Mealy
- Compare implementations

**Part 3**: UART Transmitter (20 points)
Design serial transmitter FSM:
- 8 data bits, 1 start bit, 1 stop bit
- Parallel load, serial output
- Baud rate generation
- Busy/done flags
- Implement and test

**Part 4**: FPGA Demo (10 points)
- Implement traffic light controller on DE10-Lite
- Use LEDs for lights
- Buttons for sensors
- Demo video

[Download Assignment Template](../assignments/assignment-09/)

---

## Resources

### Lecture Materials
- [Module 9 Slides](../../resources/lectures/module09_slides.pdf)

### Interactive Tools
- [FSM Designer](https://madebyevan.com/fsm/) - Visual state machine editor
- [State Diagram Drawer](https://www.draw.io/) - Diagrams
- [FSM Simulator](https://ivanzuzak.info/noam/webapps/fsm_simulator/)

### Video Tutorials
- FSM Design Methodology (40 min)
- Verilog FSM Coding Styles (30 min)
- Traffic Light Controller Example (45 min)
- Datapath + Control Architecture (35 min)

---

## Lab Exercise

### Lab 9: FSM Controllers
**Objectives**:
- Design complex state machines
- Implement using proper coding style
- Test edge cases and error conditions
- Debug state machines on hardware

**Project Options** (choose one):
- Elevator controller (3 floors)
- Parking garage gate controller
- Game controller (Simon Says, Pong, etc.)

[View Full Lab Instructions](../../labs/sequential/lab09/)

---

## Standard FSM Template (3 Always Blocks)

```verilog
module fsm_template (
    input  wire clk, reset,
    input  wire input_signal,
    output reg  output_signal
);
    // State encoding (choose one style)
    // Binary encoding:
    localparam IDLE    = 2'b00;
    localparam STATE1  = 2'b01;
    localparam STATE2  = 2'b10;
    localparam STATE3  = 2'b11;
    
    // Or One-Hot encoding:
    // localparam IDLE   = 4'b0001;
    // localparam STATE1 = 4'b0010;
    // localparam STATE2 = 4'b0100;
    // localparam STATE3 = 4'b1000;
    
    reg [1:0] current_state, next_state;
    
    // 1. State register (sequential)
    always @(posedge clk or posedge reset) begin
        if (reset)
            current_state <= IDLE;
        else
            current_state <= next_state;
    end
    
    // 2. Next-state logic (combinational)
    always @(*) begin
        // Default assignment to avoid latches
        next_state = current_state;
        
        case (current_state)
            IDLE: begin
                if (input_signal)
                    next_state = STATE1;
                else
                    next_state = IDLE;
            end
            
            STATE1: begin
                if (input_signal)
                    next_state = STATE2;
                else
                    next_state = IDLE;
            end
            
            STATE2: begin
                next_state = STATE3;
            end
            
            STATE3: begin
                next_state = IDLE;
            end
            
            default: next_state = IDLE;
        endcase
    end
    
    // 3. Output logic (combinational for Moore, can be in next-state for Mealy)
    always @(*) begin
        // Default assignments
        output_signal = 1'b0;
        
        case (current_state)
            IDLE:    output_signal = 1'b0;
            STATE1:  output_signal = 1'b0;
            STATE2:  output_signal = 1'b1;
            STATE3:  output_signal = 1'b1;
            default: output_signal = 1'b0;
        endcase
    end
    
endmodule
```

---

## Design Examples

### Traffic Light Controller (Simplified)
```verilog
module traffic_light (
    input  wire clk, reset,
    input  wire sensor,      // Car detected
    output reg  [2:0] light  // {R, Y, G}
);
    // State encoding
    localparam NS_GREEN  = 3'b000;
    localparam NS_YELLOW = 3'b001;
    localparam EW_GREEN  = 3'b010;
    localparam EW_YELLOW = 3'b011;
    
    reg [2:0] state, next_state;
    reg [3:0] timer;
    
    // State register
    always @(posedge clk or posedge reset) begin
        if (reset) begin
            state <= NS_GREEN;
            timer <= 0;
        end else begin
            state <= next_state;
            // Timer logic here
        end
    end
    
    // Next state and output logic
    // ... (implementation details)
    
endmodule
```

### Vending Machine Controller
```verilog
module vending_machine (
    input  wire       clk, reset,
    input  wire [1:0] coin_in,  // 00:none, 01:nickel, 10:dime, 11:quarter
    output reg        dispense,
    output reg  [1:0] change     // Amount to return
);
    // States represent amount deposited
    localparam S0  = 3'b000;  // $0
    localparam S5  = 3'b001;  // $0.05
    localparam S10 = 3'b010;  // $0.10
    localparam S15 = 3'b011;  // $0.15
    localparam S20 = 3'b100;  // $0.20
    
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
        next_state = state;
        dispense = 0;
        change = 0;
        
        case (state)
            S0: begin
                case (coin_in)
                    2'b01: next_state = S5;   // Nickel
                    2'b10: next_state = S10;  // Dime
                    2'b11: begin              // Quarter
                        next_state = S0;
                        dispense = 1;
                        change = 0;
                    end
                endcase
            end
            
            S5: begin
                case (coin_in)
                    2'b01: next_state = S10;
                    2'b10: next_state = S15;
                    2'b11: begin
                        next_state = S0;
                        dispense = 1;
                        change = 2'b01;  // 5 cents
                    end
                endcase
            end
            
            // ... other states
        endcase
    end
endmodule
```

---

## Common Mistakes

❌ **Incomplete case statements**
- Missing states causes latches
- Always include default case

❌ **Forgetting default assignments**
- Outputs can latch
- Assign defaults before case statement

❌ **Using blocking assignments in sequential blocks**
- Use <= in clocked always blocks
- Use = only in combinational blocks

❌ **Unreachable states**
- Every state should be reachable
- Include recovery mechanism

✅ **Good Practice**
- Use descriptive state names
- Comment state meanings
- Draw state diagram first
- Test all transitions
- Include timeout/error states
- Use parameters for constants

---

## Debugging FSM

### Simulation Techniques
1. **State transition checking**: Verify all transitions occur
2. **State coverage**: Ensure all states are visited
3. **Edge cases**: Test unusual input sequences
4. **Timing**: Verify outputs change at correct times

### Hardware Debugging
1. **SignalTap**: Monitor state in real-time
2. **LED indicators**: Display current state
3. **7-segment**: Show state code
4. **UART output**: Send state information to PC

---

## Next Steps

After completing Module 9, proceed to:
- **[Module 10: Memory Systems](module-10/)**
- RAM, ROM, FIFO design
- Memory interfacing

---

[← Previous Module](module-08/) | [Back to All Modules](../) | [Next Module →](module-10/)
