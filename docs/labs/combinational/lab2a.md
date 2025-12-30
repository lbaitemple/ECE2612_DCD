---
layout: default
title: "Lab 2a: Introduction to Testbenches"
parent: Combinational Logic Labs
grand_parent: Labs & Exercises
nav_order: 2
---

# Lab 2A – Introduction to Testbenches

## Introduction

A testbench is an important component in digital design. When developing a new or evolving design, an organization is typically divided into two functional units:

| Team | Focus |
|------|-------|
| **Design Team** | Creating the actual product design |
| **Test/Verification Team** | Verifying the design meets specifications and testing during manufacturing |

In this lab, you will be introduced to the verification process.

### Why Testbenches Matter

Both teams start with the same specification. In a simple design block, a *complete* specification can be based on an equation or truth table. By *complete*, we mean that the values of all output signals are defined for all possible combinations of input signals.

For simple designs, this process is fairly straightforward:
1. Apply all possible inputs to the design
2. Observe the outputs
3. Compare outputs to expected values

While we could check outputs by hand, this is tedious and error-prone. A better solution is to use a **self-checking testbench** that automatically compares each output signal with an expected value.

### Benefits of Self-Checking Testbenches

1. **Independent Verification** - The verification team works from the specification, not the design code. Two independent views must match, reducing functional design errors.

2. **Regression Testing** - As the design evolves (minimizing power, increasing speed), the team can quickly verify changes haven't broken functionality by reusing the testbench.

---

## Design/Module Concepts

Verilog/SystemVerilog can be used for both design and verification. However, not all language constructs translate into hardware. The testbench is an *abstract* design that:
- Applies stimuli to inputs of a real design
- Compares outputs to expected values
- Is **NOT** part of the hardware implementation

### File Naming Convention

We use a consistent naming style:

| File Type | Naming Pattern | Example |
|-----------|----------------|---------|
| Design Module | `<module_name>.sv` | `and_3_inputs.sv` |
| Testbench | `tb_<module_name>.sv` | `tb_and_3_inputs.sv` |
| Test Vectors | `tb_<module_name>.txt` | `tb_and_3_inputs.txt` |

---

## Example: Three-Input AND Gate

### The Design Under Test

```systemverilog
module and_3_inputs (output logic f, input logic a, b, c);
    // this is the design to test
    assign f = a & b & c;
endmodule
```

This design synthesizes into a three-input AND gate that can be loaded into FPGA hardware.

### Truth Table Specification

| data_in[2:0] | expected_out[0:0] |
|--------------|-------------------|
| 3'b000 | 1'b0 |
| 3'b001 | 1'b0 |
| 3'b010 | 1'b0 |
| 3'b011 | 1'b0 |
| 3'b100 | 1'b0 |
| 3'b101 | 1'b0 |
| 3'b110 | 1'b0 |
| 3'b111 | 1'b1 |

### Test Vector File (tb_and_3_inputs.txt)

```
000_0
001_0
010_0
011_0
100_0
101_0
110_0
111_1
```

> **Note:** Verilog allows underscores to separate data patterns for readability. The file has 8 rows (2³) and 4 columns.

---

## Building the Testbench

### Step 1: Module Declaration

```systemverilog
module tb_and_3_inputs (); // top level testbench wrapper
    // no inputs/outputs at top level for simulation
    ...
endmodule
```

### Step 2: Declare Parameters and Signals

```systemverilog
parameter ROWS=8, INPUTS=3, OUTPUTS=1;

logic [INPUTS-1:0] data_in;
logic [OUTPUTS-1:0] expected_out;
logic [OUTPUTS-1:0] sim_out;           // simulated output
logic [INPUTS+OUTPUTS-1:0] test_vectors [0:ROWS-1];

integer i;        // loop index
integer mm_count; // mismatch count
```

Using parameters makes the code reusable - just edit one line for different designs!

### Step 3: Instantiate Unit Under Test

```systemverilog
// instantiate the unit under test (instance name uut)
and_3_inputs uut (
    .f(sim_out), 
    .a(data_in[2]), 
    .b(data_in[1]),
    .c(data_in[0])
);
```

> **Key Concept:** Instantiation is a parallel operation. Think of the `uut` as physical hardware - change the inputs and the outputs change immediately.

### Step 4: The Initial Block

The `initial` block executes statements sequentially, starting at simulation time zero:

```systemverilog
initial begin
    $dumpfile("tb_and_3_inputs.vcd");
    $dumpvars();
    mm_count = 0;
    
    // read test vectors from file
    $readmemb("tb_and_3_inputs.txt", test_vectors);
    
    // loop over all rows
    for (i=0; i<ROWS; i=i+1) begin
        // apply test vector
        {data_in, expected_out} = test_vectors[i];
        #10; // wait 10 ns for outputs to settle
        
        // compare output to expected
        if (sim_out !== expected_out) begin
            $display("Mismatch--index: %d; input: %b, expected: %b, received: %b",
                     i, data_in, expected_out, sim_out);
            mm_count = mm_count + 1;
        end
        #10; // symmetry delay
    end
    
    // report results
    if (mm_count == 0)
        $display("Simulation complete - no mismatches!!!");
    else
        $display("Simulation complete - %d mismatches!!!", mm_count);
    
    $finish;
end
```

### Key Functions Explained

