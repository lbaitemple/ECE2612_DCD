---
layout: default
title: "Lab 6: Multiple Digit Display"
parent: Sequential Logic Labs
grand_parent: Labs & Exercises
nav_order: 3
---

# Lab 6: Multiple Digit Display (Week 10)

## Overview

In this lab, you will design a **multiple digit display driver** that can display multi-digit numbers on the DE10-Lite's six seven-segment displays. You will learn about **time-division multiplexing** and how to create a flicker-free display using counters.

## Learning Objectives

After completing this lab, you will be able to:

1. Understand **display multiplexing** concepts
2. Implement a **refresh counter** for digit selection
3. Design a **digit selector** to cycle through displays
4. Create a smooth display without visible **flicker**
5. Display multi-digit **BCD or hexadecimal** values

---

## Background: Display Multiplexing

### Why Multiplexing?

The DE10-Lite has 6 seven-segment displays, each with 7 segments. Driving all segments simultaneously would require:
- 6 displays × 7 segments = **42 I/O pins**

With multiplexing, we:
- Share segment lines across all displays
- Rapidly switch between displays
- Human eye sees all digits lit due to **persistence of vision**

### Multiplexing Principle

```
Time Slice 1: Display digit 0, others OFF
Time Slice 2: Display digit 1, others OFF
Time Slice 3: Display digit 2, others OFF
...
(Repeat fast enough that all appear lit)
```

### Refresh Rate Requirements

- **Minimum**: ~100 Hz to avoid visible flicker
- **Typical**: 1 kHz for comfortable viewing
- With 6 displays: Need 6 kHz total switching rate (1 kHz × 6)

---

## Design Architecture

### Block Diagram

```
                    ┌────────────────────────────┐
    50 MHz Clock ───┤    Refresh Counter         │
                    │    (generates ~1 kHz)      │
                    └───────────┬────────────────┘
                                │
                    ┌───────────▼────────────────┐
                    │    Digit Selector          │
                    │    (2-bit counter: 0-3)    │
                    └───────────┬────────────────┘
                                │
         ┌──────────────────────┼──────────────────────┐
         │                      │                      │
    ┌────▼────┐           ┌────▼────┐           ┌────▼────┐
    │  MUX    │           │  MUX    │           │  MUX    │
    │ (data)  │           │(enable) │           │  Decoder│
    └────┬────┘           └────┬────┘           └────┬────┘
         │                      │                      │
    ┌────▼────┐                 │               ┌────▼────┐
    │7-Seg Dec│                 │               │ Enable  │
    └────┬────┘                 │               │ Signals │
         │                      │               └────┬────┘
         └──────────┬───────────┘                    │
                    │                                │
              ┌─────▼─────┐                   ┌─────▼─────┐
              │  HEX[6:0] │                   │ HEX_EN[5:0]│
              │ (shared)  │                   │ (one-hot) │
              └───────────┘                   └───────────┘
```

---

## SystemVerilog Implementation

### Refresh Counter (Clock Divider)

```systemverilog
module refresh_counter #(
    parameter REFRESH_RATE = 1000,        // 1 kHz refresh
    parameter CLK_FREQ     = 50_000_000   // 50 MHz input clock
)(
    input  logic clk,
    input  logic rst_n,
    output logic tick          // 1 kHz tick output
);

    localparam COUNT_MAX = CLK_FREQ / REFRESH_RATE - 1;
    localparam WIDTH = $clog2(COUNT_MAX + 1);
    
    logic [WIDTH-1:0] counter;
    
    always_ff @(posedge clk or negedge rst_n) begin
        if (!rst_n) begin
            counter <= '0;
            tick <= 1'b0;
        end else if (counter == COUNT_MAX) begin
            counter <= '0;
            tick <= 1'b1;
        end else begin
            counter <= counter + 1'b1;
            tick <= 1'b0;
        end
    end

endmodule
```

### Digit Selector (Ring Counter)

```systemverilog
module digit_selector #(
    parameter NUM_DIGITS = 4
)(
    input  logic clk,
    input  logic rst_n,
    input  logic tick,                    // From refresh counter
    output logic [$clog2(NUM_DIGITS)-1:0] digit_sel  // Which digit
);

    always_ff @(posedge clk or negedge rst_n) begin
        if (!rst_n)
            digit_sel <= '0;
        else if (tick) begin
            if (digit_sel == NUM_DIGITS - 1)
                digit_sel <= '0;
            else
                digit_sel <= digit_sel + 1'b1;
        end
    end

endmodule
```

### Complete Display Driver

