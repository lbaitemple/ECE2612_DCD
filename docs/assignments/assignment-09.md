---
layout: default
title: Assignment 9 - Finite State Machines
parent: Assignments
nav_order: 10
---

# Assignment 9: Finite State Machines
**Module 9 - FSM Design**

---

## Assignment Information

- **Due Date**: End of Week 10
- **Points**: 100
- **Submission**: Canvas (PDF + Verilog files)
- **Type**: Group (2-3 students)
- **Check-off Required**: Yes (30% penalty if not completed)
- **Estimated Time**: 12-15 hours

---

## Learning Objectives

By completing this assignment, you will:
- Design and implement Mealy and Moore state machines
- Create state diagrams from specifications
- Implement FSMs in Verilog with proper state encoding
- Verify FSM behavior through simulation and hardware testing
- Apply FSM design to real-world applications

---

## Assignment Problems

### Problem 1: Sequence Detector FSM (25 points)

**Objective**: Design a Moore FSM that detects the sequence "1011" in a serial bit stream.

**Specification**:

Design a sequence detector with the following requirements:
- **Input**: `DIN` (serial data input, 1 bit)
- **Outputs**: 
  - `DETECTED` (pulses high for one clock when sequence is found)
  - `STATE[2:0]` (current state for debugging, 3 bits)
- **Clock/Reset**: `CLK`, `RST_N` (active-low asynchronous reset)

**Behavior**:
- Continuously monitors input stream
- Overlapping sequences allowed (e.g., "10110**1011**" detects twice)
- Output pulses for exactly one clock cycle when complete sequence appears
- Reset to initial state when RST_N = 0

**Part A: State Diagram (10 points)**

Draw a Moore state machine diagram with:
1. **States**: Clear, descriptive names (e.g., S0_IDLE, S1_SAW1, S2_SAW10, etc.)
2. **Transitions**: Labeled with input conditions (DIN=0, DIN=1)
3. **Outputs**: Listed in each state bubble
4. **Encoding**: Specify state encoding (binary, gray, one-hot - justify choice)

**State Definition Example**:
```
S0_IDLE:     No bits matched yet         (DETECTED = 0)
S1_SAW1:     Saw '1'                     (DETECTED = 0)
S2_SAW10:    Saw '10'                    (DETECTED = 0)
S3_SAW101:   Saw '101'                   (DETECTED = 0)
S4_SAW1011:  Complete sequence '1011'   (DETECTED = 1)
```

Requirements:
- Handle all possible input sequences
- Show recovery paths (what happens after detection?)
- Indicate reset state with double circle or arrow
- Verify all states are reachable

**Part B: State Transition Table (5 points)**

Create complete state transition table:

| Current State | DIN=0 | DIN=1 | DETECTED |
|--------------|-------|-------|----------|
| S0_IDLE | S0 | S1 | 0 |
| S1_SAW1 | S2 | S1 | 0 |
| S2_SAW10 | S0 | S3 | 0 |
| S3_SAW101 | S2 | S4 | 0 |
| S4_SAW1011 | S2 | S1 | 1 |

**Part C: Verilog Implementation (10 points)**

Implement using two-process FSM style:

```verilog
module sequence_detector_1011 (
    input  wire       CLK,
    input  wire       RST_N,
    input  wire       DIN,
    output reg        DETECTED,
    output reg  [2:0] STATE
);

    // State encoding (use parameter or localparam)
    localparam S0_IDLE     = 3'b000;
    localparam S1_SAW1     = 3'b001;
    localparam S2_SAW10    = 3'b010;
    localparam S3_SAW101   = 3'b011;
    localparam S4_SAW1011  = 3'b100;
    
    reg [2:0] current_state, next_state;
    
    // Process 1: State register
    always @(posedge CLK or negedge RST_N) begin
        // Your code here
    end
    
    // Process 2: Next state logic
    always @(*) begin
        // Your code here
    end
    
    // Process 3: Output logic (Moore machine)
    always @(*) begin
        // Your code here
    end

endmodule
```

Requirements:
- Use two or three always blocks (state register, next state, outputs)
- Proper state encoding
- Complete case statement with default
- Clean, well-commented code

---

### Problem 2: Traffic Light Controller (30 points)

**Objective**: Design a complete traffic light controller for a 4-way intersection.

**Specification**:

