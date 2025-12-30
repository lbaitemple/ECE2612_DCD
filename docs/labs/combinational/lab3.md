---
layout: default
title: "Lab 3: Seven Segment Display"
parent: Combinational Logic Labs
grand_parent: Labs & Exercises
nav_order: 5
---

# Lab 3: Seven Segment Display (Week 6)

## Overview

In this lab, you will design a **seven-segment display decoder** that converts a 4-bit binary (or BCD) input into the appropriate segment patterns to display hexadecimal digits (0-9, A-F) on the DE10-Lite's seven-segment displays.

## Learning Objectives

After completing this lab, you will be able to:

1. Understand **seven-segment display** operation and segment naming conventions
2. Design a **BCD to seven-segment decoder** using SystemVerilog
3. Implement **case statements** for combinational logic
4. Display **hexadecimal values** (0-9, A-F) on hardware

---

## Background: Seven-Segment Displays

### Display Structure

A seven-segment display consists of 7 LEDs (segments a-g) arranged in a figure-8 pattern, plus an optional decimal point:

```
     aaaa
    f    b
    f    b
     gggg
    e    c
    e    c
     dddd
```

### Active Low vs Active High

The DE10-Lite uses **common anode** displays, meaning:
- Segments are **active LOW** (0 = ON, 1 = OFF)
- The segment output must be inverted from intuitive logic

### Segment Mapping for Hexadecimal Digits

| Digit | a | b | c | d | e | f | g | HEX (active low) |
|-------|---|---|---|---|---|---|---|------------------|
| 0     | ON | ON | ON | ON | ON | ON | OFF | 7'b1000000 |
| 1     | OFF | ON | ON | OFF | OFF | OFF | OFF | 7'b1111001 |
| 2     | ON | ON | OFF | ON | ON | OFF | ON | 7'b0100100 |
| 3     | ON | ON | ON | ON | OFF | OFF | ON | 7'b0110000 |
| 4     | OFF | ON | ON | OFF | OFF | ON | ON | 7'b0011001 |
| 5     | ON | OFF | ON | ON | OFF | ON | ON | 7'b0010010 |
| 6     | ON | OFF | ON | ON | ON | ON | ON | 7'b0000010 |
| 7     | ON | ON | ON | OFF | OFF | OFF | OFF | 7'b1111000 |
| 8     | ON | ON | ON | ON | ON | ON | ON | 7'b0000000 |
| 9     | ON | ON | ON | ON | OFF | ON | ON | 7'b0010000 |
| A     | ON | ON | ON | OFF | ON | ON | ON | 7'b0001000 |
| b     | OFF | OFF | ON | ON | ON | ON | ON | 7'b0000011 |
| C     | ON | OFF | OFF | ON | ON | ON | OFF | 7'b1000110 |
| d     | OFF | ON | ON | ON | ON | OFF | ON | 7'b0100001 |
| E     | ON | OFF | OFF | ON | ON | ON | ON | 7'b0000110 |
| F     | ON | OFF | OFF | OFF | ON | ON | ON | 7'b0001110 |

---

## Design Specification

### Block Diagram

```
            ┌───────────────────────────────────┐
    bcd[3:0]│                                   │  seg[6:0]
   ─────────┤    Seven Segment Decoder          ├──────────
   (4 bits) │                                   │ (7 bits)
            │       display_on                  │
            │          ↓                        │
            └───────────────────────────────────┘
```

### Module Interface

```systemverilog
module svn_seg_decoder (
    input  logic [3:0] bcd_in,      // 4-bit input (0-15)
    input  logic       display_on,  // Enable signal (1 = on)
    output logic [6:0] seg_out      // 7-segment output {g,f,e,d,c,b,a}
);
```

---

## SystemVerilog Implementation

### Using Case Statement

```systemverilog
module svn_seg_decoder (
    input  logic [3:0] bcd_in,
    input  logic       display_on,
    output logic [6:0] seg_out
);

    logic [6:0] segments;
    
    // Decode BCD to seven-segment (active LOW)
    always_comb begin
        case (bcd_in)
            4'h0: segments = 7'b1000000;  // 0
            4'h1: segments = 7'b1111001;  // 1
            4'h2: segments = 7'b0100100;  // 2
            4'h3: segments = 7'b0110000;  // 3
            4'h4: segments = 7'b0011001;  // 4
            4'h5: segments = 7'b0010010;  // 5
            4'h6: segments = 7'b0000010;  // 6
            4'h7: segments = 7'b1111000;  // 7
            4'h8: segments = 7'b0000000;  // 8
            4'h9: segments = 7'b0010000;  // 9
            4'hA: segments = 7'b0001000;  // A
            4'hB: segments = 7'b0000011;  // b
            4'hC: segments = 7'b1000110;  // C
            4'hD: segments = 7'b0100001;  // d
            4'hE: segments = 7'b0000110;  // E
            4'hF: segments = 7'b0001110;  // F
            default: segments = 7'b1111111; // All OFF
        endcase
    end
    
    // Apply display enable (all segments off when disabled)
    assign seg_out = display_on ? segments : 7'b1111111;

endmodule
```

