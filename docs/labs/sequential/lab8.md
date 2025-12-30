---
layout: default
title: "Lab 8: Memory Systems"
parent: Sequential Logic Labs
grand_parent: Labs & Exercises
nav_order: 5
---

# Lab 8: 2-Read, 1-Write Memory (Week 13)

## Overview

In this lab, you will design a **register file** - a small, fast memory structure that is fundamental to processor design. Your register file will support **two simultaneous read ports** and **one write port**, allowing two operands to be read while writing a result in a single clock cycle.

## Learning Objectives

After completing this lab, you will be able to:

1. Understand **memory organization** and addressing
2. Implement a **register file** with multiple read/write ports
3. Learn about **synchronous write** and **asynchronous read**
4. Design memory with proper **timing** considerations
5. Understand the role of register files in **processor datapaths**

---

## Background: Register Files

### What is a Register File?

A register file is a small collection of registers that can be read and written by specifying an address. In CPU design, the register file stores the processor's general-purpose registers (like x0-x31 in RISC-V).

### Register File vs RAM

| Feature | Register File | RAM/SRAM |
|---------|---------------|----------|
| Size | Small (8-64 entries) | Large (KB to GB) |
| Speed | Very fast (1 cycle) | Slower (multiple cycles) |
| Ports | Multiple R/W ports | Typically 1-2 ports |
| Implementation | Flip-flops | Memory cells |
| Location | Inside CPU core | On-chip or external |

### Port Configuration

```
             ┌─────────────────────────┐
   rd_addr1 ─┤                         ├─ rd_data1
             │                         │
   rd_addr2 ─┤      Register File      ├─ rd_data2
             │      (8 x 8-bit)        │
   wr_addr  ─┤                         │
             │                         │
   wr_data  ─┤                         │
             │                         │
   wr_en    ─┤                         │
             │                         │
   clk      ─┤                         │
             └─────────────────────────┘
```

---

## Design Specification

### Interface

```systemverilog
module register_file #(
    parameter DATA_WIDTH = 8,      // Width of each register
    parameter ADDR_WIDTH = 3,      // Address bits (8 registers)
    parameter NUM_REGS   = 8       // Number of registers
)(
    input  logic                  clk,        // Clock
    input  logic                  rst_n,      // Active-low reset
    
    // Read Port 1
    input  logic [ADDR_WIDTH-1:0] rd_addr1,   // Read address 1
    output logic [DATA_WIDTH-1:0] rd_data1,   // Read data 1
    
    // Read Port 2
    input  logic [ADDR_WIDTH-1:0] rd_addr2,   // Read address 2
    output logic [DATA_WIDTH-1:0] rd_data2,   // Read data 2
    
    // Write Port
    input  logic [ADDR_WIDTH-1:0] wr_addr,    // Write address
    input  logic [DATA_WIDTH-1:0] wr_data,    // Write data
    input  logic                  wr_en       // Write enable
);
```

### Timing Diagram

```
        ┌───┐   ┌───┐   ┌───┐   ┌───┐   ┌───┐
   clk  ┘   └───┘   └───┘   └───┘   └───┘   └───
        
             │◄──Write Addr/Data Setup──►│
   wr_addr ──┼─────────[addr]────────────┼────
   wr_data ──┼─────────[data]────────────┼────
   wr_en  ───┼───────────────────────────┼────
             │                           │
             ▼                           ▼
           read                        write
           old value                   happens
           (async)                     (sync)
```

---

## SystemVerilog Implementation

### Basic Register File

```systemverilog
module register_file #(
    parameter DATA_WIDTH = 8,
    parameter ADDR_WIDTH = 3,
    parameter NUM_REGS   = 8
)(
    input  logic                  clk,
    input  logic                  rst_n,
    
    // Read ports (asynchronous)
    input  logic [ADDR_WIDTH-1:0] rd_addr1,
    output logic [DATA_WIDTH-1:0] rd_data1,
    input  logic [ADDR_WIDTH-1:0] rd_addr2,
    output logic [DATA_WIDTH-1:0] rd_data2,
    
    // Write port (synchronous)
    input  logic [ADDR_WIDTH-1:0] wr_addr,
    input  logic [DATA_WIDTH-1:0] wr_data,
    input  logic                  wr_en
);

    // Register array
    logic [DATA_WIDTH-1:0] regs [0:NUM_REGS-1];
    
    // Synchronous write
    always_ff @(posedge clk or negedge rst_n) begin
        if (!rst_n) begin
            // Reset all registers to 0
            for (int i = 0; i < NUM_REGS; i++) begin
                regs[i] <= '0;
            end
        end else if (wr_en) begin
            regs[wr_addr] <= wr_data;
        end
    end
    
    // Asynchronous read (combinational)
    assign rd_data1 = regs[rd_addr1];
    assign rd_data2 = regs[rd_addr2];

endmodule
```