Design an FSM to control traffic lights at an intersection with:
- **Main street**: North-South direction
- **Side street**: East-West direction
- **Sensors**: `CAR_SIDE` (detects cars on side street)
- **Timing**: Configurable green/yellow durations

**Signal Definitions**:

**Inputs**:
- `CLK`: 1 Hz clock (1 second period)
- `RST_N`: Active-low reset
- `CAR_SIDE`: High when car waiting on side street

**Outputs**:
- `MAIN_RED`, `MAIN_YELLOW`, `MAIN_GREEN`: Main street lights
- `SIDE_RED`, `SIDE_YELLOW`, `SIDE_GREEN`: Side street lights

**Timing Requirements**:
- Main green: 30 seconds (if no cars on side street: extend indefinitely)
- Main yellow: 5 seconds
- Side green: 15 seconds  
- Side yellow: 5 seconds
- Both reds during transition: 2 seconds (for safety)

**State Description**:

| State | Main Lights | Side Lights | Duration | Next State Logic |
|-------|-------------|-------------|----------|-----------------|
| MAIN_GREEN | G | R | 30s or until CAR_SIDE | If CAR_SIDE after 30s → MAIN_YELLOW |
| MAIN_YELLOW | Y | R | 5s | Always → ALL_RED1 |
| ALL_RED1 | R | R | 2s | Always → SIDE_GREEN |
| SIDE_GREEN | R | G | 15s | Always → SIDE_YELLOW |
| SIDE_YELLOW | R | Y | 5s | Always → ALL_RED2 |
| ALL_RED2 | R | R | 2s | Always → MAIN_GREEN |

**Part A: State Diagram (10 points)**

Draw complete Moore FSM with:
1. All 6 states clearly labeled
2. Timing conditions on transitions (e.g., "count == 30 && CAR_SIDE")
3. Output values in each state
4. Counters/timers noted

**Part B: Verilog Implementation (15 points)**

```verilog
module traffic_controller (
    input  wire CLK,          // 1 Hz clock
    input  wire RST_N,
    input  wire CAR_SIDE,     // Side street sensor
    output reg  MAIN_RED,
    output reg  MAIN_YELLOW,
    output reg  MAIN_GREEN,
    output reg  SIDE_RED,
    output reg  SIDE_YELLOW,
    output reg  SIDE_GREEN
);

    // State encoding
    localparam MAIN_GREEN  = 3'd0;
    localparam MAIN_YELLOW = 3'd1;
    localparam ALL_RED1    = 3'd2;
    localparam SIDE_GREEN  = 3'd3;
    localparam SIDE_YELLOW = 3'd4;
    localparam ALL_RED2    = 3'd5;
    
    reg [2:0] state, next_state;
    reg [5:0] counter;  // 0-59 for timing
    
    // Your code here
    
endmodule
```

Requirements:
- Implement all 6 states
- Use counter for timing (resets on state change)
- Proper light encoding (only one light on per direction except all red)
- Handle CAR_SIDE correctly (extend main green if no cars)

**Part C: Testbench and Validation (5 points)**

Create testbench that:
1. Tests full cycle: Main green → All transitions → back to main green
2. Tests car arrival on side street during main green
3. Verifies timing durations
4. Checks that illegal states never occur (both greens, etc.)

Provide:
- Testbench code
- Simulation waveform screenshot showing at least one complete cycle
- Explanation of key test scenarios

---

### Problem 3: Vending Machine FSM (20 points)

**Objective**: Design a Mealy FSM for a vending machine.

**Specification**:

Simple vending machine that:
- Dispenses items costing 25 cents
- Accepts nickels (5¢), dimes (10¢), and quarters (25¢)
- Returns change if overpayment

**Inputs**:
- `NICKEL`, `DIME`, `QUARTER`: Pulses (one clock cycle when coin inserted)
- `CLK`, `RST_N`

**Outputs**:
- `DISPENSE`: Pulses when item dispensed
- `RETURN_5`, `RETURN_10`, `RETURN_15`, `RETURN_20`: Change signals (pulse)
- `AMOUNT[4:0]`: Current amount (for display)

**Part A: State Diagram (8 points)**

Draw Mealy FSM with:
- States representing accumulated amount: S0 (0¢), S5 (5¢), S10 (10¢), S15 (15¢), S20 (20¢)
- Transitions labeled with input/output: e.g., "NICKEL / -" or "QUARTER / DISPENSE"
- Handle all coin combinations that lead to ≥25¢

