---
layout: default
title: Assignment 10 - Memory Systems
parent: Assignments
nav_order: 11
---

# Assignment 10: Memory Systems and Storage
**Module 10 - Memory Systems**

---

## Assignment Information

- **Due Date**: End of Week 11
- **Points**: 100
- **Submission**: Canvas (PDF + Verilog files)
- **Type**: Group (2-3 students)
- **Check-off Required**: Yes (30% penalty if not completed)
- **Estimated Time**: 12-15 hours

---

## Learning Objectives

- Understand memory architectures (ROM, RAM, FIFO)
- Design memory interfacing circuits
- Implement lookup tables using ROM
- Create synchronous memory systems
- Build FIFO buffers for data streaming

---

## Problems

### Problem 1: ROM-Based Lookup Table (25 points)

**Objective**: Design ROM to implement 4-bit sine wave generator.

**Specification**:
- 16 samples of sine wave (one complete cycle)
- 8-bit amplitude values
- Address input cycles through 0-15

**Part A: ROM Content (10 points)**

Create lookup table:
1. Calculate 16 sine values: $\sin(2\pi \cdot i / 16)$ for i=0 to 15
2. Scale to 8-bit unsigned (0-255, with 128 as midpoint)
3. Table format:

| Address | Angle | Sin Value | 8-bit Code |
|---------|-------|-----------|------------|
| 0000 | 0° | 0.0 | 10000000 |
| 0001 | 22.5° | 0.383 | 10110001 |
| ... | ... | ... | ... |

**Part B: Verilog ROM (10 points)**
```verilog
module sine_rom (
    input  wire [3:0] ADDR,
    output reg  [7:0] DATA
);
    always @(*) begin
        case (ADDR)
            4'd0:  DATA = 8'd128;
            4'd1:  DATA = 8'd177;
            // Complete all 16 entries
            default: DATA = 8'd0;
        endcase
    end
endmodule
```

**Part C: Sine Wave Generator (5 points)**
- Add counter to auto-increment address
- Clock divider for visible frequency
- Display on LEDs or DAC output

---

### Problem 2: Synchronous RAM Design (25 points)

**Objective**: Design single-port synchronous RAM.

**Specification**:
- **Capacity**: 256 words × 8 bits
- **Ports**: Single read/write port
- **Control**: `WE` (write enable), `CS` (chip select)
- **Synchronous**: All operations on clock edge

**Part A: RAM Architecture (8 points)**
1. Block diagram
2. Timing diagram (read cycle, write cycle)
3. Explain synchronous vs asynchronous

**Part B: Verilog Implementation (12 points)**
```verilog
module sync_ram_256x8 (
    input  wire       CLK,
    input  wire       CS,      // Chip select
    input  wire       WE,      // Write enable
    input  wire [7:0] ADDR,
    input  wire [7:0] DIN,
    output reg  [7:0] DOUT
);
    reg [7:0] mem [0:255];
    
    always @(posedge CLK) begin
        if (CS) begin
            if (WE)
                mem[ADDR] <= DIN;
            else
                DOUT <= mem[ADDR];
        end
    end
endmodule
```

**Part C: Memory Tester (5 points)**

Write testbench that:
1. Writes test pattern to all addresses
2. Reads back and verifies
3. Tests corner cases (address 0, 255)
4. Demonstrates read-modify-write

---

### Problem 3: FIFO Buffer (30 points)

**Objective**: Design synchronous FIFO (First-In-First-Out) buffer.

**Specification**:
- **Depth**: 16 words
- **Width**: 8 bits per word
- **Ports**: Separate read and write (dual clock if bonus)
- **Status**: `FULL`, `EMPTY`, `COUNT[4:0]` (number of items)
- **Operations**: 
  - Write: `WR_EN` high, data on `DIN`
  - Read: `RD_EN` high, data appears on `DOUT`

**Part A: FIFO Architecture (10 points)**
1. Block diagram showing:
   - Memory array
   - Write pointer
   - Read pointer
   - Control logic
2. Explain circular buffer operation
3. Full/empty detection logic

**Part B: Verilog Implementation (15 points)**
```verilog
module fifo_16x8 (
    input  wire       CLK,
    input  wire       RST_N,
    input  wire       WR_EN,
    input  wire       RD_EN,
    input  wire [7:0] DIN,
    output reg  [7:0] DOUT,
    output wire       FULL,
    output wire       EMPTY,
    output reg  [4:0] COUNT
);
    reg [7:0] mem [0:15];
    reg [3:0] wr_ptr, rd_ptr;
    
    // Your implementation
    
endmodule
```

Requirements:
- Prevent write when full
- Prevent read when empty
- Accurate count tracking
- Handle simultaneous read/write

**Part C: Verification (5 points)**

Testbench scenarios:
1. Fill FIFO completely (verify FULL)
2. Empty FIFO completely (verify EMPTY)
3. Continuous write/read (verify data integrity)
4. Simultaneous read/write
5. Overflow/underflow protection

---

### Problem 4: Memory-Based Pattern Sequencer (20 points)

**Objective**: Create LED pattern sequencer using memory.

**Specification**:
- Store multiple LED patterns in RAM
- Cycle through patterns with user control
- Allow programming new patterns

**Part A: System Design (8 points)**
1. Architecture:
   - Pattern memory (64 patterns × 10 LEDs)
   - Pattern counter
   - Speed control
   - Pattern programming mode
2. Control FSM (RUN, PROGRAM modes)

**Part B: Verilog Implementation (8 points)**
- Memory to store patterns
- Sequential playback logic
- Programming interface (use switches/buttons)
- Speed control

**Part C: FPGA Demo (4 points)**
- Default patterns pre-loaded
- Demonstrate playback
- Show programming new pattern
- Speed adjustment

---

## Grading Rubric

### Problem 1 (25 points)
- Sine table calculation: 10 points
- Verilog ROM: 10 points
- Generator integration: 5 points

### Problem 2 (25 points)
- Architecture and timing: 8 points
- Verilog RAM: 12 points
- Testing: 5 points

### Problem 3 (30 points)
- FIFO architecture: 10 points
- Verilog implementation: 15 points
- Verification: 5 points

### Problem 4 (20 points)
- System design: 8 points
- Verilog: 8 points
- FPGA demo: 4 points

---

## Check-off Requirements

Demonstrate:
1. **Sine ROM**: Show waveform generation
2. **RAM**: Memory read/write operations
3. **FIFO**: Fill, empty, and data flow
4. **Pattern Sequencer**: Playback and programming

---

## Resources
- Memory Design Guide
- FIFO Architecture Tutorial
- ROM Initialization Methods
- Pointer Management Techniques

---

**Memory systems are foundational. Master these concepts!** 💾
