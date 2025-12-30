---
layout: default
title: Assignment 11 - Advanced Topics
parent: Assignments
nav_order: 12
---

# Assignment 11: Advanced Digital Design Topics
**Module 11 - Advanced Concepts**

---

## Assignment Information

- **Due Date**: End of Week 12
- **Points**: 100
- **Submission**: Canvas (PDF + Verilog files)
- **Type**: Group (2-3 students)
- **Check-off Required**: Yes (30% penalty if not completed)
- **Estimated Time**: 15-18 hours

---

## Learning Objectives

- Understand clock domain crossing (CDC)
- Design pipelined circuits
- Implement timing optimization techniques
- Create complex hierarchical systems
- Apply advanced synthesis constraints

---

## Problems

### Problem 1: Clock Domain Crossing (25 points)

**Objective**: Design safe CDC circuits for asynchronous data transfer.

**Part A: Single-Bit CDC (10 points)**

Implement 2-FF synchronizer with analysis:
1. Verilog implementation
2. MTBF calculation
3. Metastability waveform diagram
4. Explain why 2 FFs reduce risk

**Part B: Multi-Bit CDC (10 points)**

Design Gray code counter for multi-bit CDC:
- 4-bit counter in clock domain A (fast)
- Transfer count to clock domain B (slow)
- Use Gray code encoding
- Synchronize with 2-FF chain

Explain why Gray code is necessary.

**Part C: Handshake Protocol (5 points)**

Implement REQ/ACK handshake for data transfer:
```verilog
module cdc_handshake (
    // Clock domain A
    input  wire       CLKA,
    input  wire [7:0] DATA_A,
    input  wire       VALID_A,
    output wire       READY_A,
    
    // Clock domain B
    input  wire       CLKB,
    output reg  [7:0] DATA_B,
    output reg        VALID_B
);
    // Your implementation
endmodule
```

---

### Problem 2: Pipelined Multiplier (30 points)

**Objective**: Design 8×8 pipelined multiplier.

**Part A: Unpipelined Baseline (10 points)**
1. Design 8×8 unsigned multiplier
2. Analyze combinational delay
3. Calculate maximum frequency

**Part B: 2-Stage Pipeline (12 points)**

Add pipeline registers:
- Stage 1: Partial products generation
- Stage 2: Addition and final result

Implementation:
```verilog
module pipelined_mult_8x8 (
    input  wire        CLK,
    input  wire [7:0]  A, B,
    output reg  [15:0] PRODUCT
);
    // Pipeline registers
    reg [7:0] a_reg, b_reg;
    reg [15:0] partial_sum;
    
    // Stage 1
    always @(posedge CLK) begin
        a_reg <= A;
        b_reg <= B;
        partial_sum <= /* partial product calculation */;
    end
    
    // Stage 2
    always @(posedge CLK) begin
        PRODUCT <= /* final result */;
    end
endmodule
```

**Part C: Performance Analysis (8 points)**
1. Compare timing: unpipelined vs pipelined
2. Calculate throughput improvement
3. Latency vs throughput trade-off
4. Draw pipeline diagram

---

### Problem 3: Timing Constraints and Optimization (25 points)

**Objective**: Apply timing constraints and optimize design.

**Part A: Static Timing Analysis (10 points)**

For given circuit with:
- Flip-flop Tcq = 1ns
- Logic delays: 5ns, 7ns, 4ns (three paths)
- Setup time = 0.5ns

Calculate:
1. Critical path delay
2. Maximum clock frequency
3. Slack for each path
4. Clock period needed for 200 MHz

**Part B: SDC Constraints (8 points)**

Write Synopsys Design Constraints:
```tcl
# Create clock constraint
create_clock -name CLK -period 10.0 [get_ports CLK]

# Input/output delays
set_input_delay -clock CLK 2.0 [get_ports DATA_IN]
set_output_delay -clock CLK 1.5 [get_ports DATA_OUT]

# False paths
set_false_path -from [get_ports RST_N] -to [all_registers]

# Multicycle paths
set_multicycle_path 2 -from [get_cells SLOW_*] -to [get_cells FAST_*]
```

Explain each constraint type.

**Part C: Retiming Optimization (7 points)**
1. Explain retiming technique
2. Show example of moving registers to balance logic
3. Implement in Verilog before/after retiming

---

### Problem 4: Complete System Integration (20 points)

**Objective**: Build UART transmitter/receiver system.

**Specification**:
- Baud rate: 9600 bps
- Data: 8 bits, 1 stop bit, no parity
- TX: Transmit parallel byte as serial
- RX: Receive serial data to parallel byte

**Part A: UART Transmitter (8 points)**
```verilog
module uart_tx (
    input  wire       CLK,        // 50 MHz
    input  wire       RST_N,
    input  wire [7:0] DATA,
    input  wire       START,
    output reg        TX,
    output reg        BUSY
);
    // Baud rate generator (50MHz / 9600)
    // State machine: IDLE, START, DATA[0-7], STOP
endmodule
```

**Part B: UART Receiver (8 points)**
```verilog
module uart_rx (
    input  wire       CLK,
    input  wire       RST_N,
    input  wire       RX,
    output reg  [7:0] DATA,
    output reg        VALID
);
    // Baud rate generator
    // State machine: IDLE, START, DATA[0-7], STOP
    // Sample at middle of bit period
endmodule
```

**Part C: System Integration (4 points)**
- Loopback test (TX → RX)
- FPGA demonstration
- PC communication (bonus)

---

## Grading Rubric

### Problem 1 (25 points)
- 2-FF synchronizer: 10 points
- Gray code CDC: 10 points
- Handshake protocol: 5 points

### Problem 2 (30 points)
- Unpipelined design: 10 points
- Pipelined design: 12 points
- Analysis: 8 points

### Problem 3 (25 points)
- Timing analysis: 10 points
- SDC constraints: 8 points
- Retiming: 7 points

### Problem 4 (20 points)
- UART TX: 8 points
- UART RX: 8 points
- Integration: 4 points

---

## Check-off Requirements

Demonstrate:
1. **CDC Handshake**: Data transfer between clock domains
2. **Pipelined Multiplier**: Verify throughput
3. **UART System**: Loopback or PC communication

---

## Resources
- CDC Design Techniques
- Pipeline Architecture Guide
- Timing Optimization Tutorial
- UART Protocol Specification

---

**This is your capstone assignment—show what you've learned!** 🎓