### With Write-First Behavior

Sometimes you want to read the new value being written in the same cycle (write-first or bypass):

```systemverilog
module register_file_bypass #(
    parameter DATA_WIDTH = 8,
    parameter ADDR_WIDTH = 3,
    parameter NUM_REGS   = 8
)(
    input  logic                  clk,
    input  logic                  rst_n,
    input  logic [ADDR_WIDTH-1:0] rd_addr1,
    output logic [DATA_WIDTH-1:0] rd_data1,
    input  logic [ADDR_WIDTH-1:0] rd_addr2,
    output logic [DATA_WIDTH-1:0] rd_data2,
    input  logic [ADDR_WIDTH-1:0] wr_addr,
    input  logic [DATA_WIDTH-1:0] wr_data,
    input  logic                  wr_en
);

    logic [DATA_WIDTH-1:0] regs [0:NUM_REGS-1];
    
    // Synchronous write
    always_ff @(posedge clk or negedge rst_n) begin
        if (!rst_n) begin
            for (int i = 0; i < NUM_REGS; i++)
                regs[i] <= '0;
        end else if (wr_en) begin
            regs[wr_addr] <= wr_data;
        end
    end
    
    // Read with bypass: if writing to same address, return new data
    assign rd_data1 = (wr_en && (rd_addr1 == wr_addr)) ? wr_data : regs[rd_addr1];
    assign rd_data2 = (wr_en && (rd_addr2 == wr_addr)) ? wr_data : regs[rd_addr2];

endmodule
```

### With Register 0 Hardwired to Zero (RISC-V style)

```systemverilog
module register_file_zero #(
    parameter DATA_WIDTH = 8,
    parameter ADDR_WIDTH = 3,
    parameter NUM_REGS   = 8
)(
    input  logic                  clk,
    input  logic                  rst_n,
    input  logic [ADDR_WIDTH-1:0] rd_addr1,
    output logic [DATA_WIDTH-1:0] rd_data1,
    input  logic [ADDR_WIDTH-1:0] rd_addr2,
    output logic [DATA_WIDTH-1:0] rd_data2,
    input  logic [ADDR_WIDTH-1:0] wr_addr,
    input  logic [DATA_WIDTH-1:0] wr_data,
    input  logic                  wr_en
);

    logic [DATA_WIDTH-1:0] regs [0:NUM_REGS-1];
    
    // Synchronous write (ignore writes to reg 0)
    always_ff @(posedge clk or negedge rst_n) begin
        if (!rst_n) begin
            for (int i = 0; i < NUM_REGS; i++)
                regs[i] <= '0;
        end else if (wr_en && (wr_addr != '0)) begin
            regs[wr_addr] <= wr_data;
        end
    end
    
    // Read (register 0 always returns 0)
    assign rd_data1 = (rd_addr1 == '0) ? '0 : regs[rd_addr1];
    assign rd_data2 = (rd_addr2 == '0) ? '0 : regs[rd_addr2];

endmodule
```

---

## Hardware Implementation

### Top-Level Wrapper