```systemverilog
module display_driver (
    input  logic        clk,
    input  logic        rst_n,
    input  logic [15:0] value,     // 4-digit hex value
    output logic [6:0]  HEX0,
    output logic [6:0]  HEX1,
    output logic [6:0]  HEX2,
    output logic [6:0]  HEX3
);

    // Extract individual digits
    logic [3:0] digit0, digit1, digit2, digit3;
    
    assign digit0 = value[3:0];     // Ones
    assign digit1 = value[7:4];     // Sixteens  
    assign digit2 = value[11:8];    // 256s
    assign digit3 = value[15:12];   // 4096s
    
    // Seven-segment decoders for each digit
    svn_seg_decoder u_d0 (.bcd_in(digit0), .display_on(1'b1), .seg_out(HEX0));
    svn_seg_decoder u_d1 (.bcd_in(digit1), .display_on(1'b1), .seg_out(HEX1));
    svn_seg_decoder u_d2 (.bcd_in(digit2), .display_on(1'b1), .seg_out(HEX2));
    svn_seg_decoder u_d3 (.bcd_in(digit3), .display_on(1'b1), .seg_out(HEX3));

endmodule
```

### Alternative: Multiplexed Version (Shared Decoder)

```systemverilog
module display_driver_mux (
    input  logic        clk,
    input  logic        rst_n,
    input  logic [15:0] value,
    output logic [6:0]  seg_out,     // Shared segment output
    output logic [3:0]  digit_en     // One-hot digit enable
);

    logic       tick;
    logic [1:0] digit_sel;
    logic [3:0] current_digit;
    
    // Generate refresh tick
    refresh_counter #(.REFRESH_RATE(1000)) u_refresh (
        .clk(clk), .rst_n(rst_n), .tick(tick)
    );
    
    // Select which digit
    digit_selector #(.NUM_DIGITS(4)) u_select (
        .clk(clk), .rst_n(rst_n), .tick(tick), .digit_sel(digit_sel)
    );
    
    // MUX to select current digit value
    always_comb begin
        case (digit_sel)
            2'd0: current_digit = value[3:0];
            2'd1: current_digit = value[7:4];
            2'd2: current_digit = value[11:8];
            2'd3: current_digit = value[15:12];
            default: current_digit = 4'h0;
        endcase
    end
    
    // Decode current digit
    svn_seg_decoder u_decoder (
        .bcd_in(current_digit),
        .display_on(1'b1),
        .seg_out(seg_out)
    );
    
    // Generate digit enable (one-hot)
    always_comb begin
        digit_en = 4'b0000;
        digit_en[digit_sel] = 1'b1;
    end

endmodule
```

---

## Hardware Implementation

### Top-Level Wrapper

```systemverilog
module lab6_top (
    input  logic        MAX10_CLK1_50,
    input  logic [9:0]  SW,
    input  logic [1:0]  KEY,
    output logic [6:0]  HEX0,
    output logic [6:0]  HEX1,
    output logic [6:0]  HEX2,
    output logic [6:0]  HEX3,
    output logic [6:0]  HEX4,
    output logic [6:0]  HEX5
);

    logic clk, rst_n;
    
    assign clk   = MAX10_CLK1_50;
    assign rst_n = KEY[0];
    
    // Display the switch values on 4 digits
    display_driver u_display (
        .clk   (clk),
        .rst_n (rst_n),
        .value ({6'b0, SW}),    // Zero-extend switches to 16 bits
        .HEX0  (HEX0),
        .HEX1  (HEX1),
        .HEX2  (HEX2),
        .HEX3  (HEX3)
    );
    
    // Disable unused displays
    assign HEX4 = 7'b1111111;
    assign HEX5 = 7'b1111111;

endmodule
```

---

## Verification

### Testing Procedure

1. Load design onto DE10-Lite
2. Set switches to different patterns
3. Verify displays show correct hex values
4. Check for flicker (should be imperceptible)
5. Test edge cases: 0x0000, 0xFFFF

### Simulation Testbench

```systemverilog
module display_driver_tb;
    logic        clk, rst_n;
    logic [15:0] value;
    logic [6:0]  HEX0, HEX1, HEX2, HEX3;
    
    display_driver uut (.*);
    
    // 50 MHz clock
    initial clk = 0;
    always #10 clk = ~clk;
    
    initial begin
        rst_n = 0;
        value = 16'h0000;
        #100;
        
        rst_n = 1;
        
        // Test different values
        value = 16'h1234; #1000;
        value = 16'hABCD; #1000;
        value = 16'hFFFF; #1000;
        
        $finish;
    end
endmodule
```

---

## Lab Manual

📄 [Download Lab 6 Manual (PDF)](lab6_v12.pdf)

---

## Deliverables

- [ ] **SystemVerilog Design**: `refresh_counter.sv`, `display_driver.sv`, `lab6_top.sv`
- [ ] **Testbench**: Verify digit switching and values
- [ ] **Simulation Waveform**: Show multiplexing operation
- [ ] **Hardware Demo**: Display multi-digit values without flicker
- [ ] **Individual Report**: Include timing analysis
- [ ] **Submission**: Upload `lab6_top.svf` file

---

## Common Issues

1. **Flickering**: Refresh rate too slow (< 100 Hz)
2. **Ghosting**: Adjacent digits partially visible (timing issue)
3. **Dim display**: Too fast switching, insufficient duty cycle
4. **Wrong digits**: Check MUX select logic and bit ordering