| Function | Purpose |
|----------|---------|
| `$dumpfile()` | Creates VCD file for waveform viewing |
| `$dumpvars()` | Records all signals to VCD file |
| `$readmemb()` | Reads binary data from text file |
| `$display()` | Prints formatted message (like C's printf) |
| `$finish` | Ends simulation cleanly |

### Timescale Directive

```systemverilog
`timescale 1ns / 1ps
```

This defines:
- **Time units:** 1 ns
- **Precision:** 1 ps

So `#10` means delay 10 nanoseconds.

---

## Complete Testbench Template

```systemverilog
`timescale 1ns / 1ps

module tb_and_3_inputs ();

    parameter ROWS=8, INPUTS=3, OUTPUTS=1;
    
    logic [INPUTS-1:0] data_in;
    logic [OUTPUTS-1:0] expected_out;
    logic [OUTPUTS-1:0] sim_out;
    logic [INPUTS+OUTPUTS-1:0] test_vectors [0:ROWS-1];
    
    integer i;
    integer mm_count;
    
    // instantiate the unit under test
    and_3_inputs uut (
        .f(sim_out), 
        .a(data_in[2]), 
        .b(data_in[1]),
        .c(data_in[0])
    );
    
    initial begin
        $dumpfile("tb_and_3_inputs.vcd");
        $dumpvars();
        mm_count = 0;
        
        $readmemb("tb_and_3_inputs.txt", test_vectors);
        
        for (i=0; i<ROWS; i=i+1) begin
            {data_in, expected_out} = test_vectors[i];
            #10;
            if (sim_out !== expected_out) begin
                $display("Mismatch--index: %d; input: %b, expected: %b, received: %b",
                         i, data_in, expected_out, sim_out);
                mm_count = mm_count + 1;
            end
            #10;
        end
        
        if (mm_count == 0)
            $display("Simulation complete - no mismatches!!!");
        else
            $display("Simulation complete - %d mismatches!!!", mm_count);
        
        $finish;
    end

endmodule
```

---

## Lab Exercise: Hamming Encoder Testbench

### Design Specification

Create a testbench for the Hamming(7,4) encoder:

```systemverilog
module hamming7_4_encode(output logic [7:1] e, input logic [4:1] d);
    ...
endmodule
```

### Truth Table

| d[4:1] | e[7:1] |
|--------|--------|
| 4'b0000 | 7'b0000000 |
| 4'b0001 | 7'b0000111 |
| 4'b0010 | 7'b0011001 |
| 4'b0011 | 7'b0011110 |
| 4'b0100 | 7'b0101010 |
| 4'b0101 | 7'b0101101 |
| 4'b0110 | 7'b0110011 |
| 4'b0111 | 7'b0110100 |
| 4'b1000 | 7'b1001011 |
| 4'b1001 | 7'b1001100 |
| 4'b1010 | 7'b1010010 |
| 4'b1011 | 7'b1010101 |
| 4'b1100 | 7'b1100001 |
| 4'b1101 | 7'b1100110 |
| 4'b1110 | 7'b1111000 |
| 4'b1111 | 7'b1111111 |

### Steps to Complete

1. Open `tb_template.sv` in one window
2. Create new file: `tb_hamming7_4_encode.sv`
3. Copy the template and modify:
   - Change `ROWS=16, INPUTS=4, OUTPUTS=7`
   - Update module instantiation
   - Update file names
4. Create `tb_hamming7_4_encode.txt` with truth table data
5. Test syntax by running `tb_hamming7_4_encode.m_sim`

### Expected Output (Before Design Complete)

Since the Hamming encoder design is empty, you should see:

```
Mismatch--loop index i: 0; input: 0000, expected: 0000000, received: xxxxxxx
Mismatch--loop index i: 1; input: 0001, expected: 0000111, received: xxxxxxx
...
Mismatch--loop index i: 15; input: 1111, expected: 1111111, received: xxxxxxx
Simulation complete - 16 mismatches!!!
```

---

## Viewing the Waveform

The VCD file contains signal data useful for debugging.

### Using WaveTrace (VS Code Extension)

Your lab instructor will demonstrate using WaveTrace, which provides waveform viewing directly in VS Code.

### Alternative: EPWave (Online)

1. **Download VCD file** - Right-click on `tb_hamming7_4_encode.vcd` and select Download (do NOT open it directly)
2. **Open EPWave** - Go to [https://www.edaplayground.com/w/home](https://www.edaplayground.com/w/home)
3. **Upload file** - Select Upload and choose your VCD file
4. **Select signals** - Click "Get Signals" and select `.uut` to view design signals
5. **View waveforms** - Use "Append All" to add signals to the viewer

> **Tip:** Change display format from hex to binary using the Radix dropdown.

---

## Important: Simulation vs Hardware

> ⚠️ **Critical Rule:** If your design does not pass simulation, don't waste time synthesizing and loading it into hardware!

### Why This Matters

- Mismatches in simulation will **NOT** magically correct in hardware
- Hardware debugging has limited visibility into the FPGA
- Simulation provides complete visibility of any signal at any time
- Self-checking testbenches point you directly to problem patterns

### The Golden Rule

**A passing simulation almost guarantees that your design will operate correctly in hardware.**

---

## Synthesis

There is no synthesis for this lab. You are creating the testbench that will be used to verify the Hamming encoder design in the next lab.

---

## Deliverables

- [ ] Completed `tb_hamming7_4_encode.sv` testbench
- [ ] Completed `tb_hamming7_4_encode.txt` test vector file
- [ ] Screenshot showing simulation results (16 mismatches expected)

## Lab Manual

📄 [Download Lab 2A Manual (PDF)](lab2a_v10.pdf)