**Example Transitions**:
```
From S0:
  - NICKEL: go to S5, no output
  - DIME: go to S10, no output
  - QUARTER: go to S0, output DISPENSE
  
From S20:
  - NICKEL: go to S0, output DISPENSE
  - DIME: go to S0, output DISPENSE + RETURN_5
  - QUARTER: go to S0, output DISPENSE + RETURN_20
```

**Part B: State Transition and Output Table (6 points)**

| Current State | NICKEL | DIME | QUARTER | Outputs |
|--------------|--------|------|---------|---------|
| S0 (0¢) | S5 | S10 | S0 | -, -, DISPENSE |
| S5 (5¢) | S10 | S15 | S0 | -, -, DISPENSE |
| S10 (10¢) | S15 | S20 | S0 | -, -, DISPENSE+RETURN_15 |
| S15 (15¢) | S20 | S0 | S0 | -, DISPENSE+RETURN_5, DISPENSE+RETURN_10 |
| S20 (20¢) | S0 | S0 | S0 | DISPENSE, DISPENSE+RETURN_5, DISPENSE+RETURN_20 |

**Part C: Verilog Implementation (6 points)**

```verilog
module vending_machine (
    input  wire       CLK,
    input  wire       RST_N,
    input  wire       NICKEL,
    input  wire       DIME,
    input  wire       QUARTER,
    output reg        DISPENSE,
    output reg        RETURN_5,
    output reg        RETURN_10,
    output reg        RETURN_15,
    output reg        RETURN_20,
    output reg  [4:0] AMOUNT
);

    localparam S0  = 3'd0;  // 0 cents
    localparam S5  = 3'd1;  // 5 cents
    localparam S10 = 3'd2;  // 10 cents
    localparam S15 = 3'd3;  // 15 cents
    localparam S20 = 3'd4;  // 20 cents
    
    reg [2:0] state, next_state;
    
    // Your code here
    
endmodule
```

Requirements:
- Mealy machine (outputs depend on state AND inputs)
- Outputs asserted combinationally
- Proper change calculation
- Handle all coin combinations

---

### Problem 4: FPGA Implementation - Combination Lock (25 points)

**Objective**: Implement a 4-digit combination lock on the DE10-Lite FPGA.

**Specification**:

Design an FSM combination lock with:
- **Combination**: 4 switch positions (e.g., SW3=1, SW2=0, SW1=1, SW0=0)
- **Reset**: KEY0
- **Check**: KEY1 (pulse to check current switch settings)
- **LED Indicators**: 
  - LEDR9: Locked (red)
  - LEDR0: Unlocked (green)
  - LEDR[3:0]: Progress indicators (light up as correct digits entered)
- **7-Segment Display**: HEX0 shows current digit position (0-4)

**Behavior**:
1. Lock starts in LOCKED state (LEDR9 on)
2. User sets switches to match position 0 of combo, presses KEY1
3. If correct, progress LED lights, move to next digit
4. If incorrect, reset to start
5. After 4 correct digits in sequence, unlock (LEDR0 on, LEDR9 off)
6. Stays unlocked until reset (KEY0)

**Part A: System Design (10 points)**

Provide:
1. State diagram (at least 6 states: LOCKED, CHECK_DIG0, CHECK_DIG1, CHECK_DIG2, CHECK_DIG3, UNLOCKED)
2. Pin assignment table for switches, keys, LEDs
3. Block diagram showing FSM, debouncer, and 7-seg decoder

**Part B: Verilog Implementation (10 points)**

```verilog
module combination_lock (
    input  wire       CLK,
    input  wire       RST_N,         // KEY0
    input  wire       CHECK,         // KEY1 (debounced)
    input  wire [3:0] SWITCHES,      // Current switch settings
    output reg        LOCKED,        // LEDR9
    output reg        UNLOCKED,      // LEDR0
    output reg  [3:0] PROGRESS,      // LEDR[3:0]
    output reg  [6:0] HEX0           // Position display
);

    // Combination (make it changeable via parameters)
    parameter COMBO_0 = 4'b1010;
    parameter COMBO_1 = 4'b0101;
    parameter COMBO_2 = 4'b1100;
    parameter COMBO_3 = 4'b0011;
    
    // Your FSM code here
    
endmodule
```

