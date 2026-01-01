---
layout: default
title: Module 8 - Counters & Registers
parent: Course Modules
nav_order: 9
permalink: /docs/modules/module-08/
---

# Module 8: Counters, Shift Registers, and Timers
**Week 10**

---

## Overview

Design specialized sequential circuits: counters, shift registers, and timing circuits that are fundamental building blocks in digital systems.

**Duration**: 1 week  
**Prerequisites**: Modules 6-7 completed

---

## Learning Objectives

By the end of this module, you will be able to:
1. Design binary and BCD counters
2. Implement up/down counters with parallel load
3. Create shift registers (SISO, SIPO, PISO, PIPO)
4. Design timer and frequency divider circuits
5. Cascade counters for larger bit widths
6. Implement ring and Johnson counters

---

## Topics

### 1. Binary Counters
- Simple up counter
- Up/down counter
- Modulo-N counters
- Counter with parallel load
- Synchronous vs asynchronous counters
- Terminal count detection

### 2. BCD Counters
- Decade counter (0-9)
- Cascading for multi-digit displays
- BCD to 7-segment decoder interface
- Digital clock applications

### 3. Shift Registers

#### Types
- **SISO**: Serial In, Serial Out
- **SIPO**: Serial In, Parallel Out
- **PISO**: Parallel In, Serial Out
- **PIPO**: Parallel In, Parallel Out

#### Applications
- Data conversion (serial ↔ parallel)
- Data delay/pipeline
- Pattern generation
- Communication interfaces

### 4. Special Counters
- **Ring Counter**: One-hot rotating pattern
- **Johnson Counter**: Modified ring counter
- **LFSR**: Linear Feedback Shift Register (pseudo-random)

### 5. Timer Circuits
- Programmable timer
- Watchdog timer
- PWM generator
- Frequency divider

### 6. Practical Applications
- Digital clocks
- Event counters
- Frequency measurement
- Data transmission

---

## Assignment 8

**Due**: End of Week 10  
**Points**: 100

### Requirements

**Part 1**: Counter Design (30 points)
Design 8-bit up/down counter with:
- Count up/down control
- Synchronous parallel load
- Synchronous clear
- Terminal count output
- Implement in Verilog, test all features

**Part 2**: Shift Register (25 points)
Design 8-bit universal shift register:
- Modes: Hold, Shift Left, Shift Right, Parallel Load
- Serial input/output
- Parallel input/output
- 2-bit mode select
- Comprehensive testbench

**Part 3**: Digital Clock (30 points)
Design clock displaying HH:MM:SS:
- BCD counters for seconds, minutes, hours
- 60-count and 24-count rollover
- 1Hz clock divider from 50MHz
- Display on 7-segment displays
- Set time functionality

**Part 4**: FPGA Implementation (15 points)
- Implement digital clock on DE10-Lite
- Use all six 7-segment displays
- Buttons for time setting
- Demo video

[Download Assignment Template](../../assignments/assignment-08.md)

---

## Resources

### Lecture Materials
- [Module 8 Slides](../../resources/lectures/module08_slides.pdf)

