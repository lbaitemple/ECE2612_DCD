---
layout: default
title: Module 10 - Memory Systems
parent: Course Modules
nav_order: 11
permalink: /docs/modules/module-10/
---

# Module 10: Memory Systems
**Week 13**

---

## Overview

Design and implement memory structures including RAM, ROM, FIFO buffers, and memory controllers.

**Duration**: 1 week  
**Prerequisites**: Modules 6-9 completed

---

## Learning Objectives

By the end of this module, you will be able to:
1. Understand memory organization and addressing
2. Design RAM and ROM structures in Verilog
3. Implement memory controllers
4. Work with dual-port and multi-port memories
5. Design FIFO (First-In-First-Out) buffers
6. Optimize memory access patterns for performance

---

## Topics

### 1. Memory Fundamentals

#### Memory Organization
- **Address Lines (A)**: Select memory location (n bits → 2^n locations)
- **Data Lines (D)**: Read/write data (m bits = word size)
- **Control Lines**: Read Enable (RE), Write Enable (WE), Chip Select (CS)
- **Capacity**: Total storage = 2^n × m bits

#### Memory Parameters
- **Access Time**: Time to read/write data
- **Cycle Time**: Minimum time between operations
- **Bandwidth**: Data transfer rate
- **Latency**: Delay to first data

### 2. ROM (Read-Only Memory)

#### Types
- **Mask ROM**: Factory programmed
- **PROM**: One-time programmable
- **EPROM/EEPROM**: Erasable and reprogrammable
- **Flash**: Block-erasable non-volatile memory

#### Applications
- Lookup tables (LUTs)
- Character generators
- Waveform storage
- Firmware/bootloaders

### 3. RAM (Random Access Memory)

#### SRAM (Static RAM)
- Fast, expensive
- Uses flip-flops
- Doesn't need refresh
- Common in caches, registers

#### DRAM (Dynamic RAM)
- Slower, cheaper, dense
- Uses capacitors
- Requires refresh
- Common in main memory

#### Dual-Port RAM
- Two independent access ports
- Simultaneous read/write
- Used in communication buffers

### 4. FIFO Buffers
- First-In-First-Out data structure
- Write and read pointers
- Full/Empty flags
- Synchronous and asynchronous types
- Applications: Data buffering, rate matching

### 5. Memory Controllers
- Address generation
- Control signal timing
- Read/write arbitration
- Burst transfers
- Memory refresh (for DRAM)

### 6. Memory in FPGAs

#### Block RAM (BRAM)
- Dedicated memory blocks
- Configurable width and depth
- True dual-port capability
- Fast access

#### Distributed RAM
- Uses logic elements (LUTs)
- Smaller, more flexible
- Faster for small memories

---

## Assignment 10

**Due**: End of Week 13  
**Points**: 100

### Requirements

**Part 1**: ROM Design (20 points)
Design ROM for sine wave lookup table:
- 256 samples, 8-bit resolution
- Initialize from file or case statement
- Create testbench to verify all addresses
- Generate waveform output

**Part 2**: Dual-Port RAM (30 points)
Design 256×16 dual-port RAM:
- Independent read/write ports
- Synchronous operation
- Write-through or read-first mode
- Handle simultaneous access
- Comprehensive testbench

**Part 3**: FIFO Buffer (35 points)
Design synchronous FIFO:
- Depth: 16 words, Width: 8 bits
- Read/write enables
- Full, empty, almost-full, almost-empty flags
- Counter for number of items
- Test overflow/underflow handling

**Part 4**: Memory-Based Design (15 points)
- Implement circular buffer for audio delay
- Or character display buffer
- Test on DE10-Lite
- Demo video

[Download Assignment Template](../assignments/assignment-10/)

---

## Resources

### Lecture Materials
- [Module 10 Slides](../../resources/lectures/module10_slides.pdf)