Requirements:
- Implement complete FSM
- Use key debouncer (provided module or your own)
- Drive 7-segment display to show position
- Clear progress on incorrect entry

**Part C: Testing and Demo (5 points)**

Provide:
1. **Test procedure**: Step-by-step instructions to test your lock
2. **Video or photos**: Show:
   - Initial locked state
   - Entering correct combo (all 4 digits)
   - Unlocked state
   - Failed attempt (wrong digit)
3. **Brief reflection**: What was challenging? How did you debug?

---

## Grading Rubric

### Problem 1: Sequence Detector (25 points)

| Component | Points | Excellent | Good | Satisfactory | Needs Improvement |
|-----------|--------|-----------|------|--------------|-------------------|
| **State Diagram** | 10 | Perfect diagram, all transitions | Minor errors | Some missing transitions | Many errors |
| **State Table** | 5 | Complete, correct | 1-2 errors | Several errors | Many errors |
| **Verilog** | 10 | Works perfectly, clean code | Minor bugs | Several bugs | Doesn't work |

**State Diagram Rubric Details**:
- Clear state names: 2 pts
- All transitions labeled: 3 pts
- Correct outputs in states: 2 pts
- Handles overlapping sequences: 2 pts
- Professional appearance: 1 pt

**Verilog Rubric Details**:
- Two/three process structure: 2 pts
- Proper state encoding: 2 pts
- Complete case statements: 2 pts
- Correct reset logic: 2 pts
- Code quality: 2 pts

---

### Problem 2: Traffic Light Controller (30 points)

| Component | Points | Criteria |
|-----------|--------|----------|
| **State Diagram** | 10 | All 6 states, timing noted, transitions correct |
| **Verilog FSM** | 12 | All states implemented, timing counters work, proper light control |
| **Testbench** | 5 | Tests full cycle, car sensor, timing verification |
| **Code Quality** | 3 | Well-commented, good style, clear logic |

**Detailed Grading**:

**State Diagram (10 points)**:
- 6 states clearly drawn: 4 pts
- Timing conditions on transitions: 3 pts
- Output encoding correct: 2 pts
- Professional diagram: 1 pt

**Verilog Implementation (12 points)**:
- State machine structure: 3 pts
- Timing counter implementation: 3 pts
- CAR_SIDE handling: 2 pts
- Light output logic: 3 pts
- No illegal states: 1 pt

**Testbench (5 points)**:
- Testbench code provided: 2 pts
- Simulation waveform: 2 pts
- Explanation of tests: 1 pt

**Common Errors to Avoid**:
- ❌ Multiple lights on same street (should be mutually exclusive)
- ❌ Skipping ALL_RED states (safety hazard!)
- ❌ Counter doesn't reset on state change
- ❌ CAR_SIDE ignored

---

### Problem 3: Vending Machine (20 points)

| Component | Points | Excellent | Good | Satisfactory | Poor |
|-----------|--------|-----------|------|--------------|------|
| **State Diagram** | 8 | Complete Mealy diagram | Minor issues | Missing transitions | Incorrect |
| **State/Output Table** | 6 | All correct | 1-2 errors | Several errors | Many errors |
| **Verilog** | 6 | Perfect Mealy machine | Minor bugs | Works partially | Doesn't work |

**Mealy Machine Requirements**:
- ✅ Outputs depend on both state AND input
- ✅ Outputs in combinational logic
- ✅ Proper change calculation
- ✅ Returns to S0 after dispensing
- ✅ Handles exact change and overpayment

**Change Logic Examples**:
- 20¢ + nickel (5¢) = 25¢ → DISPENSE, return to S0
- 20¢ + dime (10¢) = 30¢ → DISPENSE + RETURN_5, return to S0
- 15¢ + quarter (25¢) = 40¢ → DISPENSE + RETURN_15, return to S0

---

### Problem 4: Combination Lock FPGA (25 points)

| Component | Points | Excellent | Good | Satisfactory | Needs Improvement |
|-----------|--------|-----------|------|--------------|-------------------|
| **Design Docs** | 10 | Complete diagram, table, block | Good docs, minor gaps | Basic docs | Incomplete |
| **Verilog** | 10 | Works perfectly | Minor issues | Partially works | Doesn't work |
| **Demo** | 5 | Excellent demo, clear | Good demo | Basic demo | No demo |