### Alternative: Using Conditional Operator

```systemverilog
module svn_seg_decoder (
    input  logic [3:0] bcd_in,
    input  logic       display_on,
    output logic [6:0] seg_out
);

    assign seg_out = ~display_on ? 7'b1111111 :
                     (bcd_in == 4'h0) ? 7'b1000000 :
                     (bcd_in == 4'h1) ? 7'b1111001 :
                     (bcd_in == 4'h2) ? 7'b0100100 :
                     (bcd_in == 4'h3) ? 7'b0110000 :
                     (bcd_in == 4'h4) ? 7'b0011001 :
                     (bcd_in == 4'h5) ? 7'b0010010 :
                     (bcd_in == 4'h6) ? 7'b0000010 :
                     (bcd_in == 4'h7) ? 7'b1111000 :
                     (bcd_in == 4'h8) ? 7'b0000000 :
                     (bcd_in == 4'h9) ? 7'b0010000 :
                     (bcd_in == 4'hA) ? 7'b0001000 :
                     (bcd_in == 4'hB) ? 7'b0000011 :
                     (bcd_in == 4'hC) ? 7'b1000110 :
                     (bcd_in == 4'hD) ? 7'b0100001 :
                     (bcd_in == 4'hE) ? 7'b0000110 :
                     7'b0001110; // F
endmodule
```

---

## Hardware Implementation

### Top-Level Wrapper

```systemverilog
module lab3_top (
    input  logic [9:0] SW,      // Slide switches
    output logic [6:0] HEX0,    // 7-segment display 0
    output logic [6:0] HEX1,    // 7-segment display 1
    output logic [6:0] HEX2,    // 7-segment display 2
    output logic [6:0] HEX3,    // 7-segment display 3
    output logic [6:0] HEX4,    // 7-segment display 4
    output logic [6:0] HEX5     // 7-segment display 5
);

    // Display SW[3:0] on HEX0
    svn_seg_decoder u_hex0 (
        .bcd_in     (SW[3:0]),
        .display_on (1'b1),
        .seg_out    (HEX0)
    );
    
    // Display SW[7:4] on HEX1
    svn_seg_decoder u_hex1 (
        .bcd_in     (SW[7:4]),
        .display_on (1'b1),
        .seg_out    (HEX1)
    );
    
    // Turn off unused displays
    assign HEX2 = 7'b1111111;
    assign HEX3 = 7'b1111111;
    assign HEX4 = 7'b1111111;
    assign HEX5 = 7'b1111111;

endmodule
```

### DE10-Lite Seven-Segment Pin Assignments

| Signal | FPGA Pins (HEX0) | FPGA Pins (HEX1) |
|--------|------------------|------------------|
| seg[0] (a) | PIN_C14 | PIN_C17 |
| seg[1] (b) | PIN_E15 | PIN_D17 |
| seg[2] (c) | PIN_C15 | PIN_E16 |
| seg[3] (d) | PIN_C16 | PIN_C18 |
| seg[4] (e) | PIN_E16 | PIN_D18 |
| seg[5] (f) | PIN_D17 | PIN_E18 |
| seg[6] (g) | PIN_C17 | PIN_B16 |

---

## Verification

### Testing Procedure

1. Set SW[3:0] to each hexadecimal value (0-F)
2. Verify HEX0 displays the correct digit
3. Test display_on functionality (if implemented)
4. Check all 16 combinations

### Simulation Testbench

```systemverilog
module svn_seg_decoder_tb;
    logic [3:0] bcd_in;
    logic       display_on;
    logic [6:0] seg_out;
    
    svn_seg_decoder uut (.*);
    
    initial begin
        display_on = 1'b1;
        
        $display("Input | Seg Output | Expected Digit");
        $display("------|------------|----------------");
        
        for (int i = 0; i < 16; i++) begin
            bcd_in = i;
            #10;
            $display("  %h  |  %b  | %h", bcd_in, seg_out, bcd_in);
        end
        
        // Test display off
        display_on = 1'b0;
        bcd_in = 4'h5;
        #10;
        $display("\nDisplay OFF: seg_out = %b (should be 1111111)", seg_out);
        
        $finish;
    end
endmodule
```

---

## Lab Manual

📄 [Download Lab 3 Manual (PDF)](lab3_v15.pdf)

---

## Deliverables

- [ ] **SystemVerilog Design**: `svn_seg_decoder.sv` and `lab3_top.sv`
- [ ] **Testbench**: `svn_seg_decoder_tb.sv`
- [ ] **Simulation Waveform**: Screenshot showing all 16 test cases
- [ ] **Hardware Demo**: Demonstrate all hex digits on DE10-Lite
- [ ] **Individual Report**: Include design, truth table, and test results
- [ ] **Submission**: Upload `lab3_top.svf` file

---

## Common Mistakes to Avoid

1. **Forgetting active-low logic**: Segments are ON when output is 0
2. **Wrong segment order**: Ensure `seg_out = {g,f,e,d,c,b,a}`
3. **Missing default case**: Always include a default in case statements
4. **Segment polarity errors**: Double-check each segment pattern