### Interactive Tools
- [Digital Circuit Simulator](https://www.falstad.com/circuit/)
- [Counter Visualization Tool](https://circuitverse.org/)
- [Timing Diagram Generator](https://wavedrom.com/)

### Video Tutorials
- Binary Counter Design (20 min)
- Shift Register Types and Uses (25 min)
- Digital Clock Design Walkthrough (35 min)

---

## Lab Exercise

### Lab 8: Counters and Shift Registers
**Objectives**:
- Implement various counter types
- Create universal shift register
- Build practical timer circuit
- Test on FPGA hardware

**Deliverables**:
- Modulo-10 BCD counter
- 8-bit bidirectional shift register
- Programmable frequency divider
- Demonstration and report

[View Full Lab Instructions](../../labs/sequential/lab08/)

---

## Design Examples

### 4-Bit Binary Up Counter
```verilog
module counter_4bit (
    input  wire clk, reset, enable,
    output reg  [3:0] count,
    output wire tc  // Terminal count
);
    always @(posedge clk or posedge reset) begin
        if (reset)
            count <= 4'b0000;
        else if (enable)
            count <= count + 1;
    end
    
    assign tc = (count == 4'b1111) && enable;
endmodule
```

### 8-Bit Up/Down Counter with Load
```verilog
module counter_updown_8bit (
    input  wire       clk, reset, enable, load, up_down,
    input  wire [7:0] data_in,
    output reg  [7:0] count
);
    always @(posedge clk or posedge reset) begin
        if (reset)
            count <= 8'b0;
        else if (load)
            count <= data_in;
        else if (enable) begin
            if (up_down)
                count <= count + 1;  // Count up
            else
                count <= count - 1;  // Count down
        end
    end
endmodule
```

### BCD Counter (Modulo-10)
```verilog
module bcd_counter (
    input  wire clk, reset, enable,
    output reg  [3:0] bcd,
    output reg  carry_out
);
    always @(posedge clk or posedge reset) begin
        if (reset) begin
            bcd <= 4'b0000;
            carry_out <= 1'b0;
        end else if (enable) begin
            if (bcd == 4'b1001) begin
                bcd <= 4'b0000;
                carry_out <= 1'b1;
            end else begin
                bcd <= bcd + 1;
                carry_out <= 1'b0;
            end
        end
    end
endmodule
```

### Universal Shift Register
```verilog
module shift_register_universal (
    input  wire       clk, reset,
    input  wire [1:0] mode,  // 00:hold, 01:left, 10:right, 11:load
    input  wire       serial_in_left, serial_in_right,
    input  wire [7:0] parallel_in,
    output reg  [7:0] q,
    output wire       serial_out_left, serial_out_right
);
    always @(posedge clk or posedge reset) begin
        if (reset)
            q <= 8'b0;
        else
            case (mode)
                2'b00: q <= q;                              // Hold
                2'b01: q <= {q[6:0], serial_in_left};      // Shift left
                2'b10: q <= {serial_in_right, q[7:1]};     // Shift right
                2'b11: q <= parallel_in;                    // Parallel load
            endcase
    end
    
    assign serial_out_left  = q[7];
    assign serial_out_right = q[0];
endmodule
```

### Clock Divider (50MHz to 1Hz)
```verilog
module clock_divider_1hz (
    input  wire clk_50mhz,
    input  wire reset,
    output reg  clk_1hz
);
    localparam MAX_COUNT = 25_000_000;  // 50MHz / 2 = 25M for 1Hz
    reg [24:0] counter;
    
    always @(posedge clk_50mhz or posedge reset) begin
        if (reset) begin
            counter <= 0;
            clk_1hz <= 0;
        end else begin
            if (counter == MAX_COUNT - 1) begin
                counter <= 0;
                clk_1hz <= ~clk_1hz;  // Toggle
            end else begin
                counter <= counter + 1;
            end
        end
    end
endmodule
```

---

## Common Mistakes

❌ **Asynchronous counter cascading**
- Ripple counters have cumulative delay
- Use synchronous counters for reliability

❌ **Incorrect modulo logic**
- Counter resets at wrong count
- Off-by-one errors in terminal count

❌ **Missing load/clear priority**
- Specify priority: reset > load > count
- Document in comments

❌ **Shift direction confusion**
- Clearly label left/right, MSB/LSB
- Test both directions

✅ **Good Practice**
- Use synchronous design
- Include enable inputs
- Provide terminal count outputs
- Document count sequences
- Test rollover conditions

---

## Counter Applications

### Digital Clock Architecture
```
50MHz System Clock
    ↓
Clock Divider (÷50M) → 1Hz
    ↓
Seconds Counter (÷60) → 1/60 Hz
    ↓
Minutes Counter (÷60) → 1/3600 Hz
    ↓
Hours Counter (÷24) → 1/86400 Hz
```

### Frequency Measurement
Use counter to count input pulses over known time period:
```
Frequency = Count / Time_Period
```

---

## Advanced Topics

### Ring Counter
```verilog
module ring_counter_8bit (
    input  wire clk, reset,
    output reg  [7:0] q
);
    always @(posedge clk or posedge reset) begin
        if (reset)
            q <= 8'b00000001;
        else
            q <= {q[6:0], q[7]};  // Rotate
    end
endmodule
```

### Johnson Counter
```verilog
module johnson_counter_4bit (
    input  wire clk, reset,
    output reg  [3:0] q
);
    always @(posedge clk or posedge reset) begin
        if (reset)
            q <= 4'b0000;
        else
            q <= {q[2:0], ~q[3]};  // Rotate with inversion
    end
endmodule
```

---

## Next Steps

After completing Module 8, proceed to:
- **[Module 9: Finite State Machines](module-09/)**
- Advanced FSM design
- Controller architectures

---

[← Previous Module](module-07/) | [Back to All Modules](../) | [Next Module →](module-09/)