**Design Documentation (10 points)**:
- State diagram: 4 pts
- Pin assignment table: 3 pts
- Block diagram: 3 pts

**Verilog Implementation (10 points)**:
- FSM structure: 3 pts
- Correct digit checking: 3 pts
- Progress indicators: 2 pts
- 7-segment display: 2 pts

**Demo and Testing (5 points)**:
- Test procedure: 2 pts
- Evidence (video/photos): 2 pts
- Reflection: 1 pt

**Extra Credit Opportunities** (+5 pts each):
- Add lockout after 3 failed attempts
- Implement timed auto-lock (lock after 30 seconds unlocked)
- Add audible feedback (buzzer) for correct/incorrect

---

## Submission Requirements

### Required Files

**PDF Document** (`GroupName_Assignment9.pdf`):
1. **Cover Page**: 
   - Assignment title
   - Group members' names
   - Date

2. **Problem 1**:
   - State diagram
   - State transition table
   - Verilog code
   - Brief explanation

3. **Problem 2**:
   - State diagram
   - Verilog code
   - Testbench code
   - Simulation waveform
   - Analysis

4. **Problem 3**:
   - State diagram (Mealy)
   - State/output table
   - Verilog code
   - Example trace

5. **Problem 4**:
   - System design (diagrams, tables)
   - Verilog code
   - Demo evidence
   - Reflection

**Verilog Source Files**:
- `sequence_detector_1011.v`
- `traffic_controller.v`
- `vending_machine.v`
- `combination_lock.v`
- `combination_lock_top.v` (top-level with debouncer, 7-seg)
- Optional: testbench files

**Demo Evidence**:
- Photos or video of combination lock working
- Can be links to YouTube/Google Drive (ensure public access)

---

## Check-off Requirements

**Group Check-off Session** (30% of grade if not completed):

Demonstrate to instructor or TA:
1. **Traffic Light Controller**: Working on FPGA
   - Show full cycle
   - Demonstrate car sensor triggering
   - Verify all lights work correctly

2. **Combination Lock**: Working on FPGA
   - Show locked state
   - Enter correct combo successfully
   - Show failed attempt behavior
   - Explain your state machine design

**Check-off Tips**:
- Test thoroughly before check-off
- Have block diagram ready to explain your design
- Be prepared to answer questions about state encoding, timing, edge cases
- If it doesn't work, can still get partial credit by explaining design

**Scheduling**:
- Sign up for 15-minute slot in Week 10
- Both/all group members must attend
- If absent, schedule make-up within 3 days

---

## Common Issues & Solutions

### FSM Design Issues

**❌ Issue**: States unreachable or deadlock
**✅ Solution**: Verify all states have outgoing transitions for all input combinations

**❌ Issue**: Moore vs Mealy confusion
**✅ Solution**: 
- Moore: outputs depend only on state
- Mealy: outputs depend on state AND inputs

**❌ Issue**: Race conditions in combinational logic
**✅ Solution**: Register all outputs, avoid feedback loops

### Verilog Coding Issues

**❌ Issue**: "Inferred latch" warnings
**✅ Solution**: Assign all outputs in all branches, use default case

**❌ Issue**: State gets stuck in unknown state
**✅ Solution**: Add default case in state machine, handle all possible states

**❌ Issue**: Outputs glitch or multiple pulses
**✅ Solution**: Register outputs, ensure clean state transitions

### Timing Issues

**❌ Issue**: Counter overflows or wrong duration
**✅ Solution**: Check counter width (6 bits for counts up to 63)

**❌ Issue**: Transitions happen too fast
**✅ Solution**: Clock divider for 1 Hz clock, or use slow mode for testing

### Hardware Issues

**❌ Issue**: Key bouncing causes multiple triggers
**✅ Solution**: Use debouncer circuit (simple counter-based or synchronizer)

**❌ Issue**: 7-segment display shows garbage
**✅ Solution**: Verify segment encoding, check for uninitialized signals

---

## Resources