```systemverilog
module lab8_top (
    input  logic        MAX10_CLK1_50,
    input  logic [9:0]  SW,
    input  logic [1:0]  KEY,
    output logic [9:0]  LEDR,
    output logic [6:0]  HEX0,
    output logic [6:0]  HEX1,
    output logic [6:0]  HEX2,
    output logic [6:0]  HEX3,
    output logic [6:0]  HEX4,
    output logic [6:0]  HEX5
);

    logic clk, rst_n, wr_en;
    logic [2:0] rd_addr1, rd_addr2, wr_addr;
    logic [7:0] rd_data1, rd_data2, wr_data;
    
    assign clk = MAX10_CLK1_50;
    assign rst_n = KEY[0];
    assign wr_en = ~KEY[1];          // Write when KEY[1] pressed
    
    // Address and data from switches
    assign rd_addr1 = SW[2:0];       // Read address 1
    assign rd_addr2 = SW[5:3];       // Read address 2  
    assign wr_addr  = SW[2:0];       // Write address (same as rd1)
    assign wr_data  = SW[9:2];       // Write data from upper switches
    
    register_file u_regfile (
        .clk      (clk),
        .rst_n    (rst_n),
        .rd_addr1 (rd_addr1),
        .rd_data1 (rd_data1),
        .rd_addr2 (rd_addr2),
        .rd_data2 (rd_data2),
        .wr_addr  (wr_addr),
        .wr_data  (wr_data),
        .wr_en    (wr_en)
    );
    
    // Display read data 1 on HEX0-1
    svn_seg_decoder u_h0 (.bcd_in(rd_data1[3:0]), .display_on(1'b1), .seg_out(HEX0));
    svn_seg_decoder u_h1 (.bcd_in(rd_data1[7:4]), .display_on(1'b1), .seg_out(HEX1));
    
    // Display read data 2 on HEX2-3
    svn_seg_decoder u_h2 (.bcd_in(rd_data2[3:0]), .display_on(1'b1), .seg_out(HEX2));
    svn_seg_decoder u_h3 (.bcd_in(rd_data2[7:4]), .display_on(1'b1), .seg_out(HEX3));
    
    // Display addresses on HEX4-5
    svn_seg_decoder u_h4 (.bcd_in({1'b0, rd_addr1}), .display_on(1'b1), .seg_out(HEX4));
    svn_seg_decoder u_h5 (.bcd_in({1'b0, rd_addr2}), .display_on(1'b1), .seg_out(HEX5));
    
    assign LEDR = SW;  // Echo switches

endmodule
```

---

## Verification

### Testing Procedure

1. **Reset**: Press KEY[0] to reset all registers to 0
2. **Write**: Set SW[2:0] to address, SW[9:2] to data, press KEY[1]
3. **Read**: Change SW[2:0] (addr1) and SW[5:3] (addr2) to read
4. **Verify**: HEX0-1 shows data from addr1, HEX2-3 from addr2

### Simulation Testbench

```systemverilog
module register_file_tb;
    logic       clk, rst_n, wr_en;
    logic [2:0] rd_addr1, rd_addr2, wr_addr;
    logic [7:0] rd_data1, rd_data2, wr_data;
    
    register_file uut (.*);
    
    initial clk = 0;
    always #5 clk = ~clk;
    
    initial begin
        // Reset
        rst_n = 0; wr_en = 0;
        rd_addr1 = 0; rd_addr2 = 0;
        wr_addr = 0; wr_data = 0;
        #20 rst_n = 1;
        
        // Write 0xAB to register 3
        wr_addr = 3; wr_data = 8'hAB; wr_en = 1;
        #10 wr_en = 0;
        
        // Write 0xCD to register 5
        wr_addr = 5; wr_data = 8'hCD; wr_en = 1;
        #10 wr_en = 0;
        
        // Read both simultaneously
        rd_addr1 = 3; rd_addr2 = 5;
        #10;
        $display("Reg[3]=%h, Reg[5]=%h", rd_data1, rd_data2);
        
        // Verify
        assert(rd_data1 == 8'hAB) else $error("Reg 3 mismatch!");
        assert(rd_data2 == 8'hCD) else $error("Reg 5 mismatch!");
        
        $display("All tests passed!");
        $finish;
    end
endmodule
```

---

## Lab Manual

📄 [Download Lab 8 Manual (PDF)](lab8.pdf)

---

## Deliverables

- [ ] **SystemVerilog Design**: `register_file.sv` and `lab8_top.sv`
- [ ] **Testbench**: Verify read/write operations
- [ ] **Simulation Waveform**: Show simultaneous reads and writes
- [ ] **Hardware Demo**: Demonstrate register file on DE10-Lite
- [ ] **Individual Report**: Include timing analysis
- [ ] **Submission**: Upload `lab8_top.svf` file

---

## Applications

- **CPU Register Files**: Store operands for ALU operations
- **GPU Shader Registers**: Store vertex/pixel data
- **Cache Tag Storage**: Fast lookup of cache contents
- **Network Buffers**: Packet header storage