### Intel FPGA Documentation
- [Quartus Memory (RAM/ROM) User Guide](https://www.intel.com/content/www/us/en/docs/programmable/683082/)
- [Embedded Memory User Guide](https://www.intel.com/content/www/us/en/docs/programmable/683423/)

### Video Tutorials
- RAM and ROM Fundamentals (25 min)
- Dual-Port Memory Design (20 min)
- FIFO Buffer Implementation (30 min)

---

## Lab Exercise

### Lab 10: Memory Systems
**Objectives**:
- Implement various memory types
- Design FIFO buffer
- Create memory controller
- Test with real data

**Tasks**:
- ROM-based waveform generator
- RAM-based circular buffer
- Async FIFO for clock domain crossing

[View Full Lab Instructions](../../labs/advanced/lab10/)

---

## Design Examples

### Simple ROM (256×8)
```verilog
module rom_256x8 (
    input  wire [7:0] address,
    output reg  [7:0] data
);
    always @(*) begin
        case (address)
            8'h00: data = 8'hA5;
            8'h01: data = 8'h3C;
            8'h02: data = 8'hF0;
            // ... more addresses
            default: data = 8'h00;
        endcase
    end
endmodule
```

### ROM Initialized from File
```verilog
module rom_from_file (
    input  wire       clk,
    input  wire [7:0] addr,
    output reg  [7:0] data
);
    reg [7:0] memory [0:255];
    
    initial begin
        $readmemh("rom_data.hex", memory);
    end
    
    always @(posedge clk) begin
        data <= memory[addr];
    end
endmodule
```

### Single-Port RAM (256×8)
```verilog
module ram_256x8 (
    input  wire       clk,
    input  wire       we,       // Write enable
    input  wire [7:0] addr,
    input  wire [7:0] data_in,
    output reg  [7:0] data_out
);
    reg [7:0] memory [0:255];
    
    always @(posedge clk) begin
        if (we)
            memory[addr] <= data_in;
        data_out <= memory[addr];  // Read-first mode
    end
endmodule
```

### True Dual-Port RAM
```verilog
module ram_dual_port (
    input  wire        clk,
    // Port A
    input  wire        we_a,
    input  wire [7:0]  addr_a,
    input  wire [15:0] data_in_a,
    output reg  [15:0] data_out_a,
    // Port B
    input  wire        we_b,
    input  wire [7:0]  addr_b,
    input  wire [15:0] data_in_b,
    output reg  [15:0] data_out_b
);
    reg [15:0] memory [0:255];
    
    // Port A
    always @(posedge clk) begin
        if (we_a)
            memory[addr_a] <= data_in_a;
        data_out_a <= memory[addr_a];
    end
    
    // Port B
    always @(posedge clk) begin
        if (we_b)
            memory[addr_b] <= data_in_b;
        data_out_b <= memory[addr_b];
    end
endmodule
```

### Synchronous FIFO
```verilog
module fifo_sync #(
    parameter DATA_WIDTH = 8,
    parameter DEPTH = 16,
    parameter ADDR_WIDTH = $clog2(DEPTH)
)(
    input  wire                   clk, reset,
    input  wire                   wr_en, rd_en,
    input  wire [DATA_WIDTH-1:0]  data_in,
    output reg  [DATA_WIDTH-1:0]  data_out,
    output wire                   full, empty,
    output wire [ADDR_WIDTH:0]    count
);
    reg [DATA_WIDTH-1:0] memory [0:DEPTH-1];
    reg [ADDR_WIDTH-1:0] wr_ptr, rd_ptr;
    reg [ADDR_WIDTH:0]   fifo_count;
    
    // Write operation
    always @(posedge clk or posedge reset) begin
        if (reset) begin
            wr_ptr <= 0;
        end else if (wr_en && !full) begin
            memory[wr_ptr] <= data_in;
            wr_ptr <= wr_ptr + 1;
        end
    end
    
    // Read operation
    always @(posedge clk or posedge reset) begin
        if (reset) begin
            rd_ptr <= 0;
            data_out <= 0;
        end else if (rd_en && !empty) begin
            data_out <= memory[rd_ptr];
            rd_ptr <= rd_ptr + 1;
        end
    end
    
    // FIFO count
    always @(posedge clk or posedge reset) begin
        if (reset) begin
            fifo_count <= 0;
        end else begin
            case ({wr_en && !full, rd_en && !empty})
                2'b10: fifo_count <= fifo_count + 1;  // Write only
                2'b01: fifo_count <= fifo_count - 1;  // Read only
                default: fifo_count <= fifo_count;     // Both or neither
            endcase
        end
    end
    
    assign full  = (fifo_count == DEPTH);
    assign empty = (fifo_count == 0);
    assign count = fifo_count;
    
endmodule
```

---

## Common Mistakes

❌ **Not registering memory outputs**
- Combinational read can cause timing issues
- Use registered outputs for better timing

❌ **Unclear read/write priority**
- Specify read-first, write-first, or no-change mode
- Document behavior for simultaneous access

❌ **FIFO pointer wraparound errors**
- Use correct bit width for pointers
- Handle full/empty detection properly

❌ **Initializing RAM in synthesis**
- RAM initialization may not work in all tools
- Use initialization files or runtime loading

✅ **Good Practice**
- Use synchronous memory (clocked read/write)
- Register all outputs
- Parameterize width and depth
- Include overflow/underflow protection
- Document timing and latency

---

## Memory Capacity Calculations

### Example: 256×8 RAM
- **Address bits**: 8 (2^8 = 256 locations)
- **Word size**: 8 bits
- **Total capacity**: 256 × 8 = 2048 bits = 256 bytes

### Example: 1K×16 RAM
- **Address bits**: 10 (2^10 = 1024 locations)
- **Word size**: 16 bits
- **Total capacity**: 1024 × 16 = 16,384 bits = 2 KB

---

## FIFO Design Considerations

### Full/Empty Detection
**Empty**: `rd_ptr == wr_ptr` and `count == 0`  
**Full**: `rd_ptr == wr_ptr` and `count == DEPTH`

Or use extra bit in pointers for unambiguous detection.

### Almost-Full/Almost-Empty
```verilog
assign almost_full  = (count >= DEPTH - 2);
assign almost_empty = (count <= 2);
```

Useful for flow control and preventing overflow/underflow.

---

## Real-World Applications

- **Caches**: High-speed memory hierarchy
- **Buffers**: Data rate matching, packet storage
- **Lookup Tables**: Math functions, character sets
- **Frame Buffers**: Video/graphics storage
- **Instruction Memory**: Program storage in processors

---

## Next Steps

After completing Module 10, proceed to:
- **[Module 11: Advanced Topics](module-11/)**
- Clock domain crossing
- Pipelining and optimization
- Professional design practices

---

[← Previous Module](module-09/) | [Back to All Modules](../) | [Next Module →](module-11/)