### FSM Design
- [FSM Design Tutorial](https://www.asic-world.com/digital/state_machine.html)
- [Moore vs Mealy FSM](https://www.geeksforgeeks.org/difference-between-mealy-machine-and-moore-machine/)
- [FSM Verilog Coding Styles](http://www.sunburst-design.com/papers/CummingsSNUG1998SJ_FSM.pdf)

### Verilog
- [FSM Verilog Examples](https://www.fpga4fun.com/FSM.html)
- [State Machine Coding](http://www.asic-world.com/examples/verilog/fsm.html)

### Tools
- [FSM Designer Online](https://fsm-designer.github.io/)
- [State Machine Diagram Tool](https://app.diagrams.net/)

### Video Tutorials
- Finite State Machine Fundamentals (25 min)
- FSM Verilog Implementation (30 min)
- Traffic Light Controller Design (35 min)
- Debouncing Techniques (15 min)

---

## Tips for Success

### Design Process
1. **Understand spec completely** before starting
2. **Draw state diagram on paper** first
3. **Create state table** to verify all transitions
4. **Code incrementally**: one state at a time
5. **Test early and often**

### State Diagram Tips
- **Name states descriptively**: S0_IDLE better than S0
- **Number states**: Makes encoding easier
- **Check completeness**: Every state handles all inputs
- **Minimize states**: Combine similar states when possible

### Verilog Best Practices
- **Two/three process FSM**: Separates concerns cleanly
  ```verilog
  // Process 1: State register (sequential)
  always @(posedge CLK or negedge RST_N)
  
  // Process 2: Next state logic (combinational)
  always @(*)
  
  // Process 3: Output logic (combinational or registered)
  always @(*) or always @(posedge CLK)
  ```
- **State encoding**: One-hot for speed, binary for area
- **Default cases**: Always include to avoid latches

### Testing Strategy
1. **Desk check**: Trace FSM by hand with test inputs
2. **Testbench simulation**: Verify logic before FPGA
3. **Simple tests first**: Reset, single transitions
4. **Complex scenarios**: Full sequences, edge cases
5. **Hardware verification**: Program FPGA and test interactively

### Time Management
- **Day 1-2**: Complete Problems 1 and 3 (simpler FSMs)
- **Day 3-4**: Complete Problem 2 (traffic light)
- **Day 5-6**: Complete Problem 4 (FPGA implementation)
- **Day 7**: Testing, debugging, documentation
- **Day 8**: Group check-off, final PDF assembly

### Group Work
- **Divide and conquer**: Each member takes 1-2 problems
- **Code review**: Check each other's work
- **Integration**: Test all modules together
- **Practice demo**: Run through check-off scenario

---

## Example FSM Verilog Template

```verilog
module fsm_template (
    input  wire       CLK,
    input  wire       RST_N,
    input  wire       INPUT_SIG,
    output reg        OUTPUT_SIG,
    output reg  [1:0] STATE_OUT
);

    // State encoding
    localparam S0 = 2'b00;
    localparam S1 = 2'b01;
    localparam S2 = 2'b10;
    localparam S3 = 2'b11;
    
    reg [1:0] current_state, next_state;
    
    // Process 1: State register (sequential)
    always @(posedge CLK or negedge RST_N) begin
        if (!RST_N)
            current_state <= S0;
        else
            current_state <= next_state;
    end
    
    // Process 2: Next state logic (combinational)
    always @(*) begin
        case (current_state)
            S0: next_state = INPUT_SIG ? S1 : S0;
            S1: next_state = INPUT_SIG ? S2 : S0;
            S2: next_state = INPUT_SIG ? S3 : S0;
            S3: next_state = S0;
            default: next_state = S0;
        endcase
    end
    
    // Process 3: Output logic (Moore - depends only on state)
    always @(*) begin
        case (current_state)
            S0: OUTPUT_SIG = 1'b0;
            S1: OUTPUT_SIG = 1'b0;
            S2: OUTPUT_SIG = 1'b0;
            S3: OUTPUT_SIG = 1'b1;
            default: OUTPUT_SIG = 1'b0;
        endcase
    end
    
    // Debug output
    assign STATE_OUT = current_state;

endmodule
```

---

## Academic Integrity

This is a **group assignment** (2-3 students per group).

**Collaboration Policy**:
- ✅ Work together with group members
- ✅ Discuss FSM design concepts with other groups
- ✅ Share debugging strategies
- ❌ Share Verilog code between groups
- ❌ Copy state machines from online sources
- ❌ Submit work from previous semesters

**Citing Sources**:
```
// State encoding strategy from:
// www.example.com/fsm-encoding
```

---

**FSMs are powerful! Master them and you can design complex digital systems.** 🔄
